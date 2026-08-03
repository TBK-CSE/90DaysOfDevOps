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

*[screenshot: SSH connection]*

---

## Part 2: Install Docker & Nginx
*(~20 min)*

**Step 1:** Update the system.

**Step 2:** Install Nginx.

**Verify Nginx is running:**

*[screenshot: Nginx status check]*
*[screenshot: Nginx service verification]*

---

## Part 3: Security Group Configuration
*(~10 min)*

**Test web access:** Open a browser and visit `http://<your-instance-ip>` — you should see the Nginx welcome page.

*[screenshot: Nginx welcome page in browser]*

---

## Part 4: Extract Nginx Logs
*(~15 min)*

**Step 1:** View Nginx logs.

**Step 2:** Save logs to a file.

**Step 3:** Download the log file to your local machine.

*[screenshot: log file saved]*
*[screenshot: log file downloaded]*
