Assignment 3 — Production Maintenance Drill (OPS Checklist)
Task 1 — Server Access & Networking Validation

Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![alt text](<screenshots/browser .png>)

Screenshot 2 — Output of ip a

![alt text](<screenshots/Screenshot of IP A assignment 3.png>)

Screenshot 3 — Output of sudo ss -tulpen

![alt text](<screenshots/Screenhot-assignment-3 -sudo ss -tulpen.png>)

Screenshot 4 — Output of sudo ufw status

![alt text](<screenshots/Screenshot -assignment-3 -Output of sudo ufw status.png>)

Notes
Answer the following in your own words:
1. What proves Nginx is listening on 0.0.0.0:80?

We can prove this using a Linux command: sudo ss -tulpen | grep:80. The output LISTEN 0.0.0.0:80 tells the user: Nginx is actively listening on port 80 across the network interface.


2. What proves SSH is active on port 22?
In the same manner, when we command 'sudo ss -tulpen | grep:22', the output, such as 'LISTEN 0.0.0.0:22', tells the user: 'SSH is actively listening on port 22.


3. Did you find any unexpected open ports? Explain briefly.
No, I didn't find any unexpected open ports. Running sudo ss -tulpen showed only two services listening publicly (on 0.0.0.0): port 22 for SSH (which I use to access the instance) and port 80 for Nginx (serving the React app). Everything else – DNS (systemd-resolve), time sync (chronyd), and an SSH session artefact (port 6011) – was bound only to 127.0.0.1 (localhost), meaning it's not reachable from the internet.


Task 2 — Service Health & Systemd Validation (Nginx)
Screenshot 1 — Output of systemctl status nginx --no-pager

![alt text](<screenshots/systemctl status nginx --no-pager.png>)

Screenshot 2 — Output of sudo nginx -t

![alt text](<screenshots/task 6 Screenshot asignment 3 sudo nginx -t.png>)

Screenshot 3 — Output of sudo ss -lptn '( sport = :80 )'

![alt text](<screenshots/Screenshot-assignment -3  sudo ss -lptn.png>)

Notes
Answer the following in your own words:
1. What happens if Nginx fails to restart in production?

 When Nginx fails to restart, our React app site will be unreachable. Anyone trying to access it is greeted with an error message, such as connection refused or a timeout error. At this time, nothing is listening on port 80. When an Nginx server fails in such a manner, it could be as a result of a config syntax error, the port is already in use; sometimes it could result from permission issues where the nginx user can't access certain files, and finally, an SSL certificate issue could be another factor.

2. What's your basic rollback plan?
My basic rollback plan would be to keep a backup of the last known working state before making any change, so I can quickly revert if something breaks.
Which include:
1. The project config files mostly sit in the build folder before the processes commence, using the sudo cp... command line.
2. Use my Git properly.


Task 3 — Logs & Request Trace
Screenshot 1 — Output of sudo tail -n 30 /var/log/nginx/access.log

![alt text](<screenshots/Screenshot-Assignment-3  sudo tail -n 30  var log nginx access log.png>)

Screenshot 2 — Output of sudo tail -n 30 /var/log/nginx/error.log

![alt text](<screenshots/Screenshot-assignment 3 sudo tail -n 30 var log nginx error log.png>)

Screenshot 3 — Output of sudo journalctl -u nginx --no-pager -n 50
![alt text](<screenshots/Screenshot assignment 3 sudo journalctl -u nginx --no-pager -n 502026-07-17 172236.png>)

Notes
Answer the following in your own words:
1. Were there any errors in the logs?
If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
If no, explain what it means if the error log is empty or shows no recent errors during your check.
No, there were no errors in the logs — every entry showed normal start/stop/restart activity completing successfully, which means Nginx is running in a healthy, stable state.


2. If there were no errors, what does that indicate about the system?
It indicates that Nginx is running smoothly and reliably, with no crashes, misconfigurations, or failures affecting the service.


3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?
yes — my curl request was visible in the access log, which proves traffic flows correctly from the request all the way through Nginx to the React app and back.


Task 4 — System Resource Health Check (Capacity Red Flags)
Screenshot 1 — Output of uptime

![alt text](<screenshots/Screenshot assignment 3 uptime.png>)

Screenshot 2 — Output of free -h

![alt text](<screenshots/Screenshot  assignment 3 free -h .png>)

Screenshot 3 — Output of df -h

![alt text](<screenshots/Screenshot assignment 3 df -h.png>)

Screenshot 4 — Output of sudo du -sh /var/* | sort -h

![alt text](<screenshots/Screenshot assignment 3 sudo du -shvar  sort -h.png>)


Notes
Answer the following in your own words:
1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.
Based on the disc usage check, /var/lib (381M) and /var/cache (147M) are the largest resources, but neither is critical — /var/lib is normal package/application data, and /var/cache is a safely clearable apt cache; /var/log (97M) is the one worth monitoring going forward since it will keep growing continuously as the server runs and serves traffic.


2. What happens if the disc becomes 100% full on a production server?
When a production server's disk hits 100%, new writes fail immediately — logs stop recording, services crash or refuse to start, deployments fail midway, and databases risk corruption if caught mid-write. The system may even force itself into read-only mode as a safety measure, halting normal operation entirely. This is especially dangerous because logging itself often breaks first, so the very evidence you'd need to diagnose "disk full" as the root cause may be silently lost. In production, this is prevented through proactive monitoring/alerts, automatic log rotation, regular cleanup of caches and old builds, and, where possible, separating logs onto their own dedicated storage volume.


Task 5 — Configuration & Deployment Verification
Screenshot 1 — Output of ls -lah /var/www/html | head -n 20

![alt text](<screenshots/Screenshot assignment 3 ls -lah var www html  head -n 20.png>)

Screenshot 2 — Output of grep -R "Deployed by" -n /var/www/html 2>/dev/null | head

![alt text](<screenshots/Screenshot assignment3 grep -R  Deployed by  -n var www html 2  dev null   head.png>)

Screenshot 3 — Output of grep -n "try_files" /etc/nginx/sites-available/default

![alt text](<screenshots/Screenshot assignment 3 grep -n try_files etc nginx sites-available default.png>)

Notes
Answer the following in your own words:
1. How do you confirm that the correct version of the application is deployed?
ls -lah /var/www/html confirmed the presence of a genuine Create React App production build — index.html, a static/ folder with compiled JS/CSS bundles, and standard CRA metadata files — all owned by www-data, the user Nginx's worker processes need to read and serve them.
grep -R "Deployed by" -n /var/www/html confirms a specific identifying marker compiled into the live JavaScript bundle, proving this exact build — not a stale or generic one — is what's live, provided that marker was added to index.html before running npm run build.
grep -n "try_files" /etc/nginx/sites-available/default confirms Nginx's config correctly falls back to index.html for unmatched routes, ensuring the app behaves correctly across all its routes, not just the homepage.
Finally, this is cross-checked against curl http://localhost, which returns this exact index.html content over HTTP — tying the on-disk files, Nginx's configuration, and what's actually served to real visitors into one confirmed chain.


Task 6 — Nginx Configuration Failure Simulation
Screenshot 1 — Output of sudo nginx -t showing the syntax error (broken config)

![alt text](<screenshots/task 6 Screenshot  asignment 3 sudo nginx -t showing the syntax error (broken config).png>)

Screenshot 2 — Output of sudo nginx -t showing syntax ok (fixed config)

![alt text](<screenshots/Screenshotassignment 3 -sudo nginx -t.png>)

Screenshot 3 — Output of curl -I http://<public-ip> confirming recovery (200 OK)

![alt text](<screenshots/Task 7 Screenshot  Assignment curl -I httppublic-ip 200.png>)

Notes
Answer the following in your own words:
1. What caused the configuration failure?
The configuration failure was caused by a missing semicolon at the end of the listen 80 directive in the Nginx config file. Nginx requires every directive inside a config block to end with a semicolon — without it, Nginx can't tell where that instruction ends and the next one begins, so it throws a syntax error and refuses to load the config. Running sudo nginx -t caught this immediately, showing exactly which file and line number had the problem, which let me fix it before it ever affected the live, running service.


2. How did you fix the issue?
I fixed the issue by restoring the configuration file from the backup I'd made before intentionally breaking it, using sudo cp /etc/nginx/sites-available/default.bak /etc/nginx/sites-available/default. This instantly reverted the file back to its last known-good state, without needing to manually hunt for and retype the missing semicolon. After restoring it, I ran sudo nginx -t again to confirm the syntax was valid, and only once that came back successful did I run sudo service nginx reload to safely apply the fix — this way the corrected config took effect without ever taking the live site down.


3. How can you avoid this kind of issue in real production systems?
In real production systems, I'd avoid this kind of issue with a few habits: always back up the config before editing it, so I have an instant, reliable way back to a known-good state; always run sudo nginx -t to test the config before reloading or restarting, so a broken config never gets applied to the live service in the first place; and use reload instead of restart once the test passes, since reload applies changes without dropping active connections. Beyond that, real teams often go further by keeping configs in version control (Git), so every change is tracked and reversible, and by using CI/CD pipelines that automatically run nginx -t as a required check before any deployment can proceed — catching mistakes before they ever reach production at all.



Task 7 — Web Application Failure Simulation
Screenshot 1 — Output of curl -I http://<public-ip> showing failure (non-200 response)

![alt text](<screenshots/Task 7 Screenshot Assignment 3 curl - http public-ip.png>)

Screenshot 2 — Output of curl -I http://<public-ip> confirming recovery (200 OK)

![alt text](<screenshots/Task 7 Screenshot  Assignment curl -I httppublic-ip 200.png>)

Notes
Answer the following in your own words:
1. What caused the application to break in this scenario?
The application broke because I deleted index.html — the main file the browser needs to load and display the React app from the live deployment folder. Without that file, Nginx had nothing to serve when a visitor requested the homepage, so it returned an error response (500) instead of the actual app. This simulates a real-world mistake, like an incomplete deployment or an accidental deletion, where critical files go missing from production without anyone immediately noticing  until a user (or a monitoring check) hits the broken page.


2. How did you fix the issue and restore the application?
I fixed it by restoring the missing files from the backup I made before breaking anything. First, I removed the incomplete /var/www/html folder entirely with sudo rm -rf /var/www/html, then copied the full backup back into place with sudo cp -r /var/www/html_backup /var/www/html. Since copying a fresh backup can sometimes reset file ownership, I re-applied the correct permissions with sudo chown -R www-data:www-data /var/www/html and sudo chmod -R 755 /var/www/html, so Nginx could actually read the files again. Finally, I confirmed the fix worked by running curl -I http://localhost and seeing a 200 OK response, proving the app was fully restored and serving correctly.


3. What steps would you take to prevent this kind of issue in real production systems?
overwriting it, so recovery is instant rather than improvised; using version control (Git) for the source code, so I can always rebuild the exact same version if files go missing; and verifying a deployment succeeded with a post-deploy health check, like curl -I confirming a 200 OK response, rather than assuming it worked.




Task 8 — Security & Reliability Review
Security & Reliability Notes
Answer the following in your own words:
1. Why is SSH key-based authentication more secure than sharing passwords?
SSH key-based authentication is more secure than passwords because it relies on a private key that never travels over the network and is practically impossible to guess or brute-force, whereas passwords can be guessed, reused


2. Why should only required ports be open on a production server?

Only required ports should be open on a production server because every open port is a potential entry point for attackers — each one increases what's called the attack surface


3. Why is it important for Nginx to be enabled on boot?
It's important for Nginx to be enabled on boot because it ensures the web server automatically starts back up after a server reboot


4. What are the risks of sharing secrets, keys, or credentials publicly?
Sharing secrets, keys, or credentials publicly puts you at risk of unauthorized access, since anyone who finds them can log in, control resources, or steal data as if they were you — and because this often includes financial risk too (e.g., an exposed AWS key can let someone spin up expensive resources on your account)


5. Why should cloud resources be stopped or terminated when they are no longer needed?
Cloud resources should be stopped or terminated when no longer needed mainly to avoid unnecessary costs, since providers like AWS charge for running resources by the hour or by usage even if nothing meaningful is happening on them — and beyond cost, leaving unused resources running also unnecessarily expands your attack surface


LinkedIn Post (Required)
Evidence
LinkedIn Post URL
https://www.linkedin.com/posts/oyeku-michael-2215a920_dmibypravinmishra-devops-agenticai-ugcPost-7483979312291840000-Gii-/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAARb4_kBmnrqkDDsuuYPPXrVCKNYnevZPAo


# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

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

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
