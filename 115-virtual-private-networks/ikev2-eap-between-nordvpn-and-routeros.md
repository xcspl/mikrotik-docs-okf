---
type: Reference
title: "IKEv2 EAP between NordVPN and RouterOS"
description: "Starting from RouterOS v6.45, it is possible to establish IKEv2 secured tunnel to NordVPN servers using EAP authentication. This manual page explains how to configure it."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# IKEv2 EAP between NordVPN and RouterOS

Installing the root CA Finding out the server's hostname Setting up the IPsec tunnel Choosing what to send over the tunnel Option 1: Sending all traffic over the tunnel Option 2: Accessing certain addresses over the tunnel

Starting from RouterOS v6.45, it is possible to establish IKEv2 secured tunnel to NordVPN servers using EAP authentication. This manual page explains how to configure it.

### Installing the root CA

Start off by downloading and importing the NordVPN root CA certificate. /tool fetch url="https://downloads.nordvpn.com/certificates/root.der" /certificate import file-name=root.der

There should now be the trusted NordVPN Root CA certificate in System/Certificates menu. [admin@MikroTik] > /certificate print where name~"root.der" Flags: K-private-key, L-crl, C-smart-card-key, A-authority, I-issued, R-revoked, E-expired, T-trusted # NAME COMMON-NAME SUBJECT-ALT-NAME FINGERPRINT 0 T root.der_0 NordVPN Root CA 8b5a495db498a6c2c8c...

### Finding out the server's hostname

Navigate to https://nordvpn.com/servers/tools/ and find out the recommended server's hostname. In this case, it is lv20.nordvpn.com.

### Setting up the IPsec tunnel

It is advised to create a separate Phase 1 profile and Phase 2 proposal configurations to not interfere with any existing or future IPsec configuration. /ip ipsec profile add name=NordVPN /ip ipsec proposal add name=NordVPN pfs-group=none

While it is possible to use the default policy template for policy generation, it is better to create a new policy group and template to separate this configuration from any other IPsec configuration. /ip ipsec policy group add name=NordVPN /ip ipsec policy add dst-address=0.0.0.0/0 group=NordVPN proposal=NordVPN src-address=0.0.0.0/0 template=yes

Create a new mode config entry with responder=no that will request configuration parameters from the server. /ip ipsec mode-config add name=NordVPN responder=no

Lastly, create peer and identity configurations. Specify your NordVPN credentials in username and password parameters. /ip ipsec peer add address=lv20.nordvpn.com exchange-mode=ike2 name=NordVPN profile=NordVPN /ip ipsec identity add auth-method=eap certificate="" eap-methods=eap-mschapv2 generate-policy=port-strict mode-config=NordVPN peer=NordVPN policy-template-group=NordVPN username=support@mikrotik.com password=secret

Verify that the connection is successfully established. /ip ipsec active-peers print installed-sa print

Choosing what to send over the tunnel

If we look at the generated dynamic policies, we see that only traffic with a specific (received by mode config) source address will be sent through the tunnel. But a router in most cases will need to route a specific device or network through the tunnel. In such a case, we can use source NAT to change the source address of packets to match the mode config address. Since the mode config address is dynamic, it is impossible to create a static source NAT rule. In RouterOS it is possible to generate dynamic source NAT rules for mode config clients.

Option 1: Sending all traffic over the tunnel

In this example, we have a local network 10.5.8.0/24 behind the router and we want all traffic from this network to be sent over the tunnel. First of all, we have to make a new IP/Firewall/Address list which consists of our local network. /ip firewall address-list add address=10.5.8.0/24 list=local

It is also possible to specify only single hosts from which all traffic will be sent over the tunnel. Example: /ip firewall address-list add address=10.5.8.120 list=local add address=10.5.8.23 list=local

When it is done, we can assign newly created IP/Firewall/Address list to mode config configuration. /ip ipsec mode-config set [ find name=NordVPN] src-address-list=local

Verify correct source NAT rule is dynamically generated when the tunnel is established. [admin@MikroTik] > /ip firewall nat print Flags: X-disabled, I-invalid, D-dynamic 0 D ;;; ipsec mode-config chain=srcnat action=src-nat to-addresses=192.168.77.254 src-address-list=local dst-address-list=!local

Warning

Make sure the dynamic mode config address is not a part of the local network.

It is also possible to combine both options (1 and 2) to allow access to specific addresses only for specific local addresses/networks

Option 2: Accessing certain addresses over the tunnel

It is also possible to send only specific traffic over the tunnel by using the connection-mark parameter in the Mangle firewall. It works similarly as Option 1 - a dynamic NAT rule is generated based on configured connection-mark parameter under mode config.

First of all, set the connection-mark under your mode config configuration. /ip ipsec mode-config set [ find name=NordVPN] connection-mark=NordVPN

When it is done, a NAT rule is generated with the dynamic address provided by the server: [admin@MikroTik] > /ip firewall nat print Flags: X-disabled, I-invalid, D-dynamic 0 D ;;; ipsec mode-config chain=srcnat action=src-nat to-addresses=192.168.77.254 connection-mark=NordVPN

After that, it is possible to apply this connection-mark to any traffic using Mangle firewall. In this example, access to mikrotik.com and 8.8.8.8 is granted over the tunnel.

Create a new address list: /ip firewall address-list add address=mikrotik.com list=VPN add address=8.8.8.8 list=VPN

Apply connection-mark to traffic matching the created address list: /ip firewall mangle add action=mark-connection chain=prerouting dst-address-list=VPN new-connection-mark=NordVPN passthrough=yes

It is also possible to combine both options (1 and 2) to allow access to specific addresses only for specific local addresses/networks

QKD

## QKD Integration in RouterOS IPsec (PPK)

1. Introduction This manual describes the Post-Quantum Pre-shared Key (RFC9867) feature in RouterOS IPsec and its integration with Quantum Key Distribution (QKD). PPK provides forward security against quantum attacks by using keys that are either dynamically distributed or statically configured. All PPK types (static, PSK, QKD) benefit from RFC 8784 recommendations: keys should have at least 256 bits of entropy to provide ~128 bits of post-quantum security. RouterOS supports three PPK sources: Static PPK — manually configured per-peer secret. PSK (Pre-shared Key) — one-time generated keys, optionally usable only for initial IKE SA. QKD — dynamically distributed keys from a QKD server. Dynamic keys (PSK/QKD) are consumed and invalidated after use. Static keys remain valid across sessions but offer weaker security if reused.
2. Concepts PPK (Post-Quantum Pre-shared Key): An additional secret shared during IKE negotiation to resist quantum attacks. QKD: Quantum-based key distribution providing fresh symmetric keys via a Key Management Entity (KME). IKE SA vs ESP SA: IKE SA: Controls tunnel negotiation. ESP SA: Carries encrypted user data. Static vs Dynamic keys: Dynamic: ephemeral PSK or QKD-distributed secrets, used once and discarded. Static: manually set per peer, persistent across sessions.

|2.1 RouterOS PPK Sources|||
|---|---|---|
|PPK Source||Description|
|Static||Persistent, manually configured secret.|
|PSK||One-time dynamically generated pre-shared keys. Can optionally be used only for initial IKE SA (psk-ike-initial).|
|QKD||Keys pulled dynamically from a QKD server, consumed after use.|

3. Security Recommendations All PPK keys should meet RFC 8784 recommendations: ≥256 bits of entropy. Static PPK keys improve post-quantum protection if sufficiently long, but re-use reduces security. Dynamic keys (PSK/QKD) offer stronger security since they are one-time use. Synchronization failure may cause key desynchronization.
4. Two-Device Setup Overview This manual focuses on a minimal setup with two devices:

|Role|Device|Function|
|---|---|---|
|Server|RouterOS|Hosts IPsec tunnel; provides QKD/PPK key|
|Client The RouterOS server may act as a QKD client to a KME, so no third device is required.|ROS/LibreSwan|Connects to server using QKD/PPK|

5. Configuration Objects
5.1 Certificates QKD requires: CA certificate (to validate the server). SAE client certificate (for authentication to the QKD server). /certificate import file-name=ca.crt.pem /certificate import file-name=sae-server.crt.pem /certificate import file-name=sae-server.key.pem
5.2 PSK Example Generate one-time PSKs for PPK use: /ip ipsec key psk generate count=10 key-size=32 count → number of PSKs to generate. key-size → size of each key in bytes (32 bytes = 256 bits).
5.3 QKD Key Manager RouterOS server can act as a QKD client: /ip ipsec key qkd set address=10.2.3.4:8020 \ cache-size=1 \ certificate=sae-server \ key-size=32 \ kme-id=server-kme-id \ peer-sae-id=client-sae-id Parameter descriptions:

|Parameter||Description|
|---|---|---|
|cache-size||Number of keys IPsec will prefetch from QKD server.|
|cache-state||Current number of keys cached and available.|
|key-size||Requested size of each key in bytes (e.g., 32 bytes = 256 bits).|

kme-id Used for certificate validation. If not specified, KME identity will not be validated.

peer-sae-id Identifier for the peer SAE.

5.4 Profiles and Peers /ip ipsec profile add name=qkd-profile ppk=qkd /ip ipsec peer add address=10.2.1.2 exchange-mode=ike2 \ name=peer-client profile=qkd-profile proposal-check=obey /ip ipsec identity add peer=peer-client profile=qkd-profile PPK options for profiles: Option Description no PPK disabled. psk One-time PSK used for IKE and ESP rekey. psk-ike-initial PSK used only for the initial IKE SA (renamed from psk-ike-only). qkd Keys retrieved from QKD server.
5.5 Proposal / Policy /ip ipsec proposal add name=qkd-proposal auth-algorithms=sha256 \ enc-algorithms=aes-256-gcm pfs-group=modp2048 /ip ipsec policy add src-address=10.1.0.0/24 dst-address=10.2.0.0/24 \ peer=peer-client proposal=qkd-proposal tunnel=yes
6. Behaviour Dynamic keys: Pulled from /ip/ipsec/key/psk/ or QKD server, consumed once, then deleted. Static key: Configured per peer, used repeatedly. One-time dynamic keys ensure strongest protection but require synchronization. Static fallback guarantees tunnel establishment but should be long enough (≥256 bits entropy). PPK usage can optionally be restricted to IKE SA only (psk-ike-initial) to reduce key consumption.
7. Debugging and Troubleshooting To verify QKD integration and key retrieval, enable IPsec debug logging: /system logging add topics=ipsec,debug action=memory Sample debug output showing QKD key retrieval: 2025-10-11 17:32:38 ipsec,debug,packet POST /api/v1/keys/mt-aaa/enc_keys HTTP/1.1\r\n 2025-10-11 17:32:38 ipsec,debug,packet Host: 10.2.3.4\r\n 2025-10-11 17:32:38 ipsec,debug,packet {"number":1,"size":64} 2025-10-11 17:32:38 ipsec,debug,packet HTTP/1.1 200 OK\r\n 2025-10-11 17:32:38 ipsec,debug,packet {"keys":[{"key_ID":"37f4c842-dd82-4c49-8dfc-52a3793e5331","key":"m /JIEIUCzAE="}]} 2025-10-11 17:32:38 ipsec,debug,packet qkd: add to cache key 37f4c842-dd82-4c49-8dfc-52a3793e5331: 9bf24 If keys are not being added to cache, check network connectivity to the KME, certificate validation, and correct kme-id and peer-sae-id configuration.
8. Example Export (Two-Device Setup) RouterOS Server

/ip ipsec key qkd set address=10.2.3.4:8020 cache-size=1 certificate=sae-server key-size=32 \ kme-id=server-kme-id peer-sae-id=client-sae-id /ip ipsec profile add name=qkd-profile ppk=qkd /ip ipsec proposal add name=qkd-proposal auth-algorithms=sha256 enc-algorithms=aes-256-gcm pfs-group=modp2048 /ip ipsec peer add address=10.2.1.2 exchange-mode=ike2 name=peer-client profile=qkd-profile proposal-check=obey /ip ipsec identity add peer=peer-client profile=qkd-profile /ip ipsec policy add src-address=10.1.0.0/24 dst-address=10.2.0.0/24 peer=peer-client proposal=qkd-proposal tunnel=yes

Client Device

/ip ipsec key qkd set address=10.2.3.4:8020 cache-size=1 certificate=sae-client key-size=32 \ kme-id=client-kme-id peer-sae-id=server-sae-id /ip ipsec profile add name=qkd-profile ppk=qkd /ip ipsec proposal add name=qkd-proposal auth-algorithms=sha256 enc-algorithms=aes-256-gcm pfs-group=modp2048 /ip ipsec peer add address=10.2.1.1 exchange-mode=ike2 name=peer-server profile=qkd-profile proposal-check=obey /ip ipsec identity add peer=peer-server profile=qkd-profile /ip ipsec policy add src-address=10.2.0.0/24 dst-address=10.1.0.0/24 peer=peer-server proposal=qkd-proposal tunnel=yes

9. References https://datatracker.ietf.org/doc/html/rfc9867 Notes QKD as a Distribution Mechanism
QKD in RouterOS is not a new encryption method itself-it’s a key distribution mechanism. It provides dynamically generated keys via the Key Management Entity (KME), which both peers retrieve securely. Dynamic vs Static Sources

Dynamic sources: QKD-distributed keys, one-time PSKs from /ip/ipsec/key/psk/. Static sources: Per-peer configured static PPK secret. Recommendation: prefer dynamic keys for long-term security; keep a static fallback to prevent tunnel drops if dynamic keys run out. Security Guidelines (RFC 8784)

Post-quantum preshared keys should contain at least 256 bits of entropy to provide 128-bit post-quantum security. Using only one static key for IKE SA protection is possible, but carries risk if reused. Operational Considerations

Key exhaustion: one-time PSKs are consumed quickly during aggressive rekeying (IKE + ESP). QKD avoids this by continuously providing fresh keys. Hub-and-spoke topologies: dynamic PSKs need peer association to avoid desynchronization between spokes. Fallback behavior: ensure the system can gracefully switch to static PPK if dynamic keys are unavailable. Compatibility Notes

RouterOS-RouterOS: supports both PSK and QKD PPK. RouterOS-LibreSwan: works with static PPK; dynamic PSK may require custom builds. RouterOS-StrongSwan: requires adaptation, as identifiers differ between draft versions.
