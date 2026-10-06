---
type: Reference
title: "Python3 Example"
description: "These examples are meant for you to make your own Python3 based RouterOS API client, they are just templates, or starting points. Use them at your own risk."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Python3 Example

These examples are meant for you to make your own Python3 based RouterOS API client, they are just templates, or starting points. Use them at your own risk.

### Minimal example

Bare minimum, no SSL, no error handling, timeouts or graceful shutdowns.

python3 python_api_minimal.py 192.168.88.1 admin "" /system/resource/print python3 python_api_minimal.py 10.0.0.1 admin secret /interface/print

#!/usr/bin/python3 """ Minimal MikroTik RouterOS API example. Usage: python_api_minimal.py <ip> <user> <password> <command> Example: python_api_minimal.py 192.168.88.1 admin "" /system/resource/print """

import socket, hashlib, binascii, sys

def write_word(s, w): data = w.encode('utf-8') length = len(data) if length < 0x80:

s.send(length.to_bytes(1, 'big')) elif length < 0x4000:
s.send((length | 0x8000).to_bytes(2, 'big')) elif length < 0x200000:
s.send((length | 0xC00000).to_bytes(3, 'big')) elif length < 0x10000000:
s.send((length | 0xE0000000).to_bytes(4, 'big')) else:
s.send(b'\xF0' + length.to_bytes(4, 'big'))
s.send(data) def read_word(s): c = s.recv(1)[0] if (c & 0x80) == 0x00: length = c elif (c & 0xC0) == 0x80: length = ((c & 0x3F) << 8) + s.recv(1)[0] elif (c & 0xE0) == 0xC0: length = ((c & 0x1F) << 16) + (s.recv(1)[0] << 8) + s.recv(1)[0] elif (c & 0xF0) == 0xE0: length = ((c & 0x0F) << 24) + (s.recv(1)[0] << 16) + (s.recv(1)[0] << 8) + s.recv(1)[0] else: length = (s.recv(1)[0] << 24) + (s.recv(1)[0] << 16) + (s.recv(1)[0] << 8) + s.recv(1)[0] return s.recv(length).decode('utf-8') if length else '' def send_sentence(s, words): for w in words: write_word(s, w) write_word(s, '') def read_sentence(s): r = [] while True: w = read_word(s) if w == '': return r
r.append(w) def login(s, user, pwd): send_sentence(s, ['/login', '=name=' + user, '=password=' + pwd]) response = read_sentence(s) if response[0] == '!done' and len(response) > 1 and response[1].startswith('=ret='):

# Legacy auth (RouterOS < 6.43) challenge = binascii.unhexlify(response[1][5:]) md = hashlib.md5() md.update(b'\x00' + pwd.encode('utf-8') + challenge) send_sentence(s, ['/login', '=name=' + user, '=response=00' + md.hexdigest()]) read_sentence(s)

if __name__ == '__main__': ip, user, pwd, cmd = sys.argv[1], sys.argv[2], sys.argv[3], sys.argv[4]

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.connect((ip, 8728)) login(s, user, pwd) send_sentence(s, [cmd]) while True: sentence = read_sentence(s) for word in sentence: print(word) if sentence[0] == '!done': break
s.close()
Example with SSL and validation MikroTik RouterOS API Client

Usage: python_api_fixed.py <ip-address> [username] [password] [secure] [port] [verify_ssl]

Arguments: ip-address : Router IP address (required) username : Login username (default: admin) password : Login password (default: empty) secure : Use SSL/TLS-true/false/1/0/yes/no (default: false) port : API port (default: 8728 or 8729 for secure) verify_ssl : Verify SSL certificate-true/false (default: false)

Examples: python_api_fixed.py 10.0.0.1 python_api_fixed.py 10.0.0.1 admin MyPassword123 python_api_fixed.py 10.0.0.1 admin MyPassword123 true python_api_fixed.py 10.0.0.1 admin MyPassword123 true 8729 python_api_fixed.py 10.0.0.1 admin MyPassword123 true 8729 true

After connecting, type API commands, pressing Enter after each word. Press Enter twice (empty line) to send the command to the router.

#!/usr/bin/python3 # -*- coding: utf-8 -*-

import sys import binascii import socket import select import ssl import hashlib import re

SENSITIVE_PATTERNS = re.compile(r'(=password=|=response=)(.+)', re.IGNORECASE)

def mask_sensitive(word): """Mask sensitive data in API words for logging""" return SENSITIVE_PATTERNS.sub(r'\1***', word)

class ApiRos: """RouterOS API client"""

def __init__(self, sk): self.sk = sk

def login(self, username, pwd): for repl, attrs in self.talk(["/login", "=name=" + username, "=password=" + pwd]): if repl == '!trap': return False elif '=ret' in attrs: # Legacy authentication (RouterOS < 6.43) chal = binascii.unhexlify((attrs['=ret']).encode('utf-8')) md = hashlib.md5() md.update(b'\x00') md.update(pwd.encode('utf-8')) md.update(chal) for repl2, attrs2 in self.talk(["/login", "=name=" + username, "=response=00" + binascii.hexlify(md.digest()).decode('utf-8')]): if repl2 == '!trap': return False return True

def talk(self, words): if self.writeSentence(words) == 0: return [] r = [] while True: i = self.readSentence() if len(i) == 0: continue reply = i[0] attrs = {} for w in i[1:]: j = w.find('=', 1) if j == -1: attrs[w] = '' else: attrs[w[:j]] = w[j+1:]

r.append((reply, attrs)) if reply == '!done': return r def writeSentence(self, words): ret = 0 for w in words: self.writeWord(w) ret += 1 self.writeWord('') return ret def readSentence(self): r = [] while True: w = self.readWord() if w == '': return r
r.append(w) def writeWord(self, w): print("<<< " + mask_sensitive(w)) data = w.encode('utf-8') self.writeLen(len(data)) self.writeBytes(data) def readWord(self): ret = self.readStr(self.readLen()) print(">>> " + mask_sensitive(ret)) return ret

def writeLen(self, l): if l < 0x80: self.writeBytes(l.to_bytes(1, 'big')) elif l < 0x4000: self.writeBytes((l | 0x8000).to_bytes(2, 'big')) elif l < 0x200000: self.writeBytes((l | 0xC00000).to_bytes(3, 'big')) elif l < 0x10000000: self.writeBytes((l | 0xE0000000).to_bytes(4, 'big')) else: self.writeBytes(b'\xF0' + l.to_bytes(4, 'big'))

def readLen(self): c = ord(self.readBytes(1)) if (c & 0x80) == 0x00: pass elif (c & 0xC0) == 0x80: c &= ~0xC0 c <<= 8 c += ord(self.readBytes(1)) elif (c & 0xE0) == 0xC0: c &= ~0xE0 c <<= 8 c += ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) elif (c & 0xF0) == 0xE0: c &= ~0xF0 c <<= 8 c += ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) elif (c & 0xF8) == 0xF0: c = ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) c <<= 8 c += ord(self.readBytes(1)) return c

def writeBytes(self, data): """Write raw bytes to socket""" n = 0 while n < len(data): r = self.sk.send(data[n:]) if r == 0: raise RuntimeError("connection closed by remote end") n += r

def readBytes(self, length): """Read exact number of bytes from socket""" ret = b'' while len(ret) < length: s = self.sk.recv(length-len(ret)) if s == b'': raise RuntimeError("connection closed by remote end") ret += s return ret

def readStr(self, length): """Read string of specified length from socket""" data = self.readBytes(length) return data.decode('utf-8', errors='replace')

def parse_bool(value): """Parse string to boolean"""

return value.lower() in ('true', '1', 'yes', 'on')

def parse_port(value): """Parse and validate port number""" try: port = int(value) except ValueError: raise ValueError(f"Invalid port number: {value}") if not 1 <= port <= 65535: raise ValueError(f"Port must be between 1 and 65535, got {port}") return port

def open_socket(dst, port, secure=False, verify_ssl=False): """Open socket connection to RouterOS device""" res = socket.getaddrinfo(dst, port, socket.AF_UNSPEC, socket.SOCK_STREAM) af, socktype, proto, canonname, sockaddr = res[0] s = socket.socket(af, socktype, proto)

try: if secure: context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT) context.minimum_version = ssl.TLSVersion.TLSv1_2 if verify_ssl: context.verify_mode = ssl.CERT_REQUIRED context.load_default_certs() else: context.check_hostname = False context.verify_mode = ssl.CERT_NONE s = context.wrap_socket(s, server_hostname=dst)

s.connect(sockaddr) return s except:
s.close() raise def main(): if len(sys.argv) < 2: print(__doc__) sys.exit(1) dst = sys.argv[1] user = "admin" passw = "" secure = False port = 0 verify_ssl = False arg_nr = len(sys.argv) if arg_nr > 2: user = sys.argv[2] if arg_nr > 3: passw = sys.argv[3] if arg_nr > 4: secure = parse_bool(sys.argv[4]) if arg_nr > 5: try: port = parse_port(sys.argv[5]) except ValueError as e: print(f"Error: {e}") sys.exit(1) if arg_nr > 6: verify_ssl = parse_bool(sys.argv[6]) if port == 0: port = 8729 if secure else 8728 try:

s = open_socket(dst, port, secure, verify_ssl) except socket.gaierror as e: print(f"Error: Could not resolve hostname '{dst}': {e}") sys.exit(1) except socket.error as e: print(f"Error: Could not connect to {dst}:{port}: {e}") sys.exit(1) except ssl.SSLError as e: print(f"Error: SSL connection failed: {e}") sys.exit(1)

apiros = ApiRos(s)

if not apiros.login(user, passw): print("Error: Login failed")

s.close() sys.exit(1) print(f"Connected to {dst}:{port} as {user}") print("Enter API commands (empty line to send, Ctrl+C to exit)") inputsentence = [] try: while True: r = select.select([s, sys.stdin], [], [], None) if s in r[0]: apiros.readSentence() if sys.stdin in r[0]: # Read line from input and strip newline l = sys.stdin.readline() if l == '': # EOF reached break l = l.rstrip('\n\r') # Empty line sends the sentence if l == '': if inputsentence: apiros.writeSentence(inputsentence) inputsentence = [] else: inputsentence.append(l) except KeyboardInterrupt: print("\nDisconnecting...") finally:
s.close() if __name__ == '__main__': main()
