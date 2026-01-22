# docker-ssh-setup



Absolutely! Here's the \*\*entire README.md in one block\*\* that you can copy and paste directly:



---



```markdown

\# Docker SSH Setup Project



This project demonstrates how to configure \*\*Docker containers with SSH\*\* for learning and testing purposes.  

It includes \*\*two Ubuntu containers\*\*:



\- \*\*container1\*\*: SSH server installed and configured

\- \*\*container2\*\*: SSH client installed to connect to container1



---



\## Project Structure



```



docker-ssh/

├── Dockerfile           # Docker image definition

├── setup.sh             # Optional setup script for container initialization

├── README.md            # Project documentation

└── any other scripts    # Example scripts for testing SSH connectivity



````



---



\## Step 1: Build Docker Image



Build the Docker image for your containers:



```bash

docker build -t myubuntu .

````



---



\## Step 2: Run Container1 (SSH Server)



```bash

docker run -it --name container1 myubuntu

```



Inside container1:



```bash

apt-get update

apt-get install -y openssh-server nano

nano /etc/ssh/sshd\_config

\# Uncomment or add: PermitRootLogin yes

passwd root   # Set root password

service ssh start

exit

```



---



\## Step 3: Run Container2 (SSH Client)



```bash

docker run -it --name container2 myubuntu

```



Inside container2:



```bash

apt-get update

apt-get install -y openssh-client

exit

```



---



\## Step 4: Connect via SSH



1\. Start containers if they are stopped:



```bash

docker start container1

docker start container2

```



2\. Enter container2:



```bash

docker exec -it container2 bash

```



3\. Connect to container1 via SSH:



```bash

ssh root@<container1-IP>

\# Example:

ssh root@172.17.0.2

```



---



\## Step 5: Docker Networking (Optional)



\* To make SSH connections easier, create a user-defined network:



```bash

docker network create mynet

docker network connect mynet container1

docker network connect mynet container2

ssh root@container1

```



---



\## Step 6: GitHub Integration



\* The project is stored on GitHub: `https://github.com/chiragvaryani/docker-ssh-setup`

\* To update:



```bash

git add .

git commit -m "Update Docker SSH setup"

git push

```



---



\## Notes / Best Practices



\* Avoid SSH in production containers; prefer `docker exec` for access

\* Keep Docker containers \*\*ephemeral\*\*; save changes by creating an image if needed:



```bash

docker commit container1 myubuntu:ssh

```



\* Avoid special characters (like apostrophes) in folder names for Windows compatibility



---



\## References



\* \[Docker Official Documentation](https://docs.docker.com/)

\* \[OpenSSH Documentation](https://www.openssh.com/manual.html)



---



\## Author



Chirag Varyani



```



---



If you want, I can also make a \*\*version with Windows PowerShell instructions included\*\*, so someone can follow it on Windows without errors from `'` in folder names or Git commands.  



Do you want me to do that?

```



