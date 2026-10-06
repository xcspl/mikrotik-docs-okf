---
type: Reference
title: "Fetch"
description: "Fetch is one of the console tools in MikroTik RouterOS. It is used to copy files to/from a network device via HTTP, HTTPS, FTP or SFTP. It can also be used to send POST/GET requests and send any kind of data to a remote ."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Fetch

Summary Properties Configuration Examples Sending information to a remote host Return value to a variable Example 1 Example 2

## Summary

Fetch is one of the console tools in MikroTik RouterOS. It is used to copy files to/from a network device via HTTP, HTTPS, FTP or SFTP. It can also be used to send POST/GET requests and send any kind of data to a remote server. In HTTPS mode by default, no certificate checks are made, setting check- certificate to yes enables trust chain validation from the local certificate store (can be used only in HTTPS mode).

## Properties

Property Description

address (string; Default: ) IP address of the device to copy file from. Also at the end of the address you can specify "@vrf_name" in order to run fetch on particular VRF. You can skip specifying address and specify only VRF on this parameter, if you use URL parameter.

as-value (set | not-set; Store the output in a variable, should be used with the output property. Default: not-set)

ascii (yes | no; Default: no) Can be used with FTP and TFTP

certificate (string; Default: ) Certificate that should be used for host verification. Can be used only in HTTPS mode.

check-certificate (yes | Enables trust chain validation from local certificate store. yes-without-crl, validates a certificate, not performing CRL yes-without-crl | no; check (certificate revocation list).  Can be used only in HTTPS mode. Default: no)

dst-path (string; Default: ) Destination path. Can be used to download file directly into an external disk, for example.

duration (time; Default: ) Time how long fetch should run.

host (string; Default: ) A domain name or virtual domain name (if used on a website, from which you want to copy information). For example, address=wiki.mikrotik.com host=forum.mikrotik.com

In this example the resolved ip address is the same (66.228.113.27), but hosts are different.

http-auth-scheme (basic|di HTTP authentication scheme gest; Default: basic)

http-method (delete|get|he HTTP method to use ad|post|put|patch; Default: get)

http-data (string; Default: ) The data, that is going to be sent. Data limit is 64Kb.

http-header-field (string; List of all header fields and their values, in the form of http-header-field="h1:fff,h2:yyy" or http-header- Default: *empty*) field="h:fff\\,yyy" (within a single header multiple values need to be "escaped" using two backlashes).

http-content-encoding (defl Encodes the payload using gzip or deflate compression and adds a corresponding Content-Encoding header. Usable ate|gzip; Default: *empty*) for HTTP POST and PUT only.

http-max-redirect-count (int Allows to follow redirects the specified number of times. eger; Default: 2)

|http-percent-encoding (yes | no; Default: no) http-version (http1_1 http2; Default: http1_1) idle-timeout (time; Default: 10s) keep-result (yes | no; Default: yes) mode (ftp|http|https|sftp|tftp; Default: http) output (none|file|user|user- with-headers; Default: file) password (string; Default: anonymous) port (integer; Default:) src-address (ip address; Default:) src-path (string; Default:) upload (yes | no; Default: no) url (string; Default:) user (string; Default: anony mous)|| Configuration Examples|Enables HTTP percent encoding Specifies which HTTP version to use HTTP2 supported only on ARM64 and x86/CHR devices Idle timeout since last read/write action. If yes, creates an input file. Choose the protocol of connection-http, https, ftp, sftp or tftp. Mode option is deprecated. To specify a protocol that you wish to use, we advise using "url" parameter instead (for example, like this "url=sftp://your_IP_address"). Sets where to store the downloaded data. none-do not store downloaded data file-store downloaded data in a file user-store downloaded data in the data variable (variable limit is 64Kb) user-with-headers-store downloaded data and headers in the data variable (variable limit is 64Kb (20Kb for downloaded data, 44Kb for headers)) Password, which is needed for authentication to the remote device. Connection port. Source address that is used to establish connection. Can be used only HTTP/S and SFTP modes. Title of the remote file you need to copy. Only (S)FTP modes support upload. If enabled then fetch will be used to upload files to a remote server. Requires src- path and dst-path parameters to be set. URL pointing to file. Can be used instead of address and src-path parameters. Username, which is needed for authentication to the remote device. The following example shows how to copy the file with filename "conf.rsc" from a device with ip address 192.168.88.2 by FTP protocol and save it as file with filename "123.rsc". User and password are needed to login into the device.|
|---|---|---|
|host="" keep-result=yes|Example to upload file to another router: Another file download example that demonstrates the usage of url property.|[admin@MikroTik] /tool> fetch address=192.168.88.2 src-path=conf.rsc \ user=admin mode=ftp password=123 dst-path=123.rsc port=21 \ [admin@MikroTik] /tool> fetch address=192.168.88.2 src-path=conf.rsc \ user=admin mode=ftp password=123 dst-path=123.rsc upload=yes|

[admin@MikroTik] /> /tool fetch url="https://www.mikrotik.com/img/netaddresses2.pdf" mode=http status: finished

[admin@test_host] /> /file print # NAME TYPE SIZE CREATION-TIME ... 5 netaddresses2.pdf .pdf file 11547 jun/01/2010 11:59:51

It is also possible to transfer files over some specific VRF. You can specify VRF at the end of the URL address part (url="http://192.168.88.2@vrf1/..." - will not work for SFTP), address property combined with address and separated with "@" (address=192.168.88.2@vrf1) or simply as address parameter with "@" symbol before the VRF name as in the example (uses address from URL and combines it with VRF name from address parameter):

[admin@MikroTik] /> /tool/fetch url="sftp://192.168.88.2" address=@test src-path=test.txt user=admin password="" upload=yes

status: finished

### Sending information to a remote host

It is possible to use an HTTP POST request to send information to a remote server, that is prepared to accept it. In the following example, we send geographic coordinates to a PHP page:

/tool/fetch http-method=post http-header-field="Content-Type:application/json" http-data="{\"lat\":\"56.12\",\" lon\":\"25.12\"}" url="https://testserver.lv/index.php"

In this example, the data is uploaded as a file. Important note, since variable data comes from a file, a file can only be in size up to 4KB. This is a limitation of RouterOS variables.

/export file=export.rsc

:global data [/file get [/file find name=export.rsc] contents];
:global $url "https://prod-51.westeurope.logic.azure.com:443/workflows/blabla/triggers/manual/paths/invoke....";

/tool fetch mode=https http-method=put http-data=$data url=$url

### Return value to a variable

It is possible to save the result of the fetch command to a variable.

Example 1

It's possible to trigger a certain action based on the result that an HTTP page returns. You can find a very simple example below that disables ether2 whenever a PHP page returns "0":

{ :local result [/tool fetch url=https://10.0.0.1/disable_ether2.php as-value output=user]; :if ($result->"status" = "finished") do={ :if ($result->"data" = "0") do={ /interface ethernet set ether2 disabled=yes; } else={ /interface ethernet set ether2 disabled=no; } } }

Example 2

In case fetch fails, it is possible to access error code ("code") and returned HTTP headers ("http-headers").

:onerror err,attr in={ /tool/fetch http://127.0.0.1/error as-value} do={:put $err;:put ($attr->"code");:put ($attr->"http-headers")} failure: Status 404, Not Found 404 Cache-Control: no-store;Connection: Keep-Alive;Content-Length: 99;Content-Type: text/html;Date: Tue, 09 Dec 2025 13:27:44 GMT;Expires: 0;Pragma: no-cache;X-Frame-Options: sameorigin
