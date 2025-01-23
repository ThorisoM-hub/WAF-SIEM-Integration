 # WAF-SIEM-Integration 

## Overview

The **WAF-SIEM-Integration** project demonstrates the integration of a **Web Application Firewall (WAF)** using **ModSecurity** and a **Security Information and Event Management (SIEM)** system using **Splunk**. This project is designed to provide hands-on experience in web application security, attack detection, log management, and incident monitoring.

This guide will take you through the process of setting up both ModSecurity (WAF) and Splunk (SIEM), configuring them to work together, and simulating attacks to test the security controls.

---

## Project Structure

- **WAF Setup with ModSecurity**: Protects web applications from attacks like **SQL Injection** and **XSS**.
- **SIEM Setup with Splunk**: Aggregates logs from ModSecurity and provides insights into security events, enabling incident detection and response.
- **Attack Simulation**: Simulates common web application attacks such as **SQL Injection** and **XSS** to test the effectiveness of the WAF and SIEM setup.
- **Monitoring and Reporting**: Configures **Splunk** to generate alerts and dashboards based on the logs received from ModSecurity.

---

## Skills

### Security Analyst (Level 2)

- **WAF Management & Tuning**: Experience with configuring, deploying, and fine-tuning web application firewalls like **ModSecurity** for detecting and blocking web attacks.
- **Splunk Setup & Querying**: Expertise in setting up **Splunk** to collect and index security logs, as well as building custom queries for analysis and alerting.
- **Security Incident Investigation**: Ability to investigate and respond to security incidents by analyzing logs from **ModSecurity** and **Splunk**, ensuring timely responses to attacks.
- **Web Application Security**: Knowledge of common web application vulnerabilities like **SQL Injection**, **XSS**, and how to prevent them using WAFs.
- **Alerting & Reporting**: Proficient in creating custom **Splunk dashboards** and alerts to identify malicious behavior in real-time.

---

## Installation Guidelines

Follow the steps below to set up **WAF-SIEM-Integration** on your Windows system.

### 1. Install **XAMPP** for Apache and PHP

- Download **XAMPP** from [Apache Friends](https://www.apachefriends.org/index.html).
- Run the installer and follow the default installation instructions.
- In the **XAMPP Control Panel**, start **Apache** and **MySQL** (you can skip MySQL for this project).
- Ensure **Apache** is running to host your web application.

### 2. Install **ModSecurity** with Apache

1. **Download ModSecurity**:
   - Visit the [ModSecurity GitHub Repository](https://github.com/SpiderLabs/ModSecurity) and download the latest release.

2. **Install ModSecurity**:
   - Extract the ModSecurity files and copy `mod_security2.so` into the `C:\xampp\apache\modules\` directory.
   - Open `C:\xampp\apache\conf\httpd.conf` and add the following lines:
     ```apache
     LoadModule security2_module modules/mod_security2.so
     Include conf/extra/modsecurity.conf
     ```

3. **Create ModSecurity Configuration**:
   - Create `modsecurity.conf` under `C:\xampp\apache\conf\extra\` and add:
     ```apache
     SecRuleEngine On
     SecRequestBodyAccess On
     SecResponseBodyAccess On
     SecAuditEngine On
     SecAuditLog logs/modsec_audit.log

     # Include OWASP CRS rules
     Include C:/xampp/apache/conf/extra/owasp-modsecurity-crs/crs-setup.conf
     Include C:/xampp/apache/conf/extra/owasp-modsecurity-crs/rules/*.conf
     ```

4. **Download OWASP CRS**:
   - Download the **OWASP ModSecurity CRS** from [GitHub](https://github.com/SpiderLabs/owasp-modsecurity-crs) and extract the files to `C:/xampp/apache/conf/extra/owasp-modsecurity-crs`.

5. **Restart Apache**:
   - Restart Apache from the **XAMPP Control Panel** to apply the changes.

### 3. Install **Splunk Free Version**

1. **Download Splunk**:
   - Go to [Splunk Downloads](https://www.splunk.com/en_us/download.html) and download the **Splunk Free** version for Windows.

2. **Install Splunk**:
   - Run the installer and follow the default instructions.

3. **Start Splunk**:
   - Open Splunk from the **Start Menu** and log in with the default username (`admin`) and password (`changeme`).

4. **Create HTTP Event Collector (HEC) Token**:
   - Go to **Settings** → **Data Inputs** → **HTTP Event Collector** → **New Token**.
   - Name the token (e.g., `modsec_logs`) and save the generated token.

### 4. Configure **Log Forwarding** to Splunk

1. **Create a Batch Script**:
   - Create a batch script (`forward_modsec_logs.bat`) to forward ModSecurity logs to Splunk using the HEC token.
     ```batch
     @echo off
     curl -k -X POST "http://localhost:8088/services/collector/event" -H "Authorization: Splunk YOUR_SPLUNK_HEC_TOKEN" -d "{\"event\": \"$(cat C:/xampp/apache/logs/modsec_audit.log)\", \"sourcetype\": \"modsec_audit\"}"
     ```
   - Replace `YOUR_SPLUNK_HEC_TOKEN` with the token from Splunk.

2. **Run the Batch Script**:
   - Double-click the batch file to forward logs from **ModSecurity** to **Splunk**.

### 5. Deploy and Configure **OWASP Juice Shop**

1. **Download OWASP Juice Shop**:
   - Download the vulnerable web application **OWASP Juice Shop** from [GitHub](https://github.com/OWASP/juice-shop).

2. **Deploy on XAMPP**:
   - Extract the **OWASP Juice Shop** files to `C:\xampp\htdocs\`.
   - Access the app by visiting `http://localhost/juice-shop` in your browser.

### 6. Test and Simulate Attacks

1. **Simulate SQL Injection** and **XSS**:
   - Use tools like **Burp Suite** or manually input malicious strings (e.g., `1' OR '1'='1` for SQLi) to simulate attacks on Juice Shop.
   - **ModSecurity** should block the attacks and log them to `modsec_audit.log`.

2. **Verify Splunk Logs**:
   - In **Splunk**, go to the **Search & Reporting** section and search for `sourcetype="modsec_audit"` to view the logs.
   - Verify that **Splunk** is receiving the logs and triggering alerts for the simulated attacks.

---

## Screenshots

### 1. **ModSecurity Configuration**:
   ![ModSecurity Config Screenshot](link_to_image_1)
   - Example of Apache configuration to include ModSecurity rules.

### 2. **Splunk Dashboard**:
   ![Splunk Dashboard Screenshot](link_to_image_2)
   - A Splunk dashboard showing alerts from ModSecurity logs.

### 3. **Juice Shop Attack Simulation**:
   ![Juice Shop Screenshot](link_to_image_3)
   - Simulating SQL Injection on the Juice Shop application and showing ModSecurity blocking the attack.

### 4. **Splunk Alert from ModSecurity Logs**:
   ![Splunk Alert Screenshot](link_to_image_4)
   - Example of a Splunk alert triggered by ModSecurity logs.

### 5. **SQL Injection Blocked by ModSecurity**:
   ![SQL Injection Block Screenshot](link_to_image_5)
   - Example of SQL Injection attack blocked by ModSecurity.

### 6. **XSS Attack Blocked by ModSecurity**:
   ![XSS Block Screenshot](link_to_image_6)
   - Example of XSS attack blocked by ModSecurity.

### 7. **Splunk Event Logs**:
   ![Splunk Logs Screenshot](link_to_image_7)
   - Example of ModSecurity event logs received and processed in Splunk.

### 8. **ModSecurity Log File Example**:
   ![ModSecurity Log Screenshot](link_to_image_8)
   - Example of a ModSecurity log entry from `modsec_audit.log`.

---

## Video Demonstration

For a more detailed walkthrough of the setup, configuration, and testing of the **WAF-SIEM-Integration** project, watch the video demonstration below:

[Watch the Video on YouTube](https://www.youtube.com/watch?v=your-video-link)

---

## Conclusion

This project demonstrates how to integrate a Web Application Firewall (WAF) with a Security Information and Event Management (SIEM) platform for real-time threat detection and incident response.

By following this guide, you’ve learned how to:

- Set up **ModSecurity** for WAF protection.
- Configure **Splunk** for SIEM functionality.
- Simulate common web application attacks and detect them in Splunk.

With this knowledge, you are better prepared for **Security Operations Center (SOC)** roles, including skills in incident investigation, log analysis, and alert management.

Feel free to explore
