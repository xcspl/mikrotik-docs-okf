---
type: Reference
title: "REST API"
description: "The term \"REST API\" generally refers to source-oriented URLs. an API accessed via HTTP protocol at a predefined set of re Starting from RouterOS v7.1beta4, it is implemented as a JSON wrapper interface of the console API."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# REST API

Overview Authentication JSON format HTTP Methods GET PATCH PUT DELETE POST Proplist Query Timeout Errors Examples

## Overview

Watch our video about this feature.

The term "REST API" generally refers to source-oriented URLs. an API accessed via HTTP protocol at a predefined set of re Starting from RouterOS v7.1beta4, it is implemented as a JSON wrapper interface of the console API. It allows to create, read, update and delete resources and call arbitrary console commands.

To start using REST API, the www-ssl or www (starting with RouterOS v7.9) service must be configured and running. When the www-ssl service (HTTPS access) is enabled, the REST service can be accessed by connecting to https://<routers_IP>/rest. When www service (HTTP access) is enabled the REST service can be accessed by connecting to http://<routers_IP>/rest.

We do not advise enabling HTTP access (www service). The main risk is that authentication credentials can be read with passive eavesdropping. You can use it only when performing tests (not in a production environment) and when you are certain that nobody can listen in (inspect your traffic)!

The easiest way to start is to use cURL, wget, or any other HTTP client even RouterOS fetch tool.

$ curl -k -u admin: [https://10.155.101.214/rest/system/resource](https://10.155.101.214/rest/system/resource) [{"architecture-name":"tile","board-name":"CCR1016-12S-1S+", "build-time":"Dec/04/2020 14:19:51","cpu":"tilegx","cpu-count":"16", "cpu-frequency":"1200","cpu-load":"1","free-hdd-space":"83439616", "free-memory":"1503133696","platform":"MikroTik", "total-hdd-space":"134217728","total-memory":"2046820352", "uptime":"2d20h12m20s","version":"7.1beta4 (development)"}]

## Authentication

Authentication to the REST API is performed via HTTP Basic Auth. Provide your Username and password are the same as for the console user (by default "admin" with no password).

You have to set up certificates to use secure HTTPS, if self-signed certs are used, then CA must be imported to the trusted root. However, for testing purposes, it is possible to connect insecurely (for cUrl use -k flag, for wget use eck-certificate).--no-ch

### JSON format

Server broadly follows ECMA-404 standard, with following notes:

In JSON replies all object values are encoded as strings, even if the underlying data is a number or a boolean.

The server also accepts numbers in octal format (begins with 0) and hexadecimal format (begins with 0x). If the numbers are sent in a string format, they are assumed to be in decimal format. Numbers with exponents are not supported.

## HTTP Methods

Below is a table summarising supported HTTP methods

|HTTP Verv|CRUD|ROS|Description|
|---|---|---|---|
|GET|Read|print|To get the records.|
|PATCH|Update/Modify|set|To update a single record.|
|PUT|Create|add|To create a new record.|
|DELETE POST|Delete|remove|To delete a single record. Universal method to get access to all console commands.|

GET

This method allows getting the list of all records or a single record from the specified menu encoded in the URL. For example, get all IP addresses (equivalent to the 'ip/address/print' command from the CLI):

$ curl -k -u admin: [https://10.155.101.214/rest/ip/address](https://10.155.101.214/rest/ip/address) [{".id":"*1","actual-interface":"ether2","address":"10.0.0.111/24","disabled":"false", "dynamic":"false","interface":"ether2","invalid":"false","network":"10.0.0.0"}, {".id":"*2","actual-interface":"ether3","address":"10.0.0.109/24","disabled":"true", "dynamic":"false","interface":"ether3","invalid":"false","network":"10.0.0.0"}]

To return a single record, append the ID at the end of the URL:

$ curl -k -u admin: [https://10.155.101.214/rest/ip/address/*1](https://10.155.101.214/rest/ip/address/*1) {".id":"*1","actual-interface":"ether2","address":"10.0.0.111/24","disabled":"false", "dynamic":"false","interface":"ether2","invalid":"false","network":"10.0.0.0"}

If table contains named parameters, then name instread of ID can be used, for example, get ether1:

$ curl -k -u admin: [https://10.155.101.214/rest/interface/ether1](https://10.155.101.214/rest/interface/ether1)

It is also possible to filter the output, for example, return only valid addresses that belong to the 10.155.101.0 network:

$ curl -k -u admin: "[https://10.155.101.214/rest/ip/address?network=10.155.101.0&dynamic=true"](https://10.155.101.214/rest/ip/address?network=10.155.101.0&dynamic=true") [{".id":"*8","actual-interface":"sfp12","address":"10.155.101.214/24","disabled":"false", "dynamic":"true","interface":"sfp12","invalid":"false","network":"10.155.101.0"}]

Another example returns only addresses on the "dummy" interface and with the comment "test":

$ curl -k -u admin: '[https://10.155.101.214/rest/ip/address?comment=test&interface=dummy'](https://10.155.101.214/rest/ip/address?comment=test&interface=dummy') [{".id":"*3","actual-interface":"dummy","address":"192.168.99.2/24","comment":"test", "disabled":"false","dynamic":"false","interface":"dummy","invalid":"false","network":"192.168.99.0"}]

If you want to return only specific properties, you can use the '.proplist', followed by the '=' and a list of comma-separated properties. For example, to show only the address and if it's disabled:

$ curl -k -u admin: [https://10.155.101.214/rest/ip/address?.proplist=address,disabled](https://10.155.101.214/rest/ip/address?.proplist=address,disabled) [{"address":"10.0.0.111/24","disabled":"false"},{"address":"10.0.0.109/24","disabled":"true"}]

PATCH

This method is used to update a single record. Set PATCH call body as a JSON object which contains fields and values of the properties to be updated. For example, add a comment:

$ curl -k -u admin: -X PATCH [https://10.155.101.214/rest/ip/address/*3](https://10.155.101.214/rest/ip/address/*3) \ --data '{"comment": "test"}' -H "content-type: application/json" {".id":"*3","actual-interface":"dummy","address":"192.168.99.2/24","comment":"test", "disabled":"false","dynamic":"false","interface":"dummy","invalid":"false","network":"192.168.99.0"}

In case of a successful update, the server returns the updated object with all its parameters.

PUT

A method is used to create new records in the menu encoded in the URL. The body should be set as a JSON object containing parameters applied to the newly created record.

In case of success, the server returns the created object with all its parameters.

Only one resource can be created in a single request.

For example, add an IP address to a dummy interface:

$ curl -k -u admin: -X PUT [https://10.155.101.214/rest/ip/address](https://10.155.101.214/rest/ip/address) \ --data '{"address": "192.168.111.111", "interface": "dummy"}' -H "content-type: application/json" {".id":"*A","actual-interface":"dummy","address":"192.168.111.111/32","disabled":"false", "dynamic":"false","interface":"dummy","invalid":"false","network":"192.168.111.111"}

DELETE

This method is used to delete the record with a specified ID from the menu encoded in the URL. If the deletion has been succeeded, the server responds with an empty response. For example, call to delete the record twice, on second call router will return 404 error:

$ curl -k -u admin: -X DELETE [https://10.155.101.214/rest/ip/address/*9](https://10.155.101.214/rest/ip/address/*9) $ curl -k -u admin: -X DELETE [https://10.155.101.214/rest/ip/address/*9](https://10.155.101.214/rest/ip/address/*9) {"error":404,"message":"Not Found"}

POST

All the API features are available through the POST method. The command word is encoded in the header and optional parameters are passed in the JSON object with the corresponding fields and values. For example, to change the password of the active user, send

POST [https://router/rest/password](https://router/rest/password) {"old-password":"old","new-password":"N3w", "confirm-new-password":"N3w"}

REST response is structured similar to API response:

If the response contains '!re' sentences (records), the JSON reply will contain a list of objects. !done'If the ' sentence contains data, the JSON reply will contain an object with the data. !done'If there are no records or data in the ' sentence, the response will hold an empty list.

There are two special keys: .proplist and .query, which are used with the print command word. Read more about APIs responses, prop lists, and queries in the API documentation.

Proplist

The '.proplist' key is used to create .proplist attribute word. The values can be a single string with comma-separated values:

POST [https://router/rest/interface/print](https://router/rest/interface/print) {".proplist":"name,type"}

or a list of strings:

POST [https://router/rest/interface/print](https://router/rest/interface/print) {".proplist":["name","type"]}

For example, return address and interface properties from the ip/address list:

$ curl -k -u admin: -X POST [https://10.155.101.214/rest/ip/address/print\](https://10.155.101.214/rest/ip/address/print\) --data '{"_proplist": ["address","interface"]}' -H "content-type: application/json" [{"address":"192.168.99.2/24","interface":"dummy"}, {"address":"172.16.5.1/24","interface":"sfpplus1"}, {"address":"172.16.6.1/24","interface":"sfp2"}, {"address":"172.16.7.1/24","interface":"sfp3"}, {"address":"10.155.101.214/24","interface":"sfp12"}, {"address":"192.168.111.111/32","interface":"dummy"}]

Query

The '.query' key is used to create a query stack. The value is a list of query words. For example this POST request :

POST [https://router/rest/interface/print](https://router/rest/interface/print) {".query":["type=ether","type=vlan","#|!"]}

is equivalent to this API sentence

/interface/print ?type=ether ?type=vlan ?#|!

For example, let's combine 'query' and 'proplist', to return '.id address', '', and 'interface' properties for all dynamic records and records with the network

192.168.111.111 $ curl -k -u admin: -X POST [https://10.155.101.214/rest/ip/address/print](https://10.155.101.214/rest/ip/address/print) \ --data '{".proplist": [".id","address","interface"], ".query": ["network=192.168.111.111","dynamic=true"," #|"]}'\ -H "content-type: application/json" [{".id":"*8","address":"10.155.101.214/24","interface":"sfp12"}, {".id":"*A","address":"192.168.111.111/32","interface":"dummy"}] Timeout If the command runs indefinitely, it will timeout and the connection will be closed with an error. The current timeout interval is 60 seconds. To avoid timeout errors, add a parameter that would sufficiently limit the command execution time. Timeout is not affected by the parameters passed to the commands. If the command is set to run for an hour, it will terminate early and return an error message. For example, let's see what we get when the ping command exceeds the timeout and how to prevent this by adding a count parameter: $ curl -k -u admin: -X POST [https://10.155.101.214/rest/ping](https://10.155.101.214/rest/ping) \ --data '{"address":"10.155.101.1"}' \ -H "content-type: application/json" {"detail":"Session closed","error":400,"message":"Bad Request"}

curl -k -u <username>:<password> https://<ip-address>/rest/export --data '{"compact":"","file":"test.rsc"}' -H "content-type: application/json"

Move a firewall entry (switch positions): curl -k -u <username>:<password> -X POST http://<ip-address>/rest/ip/firewall/nat/move --data '{".id":"*9",". id":"*C"}' -H "content-type: application/json"

LTE firmware update: curl -k -u <username>:<password> -X POST 'http://<ip-address>/rest/interface/lte/firmware-upgrade' --data '{"number":"lte2"}' -H "content-type: application/json"

Get OIDs from /system resource: curl -k -u <username>:<password> -X POST http://<ip-address>/rest/system/resource/print --data '{"oid":""}' -H "content-type: application/json"

There is no option to run a "continuous" command, like "monitor" via REST API. Use "monitor once" parameter instead to print the result once.

An example of using /tool fetch to run a REST API POST to another RouterOS device:

/tool fetch http-method=post url="http://<ip-address>/rest/execute" http-data="{\"script\":\"/log info fetchtest\"}" http-header-field="Content-Type:application/json" output=user user=<username> password=<password>
