---
type: Reference
title: "E-mail"
description: "An E-mail tool is a utility that allows sending e-mails from the router. The tool can be used to send regular configuration backups and exports to a network administrator."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# E-mail

Properties Sending Email Basic examples

An E-mail tool is a utility that allows sending e-mails from the router. The tool can be used to send regular configuration backups and exports to a network administrator.

Email tool uses only plain authentication and TLS encryption. Other methods are not supported.

## Properties

/tool e-mail

This submenu allows setting SMTP server that will be used.

Property Description

address (IP/IPv6 address; Default: 0.0.0.0 SMTP server's IP address. )

certificate-verification (yes yes-without-| Enables trust chain validation from local certificate store. yes-without-crl, validates a certificate, not crl no |; Default: no) performing CRL check (certificate revocation list).

from (string; Default: <>) Name or email address that will be shown as a receiver.

password (string; Default: "") sensitive Password used for authenticating to an SMTP server.

port (integer[0..65535]; Default: 25) SMTP server's port.

tls (no|yes|starttls; Default: no) Whether to use TLS encryption:

yes-sends STARTTLS and drops the session if TLS is not available on the server no-do not send STARTTLS

- sends STARTTLS and continue without TLS if a server responds that TLS is not availablestarttls
user (string; Default: "") The username used for authenticating to an SMTP server.

vrf (VRF name; default value: main) Set VRF on which service is creating outgoing connections.

Note: All server's configurations (if specified) can be overridden by send command.

## Sending Email

/tool e-mail send

Send command takes the following parameters:

Property Description

body (string; Default: ) The actual body of the email message

cc (string; Default: ) Send a copy to listed recipients. Multiple addresses allowed, use "," to separate entries

certificate-verification (yes yes-without-| Enables trust chain validation from local certificate store. yes-without-crl, validates a certificate, not crl no |; Default: no) performing CRL check (certificate revocation list).

file (File[,File]; Default: ) List of the file names that will be attached to the mail separated by a comma.

from (string; Default: ) Name or email address which will appear as the sender. If a not specified value from server's the configuration is used.

password (string; Default: ) sensitive Password used to authenticate to an SMTP server. If a not specified value from server's the configuration is used.

port (integer[0..65535]; Default: ) Port of SMTP server. If not specified, a value from server's configuration is used. the

server (IP/IPv6 address; Default: ) Ip or IPv6 address of SMTP server. If not specified, a value from server's configuration is used. the

tls (yes|no|starttls; Default: no) Whether to use TLS encryption:

yes-sends STARTTLS and drops the session if TLS is not available on the server no-do not send STARTTLS

- sends STARTTLS and continue without TLS if a server responds that TLS is not availablestarttls
subject (string; Default: ) The subject of the message.

to (string; Default: ) Destination email address. Single address allowed.

user (string; Default: ) The username used to authenticate to an SMTP server. If not specified, a value from server's the configuration is used.

## Basic examples

This example will show how to send an email with configuration export every 24hours.

1. Configure SMTP server [admin@MikroTik] /tool e-mail> set server=10.1.1.1 port=25 from="router@mydomain.com"
2. Add a new script named "export-send": /export file=export /tool e-mail send to="config@mydomain.com" subject="$[/system identity get name] export" \ body="$[/system clock get date] configuration file" file=export.rsc
3. Add scheduler to run our script: /system scheduler add on-event="export-send" start-time=00:00:00 interval=24h Send e-mail to a server using TLS/SSL encryption. For example, Google mail requires that. After the Google mail added a new security policy that does not allow 3d-party devices to authenticate using your standard Gmail password → you need to generate a 16-digit passcode ("App password") and use it instead of your Gmail password. To configure this, navigate to the "Securi ty>How you sign in to Google" section settings and:
Enable 2-Step Verification; Generate an App password.

Use the newly generated App password in the "set password=mypassword" setting shown below.

1. configure a client to connect to the correct server: /tool e-mail set address=smtp.gmail.com set port=465 set tls=yes set from=myuser@gmail.com set user=myuser set password=mypassword
2. send e-mail using send command: /tool e-mail send to=myuser@anotherdomain.com subject="email test" body="email test"
