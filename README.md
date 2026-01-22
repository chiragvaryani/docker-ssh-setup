
---

# 🚀 Docker SSH Setup Project

This project demonstrates how to configure **Docker containers with SSH** for learning and testing purposes.  

It includes **two Ubuntu containers**:

- **container1** → SSH server installed and configured  
- **container2** → SSH client installed to connect to container1  

---

## 📂 Project Structure

```
docker-ssh/
├── Dockerfile           # Docker image definition
├── setup.sh             # Setup script for container initialization
├── README.md            # Project documentation
└── scripts/             # Example scripts for testing SSH connectivity
```

---

## 🛠 Step 1: Build Docker Image

```bash
docker build -t myubuntu .
```

---

## 🖥 Step 2: Run Container1 (SSH Server)

```bash
docker run -dit --name container1 myubuntu
```

The Dockerfile already installs and configures SSH:

```dockerfile
FROM ubuntu:20.04

RUN apt-get update && \
    apt-get install -y openssh-server nano && \
    mkdir /var/run/sshd && \
    echo 'root:rootpassword' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
```

👉 No need to manually edit configs or set passwords inside the container.

---

## 🖥 Step 3: Run Container2 (SSH Client)

```bash
docker run -dit --name container2 myubuntu
```

The Dockerfile also installs the SSH client:

```dockerfile
RUN apt-get update && \
    apt-get install -y openssh-client
```

---

## 🔗 Step 4: Connect via SSH

1. Start containers if stopped:

```bash
docker start container1 container2
```

2. Enter container2:

```bash
docker exec -it container2 bash
```

3. Connect to container1:

```bash
ssh root@container1
# password: rootpassword
```

---

## 🌐 Step 5: Docker Networking (Optional)

To simplify connections, use a user-defined network:

```bash
docker network create mynet
docker network connect mynet container1
docker network connect mynet container2
```

Now you can SSH by container name:

```bash
ssh root@container1
```

---

## 📦 Step 6: GitHub Integration

```bash
git add .
git commit -m "Update Docker SSH setup"
git push
```

---

## ✅ Notes / Best Practices

- Avoid SSH in production containers; prefer `docker exec` for access.  
- Keep containers **ephemeral**; commit changes if needed:  

```bash
docker commit container1 myubuntu:ssh
```

- Use simple folder names for cross-platform compatibility.  

---

## 📚 References

- [Docker Official Documentation](https://docs.docker.com/)  
- [OpenSSH Documentation](https://www.openssh.com/manual.html)  

---

## 👤 Author

Chirag Varyani  

---

