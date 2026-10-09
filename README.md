# 🛡️ Basic Network Sniffer Using Python and Scapy

![CodeAlpha](https://img.shields.io/badge/Internship-CodeAlpha-blue)
![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Scapy](https://img.shields.io/badge/Library-Scapy-green)
![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux-557C94?logo=kalilinux&logoColor=white)
![Network Security](https://img.shields.io/badge/Focus-Network%20Security-orange)
![Status](https://img.shields.io/badge/Project-Basic%20Packet%20Sniffer-success)
![License](https://img.shields.io/badge/Use-Educational-lightgrey)

---

## 📌 Project Overview

The **Basic Network Sniffer** is a Python-based cybersecurity project developed as part of the **CodeAlpha Cyber Security Internship, Task 1**.

The purpose of this project is to demonstrate how network packets can be captured and analyzed to understand network communication and the structure of transmitted data.

The application uses **Python and Scapy** to capture network packets and display useful information, including source and destination IP addresses, protocols, port numbers, and available packet payloads.

The project was developed for educational purposes in a Kali Linux environment to build practical knowledge of network traffic analysis and network security.

## 🎯 Project Objectives

The main objectives of this project are to:

- Develop a basic network packet sniffer using Python.
- Capture network packets from an authorized network interface.
- Identify source and destination IP addresses.
- Recognize common protocols such as TCP, UDP, and ICMP.
- Display source and destination port numbers where applicable.
- Inspect available packet payload data.
- Understand how data travels across a network.
- Develop practical skills in network analysis and cybersecurity.

## 🛠️ Technologies and Tools

| Technology | Purpose |
|---|---|
| Python 3 | Programming language |
| Scapy | Packet capture and analysis |
| Kali Linux | Development and testing environment |
| Linux Terminal | Running commands and scripts |
| Git | Version control |
| GitHub | Source code hosting and documentation |

## 🖥️ Project Environment

The project is designed to run in the following environment:

- Operating system: Kali Linux
- Programming language: Python 3
- Packet manipulation library: Scapy
- Execution environment: Linux terminal
- Network access: Authorized test network

---

## ⚙️ Installation and Setup

### Step 1: Update the package list

Open the Kali Linux terminal and run:

```bash
sudo apt update
```

### Step 2: Check the Python version

```bash
python3 --version
```

### Step 3: Install Scapy

```bash
sudo apt install python3-scapy -y
```

### Step 4: Verify the Scapy installation

```bash
python3 -c "from scapy.all import sniff; print('Scapy installed successfully')"
```

Expected output:

```text
Scapy installed successfully
```

---

## 📂 Project Structure

The recommended repository structure is:

```text
CodeAlpha_Basic_Network_Sniffer/
│
├── network_sniffer.py
├── README.md
└── screenshots/
    ├── python-version.png
    ├── scapy-installation.png
    ├── source-code.png
    └── packet-capture.png
```

The screenshot files should be added after capturing the actual results from the Kali Linux environment.

---

## 🐍 Python Implementation

### Step 1: Create the project directory

```bash
mkdir -p ~/CodeAlpha_Basic_Network_Sniffer/screenshots
cd ~/CodeAlpha_Basic_Network_Sniffer
```

### Step 2: Create the Python script

```bash
nano network_sniffer.py
```

Paste the following code into the file:

```python
#!/usr/bin/env python3

"""
Basic Network Sniffer
CodeAlpha Cyber Security Internship - Task 1

Purpose:
Capture and analyze network packets in an authorized
laboratory environment.

Features:
- Displays source and destination IP addresses.
- Identifies common network protocols.
- Displays TCP and UDP port numbers.
- Displays a limited preview of available payload data.
"""

from scapy.all import sniff, IP, TCP, UDP, ICMP, Raw


def packet_callback(packet):
    """Display relevant information about a captured packet."""

    print("\n" + "=" * 60)
    print("PACKET CAPTURED")
    print("=" * 60)

    if IP not in packet:
        print("Non-IP packet detected.")
        return

    source_ip = packet[IP].src
    destination_ip = packet[IP].dst

    print(f"Source IP       : {source_ip}")
    print(f"Destination IP  : {destination_ip}")

    if TCP in packet:
        protocol = "TCP"
    elif UDP in packet:
        protocol = "UDP"
    elif ICMP in packet:
        protocol = "ICMP"
    else:
        protocol = "Other IP"

    print(f"Protocol        : {protocol}")

    if TCP in packet:
        print(f"Source Port     : {packet[TCP].sport}")
        print(f"Destination Port: {packet[TCP].dport}")

    elif UDP in packet:
        print(f"Source Port     : {packet[UDP].sport}")
        print(f"Destination Port: {packet[UDP].dport}")

    if Raw in packet:
        payload = bytes(packet[Raw].load)

        # Display a limited, printable preview only.
        preview = payload[:80].decode(
            "utf-8",
            errors="replace"
        )

        print(f"Payload Preview : {preview!r}")

    else:
        print("Payload Preview : No Raw payload layer detected.")


def main():
    """Start packet capture until the user stops the program."""

    print("=" * 60)
    print("BASIC NETWORK SNIFFER")
    print("CodeAlpha Cyber Security Internship - Task 1")
    print("=" * 60)

    print("Starting packet capture...")
    print("Press CTRL+C to stop.")

    try:
        sniff(
            prn=packet_callback,
            store=False
        )

    except KeyboardInterrupt:
        print("\nPacket capture stopped by the user.")

    except PermissionError:
        print(
            "\nPermission denied. Run the program with "
            "the required privileges."
        )

    except Exception as error:
        print(f"\nAn error occurred: {error}")


if __name__ == "__main__":
    main()
```

Save the file using:

1. `CTRL + O`
2. Press `Enter`
3. `CTRL + X`

### Step 3: Verify the source file

```bash
cat network_sniffer.py
```

### Step 4: Check the Python syntax

```bash
python3 -m py_compile network_sniffer.py
```

If the command produces no output, the file has passed the Python syntax compilation check.

---

## 🚀 Running the Network Sniffer

### Step 1: Start the sniffer

On Kali Linux, packet capture may require elevated privileges:

```bash
sudo python3 network_sniffer.py
```

The program should display:

```text
============================================================
BASIC NETWORK SNIFFER
CodeAlpha Cyber Security Internship - Task 1
============================================================
Starting packet capture...
Press CTRL+C to stop.
```

### Step 2: Generate controlled test traffic

Open a second terminal window and run:

```bash
ping -c 4 10.0.0.1
```

Use this example only if `10.0.0.1` is your own gateway or an authorized test host. Otherwise, replace it with the IP address of a machine you are permitted to test.

You can also visit a website normally through your browser to generate traffic on your own device.

### Step 3: Observe captured packets

Return to the terminal running the sniffer.

Depending on the traffic visible to the selected interface, you may see output resembling:

```text
============================================================
PACKET CAPTURED
============================================================
Source IP       : 10.0.0.3
Destination IP  : 10.0.0.1
Protocol        : ICMP
Payload Preview : No Raw payload layer detected.
```

**Note:** The addresses above are illustrative. Actual output depends on your network configuration and captured traffic.

### Step 4: Stop the program

Press:

```text
CTRL + C
```

The program will stop packet capture.

---

## 🔍 Understanding the Packet Information

### 1. Source IP Address

The source IP identifies the IP address from which a packet originates.

### 2. Destination IP Address

The destination IP identifies the intended IP recipient of the packet.

### 3. Protocol

The program identifies common protocols:

- **TCP:** Transmission Control Protocol
- **UDP:** User Datagram Protocol
- **ICMP:** Internet Control Message Protocol

### 4. Source and Destination Ports

TCP and UDP packets can contain port numbers that help identify the communicating applications or services.

### 5. Payload Preview

The program displays a limited preview of the Raw payload layer when available.

Not all packets contain a Raw layer. Some application data may also be encrypted, so the displayed bytes might not be readable text.

---

## 🧪 Testing and Verification

The following commands can be used to verify the project setup.

### Verify Python

```bash
python3 --version
```

### Verify Scapy

```bash
python3 -c "import scapy; print('Scapy is available')"
```

### Verify the project files

```bash
ls -lah
```

### Check Python syntax

```bash
python3 -m py_compile network_sniffer.py
```

### Run the sniffer

```bash
sudo python3 network_sniffer.py
```

### Generate test traffic
```bash
ping -c 4 10.0.0.1
```

### Stop packet capture

Press `CTRL + C`.

These commands help verify the installation, source code, and basic packet-capture workflow. Successful packet detection should be confirmed from the actual program output.

---

Shows the installed Python version.

## 🔐 Security and Ethical Considerations

This project is intended for educational purposes and authorized network analysis.

Important precautions include:

- Capture traffic only on networks and devices you own or have permission to monitor.
- Do not use the tool to intercept other people's private communications.
- Avoid collecting or publishing sensitive payload data.
- Keep captured traffic and screenshots free from passwords, authentication tokens, and other confidential information.
- Remember that elevated privileges increase the potential impact of mistakes.

The program is a basic packet-capture demonstration, not a complete intrusion detection or prevention system.

---
## 🎓 Learning Outcomes

Through this project, I explored:

- Basic packet capture using Python.
- Scapy packet-capture functionality.
- IPv4 source and destination addresses.
- TCP, UDP, and ICMP identification.
- TCP and UDP port analysis.
- Packet payload inspection.
- Linux command-line operations.
- Python syntax verification.
- Network traffic analysis.
- Cybersecurity documentation and GitHub.
  
## 💡 Key Lessons Learned

This project demonstrates how packet sniffing can help build an understanding of network communication.

It also highlights that the visibility of network traffic depends on the network interface, operating system permissions, network architecture, and encryption.

A basic packet sniffer is useful for learning and troubleshooting, but more advanced analysis is required to identify malicious behaviour reliably.

---

# 👨🏽‍💻 Author

ATEMLEFAC NKAFU BECHEM 
Cybersecurity Engineer

LinkedIn: https://www.linkedin.com/in/atemlefac-nkafu-bechem-179987248

CodeAlpha Cyber Security Internshipk traffic analysis.
