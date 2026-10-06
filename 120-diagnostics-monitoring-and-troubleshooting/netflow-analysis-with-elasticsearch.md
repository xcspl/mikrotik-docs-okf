---
type: Reference
title: "NetFlow analysis with Elasticsearch"
description: "This guide will not use Logstash as a part of analyzing NetFlow data, it has been replaced by a Fleet Server."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# NetFlow analysis with Elasticsearch

Introduction Prerequisites Setup Elastic RouterOS Using Kibana Log retation Use a different ILM policy

## Introduction

Elasticsearch is a popular NoSQL database that can be used to store a wide range of data, including NetFlow logs. Alongside with Kibana you can create a powerful tool to analyze NetFlow data from your RouterOS devices. This guide will rely on Elasticsearch integrations and for it to work you need to have a working Elasticsearch setup. This guide will not cover setup instructions for Elasticsearch and Kibana, but will cover the relevant steps to setup NetFlow log collection and analysis.

There are many possible configurations that can be made with Elasticsearch, but for the sake of this guide we will use the following principle:

A RouterOS (10.0.0.1) device sends out NetFlow data to a server (10.0.0.2) running NetFlow integration The server (10.0.0.2) running NetFlow integration ingests NetFlow data, processes the data and sends it to a Fleet Server (10.0.0.3) A Fleet Server (10.0.0.3) stores the data in Elasticsearch (10.0.0.4) Kibana (10.0.0.5) retrieves data from Elasticsearch (10.0.0.4), analyzes it and allows you to search the data

This guide will not use Logstash as a part of analyzing NetFlow data, it has been replaced by a Fleet Server.

It is possible to install Elasticsearch, Kibana, Fleet Server and NetFlow Records integration on the same device.

## Prerequisites

Setup Elasticsearch

Elasticsearch is widely supported on many platforms. It is recommended to setup a cluster of Elasticsearch nodes.

Setup kibana

Kibana can be installed on the same device on which you installed Elasticsearch, but it can also be installed on a separate device for performance reasons. While it is possible to analyze NetFlow data without Kibana, it requires writing your own API requests, Kibana is very easy to use and has a wide range of features.

Setup Fleet Server

It is possible to setup Fleet Server on the same device on which you installed Elasticsearch and/or Kibana. It is recommended to install Fleet Server on a different device. Refer to Elasticsearch manual for recommendations on hardware and topology requirements.

## Setup

The setup instructions are divided into two parts: Elastic (configuration regarding Elasticsearch, Kibana and Fleet Server) and RouterOS (configuration that is relevant to your RouterOS device).

Elastic

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps.

1. Log into your Kibana
2. Open the Fleet section under the main menu
3. Open the "Agent policies" section
4. Press "Create agent policy" button to create a new Agent Policy
5. Give the policy a name, for example, "NetFlow policy", adjust advance settings if required, create the policy
6. Open your newly created policy by clicking on it's name
7. Press "Add integration"
8. Search for "NetfFlow Records" and press "Add NetFlow Records"
9. Adjust configuration, make sure:
- Specify "UDP host to listen on" to the IP address of your server that is going to run the NetFlow Records integration, in this example the address should be "10.0.0.2"
10. Save the integration
11. Press the "Add Elastic Agent to your host" button
12. Follow the instructions on how to add Elastic Agent to your host Official Elastic's manual recommends installing the Elastic Agent as Fleet-managed. Consider following the recommendation since managing the agents is easier when they are Fleet-managed.
13. Make sure you have opened the NetFlow port on your host and elsewhere in the path from your RouterOS device (10.0.0.1), the default destination port is 2055/UDP.
14. Your Elastic Agent is now ready to receive NetFlow data!
RouterOS

1. (optional) Create an Interface list (for example, "NetFlow_interfaces") and add interface that need NetFlow data analysis /interface list add name=NetFlow_interfaces /interface list member add interface=VLAN3000 list=NetFlow_interfaces
2. Configure Traffic-flow to send NetFlow data to your Elastic Agent (10.0.0.2)

2. /ip traffic-flow enabled=yes interfaces=NetFlow_interfaces /ip traffic-flow target add dst-address=10.0.0.2
3. You should now start to see NetFlow data being ingested!
4. Continue the guide to start using Kibana
## Using Kibana

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps.

The NetFlow Records integration provides some useful assets that can be used to analyze NetFlow data. Make sure you install the assets first before continuing. The following section will give you some basic ways how to see NetFlow data.

1. Log into your Kibana
2. Open the "Dashboards" menu in the main menu
3. Search the Dashboards and find "NetFlow"
You should now see multiple NetFlow Dashboards. For example, try opening the "[Logs Netflow] Overview". If your NetFlow data is properly ingested, then you should now see graphs that summarizes your traffic.

Another useful Dashboard is the "[Logs Netflow] Flow records", which shows you exact NetFlow records. A very useful feature is the filtering option (the + button on top), that allows you add filters to NetFlow data, for example, you can filter the records to show only a single IP address:

There are other options such as searching for a specific time range. You should read more about Discover to understand the possibilities better.

For quick reference, these are the fields that you are most likely going to want to use for searching NEtFlow data:

source.ip source.port destination.ip destination.port network.transport

If you want to examine a single record, it is recommended to use the Discover view. NetFlow data can be found as "data_stream.dataset: netflow.log".

## Log retation

Depending on your local laws you might be required to store NetFlow data for a specified period of time. Be aware that busy networks can generated a lot of NetFlow data, even terabytes per day. You are most likely going to want to adjust LIfecycle Policy. By default the NetFlow data should go under the "logs" policy. If you have multiple Elasticsearch nodes, you can utilize "phases", which allows you to store data on different types of storage media, but if you only have a single Elasticsearch node, your options are limited and you will most likely want to delete old data. For example, if you want to delete data after 6 months, then you can simply change the ILM policy to delete data after 6 months or use this API request:

PUT _ilm/policy/logs { "policy": { "phases": { "hot": { "min_age": "0ms", "actions": { "rollover": { "max_age": "30d", "max_primary_shard_size": "50gb" }, "set_priority": { "priority": 101 } } }, "delete": { "min_age": "180d", "actions": { "delete": { "delete_searchable_snapshot": true } } } } } }

If you change the "logs" policy, this will apply to ALL your logs, not just NetFlow data. If you need a different retention period for other logs, then it is better to create a new ILM policy and specify the NetFlow integration to use the newly created ILM policy.

### Use a different ILM policy

If you want your NetFlow data to have a different retention period, then you need to do the following steps:

1. Create a new ILM policy, give it a new name and set the desired period for the delete phase, or use this API request: PUT _ilm/policy/netflow-logs { "policy": { "phases": { "hot": { "min_age": "0ms", "actions": { "rollover": { "max_age": "30d", "max_primary_shard_size": "50gb" }, "set_priority": { "priority": 101 } } }, "delete": { "min_age": "1000d", "actions": { "delete": { "delete_searchable_snapshot": true } } } } } }

2. Goto Kibana, open "Stack Management", then go to "Index Management" and then "Component Templates"
3. Search for "logs-netflow.log@custom", open it and edit it
4. Go to the "Index settings" section
5. Paste in the following: { "index": { "lifecycle": { "name": "netflow-logs" } } }
6. Press "Next" and then "Save component template"
