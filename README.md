<h1 align="center">SOAR EDR PROJECT</h1>

<h1 align="center">
  
[![Made With](https://img.shields.io/badge/Made%20With-6aff08)](http://www.firsttimersonly.com/)
[![Limacharlie](https://img.shields.io/badge/Limacharlie-3e8dc9)](http://www.firsttimersonly.com/)
[![Tines](https://img.shields.io/badge/Tines-383741)](http://www.firsttimersonly.com/)
[![Slack](https://img.shields.io/badge/Slack-35b881)](http://www.firsttimersonly.com/)

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

</h1>

Automate security workflows by integrating LimaCharlie (EDR) with Tines (SOAR) for real-time threat detection and response. Learn how to configure, deploy, and enhance your cybersecurity posture with automation.
<br>
### **Key Terminologies Before Starting the Project**  

1. **SOAR (Security Orchestration, Automation, and Response)**  
   - **Description**: SOAR platforms automate security workflows by integrating various security tools, enabling faster and more efficient incident response.  
   - **Use Case**: Automating phishing email analysis by extracting indicators, checking them against threat intelligence feeds, and triggering a response.  

2. **EDR (Endpoint Detection and Response)**  
   - **Description**: EDR solutions continuously monitor endpoints for suspicious activities, detect threats in real time, and provide automated or manual response options.  
   - **Use Case**: Detecting a compromised laptop executing malicious scripts and automatically isolating it from the network.  

3. **Tines (SOAR Platform)**  
   - **Description**: A no-code SOAR platform that enables security teams to create automated workflows for incident response, threat intelligence, and security monitoring.  
   - **Use Case**: Automating security alert triage by collecting data from SIEMs, enriching it with threat intelligence, and escalating critical alerts.  

4. **LimaCharlie (EDR & Security Infrastructure)**  
   - **Description**: A cloud-native security operations platform providing EDR, log collection, automation, and security tooling as a service.  
   - **Use Case**: Deploying LimaCharlie agents across an enterprise to detect and respond to endpoint threats in real-time.  

5. **Slack (Collaboration & Incident Communication)**  
   - **Description**: A messaging platform used by security teams for real-time collaboration, alerting, and incident response coordination.  
   - **Use Case**: Integrating Slack with SOAR tools like Tines to automatically notify security teams when a critical security event occurs.

<br>

## Table of Contents
1. [Design a Logic Diagram](#design-a-logic-diagram)
   - Create playbook workflow
   - Brainstorm playbook actions
     
2. [Setup LimaCharlie](#setup-limacharlie)
   - Install and Setup LimaCharlie
   - Confirm Events
  
<br>

## Design a Logic Diagram
Use [draw.io](https://app.diagrams.net/) to draw following diagram as below:

![Diagram drawio](https://github.com/user-attachments/assets/d647cac5-31c9-419b-9d55-947da5348a70)

[Back to top](#table-of-contents)

<br>

## Setup LimaCharlie
Here’s your instruction with corrected grammar and clarity:

---

1. **Set up a Windows 10 VM** on VirtualBox or VMware.  
2. **Open a browser** inside the Windows 10 VM and create an account at [LimaCharlie](https://app.limacharlie.io/).  
3. After successfully logging in to LimaCharlie, **create an organization**.  
4. On the left-hand side, click on **Sensors** → **Installation Keys** → Click on **Create Installation Key**.  
5. In the **Description** field, enter any name and click the **Create** button.  
6. You will see a key generated with the name you entered in the Description field.  
7. Scroll down on the same page until you find **Sensors Download**.  
8. Under **EDR**, right-click on **Windows 64-bit**, copy the link, and paste it into a new tab to download the agent.  
9. Scroll back up and copy the **Sensor Key** from the generated Installation Key.  
10. **Open PowerShell as Administrator**, then navigate to the directory where the agent was downloaded.  
11. Run the following command:  
    ```
    your-agent-file.exe -i paste-sensor-key
    ```
    *(Replace `your-agent-file.exe` with the actual filename and `paste-sensor-key` with the copied Sensor Key.)*  
12. To verify that the agent was installed successfully:  
    - Go back to **LimaCharlie** in the browser.  
    - Under **Sensors**, click on **Sensors List**.  
    - If everything was done correctly, your Windows 10 VM's desktop name should appear in the list.  

![image](https://github.com/user-attachments/assets/3fe33cf6-51f7-4865-8181-decd75f0642c)


[Back to top](#table-of-contents)


