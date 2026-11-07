# Assignment 3 — Docker Networking

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will explore Docker networking by using default bridge, custom bridge, multiple bridge, and host network modes. You will verify container communication, service discovery, network isolation, public access, and host networking on a Linux VM or EC2 instance.

---

# Task 1 — Deploy a Standalone Application Using the Default Bridge Network

## Goal

Deploy an Nginx web server using Docker’s default bridge network and access it through the VM public IP address.

### Evidence

#### Screenshot 1 — Available Docker Networks

Add a screenshot of the terminal showing:

```bash
docker network ls
```

The output must include the default `bridge`, `host`, and `none` networks.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen1.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 2 — Nginx Image Pull

Add a screenshot of the terminal showing successful completion of:

```bash
docker pull nginx:alpine
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen2.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 3 — Running `myweb` Container

Add a screenshot of the terminal showing:

```bash
docker ps
```

The output must show the running `myweb` container with:

```text
0.0.0.0:80->80/tcp
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen3.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 4 — Nginx Welcome Page

Add a browser screenshot showing the Nginx Welcome Page at:

```text
<<<<<<< HEAD
http://http://18.188.255.17
=======
http://<YOUR-VM-PUBLIC-IP>
>>>>>>> upstream/main
```

Ensure that the VM public IP is visible in the address bar. Add your full name as a clear caption directly below the screenshot.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen4.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

# Task 2 — Connect Containers Using a Custom Bridge Network

## Goal

Create a custom bridge network and verify that containers can communicate using container names rather than IP addresses.

### Evidence

#### Screenshot 5 — Custom Bridge Network Created

Add a screenshot of the terminal showing `mynetwork` in:

```bash
docker network ls
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen5.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 6 — Running `web` and `client` Containers

Add a screenshot of the terminal showing:

```bash
docker ps
```

The output must show both `web` and `client` containers running without published host ports.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen6.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 7 — Service Discovery by Container Name

Add a screenshot of the terminal showing successful output from:

```bash
docker exec client wget -qO- http://web
```

The output must display the Nginx Welcome Page HTML.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen1.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 8 — Custom Network Inspection

Add a screenshot of the terminal showing:

```bash
docker network inspect mynetwork
```

The output must show both `web` and `client` connected to `mynetwork`.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen8.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

# Task 3 — Demonstrate Multi-Network Isolation

## Goal

Deploy frontend, backend, and database containers across two separate Docker networks. Verify allowed communication and confirm that the frontend cannot directly reach the database.

### Evidence

#### Screenshot 9 — Two Docker Networks

Add a screenshot of the terminal showing:

```bash
docker network ls
```

The output must include both `frontend-network` and `backend-network`.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen9.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 10 — Running Multi-Network Containers

Add a screenshot of the terminal showing:

```bash
docker ps
```

The output must show:

- `frontend` with the published port mapping `0.0.0.0:80->80/tcp`
- `backend` without a published host port
- `db` without a published host port

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen10.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 11 — Frontend Network Inspection

Add a screenshot of the terminal showing:

```bash
docker network inspect frontend-network
```

The output must show `frontend` and `backend`.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen11.png)

=======
Add your screenshot here.

---
>>>>>>> upstream/main

#### Screenshot 12 — Backend Network Inspection

Add a screenshot of the terminal showing:

```bash
docker network inspect backend-network
```

The output must show `backend` and `db`.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen12.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 13 — Frontend-to-Backend Communication

Add a screenshot of the terminal showing successful output from:

```bash
docker exec frontend wget -qO- http://backend
```

The output must display the Nginx Welcome Page HTML.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen13.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 14 — Backend-to-Database Communication

Add a screenshot of the terminal showing a successful connection to `db` on port `27017` from the `backend` container.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen14.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 15 — Frontend-to-Database Isolation

Add a screenshot of the terminal showing that the `frontend` container cannot reach `db` on port `27017`.

The output must include:

```text
Expected result: frontend cannot reach db
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen15.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 16 — Public Frontend Access

Add a browser screenshot showing the Nginx Welcome Page from the `frontend` container at:

```text
<<<<<<< HEAD
http://http://18.188.255.176
=======
http://<YOUR-VM-PUBLIC-IP>
>>>>>>> upstream/main
```

Ensure that the VM public IP is visible in the address bar. Add your full name as a clear caption directly below the screenshot.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen16.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

# Task 4 — Deploy an Application Using Docker Host Network Mode

## Goal

Run an Nginx container using Docker host network mode and compare it with bridge networking.

### Evidence

#### Screenshot 17 — Running Host-Networked Container

Add a screenshot of the terminal showing:

```bash
docker ps
```

The output must show the running `fastapp` container.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen17.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 18 — Host Network Mode Verification

Add a screenshot of the terminal showing output from:

```bash
docker inspect fastapp | grep '"NetworkMode"'
```

The output must confirm:

```text
"NetworkMode": "host"
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen18.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 19 — Host-Networked Nginx Page

Add a browser screenshot showing the Nginx Welcome Page at:

```text
<<<<<<< HEAD
http://3.15.202.63
=======
http://<YOUR-VM-PUBLIC-IP>
>>>>>>> upstream/main
```

Ensure that the VM public IP is visible in the address bar. Add your full name as a clear caption directly below the screenshot.

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen19.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

#### Screenshot 20 — Host-Networked Container Cleanup

Add a screenshot of the terminal showing successful completion of:

```bash
docker stop fastapp
docker rm fastapp
```

<<<<<<< HEAD
![screenshot](./screenshots/ass3-screen20.png)
=======
Add your screenshot here.
>>>>>>> upstream/main

---

# Networking Notes

Write a short note explaining:

- Default bridge networking
- Container-name communication on a custom bridge network
- Why the frontend could not access the database in Task 3
- The difference between bridge mode and host network mode

Write your note here.

<<<<<<< HEAD
Here’s a more natural, human version:

1. Default Bridge Networking  
Docker automatically creates a default bridge network. Containers on this network can talk to each other using IP addresses. To reach them from outside, you need to publish ports. Unlike custom bridges, the default bridge doesn’t give you automatic DNS resolution by container name.

2. Container-name Communication on Custom Bridge Networks  
Custom bridge networks come with built-in DNS service discovery. Any containers connected to the same custom network can reach each other simply by using their container names — no need to hardcode IP addresses.

3. Why the Frontend Could Not Access the Database  
The frontend and database were sitting on two separate, isolated networks. The frontend was on `frontend-network` and the database was on `backend-network`. Because the frontend wasn’t connected to the backend network, it couldn’t talk directly to the database. The backend container acted as the bridge that allowed controlled communication between the two networks.

4. Difference Between Bridge and Host Networking  
Bridge networking keeps containers isolated from the host. You have to map ports if you want external access. Host networking removes that isolation — the container shares the host’s network stack and can use the host’s network interfaces directly, so no port mapping is needed. The trade-off is less network isolation.
=======
>>>>>>> upstream/main
---

# LinkedIn Requirement

## Goal

Create a LinkedIn post about the Docker networking modes explored, one key lesson about container isolation, and the learning outcomes from this assignment.

### Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

<<<<<<< HEAD
`https://lnkd.in/p/eQpTHYMY
=======
`Add your URL here`
>>>>>>> upstream/main

---

#### LinkedIn Post Screenshot

<<<<<<< HEAD
![screenshot](./screenshots/dockerassig3-linkedInpost shot.png)

=======
Add a screenshot of the published LinkedIn post here.
>>>>>>> upstream/main

---

# Submission Instructions

- Complete all tasks in sequence.
- Include Screenshots 1–20 exactly as specified.
- Include the Networking Notes section.
- Include the LinkedIn post URL and screenshot.
- Ensure that your full name is visible in all terminal screenshots.
- Add your full name as a caption below each browser screenshot that shows the standard Nginx page.
- Do not expose private keys, passwords, access keys, tokens, account IDs, or other sensitive information.

---

# Completion Checklist

- [ ] Completed on a Linux VM or EC2 instance
- [ ] Docker Engine is running
- [ ] HTTP port 80 is allowed in the VM firewall or cloud security rules
- [ ] Default bridge networking verified
- [ ] Custom bridge network created
- [ ] Container-name communication verified
- [ ] `frontend-network` and `backend-network` created
- [ ] Frontend-to-backend communication verified
- [ ] Backend-to-database communication verified
- [ ] Frontend-to-database isolation verified
- [ ] Only the frontend published port 80 in Task 3
- [ ] Host network mode verified
- [ ] All required screenshots included
- [ ] Networking Notes completed
- [ ] LinkedIn post URL and screenshot included
- [ ] Full name visible in terminal screenshots
- [ ] Browser screenshots include full-name captions
- [ ] No sensitive information exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
