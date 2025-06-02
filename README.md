# Network Packet Capture and Analysis Report

**Student Name:** Anitosh Masal
**Date:** June 2, 2025
**Course/Task:** Network Packet Capture and Basic Protocol Identification

---

## Objective:

To capture live network packets using Wireshark and identify basic protocols and traffic types within the captured data.

## Tools Used:

* Wireshark (Free)
* Kali Linux Operating System (as indicated by the screenshots)
* Web Browser (Google, inferred from traffic)
* Terminal (for generating traffic)

---

## Deliverables:

* A packet capture (`.pcap` or `.pcapng`) file.
* A short report of protocols identified (this document).

---

## Step-by-Step Capture and Analysis Process

### 1. Wireshark Installation and Verification

**Action:** Wireshark was installed on the Kali Linux system. The provided screenshots confirm Wireshark is running and actively capturing/displaying packets.

**Configuration/Verification:**
*(Please insert your screenshot of Wireshark's initial screen showing the interfaces, or a terminal output confirming Wireshark installation. Example: `which wireshark` command output, or an image of the application launcher.)*
![Screenshot 1: Wireshark Installation Verification](placeholder_screenshot_1_wireshark_install_check.png)

---

### 2. Initiating Packet Capture

**Action:** Live packet capture was started on the `eth0` network interface, as indicated by the "Capturing from eth0" title in the Wireshark window.

**Configuration/Verification:**
*(Please insert a screenshot of Wireshark's initial screen showing the list of interfaces, with `eth0` selected, or a view of the capture in progress on `eth0`.)*
![Screenshot 2: Wireshark Capture Initiation](placeholder_screenshot_2_capture_start.png)

---

### 3. Generating Network Traffic

**Action:** Network traffic was generated, including web Browse activities (indicated by DNS queries to `gstatic.com`, `google.com`, `youtube.com` and TLS/TCP traffic to Google IPs) and a `ping` command (evidenced by ICMP traffic).

**Configuration/Verification:**
*(Please insert a screenshot of your web browser during activity, or your terminal showing a `ping` command running, to demonstrate traffic generation.)*
![Screenshot 3: Traffic Generation](placeholder_screenshot_3_traffic_generation.png)

---

### 4. Stopping Capture and Exporting Data

**Action:** The packet capture was stopped after a period of traffic generation, and the data was exported to a `.pcapng` file named `wireshark_eth02025-06-02_18_27_02.pcapng` as seen in the status bar of one of the screenshots.

**Configuration/Verification:**
*(Please insert a screenshot showing Wireshark with the capture stopped (red square button inactive) and/or the "Save As" dialog box just before saving, highlighting the `.pcapng` option.)*
![Screenshot 4: Capture Stopped and Exported](placeholder_screenshot_4_capture_stop_export.png)

---

## Protocols Identified and Packet Details

Based on the provided screenshots and the captured traffic, the following fundamental network protocols were identified and analyzed:

### 1. TCP (Transmission Control Protocol)

* **Description:** TCP is a core protocol of the Internet Protocol Suite, providing reliable, ordered, and error-checked delivery of a stream of octets between applications. It manages connection establishment, data segmentation, flow control, and retransmission.
* **Observed Traffic:** Numerous TCP packets were observed, primarily as part of establishing and maintaining web Browse sessions (HTTP/HTTPS). For instance, a TCP SYN packet was captured initiating a connection to a web server on port 443.
* **Example Details (from Packet No. 642 in `Screenshot_2025-06-02_18_29_23.jpg` - a TCP SYN packet):**
    * **Frame Length:** `74 bytes` (on wire), `392 bytes` (captured)
    * **Source IP:** `192.168.0.100`
    * **Destination IP:** `142.250.192.14`
    * **Source Port:** `50702`
    * **Destination Port:** `443`
    * **Flags:** `[SYN]`
    * **Sequence Number:** `0`
    * **Acknowledgement Number:** `0`

### 2. DNS (Domain Name System)

* **Description:** DNS is a hierarchical and decentralized naming system that translates human-readable domain names (e.g., `www.example.com`) into numerical IP addresses, which computers use to locate services on the network.
* **Observed Traffic:** DNS queries were evident when accessing new websites. A 'Standard query' for a domain name (`encrypted-tbn0.gstatic.com`) was captured, sent from the client to the local gateway (acting as a DNS forwarder).
* **Example Details (from Packet No. 238 in `Screenshot_2025-06-02_18_29_10.png` - a DNS Query packet):**
    * **Frame Length:** `298 bytes` (on wire), `190 bytes` (captured)
    * **Source IP:** `192.168.0.100`
    * **Destination IP:** `192.168.0.1`
    * **Source Port:** `59710`
    * **Destination Port:** `53`
    * **Transaction ID:** `0xed21`
    * **Flags:** `0x0100` (Standard query)
    * **Query Name:** `encrypted-tbn0.gstatic.com` (Type A)

### 3. TLSv1.3 (Transport Layer Security Protocol Version 1.3)

* **Description:** TLS is a cryptographic protocol designed to provide secure communication over a computer network, widely used for encrypting web traffic (HTTPS). TLSv1.3 is the latest version, offering enhanced security and performance.
* **Observed Traffic:** Secure web Browse traffic was encrypted using TLSv1.3. An initial 'Client Hello' handshake message was captured, indicating the client's intent to establish a secure connection with a web server.
* **Example Details (from Packet No. 649 in `Screenshot_2025-06-02_18_29_23.jpg` - a TLSv1.3 Client Hello packet):**
    * **Frame Length:** `226 bytes` (on wire), `392 bytes` (captured)
    * **Source IP:** `192.168.0.100`
    * **Destination IP:** `142.250.192.14`
    * **Source Port:** `50702`
    * **Destination Port:** `443`
    * **Handshake Protocol:** `Client Hello`
    * **Version (Record):** `TLS 1.2 (0x0303)` (
