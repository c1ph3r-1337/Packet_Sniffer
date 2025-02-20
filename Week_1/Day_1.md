# Day 1 Progress

## Setting Up Docker Containers and Networking

### 🛠️ **Creating and Connecting Containers**

```powershell
# Run a new Ubuntu container and connect it to the custom network
docker run -dit --name container3 --network my-bridge-network ubuntu
```

### 🔍 **Inspecting the Network**

```powershell
docker network inspect my-bridge-network
```

## 🏗️ **Inside the Container**

### 🚀 **Installing Ping Utility**

```bash
apt install -y iputils-ping  # Install ping command
```

### 📡 **Testing Network Connectivity**

```bash
ping container1
ping container2
ping container3
```

## 🔄 **Renaming Containers**

```powershell
# Rename an existing container
docker rename old-container-name new-container-name
```

## 🌐 **Verifying Connectivity After Renaming**

After renaming the containers, we tested connectivity from the `attacker` container to the other two containers, and both tests were successful:

### ✅ **Ping to Client**
![Ping to client](![image](https://github.com/user-attachments/assets/304beaa2-ed5b-4bd4-b44f-6eb42a2acfeb))

### ✅ **Ping to Packet Sniffer**
![Ping to packet_sniffer](![image](https://github.com/user-attachments/assets/3643e381-0754-4283-9ada-11745c662624))

---

📌 **Next Steps:** Continue exploring Docker networking, linking more services, and testing communication between containers! 🚀

