# FTP - Authentication

- **Category:** Network (Root-Me)
- **Difficulty:** Easy
- **Objective:** An authenticated file exchange achieved through FTP. Recover the password used by the user.

## 1. Traffic Analysis
After opening the `.pcap` capture file in Wireshark, the `ftp` display filter is applied to isolate unencrypted traffic.

## 2. Exploitation
Analyzing the captured packets reveals the transmission of user credentials in cleartext:
- **Packet 9 (Server Response):** `331 Enter password.`
- **Packet 11 (Client Request):** `PASS cdts3500`
- **Flag:** `cdts3500`

## 3. Key Takeaways & Remediation
- **Vulnerability:** The legacy FTP protocol transmits data in cleartext, making it vulnerable to passive eavesdropping (sniffing) on the network.
- **Remediation:** Enforce secure, encrypted protocols such as SFTP or FTPS.
