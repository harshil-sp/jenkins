# 🐳 Installing Docker on Amazon Linux

Follow this guide to install Docker on your Amazon Linux EC2 instance! 🚀

## ⚙️ Steps to Install Docker

Run the following commands to set up Docker:


### 1️⃣ Update your system packages
```bash
sudo yum update -y
```

### 2️⃣ Install Docker
```bash
sudo yum install -y docker
```

### 3️⃣ Start the Docker service
```bash
sudo service docker start
```

### 4️⃣ Add the current user to the Docker group (replace 'ec2-user' if necessary)
```bash
sudo usermod -a -G docker ec2-user
```

### 5️⃣ Verify Docker is running with this command
```bash
docker ps
```



# 🚀 Starting Jenkins with Docker Volume

This guide will help you launch Jenkins using Docker and create a persistent volume for Jenkins data. 📂

## 🛠️ Steps to Start Jenkins with Docker Volume

Run the following commands:


### 1️⃣ Start Jenkins in a Docker container with a persistent volume
```bash
docker container run -d -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts
```

### 2️⃣ Inspect the created Docker volume
```bash
docker volume inspect jenkins_home
```

### 3️⃣ Retrieve the initial admin password for Jenkins
```bash
sudo cat /var/lib/docker/volumes/jenkins_home/_data/secrets/initialAdminPassword
```



# 🚀 Starting Jenkins with Docker with permissions to Use Docker

This guide will help you set up Jenkins with Docker, enabling Docker runtime access for Jenkins. Follow these steps to get started! 🎉

### 1️⃣: Run Jenkins Container 🐳

Execute the following command to start a Jenkins container with the necessary configurations:
```bash
docker container run -d -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins jenkins/jenkins:jdk21
```

### 2️⃣: Access the Container Terminal 🔑

To access the terminal of the running Jenkins container, use:
```bash
docker exec -u 0 -it jenkins bash
```

### 3️⃣: Install Docker Inside Jenkins 🛠️

Next, download and install Docker inside the Jenkins container:
```bash
curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall
```

### 4️⃣: Check Docker Socket Permissions 🔍

List the permissions of the Docker socket to ensure proper access:
```bash
ls -l /var/run/docker.sock
```

### 5️⃣: Modify Socket Permissions 🔒

If necessary, update the permissions of the Docker socket:
```bash
chmod 666 /var/run/docker.sock
```
### 6️⃣: Log in to Docker Registry 🔐

Finally, log in to your Docker registry using the following command:
```bash
echo $PASSWORD | docker login -u $USERNAME --password-stdin
```



# 🛠️ Installing Node.js on Docker Container

Follow these steps to install Node.js in your Jenkins Docker container:

## 1️⃣: Access the Jenkins Container 🔑

First, access the terminal of your Jenkins container:
```bash
docker exec -u 0 -it jenkins /bin/bash
```

### 2️⃣: Download NodeSource Setup Script 📥

Next, download the NodeSource setup script for Node.js version 20:
```bash
curl -sL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh
```

### 3️⃣: Run the Setup Script ▶️

Execute the setup script to configure Node.js installation:
```bash
bash nodesource_setup.sh
```

### 4️⃣: Install Node.js 📦

Install Node.js using the package manager:
```bash
apt-get install nodejs -y
```

### 5️⃣: Verify the Installation ✅

Finally, check the installed versions of Node.js and npm:
```bash
node -v
npm -v
```
