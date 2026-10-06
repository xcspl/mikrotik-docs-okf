---
type: Reference
title: "Container-Matrix"
description: "To setup a Matrix server on your RouterOS device, follow the steps below."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Container-Matrix

Introduction Configuration Discord bridge

## Introduction

Matrix is a decentralized communication protocol. Each Matrix server has its own set of users and its own set of rules, you can host your own Matrix server on a RouterOS device using Containers. You can create federation between Matrix servers and communicate with users on different Matrix servers securely. You can also use Matrix bridges to relay messages from other chat platforms such as WhatsApp, Discord, Signal, Telegram and other platforms and only use a single App such as Element and be able to communicate with users on different platforms.

## Configuration

To setup a Matrix server on your RouterOS device, follow the steps below.

Make sure you have created a Container network before proceeding.

1. Create PostgreSQL Container environment variables: /container/envs/add name=postgres_synapse_envs key=POSTGRES_DB value="synapse" /container/envs/add name=postgres_synapse_envs key=POSTGRES_PASSWORD value="<POSTGRES_PASSWORD_HERE>" /container/envs/add name=postgres_synapse_envs key=POSTGRES_USER value="synapse_user" /container/envs/add name=postgres_synapse_envs key=PGDATA value="/var/lib/postgresql/data/pgdata" /container/envs/add name=postgres_synapse_envs key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc- collate='C' --lc-ctype='C'" /container/envs/add name=postgres_synapse_envs key=PGPORT value=5433
2. Create PostgreSQL Container mounts: /container/mounts/add name=synapse_postgres_data src=disk1/synapse-postgres-data dst=/var/lib/postgresql /data
3. Create a PostgreSQL Container: /container/add remote-image=postgres:17.2-alpine interface=veth1 root-dir=disk1/postgres-17.2-synapse mounts=synapse_postgres_data envlist=postgres_synapse_envs name=postgresql_synapse
4. Create Synapse Container environment variables: /container/envs/add name=synapse_envs key=SYNAPSE_CONFIG_DIR value="/data" /container/envs/add name=synapse_envs key=SYNAPSE_CONFIG_PATH value="/data/homeserver.yaml" /container/envs/add name=synapse_envs key=SYNAPSE_SERVER_NAME value="test.mt.lv" /container/envs/add name=synapse_envs key=SYNAPSE_REPORT_STATS value="yes"
5. Create Synapse Container mounts: /container/mounts/add name=synapse_data src=disk1/synapse-data dst=/data
6. Create a Synapse Container for generating required data:

6. /container/add remote-image=matrixdotorg/synapse:latest interface=veth1 cmd="generate" root-dir=disk1 /synapse mounts=synapse_data envlist=synapse_envs name=synapse
7. Start and stop the Synapse Container to allow it to generate required files: /container/start [find where name=synapse] /container/stop [find where name=synapse]
8. Remove the cmd parameter from the Synapse Container: /container/set [find where name=synapse] cmd=""
9. Connect to your RouterOS device using a SFTP client (for example, WinSCP if using Microsoft Windows) and adjust the disk1/synapse-data /homeserver.yaml file: database: name: psycopg2 args: user: synapse_user password: <POSTGRE_PASSWORD_HERE> dbname: synapse host: localhost port: 5433 cp_min: 5 cp_max: 10 keepalives_idle: 10 #optional keepalives_interval: 10 #optional keepalives_count: 3 #optional
10. Start the PostgreSQL Container: /container/start [find where name=postgresql_synapse]
11. Start the Synapse Container: /container/start [find where name=synapse]
12. Enter the Synapse Container's shell and register a new user: register_new_matrix_user -c /data/homeserver.yaml
13. You should now be able to access your Matrix server using your RouterOS device's address. Make sure you check the official documentation for Synapse to get the latest configuration steps.
### Discord bridge

The example below is for configuring a Discord bridge, but the procedure for other types of bridges is very similar. Check the official documentation of your desired bridge for more information.

1. Create PostgreSQL Discord bridge Container environment variables:

1. /container/envs/add name=postgres_discord_envs key=POSTGRES_DB value="synapse-discord" /container/envs/add name=postgres_discord_envs key=POSTGRES_PASSWORD value=" <POSTGRE_BRIDGE_PASSWORD_HERE>" /container/envs/add name=postgres_discord_envs key=POSTGRES_USER value="synapse_discord" /container/envs/add name=postgres_discord_envs key=PGDATA value="/var/lib/postgresql/data/pgdata" /container/envs/add name=postgres_discord_envs key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc- collate='C' --lc-ctype='C'" /container/envs/add name=postgres_synapse_envs key=PGPORT value=5434
2. Create PostgreSQL Discord bridge Container mounts: /container/mounts/add name=discord_postgres_data src=disk1/discord-postgres-data dst=/var/lib/postgresql /data
3. Create a PostgreSQL Container for Discord bridge: /container/add remote-image=postgres:17.2-alpine interface=veth1 root-dir=disk1/postgres-17.2-discord mounts=discord_postgres_data envlist=postgres_discord_envs name=postgresql_discord
4. Follow the guide for HAProxy Container and setup a reverse proxy for port 8080
5. sdaCreate Discord bridge Container mount points: /container/mounts/add name=synapse_discord_data src=disk1/synapse-discord-data dst=/data
6. Create a Discord Bridge Container: /container/add remote-image=litetex/mau.mautrix.discord:latest interface=veth1 root-dir=disk1/synapse- discord mounts=synapse_discord_data name=synapse_discord
7. Start and stop the Discord bridge Container to generate files: /container/start [find where name=synapse_discord] /container/stop [find where name=synapse_discord]
8. Connect to your RouterOS device using SFTP client (for example, WinSCP when using Microsoft Windows) and adjust the file disk1/dynapse- discord/config.yaml : homeserver address: http://localhost:8008 domain: test.mt.lv software: standard async_media: true appservice address: leave default hostname: leave default port: leave default database: type: postgres uri: postgres://synapse_discord:<POSTGRE_DISCORD_PASSWORD_HERE>@172.17.0.2:5434/synapse-discord? sslmode=disable bridge: encryption: allow: true permissions: "*": relay "@your_admin_user1:test.mt.lv": admin "@your_admin_user2:test.mt.lv": admin
9.

9. Start and stop the Discord bridge Container again: /container/start [find where name=synapse_discord] /container/stop [find where name=synapse_discord]
10. Download the file disk1/synapse-discord/registration.yaml  and upload it as file disk1/synapse-data/mautrix-discord- registration.yaml
11. Connect to your RouterOS device using a SFTP client (for example, WinSCP when using Microsoft Windows) and add the following lines to disk 1/synapse-data/homeserver.yaml: ... app_service_config_files:
- /data/mautrix-discord-registration.yaml
12. Start and stop the Synapse and Discord bridge Containers: /container/start [find where name=synapse_discord] /container/stop [find where name=synapse_discord] /container/start [find where name=synapse] /container/stop [find where name=synapse]
13. Your Matrix server should not have a new user called "Discord bridge bot". Follow the official documentation to create bridged rooms.
