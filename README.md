# WAF + SIEM Integration Project: ModSecurity & Splunk

## Overview

This project integrates **ModSecurity** (a Web Application Firewall) with **Splunk** (a Security Information and Event Management platform) to create a real-time security monitoring system for web applications. The setup is optimized for an Intel Celeron, 8 GB RAM system, using **XAMPP** for Apache, with ModSecurity for WAF protection, and Splunk for log aggregation and alerting.

## Features

- **Web Application Firewall (WAF)** powered by **ModSecurity**.
- **SIEM** functionality using **Splunk Free Version** for log aggregation, searching, and alerting.
- **OWASP Juice Shop** as a target application for attack simulation.
- Protects against common attacks like **SQL Injection** and **XSS**.
- Automated log forwarding from **ModSecurity** to **Splunk**.

## Prerequisites

Before you begin, make sure you have the following:

- **XAMPP** for Apache (Web server).
- **ModSecurity** for Apache (Web Application Firewall).
- **Splunk Free Version** for SIEM.
- **OWASP Juice Shop** for attack simulation.

## Installation Guide

Follow these steps to set up the WAF + SIEM integration:

### Step 1: Install XAMPP (Apache Web Server)
1. Download and install **XAMPP** from the [official website](https://www.apachefriends.org/index.html).
2. Start **Apache** in the XAMPP Control Panel.

### Step 2: Install ModSecurity
1. Download and install **ModSecurity** for Apache.
2. Edit `httpd.conf` to load the **mod_security2.so** module and include the `modsecurity.conf` file.
3. Configure ModSecurity rules, including OWASP **Core Rule Set** (CRS).

### Step 3: Install Splunk Free Version
1. Download and install **Splunk** from [Splunk's official website](https://www.splunk.com/en_us/download.html).
2. Set up **HTTP Event Collector (HEC)** to collect ModSecurity logs.

### Step 4: Test the Setup
1. Simulate attacks using **OWASP Juice Shop** and monitor how **ModSecurity** blocks them.
2. Forward **ModSecurity logs** to **Splunk** using a batch script.

### Step 5: Monitor Logs in Splunk
1. View ModSecurity logs in the **Splunk Search & Reporting** dashboard.
2. Set up alerts for detected attacks.

## Video Demonstration

- Watch the step-by-step **video demonstration** of the setup process and attack simulation:  
[Video Link](https://www.youtube.com/watch?v=example)

## Skills Learned

- **Security Analyst (Investigation Level)**:
  - Working with **ModSecurity** to defend against web application attacks.
  - Integrating **Splunk** for security log management and alerting.
  - **SQL Injection**, **XSS**, and other common web attacks.
  
- **Incident Response**:
  - Real-time monitoring of web application security events.
  - Analyzing attack patterns and using alerts to trigger responses.

- **Log Aggregation & Management**:
  - Using **Splunk** to manage large volumes of security logs.
  - Visualizing attack data through Splunk's search and reporting interface.

## Screenshots

### 1. **XAMPP Control Panel**  
   ![XAMPP Control Panel](https://github.com/your_username/WAF-SIEM-Integration/screenshots/xampp_control_panel_running.png)  
   _The **XAMPP Control Panel** with **Apache** running, ready for attack simulation._

---

### 2. **ModSecurity Configuration in httpd.conf**  
   ![ModSecurity httpd.conf Configuration](https://github.com/your_username/WAF-SIEM-Integration/screenshots/modsecurity_httpd_config.png)  
   _A screenshot of **httpd.conf** showing the **ModSecurity** configuration being loaded._

---

### 3. **ModSecurity Audit Log Showing Blocked Attack (SQL Injection)**  
   ![ModSecurity Audit Log](https://github.com/your_username/WAF-SIEM-Integration/screenshots/modsec_audit_log_example.png)  
   _Example of a **SQL Injection** attack that was detected and blocked by **ModSecurity**. The log entry includes details like the type of attack, source IP, and request details._

---

### 4. **Splunk HEC Token Creation**  
   ![Splunk HEC Token Creation](https://github.com/your_username/WAF-SIEM-Integration/screenshots/splunk_hec_token_creation.png)  
   _Creating the **HTTP Event Collector (HEC)** token in **Splunk** to collect ModSecurity logs._

---

### 5. **Splunk Search & Reporting Dashboard**  
   ![Splunk Search Dashboard](https://github.com/your_username/WAF-SIEM-Integration/screenshots/splunk_search_modsec_logs.png)  
   _A screenshot of **Splunk's Search & Reporting dashboard** displaying **ModSecurity logs** after the attack was detected and blocked. Here, you can see the captured attack pattern._

---

### 6. **OWASP Juice Shop SQL Injection Attack Simulation**  
   ![OWASP Juice Shop SQL Injection](https://github.com/your_username/WAF-SIEM-Integration/screenshots/juice_shop_sql_injection.png)  
   _**OWASP Juice Shop** demonstrating a **SQL Injection** attack, which **ModSecurity** should block._

---

### 7. **Splunk Alert Triggered by ModSecurity Logs**  
   ![Splunk Alert Dashboard](https://github.com/your_username/WAF-SIEM-Integration/screenshots/splunk_alert_triggered.png)  
   _A **Splunk alert** triggered by **ModSecurity** detecting an attack like **SQL Injection** or **XSS**. The alert in **Splunk** can trigger based on pre-configured thresholds or attack patterns._

---

### 8. **Blocked Attack Notification in ModSecurity's Error Logs**  
   ![ModSecurity Blocked Attack Notification](https://github.com/your_username/WAF-SIEM-Integration/screenshots/modsec_blocked_attack.png)  
   _**ModSecurity** log showing that a **Cross-Site Scripting (XSS)** attack was blocked, including the request's URL and attack details._

---

## Conclusion

This project demonstrates how to integrate a **Web Application Firewall (WAF)** with a **Security Information and Event Management (SIEM)** platform for **real-time threat detection** and **incident response**.

By following this guide, you’ve learned how to:

1. Set up **ModSecurity** for **WAF protection**.
2. Configure **Splunk** for **SIEM functionality**.
3. Simulate common web application attacks and detect them in **Splunk**.

With this knowledge, you are better prepared for **Security Operations Center (SOC)** roles, including skills in **incident investigation**, **log analysis**, and **alert management**.

Feel free to explore the project further or contribute by improving the integration or adding new security features!

---

### **Project Links**

- **GitHub Repository**: [WAF-SIEM-Integration](https://github.com/your_username/WAF-SIEM-Integration)
- **Video Demonstration**: [YouTube Link](https://www.youtube.com/watch?v=example)

---

### **How This Demonstrates WAF Effectiveness**

The project not only shows how **ModSecurity** is set up to protect against common attacks but also demonstrates its effectiveness by including screenshots of actual attacks being blocked, such as **SQL Injection** and **XSS**, and how **Splunk** picks up and alerts on those blocked attacks. These images make it clear that the WAF is functioning correctly and the SIEM integration allows for proper monitoring and alerting.

---

This **README.md** now includes everything necessary for users to understand the project setup, how to implement it, and how to verify that the **WAF** is effectively blocking attacks, with **clear visual demonstrations** at the end. Let me know if you need any further adjustments or additions!
