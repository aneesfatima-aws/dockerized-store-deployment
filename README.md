# dockerized-store-deployment
---

<img width="1545" height="1018" alt="lab2" src="https://github.com/user-attachments/assets/7ea7747b-8b53-49d0-a778-66a457c375ef" />

## Phase 1 — Launch EC2

### Step 1

Go to:
AWS Console

→ EC2

→ Launch Instance

Name

jewelry-store-server
---
AMI

Choose:

Ubuntu Server 24.04 LTS

---
Instance Type

t2.micro

(Free Tier)

---

Key Pair

Create:
jewelry-key

Download:
jewelry-key.pem

Keep it safe.

---

Security Group
Allow:

SSH     22

HTTP    80

Source:

0.0.0.0/0

---

Launch Instance
Wait until:
Running


---

### Step 2

Copy:

Public IPv4 Address

Example:

54.12.34.56

---

## Phase 2 — Connect to EC2

Windows PowerShell

Navigate to folder containing:

jewelry-key.pem

Run:
`ssh -i jewelry-key.pem ubuntu@YOUR_PUBLIC_IP`

Example:
`ssh -i jewelry-key.pem ubuntu@54.12.34.56`

---

Expected:

ubuntu@ip-xxx-xxx:~$

Success 🎉

---

## Phase 3 — Install Docker

### Step 3
Update packages
`sudo apt update`

---

Install Docker
`sudo apt install docker.io -y`

---

Enable Docker
`sudo systemctl enable docker`


---

Start Docker
`sudo systemctl start docker`

---

Verify
`docker --version`

Example:
`Docker version 28.x.x`

---

### Step 4

Test Docker
`sudo docker run hello-world`

Expected:
`Hello from Docker!`

---

## Phase 4 — Create Project

### Step 5

Create folder

`mkdir jewelry-store`
`cd jewelry-store`

---

Create:
`nano index.html`
Paste:
```
<!DOCTYPE html>
<html>
<head>
<title>Luxe Jewelry</title>
<style>
body{
font-family:Arial;
text-align:center;
background:#f7f2e8;
padding:50px;
}
h1{
color:#c9a227;
}
</style>
</head>
<body>

<h1>Luxe Jewelry Store</h1>

<h2>Lab 2 Docker Deployment</h2>

<p>Hosted on AWS EC2 using Docker</p>

</body>
</html>
```
Save:
`CTRL + O`
`ENTER`
`CTRL + X`

---
## Phase 5 — Dockerize App

### Step 6

Create Dockerfile
`nano Dockerfile`

Paste:
```
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```
Save:
As we save earlier with keys.
---

### Step 7

Build image

`sudo docker build -t jewelry-store .`

Don't forget to put that dot (.) in this command

---

Verify

`sudo docker images`

You should see:
jewelry-store

---

### Step 8

Run container

`sudo docker run -d -p 80:80 jewelry-store`

---

Verify

`sudo docker ps`

---

## Phase 6 — Test Website

### Step 9

Open browser

`http://YOUR_PUBLIC_IP`

Example:

`http://54.12.34.56`

Expected:

`Luxe Jewelry Store
Lab 2 Docker Deployment
Hosted on AWS EC2 using Docker`

🎉 Lab Complete

---
### Bonus Step (Highly Recommended)

Stop container

`sudo docker stop CONTAINER_ID`

Run with name

`sudo docker run -d \
--name jewelry-container \
-p 80:80 \
jewelry-store`

Now it looks more professional.
---

### Skills Learned:

- AWS EC2

- Linux Administration

- Docker

- Containerization

- SSH

- Security Groups

- Web Hosting

- Nginx


---
