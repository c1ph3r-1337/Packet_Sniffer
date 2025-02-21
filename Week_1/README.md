# Docker Packet Sniffer Project: Step-by-Step Guide

## 🗂 Project Structure
- **Client Containers**: Simulate network clients that display alerts in their terminals.
- **Attacker Container**: Performs a MITM attack and pings Client1.
- **Sniffer Container**: Detects attacks or pings on Client1 and sends a message to both clients.

---

## ✅ Step 1: Create Docker Network
```sh
docker network create mitm_network
```
This creates a bridge network where all containers can communicate.

---

## 💻 Step 2: Set Up Client Containers
1. **Create Dockerfile** for the clients:
```Dockerfile
FROM ubuntu
RUN apt update && apt install -y python3
COPY client.py /client.py
CMD ["python3", "/client.py"]
```
2. **Python Client Script (client.py)**:
```python
import socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("0.0.0.0", 9090))
server_socket.listen(1)
print("Waiting for messages...")
while True:
    conn, addr = server_socket.accept()
    message = conn.recv(1024).decode()
    print(f"Alert: {message}")
    conn.close()
```
3. **Build and Run Clients:**
```sh
docker build -t client_image -f client.Dockerfile .
docker run -dit --network mitm_network --name client1 client_image
docker run -dit --network mitm_network --name client2 client_image
```

---

## 🕶️ Step 3: Set Up Attacker Container
1. **Create Dockerfile** for the attacker:
```Dockerfile
FROM ubuntu
RUN apt update && apt install -y iputils-ping
CMD ["tail", "-f", "/dev/null"]
```
2. **Build and Run Attacker:**
```sh
docker build -t attacker_image -f attacker.Dockerfile .
docker run -dit --network mitm_network --cap-add NET_ADMIN --name attacker attacker_image
```
3. **Simulate Attack:**
```sh
docker exec -it attacker bash
ping -c 4 client1
```

---

## 📡 Step 4: Set Up Sniffer Container
1. **Create Dockerfile** for the sniffer:
```Dockerfile
FROM ubuntu
RUN apt update && apt install -y python3 tcpdump
COPY sniffer.py /sniffer.py
CMD ["python3", "/sniffer.py"]
```
2. **Python Sniffer Script (sniffer.py)**:
```python
from scapy.all import sniff, IP
import socket

def send_message(message):
    for client_ip in ["client1", "client2"]:
        try:
            with socket.create_connection((client_ip, 9090)) as sock:
                sock.sendall(message.encode())
        except Exception as e:
            print(f"Failed to send message to {client_ip}: {e}")

def packet_callback(packet):
    if IP in packet and packet[IP].dst == "client1":
        print("Attack detected on client1!")
        send_message("Attack detected on client1")

sniff(filter="icmp", prn=packet_callback)
```
3. **Build and Run Sniffer:**
```sh
docker build -t sniffer_image -f sniffer.Dockerfile .
docker run -dit --network mitm_network --name sniffer sniffer_image
```

---

## 💡 Step 5: Workflow Summary
- The **attacker** pings **Client1**.
- The **sniffer** detects ICMP packets targeting **Client1**.
- The **sniffer** sends an alert to both **clients**, which print the message in their **terminal**.

---

Now the **Docker Packet Sniffer Project** is fully set up to detect attacks and instantly alert clients! 🚨
