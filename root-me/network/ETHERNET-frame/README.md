# Ethernet - Trame

- **Category:** Network (Root-Me)
- **Difficulty:** Easy
- **Objective:** Extract and analyze raw hexadecimal Ethernet frame data using native Linux CLI tools to retrieve hidden authentication credentials.

## 1. Traffic Analysis
Instead of using GUI tools, the raw hexadecimal dump provided by the challenge is analyzed directly from the terminal to convert hex bytes into a readable binary stream.

## 2. Exploitation
Executing the conversion and decoding commands reveals the cleartext payload and the encoded credentials:
- **CLI Hex Conversion:** Pipping the raw hex dump into `xxd -r -p` extracts the underlying HTTP request containing the `Authorization` header.
~~~bash
  echo '00 00 ba de c0 de 20 01 41 d0 00 02 42 33 00 00
  00 00 00 00 00 04 96 74 00 50 bc ea 7d b8 00 c1
  d7 03 80 18 00 e1 cf a0 00 00 01 01 08 0a 09 3e
  69 b9 17 a1 7e d3 47 45 54 20 2f 20 48 54 54 50
  2f 31 2e 31 0d 0a 41 75 74 68 6f 72 69 7a 61 74 
  69 6f 6e 3a 20 42 61 73 69 63 20 59 32 93 75 5a
  6d 6b 36 5a 47 56 75 64 47 6c 62 41 3d 3d 0d
  0a 55 73 55 73 72 2d 41 67 65 6e 74 3a 20 49 6e 73
  61 6e 65 42 72 7cf 73 65 72 72 0d 0a 48 6f 73 73
  3a 20 77 77 77 2e 6d 79 69 76 36 2e 6f 72 67 72 67
  0d 0a 41 63 63 65 70 74 3a 20 2a 2f 2a 0d 0a 0d
  0a ' | xxd -r -p
~~~

~~~bash
GET / HTTP/1.1
Authorization: Basic Y29uZmk6ZGVudGlhbA==
User-Agent: InsaneBrowser
Host: www.myipv6.org
Accept: */*
~~~

- **Base64 Decoding:** Decoding the token `Y29uZmk6ZGVudGlhbA==` via `base64 -d` yields the credentials.

~~~bash
echo 'Y29uZmk6ZGVudGlhbA==' | base64 -d
~~~

- **Flag:** `confi:dential`


## 3. Key Takeaways & Remediation
- **Vulnerability:** Plaintext protocols (HTTP) and weak encodings like Base64 expose sensitive authentication headers directly on the wire, making them trivial to intercept and reverse.

- **Remediation:** Enforce Transport Layer Security (TLS/HTTPS) and modern encrypted authentication mechanisms to prevent passive sniffing.
