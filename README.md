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
   - **Description**: EDR solutions continuously monitor endpoints for suspicious activities, detect threats in real-time, and provide automated or manual response options.  
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

6. **Playbook (Incident Response Workflow)**  
   - **Description**: A structured set of predefined steps and actions that security teams follow to investigate and respond to specific security incidents.  
   - **Use Case**: A phishing incident response playbook that includes automated email analysis, URL detonation, and employee notifications.  

7. **Telemetry (Security Data Collection & Analysis)**  
   - **Description**: The continuous collection, processing, and analysis of security-related data from various sources, such as endpoints, networks, and cloud environments.  
   - **Use Case**: Using endpoint telemetry to detect and investigate anomalies, such as unauthorized process executions or unusual network connections.  

8. **LaZagne (Credential Extraction Tool)**  
   - **Description**: An open-source tool designed to retrieve stored passwords from various applications, including browsers, databases, and Wi-Fi networks.  
   - **Use Case**: Running LaZagne on a compromised endpoint to extract stored credentials and assess the impact of a security breach.  

<br>

## Table of Contents
1. [Design a Logic Diagram](#design-a-logic-diagram)
   - Create a playbook workflow
   - Brainstorm playbook actions
     
2. [Setup LimaCharlie](#setup-limacharlie)
   - Install and Setup LimaCharlie
   - Confirm Events

3. [Generate Telemetry](#generate-telemetry)
   - Generate Telemetry using LaZagne
   - Create Detection & Response Rule

4. [Setup Slack and Tines](#setup-slack-and-tines)
   - Setup Slack and Tines
   - Test Connection (LimaCharIie + Tines)

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
3. After logging in to LimaCharlie, **create an organization**.  
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

<br>

Here’s your content with corrected grammar and improved clarity:  

---

## **Generate Telemetry**  

1. **Download LaZagne**  
   - Visit the [LaZagne GitHub page](https://github.com/AlessandroZ/LaZagne).  
   - Navigate to **Releases** and download the `LaZagne.exe` file in your Windows 10 VM.  

2. **Execute LaZagne**  
   - Open **PowerShell as Administrator**.  
   - Navigate to the directory where the `LaZagne.exe` file is downloaded.  
   - Run the executable, and you should see an output similar to the one below:  

   ![Screenshot from 2025-02-21 16-51-10](https://github.com/user-attachments/assets/01514cd8-3592-4814-ac34-068d2e3189e9)  

3. **Verify Telemetry in LimaCharlie**  
   - Open the browser and go to **LimaCharlie**.  
   - Navigate to **Sensors** → **Sensors List**.  
   - Click on your **Windows 10 desktop name**.  
   - Go to **Timelines** and search for `"lazagne"`.  

   ![Screenshot from 2025-02-21 17-00-49](https://github.com/user-attachments/assets/a1b932a0-4dd5-45f0-bcf9-ef2cb9ab7848)  

4. **Create a Detection & Response (D&R) Rule**  
   - Navigate to your **organization page** → **Automation** → **D&R Rules** → **New Rule**.  
   - Name the rule as desired.  
   - Under **Detect**, enter the following configuration:  

   ```yaml
   events:
     - NEW_PROCESS
     - EXISTING_PROCESS
   op: and
   rules:
     - op: is windows
     - op: or
       rules:
       - case sensitive: false
         op: ends with
         path: event/FILE_PATH
         value: LaZagne.exe
       - case sensitive: false
         op: contains
         path: event/COMMAND_LINE
         value: LaZagne
       - case sensitive: false
         op: is
         path: event/HASH
         value: 'PASTE-YOUR-HASH-WE-SEEN-IN-STEP-3' 
   ```

   ![Screenshot from 2025-02-21 17-13-23](https://github.com/user-attachments/assets/057532ad-c885-4dab-978b-0368731d9507)  

   - Replace **PASTE-YOUR-HASH-WE-SEEN-IN-STEP-3** with the actual hash observed in **Step 3**.  
   - In this example, the hash value is:  
     ```
     467e49f1f795c1b08245ae621c59cdf06df630fc1631dc0059da9a032858a486
     ```
     *(Your hash will be different.)*  

5. **Define the Response Action**  
   - In the **Respond** field, enter the following:  

   ```yaml
   - action: report
     metadata:
       author: YOUR NAME
       description: TEST - Detects LaZagne Usage
       falsepositives:
         - ToTheMoon
       level: high
       tags:
         - attack.credential_access
     name: YOUR NAME - HackTool - LaZagne
   ```

6. **Create the Rule**  
   - Click the **Create** button to finalize the D&R rule.  

7. **Test the Rule with a Sample Event**  
   - Scroll down to **Target Event** on the same page.  
   - Paste the event found in **Step 3**.  
   - Click **Test Event**.  

   ![Screenshot from 2025-02-21 17-21-04](https://github.com/user-attachments/assets/47b31109-1c93-459c-8938-3850e9cccbb9)  

8. **Verify Rule Execution**  
   - If configured correctly, clicking **Test Event** should yield the following output:  

   ![Screenshot from 2025-02-21 17-24-00](https://github.com/user-attachments/assets/b8bec5dd-5ef5-4f5b-8644-a8807f848d4c)  

9. **Trigger an Alert**  
   - Open **PowerShell** again and execute the `LaZagne.exe` file.  
   - Go back to **LimaCharlie** → **Organization Page** → **Detection**.  
   - You should see an alert similar to this:  

   ![Screenshot from 2025-02-21 17-29-06](https://github.com/user-attachments/assets/2a28ced0-e9c2-41a8-8201-128f4d1d4137)  

10. **Troubleshooting: Missing VM in LimaCharlie Sensors**  
    - If your Windows 10 VM is not appearing in the **Sensors List**, and no alerts/logs are being generated:  
      - Open **Services** in Windows 10 VM.  
      - Restart the **LimaCharlie process**.  

    ![Screenshot from 2025-02-21 17-34-34](https://github.com/user-attachments/assets/af5d1e2f-e4d6-4f65-8612-04ed52f43bf2)  

This should resolve the issue and allow your sensor to appear in **LimaCharlie**.  

[Back to top](#table-of-contents)

<br>

## Setup Slack and Tines

[Back to top](#table-of-contents)



