# Ethernet - Trame

- **Category:** Network (Root-Me)

- **Difficulty:** Easy

- **Objective:** Extract and analyze raw hexadecimal Ethernet frame data using native Linux CLI tools to retrieve hidden authentication credentials.


## 1. Traffic Analysis
Instead of using GUI tools, the raw hexadecimal dump provided by the challenge is analyzed directly from the terminal to convert hex bytes into a readable binary stream.

## 2. Exploitation
Executing the conversion and decoding commands reveals the cleartext payload and the encoded credentials:
- **CLI Hex Conversion:** Pipping the raw hex dump into `xxd -r -p` extracts the underlying HTTP request containing the `Authorization` header.
- **Base64 Decoding:** Decoding the token `Y29uZmk6ZGVudGlhbA==` via `base64 -d` yields the credentials.
- **Flag:** `confi:dential`


## 3. Key Takeaways & Remediation
- **Vulnerability:** Plaintext protocols (HTTP) and weak encodings like Base64 expose sensitive authentication headers directly on the wire, making them trivial to intercept and reverse.

- **Remediation:** Enforce Transport Layer Security (TLS/HTTPS) and modern encrypted authentication mechanisms to prevent passive sniffing.
