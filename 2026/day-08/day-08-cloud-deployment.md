# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Task
Deploy a real web server on the cloud and practice hands-on server management.

**Steps covered:**
- Launch a cloud instance (AWS EC2 or Utho)
- Connect via SSH
- Install Nginx
- Configure security groups for web access (port 80, Nginx default)
- Extract and save logs to a file
- Verify the webpage is accessible from the internet

---

## Part 1: Launch Cloud Instance & SSH Access
*(~15 min)*

**Step 1:** Create a cloud instance.

**Step 2:** Connect via SSH.

*<img width="1228" height="609" alt="image" src="https://github.com/user-attachments/assets/28a16cc6-cb3f-4269-9d97-8064a9c99b4e" />
*

---

## Part 2: Install Docker & Nginx
*(~20 min)*

**Step 1:** Update the system.

**Step 2:** Install Nginx.

**Verify Nginx is running:**

*<img width="1015" height="319" alt="image" src="https://github.com/user-attachments/assets/c12f6ded-7704-4f42-bd7e-d35873a9fee9" />
*


---

## Part 3: Security Group Configuration
*(~10 min)*

**Test web access:** Open a browser and visit `http://<your-instance-ip>` — you should see the Nginx welcome page.

*<img width="1601" height="1042" alt="image" src="https://github.com/user-attachments/assets/f33fc121-462a-4bad-a969-3ae32a8bd19c" />
*

---

## Part 4: Extract Nginx Logs
*(~15 min)*

**Step 1:** View Nginx logs.
<img width="1320" height="265" alt="image" src="https://github.com/user-attachments/assets/5e8903f6-bdde-46df-bdaa-6c8cd07951a0" />

**Step 2:** Save logs to a file.
<img width="1428" height="736" alt="image" src="https://github.com/user-attachments/assets/d8e34c76-9ab3-4f89-9405-cac030c4ae14" />


**Step 3:** Download the log file to your local machine.

*<img width="1850" height="524" alt="image" src="https://github.com/user-attachments/assets/89ad7dd2-3764-4997-b926-73e0d8c5b9f5" />
*
