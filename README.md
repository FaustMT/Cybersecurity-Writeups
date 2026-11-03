# Telnet - Authentication

- **Category:** Network (Root-Me)
- **Difficulty:** Easy
- **Objective:** Recover compromised credentials from an unencrypted Telnet network stream.

## 1. Traffic Analysis
After opening the `.pcap` capture file in Wireshark, the `telnet` display filter is applied to isolate the unencrypted Telnet traffic. Using the "Follow TCP Stream" feature allows us to read the interactive terminal session in cleartext.

## 2. Exploitation
Analyzing the captured stream reveals the interactive login process:
- **Username entered:** `ffakee` (transmitted character by character)
- **Password prompt response:** `user`
- **Flag / Password:** `user`

## 3. Key Takeaways & Remediation
- **Vulnerability:** Telnet is an unencrypted legacy protocol. All keystrokes, commands, and credentials are sent in cleartext across the network, making them trivially intercepted via sniffing.
- **Remediation:** Replace Telnet entirely with **SSH** (Secure Shell), which encrypts the entire communication session end-to-end.
