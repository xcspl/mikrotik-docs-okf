---
type: Reference
title: "Authentication, Authorization, Accounting"
description: "trusted (no yes ) Wherever to trust certificate. If yes, certificate will be used for host certificate verification."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Authentication, Authorization, Accounting

In This Section:

|Certificates Overview Overview SCEP|Certificate Template Certificate template properties Certificate properties Sign Certificate Export Certificate Import Certificate Settings ACME client Properties Let's Encrypt certificate Built-in trust store authorities||
|---|---|---|
|/certificate|The general menu is used to manage certificates, add templates, issue certificates, and manage CRL and SCEP Clients. Certificate Template Certificate templates are used to prepare a desired certificate for signing. Certificate template is deleted right after a certificate is signed or a certificate request command is executed||
|/certificate To print out certificates:|add name=CA-Template common-name=CAtemp key-usage=key-cert-sign,crl-sign add name=Server common-name=server add name=Client common-name=client||
|trusted client client|[admin@4k11] /certificate> print detail valid=365 key-usage=key-cert-sign,crl-sign Certificate template properties During the certificate template creation process, it is possible define and configure multiple parameters to meet specific requirements.|Flags: K-private-key; L-crl; C-smart-card-key; A-authority; I-issued, R-revoked; E-expired; T - 0 name="CA-Template" key-type=rsa common-name="CAtemp" key-size=2048 subject-alt-name="" days- 1 name="Server" key-type=rsa common-name="server" key-size=2048 subject-alt-name="" days-valid=365 key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign,tls-server,tls- 2 name="Client" key-type=rsa common-name="client" key-size=2048 subject-alt-name="" days-valid=365 key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign,tls-server,tls-|
|Property||Description|
|common-name (string) copy-from (name)||Certificate common name Certificate name from which to copy general settings|

country (string) Certificate issuer country

days-valid (days Default: 365) Days certificate will be valid after signing

digest-algorithm (md5 | sha1 | sha256 | sha384 | sha512 Default: sha256 ) Certificate public key algorithm

key-size (1024 | 1536 | 2048 | 4096 | 8192 | prime256v1 | secp384r1 | secp521r1 Default: 2048) Certificate public key size

key-usage (code-sign | crl-sign | decipher-only | dvcs | encipher-only     key-cert-sign | ocsp-sign | tls-client | conten Certificate usage t-commitment | data-encipherment | digital-signature | email-protect | key-agreement | key-encipherment | timestamp | tls-server Default: digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign,tls- server,tls-client)

locality (string) Certificate issuer locality

name (string) Certificate name

organization (string) Certificate issuer organization

state (string) Certificate issuer state

subject-alt-name (DNS: | IP: | email:) Certificate subject alternative name

trusted (no | yes ) Wherever to trust certificate. If yes, certificate will be used for host certificate verification.

trust-store (all capsman dns email ipsec mqtt openflow radius sstp userman www api container dot | | | | | | | | | | | | | Specify service which can use a

|1x fetch lora netwatch ovpn tr069 wpa-eap ||| ||| ||||Default: all)||||specific certificate for certificate|
|---|---|---|---|---|---|---|---|---|
|||||||||verification or trust-chain creation (www, sstp).|
|unit (string)||||||||Certificate issuer organizational|
|||||||||unit|

1x fetch lora netwatch ovpn tr069 wpa-eap | | | | | | Default: all) specific certificate for certificate

### Certificate properties

For a signed certificate, most properties are read-only, with the exception of name, trusted, and trust-store.

Property Description

acme-status (string) ACME client status

common-name (string) Certificate common name

copy-from (name) Certificate name from which to copy general settings

country (string) Certificate issuer country

days-valid (days) Days certificate will be valid after signing

digest-algorithm (md5 | sha1 | sha256 | sha384 | sha512 ) Certificate public key algorithm

directory-url (string) ACME client directory URL

domain-names (string) ACME client used domain names

key-size (1024 | 1536 | 2048 | 4096 | 8192 | prime256v1 | secp384r1 | secp521r1) Certificate public key size

key-usage (code-sign | crl-sign | decipher-only | dvcs | encipher-only     key-cert-sign | ocsp-sign | tls-Certificate usage client | content-commitment | data-encipherment | digital-signature | email-protect | key-agreement | key-encipherment | timestamp | tls-server)

locality (string) Certificate issuer locality

organization (string) Certificate issuer organization

revoked (date) Certificate revoke time (only for certificates that are signed and revoked in specific device)

state (string) Certificate issuer state

subject-alt-name (DNS | IP | email) Certificate subject alternative name

trusted (no | yes) Wherever to trust certificate. If yes, certificate will be used for host certificate verification.

trust-store (all capsman dns email ipsec mqtt openflow radius  sstp userman www api co | | | | | | | | | | | | Specify service which can use a specific ntainer dot1x fetch lora netwatch ovpn tr069 wpa-eap | | | | | | | ) certificate for certificate verification or trust- chain creation (www, sstp).

unit (string) Certificate issuer organizational unit

serial-number (string) Certificate serial number

fingerprint (string) Certificate fingerprint

akid (string) Certificate authority ID

skid (string) Certificate subject ID

issuer (string) Certificate Authority

invalid-before (date) Date and time before which a certificate expired

invalid-after (date) Date and time after which a certificate expired

expires-after (time) Time left before expiration

key-type (string) Private key ype

ca (string) CA certificate name (shown only for certificates that are signed in specific device)

If the CA certificate is removed, all issued certificates in the chain are also removed.

### Sign Certificate

Certificates should be signed. In the following example, we will sign certificates and add CRL URL for the server certificate:

/certificate sign CA-Template sign Client sign Server ca-crl-host=192.168.88.1 name=ServerCA

Let`s check is the certificates are signed:

[admin@MikroTik] /certificate> print Flags: K-private-key; L-crl; A-authority; T-trusted Columns: NAME, COMMON-name, FINGERPRINT # NAME COMMON FINGERPRINT 0 K AT CA-Template CAtemp 0c7aaa7607a4dde1bbf33deaae6be7bac9fe4064ba47d64e8a73dcefad6cfc38 1 K AT Client client b3ff25ecb166ea41e15733a7493003f3ea66310c10390c33e98fe32364c3659f 2 KLAT ServerCA server 152b88c9d81f4b765a59e2302e01efd1fbf11ceeed6e59f4974e87787a5bb980

For a video example click here.

The time of the key signing process depends on the key size of a specific certificate. With values of 4k and higher, it might take a substantial time to sign this specific certificate on less powerful CPU-based devices.

### Export Certificate

It is possible to export client certificates with keys and CA certificates in two formats-PEM or PCKS12.

Property Description

export-passphrase (string Default: none) sensit Passphrase that will be used for exported certificate private key encryption. ive

file-name (string Default: cert_export_ Exported certificate file name. [Certificate name].crt/key/pkcs12)

type (pem | pkcs12 Default: pem) Exported certificate type.

In case of PEM, certificate will be exported with CRT extension, if export-passphrase is specified, also encrypted private KEY file will be exported.

In case of PKCS12, certificate will be exported with P12 extension, if export-passphrase is specified, exported certificate will contain encryted private key.

/certificate export-certificate CA-Template export-certificate ServerCA export-passphrase=yourpassphrase export-certificate Client export-passphrase=yourpassphrase

Exported certificates are available under the /file section:

[admin@MikroTik] > file print Columns: NAME, TYPE, SIZE, CREATION-TIME # NAME TYPE SIZE CREATION-TIME 0 skins directory jan/19/2019 00:00:04 1 flash directory jan/19/2019 01:00:00 2 pub directory jan/19/2019 02:42:16 3 cert_export_CA-Template.crt .crt file 1119 jan/19/2019 04:15:21 4 cert_export_ServerCA.crt .crt file 1229 jan/19/2019 04:15:42 5 cert_export_ServerCA.key .key file 1858 jan/19/2019 04:15:42 6 cert_export_Client.crt .crt file 1164 jan/19/2019 04:15:55 7 cert_export_Client.key .key file 1858 jan/19/2019 04:15:55

Exporting certificates requires "sensitive" user policy.

### Import Certificate

To import certificates, certificates must be uploaded to a device using one of the file upload methods.

Certificates must be imported as a file.

Supported are PEM, DER, CRT, PKCS12 formats.

Property Description

name (string Default: file-name_number) A certificate name that will be shown in the certificate manager

|||file-name (string) ||trusted (yes | no Default: yes) | ||passphrase (string Default: none) sensitive | ||trust-store (all capsman dns email ipsec mqtt openflow radius | ||| w api container dot1x fetch lora netwatch ovpn tr069 wpa-eap ||| ||| ||| |||| | sstp userman ww | Default: all)|||A file name that will be imported File passphrase if there is such Adds trusted flag for imported certificate Specify service which can use a specific certificate for certificate verification or trust-chain creation (www, sstp).|
|---|---|---|---|---|---|---|---|---|---|---|---|---|
||Settings|passphrase=file_passphrase certificates-imported: 2 private-keys-imported: 1 files-imported: 1 decryption-failures: 0 keys-with-no-certificate: 0 Columns: NAME, COMMON-NAME 0 KT name_example cert 1 T name_example_1 ca|[admin@MikroTik] > /certificate/print Flags: K-PRIVATE-KEY; T-TRUSTED||/certificate settings allows configuring Certificate Revocation List (CRL) settings. By default, CRL is not utilized, and certificates are not verified for revocation status.||# NAME COMMON-NAME|[admin@MikroTik] > /certificate/import file-name=certificate_file_name name=name_example|||||
||Property | eap | untrusted service.|| crl-download (yes | no Default: no) crl-store (ram | sytem Default: ram) crl-use (yes | no Default: no)|| | | Default: default)|||builtin-trust-store (all default capsman dns email ipsec mqtt openflow radius | ||| sstp userman www api container dot1x fetch lora netwatch ovpn tr069 wpa- ||| ||| ||| ||| | chain should be installed into a device-starting from Root CA, intermediate CA (if there are such), and certificate that is used for specific|| | | If /certificate/settings/set crl-use is set to yes, RouterOS will check CRL for each certificate in a certificate chain, therefore, an entire certificate|Description Services that can use built-in trust store authorities for certificate verification. The current defaults: fetch mqtt email netwatch container lora dns www reverse-proxy Whether to automatically download/update CRL Where to store downloaded CRL information CRL will be automatically renewed every hour for certificates which have "trusted=yes" using http protocol (ldap and ftp is currently unsupported) Whether to use CRL|

|An example on importing a root certificate. ACME client net domain name, DNS-01 challange is used. Properties|The ACME client automates the acquisition and renewal of multiple TLS certificates via ACME. To add a new ACME client via CLI, use the command /certificate add-acme. Existing ACME clients appear in the Certificates view and are marked with the (acme-manage) flag. Certificates are automatically renewed when 80% of their validity period has elapsed. If the certificate is not retrieved during the initial setup, a new ACME client must be added.|a Domain names must resolve to the router, and TCP port 80 must be accessible from the WAN (HTTP-01 challange is used). For example.sn.mynetname.|
|---|---|---|
|Property|Description||
|directory-url (string) domain-names (string) eab-hmac-key (string) eab-kid (string) name (string) Let's Encrypt certificate /directory) and domain-name. /ip/cloud/get dns-name]" dns-name]|ACME directory URL comma separated list of domain names HMAC key for ACME External Account Binding Key identifier ACME client name|To retrieve Let's Encrypt certificate with automatic certificate renewal, must manually provide ACME directory URL ([https://acme-v02.api.letsencrypt.org](https://acme-v02.api.letsencrypt.org) /certificate/add-acme directory-url=[https://acme-v02.api.letsencrypt.org/directory](https://acme-v02.api.letsencrypt.org/directory) domain-names=[DOMAIN_NAME] To generate Let's Encrypt certificate for /ip cloud name (ie. example.sn.mynetname.net), as domain-name provide dns-name from /ip/cloud menu or use "[ /certificate/add-acme directory-url=[https://acme-v02.api.letsencrypt.org/directory](https://acme-v02.api.letsencrypt.org/directory) domain-names=[/ip/cloud/get|
|SCEP SCEP client in RouterOS will:|can be protected if necessary (ciphered or signed using a received public key). get CA certificate from CA server or RA (if used); user should compare the fingerprint of the CA certificate or if it comes from the right server; generate a self-signed certificate with a temporary key; send a certificate request to the server; if the server responds with status x, then the client keeps requesting until the server sends an error or approval.|SCEP is using HTTP protocol and base64 encoded GET requests. Most of the requests are without authentication and cipher, however, important ones|

The SCEP server supports the issuance of one certificate only. RouterOS supports also renew and next-ca options:

renew-the possibility to renew the old certificate automatically with the same CA. next-ca-possibility to change the current CA certificate to the new one.

The client polls the server for any changes, if the server advertises that the next-ca is available, then the client may request the next CA or wait until CA almost expires and then request the next-ca.

The RouterOS client by default will try to use POST, AES, and SHA256 if the server advertises that. If the above algorithms are not supported, then the client will try to use 3DES, DES and SHA1, MD5.

SCEP certificates are renewed when 3/4 of their validity time has passed.

## Built-in trust store authorities

RouterOS contains list of built-in root certificate authorities that specific services can use for host certificate verification.

List of services that can use built-in root certificate authorities can be found here.

It is possible to use DoH, download Adlist from URL or use fetch tool with certificate validation without the need to manually import the relevant root certificate.

The list of built-in root certificate authorities is accessible in System → Certificates → Built In CA
