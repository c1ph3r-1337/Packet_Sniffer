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
![image](https://github.com/user-attachments/assets/59818368-1ce7-49c6-9038-547cf3e80923)


### ✅ **Ping to Packet Sniffer**
![image](https://github.com/user-attachments/assets/b7c0abb6-18d2-4d2f-a764-5c4ce837fb78)


---

📌 **Next Steps:** Continue exploring Docker networking, linking more services, and testing communication between containers! 🚀

