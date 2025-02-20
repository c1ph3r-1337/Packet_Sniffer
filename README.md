# Docker Packet Sniffer Project Overview

## 🗂 Project Structure
- **Client Containers**: Simulate network clients.
- **Attacker Container**: Executes a MITM attack and pings the clients.
- **Sniffer Container**: Captures packets and generates a report.

## 🕸 Network Setup
- All containers are connected via a Docker bridge network.

## ⚙️ Workflow
1. Clients communicate normally.
2. The attacker performs an ARP spoofing attack.
3. The attacker pings the clients.
4. The sniffer captures packets and outputs a report after the last ping.

## 🧩 Key Tools Used
- **Client**: Ubuntu with ping utilities
- **Attacker**: Kali Linux with `ettercap`
- **Sniffer**: Ubuntu with `tcpdump`

## 🚀 Quick Steps
1. Create a Docker network.
2. Build and run each container.
3. Launch the MITM attack and pings.
4. Extract the sniffer’s `.pcap` file for analysis.

## 📝 Automation (Optional)
- Add scripts to automate capture and report generation.

---

For detailed setup and commands, refer to the `README.md` in each container's directory.
