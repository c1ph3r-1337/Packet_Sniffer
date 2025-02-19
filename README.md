# Packet Sniffer

## Overview
A packet sniffer is a network analysis tool that captures and inspects packets transmitted over a network. This tool can be used for monitoring network traffic, debugging network issues, and ethical hacking purposes.

## Features
- Captures live network packets
- Displays packet details such as source/destination IP, protocol, and payload
- Supports filtering packets by protocol (TCP, UDP, ICMP, etc.)
- Provides real-time packet capture and logging

## Prerequisites
Ensure you have the following installed on your system:
- Python 3.x
- `scapy` library (for packet capture)
- Administrative or root privileges (required for network sniffing)

## Installation
1. Clone this repository:
   ```sh
   git clone https://github.com/yourusername/packet-sniffer.git
   cd packet-sniffer
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```

## Usage
Run the packet sniffer with:
```sh
sudo python sniffer.py
```
Use optional arguments for filtering:
```sh
sudo python sniffer.py --protocol TCP
```

## Example Output
```
[12:30:15] SRC: 192.168.1.5 -> DST: 8.8.8.8 | Protocol: ICMP | Length: 64 bytes
[12:30:16] SRC: 192.168.1.2 -> DST: 192.168.1.1 | Protocol: TCP | Length: 512 bytes
```

## Disclaimer
This tool is intended for ethical and educational purposes only. Unauthorized use of this tool on networks you do not own or have permission to analyze is illegal.

## License
This project is licensed under the MIT License. See `LICENSE` for details.

## Contributing
Feel free to fork this repository, create feature branches, and submit pull requests. Contributions are welcome!

## Contact
For questions or issues, open an issue on GitHub or reach out via email at `your.email@example.com`.

