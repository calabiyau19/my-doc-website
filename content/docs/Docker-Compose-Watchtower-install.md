---
title: "How to Auto Update Docker Apps With Watchtower"
date: 2025-02-18T12:00:00Z
draft: false
---

#### **Step-by-Step Guide to Install Docker, Docker Compose, Watchtower on Ubuntu Server 24.04**

This guide ensures you install the latest **Docker Engine** and **Docker Compose** on **Ubuntu Server 24.04 (Noble)**, using the official Docker repositories.  As a bonus, it also includes directions to install Watchtower which will help keep your docker contained applications updated automatically and send you a notification via ntfy if updates occur

---

## **Step 1: Update the System**

Ensure your system is up to date before installing any packages:

bash  
CopyEdit  
`sudo apt update && sudo apt upgrade -y`

---

## **Step 2: Install Required Dependencies**

Install required system packages:

bash  
CopyEdit  
`sudo apt install -y ca-certificates curl gnupg`

---

## **Step 3: Add Docker’s Official GPG Key**

Docker packages are signed, so we need to add the official GPG key:

bash  
CopyEdit  
`sudo install -m 0755 -d /etc/apt/keyrings`  
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null`  
`sudo chmod a+r /etc/apt/keyrings/docker.asc`

---

## **Step 4: Add the Docker Repository (For Ubuntu 24.04 Noble)**

Now, add the **Docker stable repository** to your system:

bash  
CopyEdit  
`echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu noble stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

Then update the package index again:

bash  
CopyEdit  
`sudo apt update`

---

## **Step 5: Install Docker Engine and Docker Compose Plugin**

Now, install the latest versions of Docker and the Compose plugin:

bash  
CopyEdit  
`sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

---

## **Step 6: Enable and Start the Docker Service**

Ensure that Docker starts on boot and is currently running:

bash  
CopyEdit  
`sudo systemctl enable --now docker`

Check the service status:

bash  
CopyEdit  
`sudo systemctl status docker`

---

## **Step 7: Verify Installation**

Check that Docker is installed correctly:

bash  
CopyEdit  
`docker --version`

Verify the Docker Compose plugin:

bash  
CopyEdit  
`docker compose version`

Run a test container to ensure everything works:

bash  
CopyEdit  
`docker run hello-world`

---

## **Step 8: Add Your User to the Docker Group (Optional, for Non-root Access)**

By default, you need `sudo` to run Docker commands. To run Docker as a regular user, add yourself to the **docker** group:

bash  
CopyEdit  
`sudo usermod -aG docker $USER`

Apply the group change immediately:

bash  
CopyEdit  
`newgrp docker`

Now test running Docker **without sudo**:

bash  
CopyEdit  
`docker run hello-world`

---

## **Step 9: Keeping Docker and Compose Updated**

Since Docker releases frequent updates, update your system regularly:

bash  
CopyEdit  
`sudo apt update && sudo apt upgrade -y`

For a more targeted update, check if a new Docker version is available:

bash  
CopyEdit  
`apt list --upgradable | grep docker`

Then update Docker only:

bash  
CopyEdit  
`sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

---

### **Final Verification**

After completing the steps, verify the installation one last time:

bash  
CopyEdit  
`docker --version`  
`docker compose version`  
`docker run hello-world`

At this point, you have **the latest Docker and Docker Compose installed on Ubuntu 24.04**, fully functional and ready to use.

##### **You said:**

Add one final step. Install Watchtower to keep the containers updated. Or should that be after freshRSS in this case, is installed?

###### **ChatGPT said:**

### **Final Step: Install Watchtower for Automatic Container Updates**

Watchtower automatically updates your running Docker containers when new versions are available. However, **you should install Watchtower after deploying key applications like FreshRSS** to ensure everything is set up correctly before automating updates.

#### **Step 11: Install Watchtower**

Once FreshRSS (or any other critical containerized applications) is running, install Watchtower with:

bash  
CopyEdit  
`docker run -d \`  
  `--name watchtower \`  
  `--restart unless-stopped \`  
  `-v /var/run/docker.sock:/var/run/docker.sock \`  
  `containrrr/watchtower`

#### **(Optional) Enable Notifications**

To get update notifications, add environment variables for your preferred service (e.g., Slack, Discord, email):

bash  
CopyEdit  
`docker run -d \`  
  `--name watchtower \`  
  `--restart unless-stopped \`  
  `-v /var/run/docker.sock:/var/run/docker.sock \`  
  `-e WATCHTOWER_NOTIFICATIONS=email \`  
  `-e WATCHTOWER_NOTIFICATION_EMAIL_FROM="your-email@example.com" \`  
  `-e WATCHTOWER_NOTIFICATION_EMAIL_TO="your-email@example.com" \`  
  `containrrr/watchtower`

#### **Verify Watchtower is Running**

Check logs to confirm Watchtower is monitoring containers:

bash  
CopyEdit  
`docker logs -f watchtower`

### **Should You Install Watchtower Before or After FreshRSS?**

✅ **After FreshRSS installation** is ideal. That way, you ensure FreshRSS is set up properly before enabling automatic updates, which could introduce changes unexpectedly.

Would you like a FreshRSS installation guide next?

##### **You said:**

With built in ntfy.sh running when watchtower runs

###### **ChatGPT said:**

### **Final Step: Install Watchtower with Built-in Ntfy.sh Notifications**

Watchtower will **automatically update Docker containers** and **send notifications via Ntfy.sh** whenever it updates a container.

---

### **Step 11: Install Watchtower with Ntfy.sh Notifications**

**Run Watchtower with Ntfy.sh**  
Replace `<your-ntfy-topic>` with your chosen topic (e.g., `freshrss-updates`):  
bash  
CopyEdit  
`docker run -d \`  
  `--name watchtower \`  
  `--restart unless-stopped \`  
  `-v /var/run/docker.sock:/var/run/docker.sock \`  
  `-e WATCHTOWER_NOTIFICATIONS=ntfy \`  
  `-e WATCHTOWER_NOTIFICATION_URL="https://ntfy.sh/<your-ntfy-topic>" \`  
  `containrrr/watchtower`

1. 

**Verify Watchtower is Running**  
Check logs to confirm Watchtower is monitoring containers and sending notifications:  
bash  
CopyEdit  
`docker logs -f watchtower`

2.   
3. **Test Ntfy.sh Notifications**  
   Open your Ntfy.sh topic URL (`https://ntfy.sh/<your-ntfy-topic>`) in a browser or use the mobile app to verify Watchtower messages.

---

### **Should You Install Watchtower Before or After FreshRSS?**

✅ **Install Watchtower after FreshRSS** to avoid automatic updates during the initial setup.

Would you like a **FreshRSS installation guide** next?

