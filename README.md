# Process Integrity and Access Control
<h2> Lab </h2>

<h2> Scenario 1 </h2>
In this hands-on lab, I will assume the role of a cybersecurity investigator at TechNet Systems, where a potential security breach is under scrutiny. The IT team has flagged unusual system activity that may point to malicious processes running undetected. My task: investigate all active processes on the system, looking for any suspicious or unauthorized programs. I am expected to capture real-time snapshots of these processes while continuously monitoring for anomalies that could indicate a deeper compromise. By documenting and analyzing these processes, I will aim to uncover any hidden threats, ensuring system integrity while following forensic protocols for investigation and reporting.<br />

<h2> Scenario 2 </h2>
The IT team has raised concerns about weak passwords across the organization, potentially putting sensitive data at risk. My mission: utilize the john program to audit the strength of user passwords, identify any vulnerabilities, and document the passwords I uncover. This process will allow me to evaluate the effectiveness of password policies and ensure that user credentials meet security standards, all while adhering to best practices in ethical hacking and data protection.<br />

<h2> Scenario 3 </h2>
Following the discovery of unauthorized access, my next task is to lock down system access, including removing privileged sudo access to prevent further escalation. My objective: edit the sudoers file to revoke elevated permissions, ensuring that unauthorized users can no longer gain administrative control. This step is crucial in halting the spread of the breach and protecting the integrity of the system, all while adhering to best practices in incident response and system hardening.<br />

<h2> Scenario 4 </h2>
The IT department has raised concerns about potential unauthorized or suspicious user accounts and group memberships, which could present security risks. My mission: audit and clean up user and group configurations to ensure proper access controls and remove any threats. I will start by reviewing each user's UID and GID to confirm they are correctly assigned. Next, I’ll verify that only authorized users, such as the sysadmin account, remain in the sudoers group. Any unauthorized users in this group will be promptly removed and documented. I will also remove any users who should not have access to the system. Additionally, I'll ensure that non-admin users, including adam, billy, sally, and max, are part of the developers group, and I’ll create this group if necessary to support future file-sharing needs. By cleaning up and securing user groups, I will strengthen the system’s security posture and eliminate unnecessary risks.<br />

<h2> Scenario 5 </h2>
Following a recent security review, concerns have been raised about improper file permissions that could expose critical configuration files to unauthorized access. My mission: secure these essential files and directories by ensuring their permissions adhere to strict security standards.<br />

Guided by a checklist from the senior administrator, I will take the following steps:<br />

-  Adjust permissions on /etc/shadow to restrict both read and write access to the root user only.<br />
-  Modify permissions on /etc/gshadow to similarly limit both read and write access to the root user only.<br />
-  Secure /etc/group by setting permissions to allow root read and write access while granting read-only access to all other users.<br />
-  Ensure /etc/passwd permissions allow root read and write access, with read-only access provided to other users.<br />

<h2> Scenario 6 </h2>
Recent assessments have flagged several legacy and insecure services that may be running on the server, exposing it to risks such as unauthorized access or data breaches. My mission: identify and eliminate these unnecessary or insecure services to ensure the server operates in a safe and efficient manner.<br />

Following the guidance of the senior administrator, I will audit the system for the presence of specific services known to pose security risks, including:<br />

-  vsftpd.service (FTP)<br />
-  xinetd.service (Telnet)<br />
-  dovecot.service (IMAP or POP3)<br />
  
For any of these services discovered on the system, I will follow a structured approach to neutralize their risk:<br />

-  Stop the service immediately to ensure it is no longer active.<br />
-  Verify that the service is no longer running using system commands.<br />
-  Disable the service to prevent it from starting during future system reboots.<br />
-  Completely remove the service from the system to eliminate it as a potential threat.<br />


<h2> Step 1: Inventory of Active System Processes </h2>
<b>Purpose: </b> To assess the system for any unauthorized or suspicious processes that may indicate a security threat, ensuring that no malicious programs are running undetected. <br />
<b>My Action: </b> I first run a script file to compromise the system and then I will execute <b>top</b> a system command to generate a comprehensive list of all active processes. I will analyze this list to identify any processes that appear unfamiliar or out of place. By comparing them against known safe processes and reviewing resource usage, I can pinpoint potential anomalies that require further investigation or immediate action. <br />
<p align="center">
<img src="https://i.imgur.com/A0kAc80.png" height="80%" width="80%" alt="Running processses"/>
<img src="https://i.imgur.com/tsho2du.png" height="80%" width="80%" alt="Running processses"/>

<h2> Step 2: Copying the Shadow Password File </h2>
<b>Purpose: </b> To obtain and analyze the shadow password file for auditing purposes, ensuring that any weak or compromised user credentials can be identified and addressed. <br />
<b>My Action: </b> I will carefully copy the /etc/shadow file using secure file management commands such as <b>cp</b> while maintaining appropriate permissions to avoid exposing sensitive data. I’ll ensure I have the necessary root or administrative privileges to access and copy the file. After executing the command, I will double-check the file’s integrity and confirm that the file was copied successfully to a secure location for further analysis. <br />
<p align="center">
<img src="https://i.imgur.com/EOaP3cs.png" height="80%" width="80%" alt="Copying shadow file"/>


<h2> Step 3: Editing the Shadow Copy File to Retain Only System Users </h2>
<b>Purpose: </b> To refine the shadow password file by isolating only the active system users, making it easier to focus on user accounts that may require further scrutiny for security auditing. <br />
<b>My Action: </b> I will edit the shadow_copy file using a text editor <b>nano</b>, removing any unnecessary or irrelevant entries that do not pertain to actual system users. I’ll carefully review each line to ensure I retain only legitimate system users and remove any potential test accounts or obsolete entries. <br />
<p align="center">
<img src="https://i.imgur.com/RAKpJJi.png" height="80%" width="80%" alt="Editing Shadow_copy file"/>
<img src="https://i.imgur.com/22nOInc.png" height="80%" width="80%" alt="Editing Shadow_copy file"/>

<h2> Step 4: Running the Shadow File Through a Password Cracker </h2>
<b>Purpose: </b> To evaluate the strength of the system’s user passwords by running the shadow file through a password cracking tool, such as <b>John the Ripper</b>, to identify weak or easily guessable passwords that could pose security risks. <br />
<b>My Action: </b> I will use the <b>john program</b> to crack the passwords in the shadow_copy file <br />
<p align="center">
<img src="https://i.imgur.com/E4vUAe5.png" height="80%" width="80%" alt="Cracking password"/>
<img src="https://i.imgur.com/5pfFUeD.png" height="80%" width="80%" alt="Cracking password"/>

<h2> Step 5: Checking Sudo Access of Users with Weak Passwords </h2>
<b>Purpose: </b> To assess the security risk posed by users with weak passwords who may have elevated privileges, ensuring that only authorized, strong password holders maintain <b>sudo</b> access. <br />
<b>My Action: </b> Using commands like <b>sudo -lU</b> for specific users, I’ll identify who has sudo privileges. Any user with weak passwords who possesses these privileges will be flagged for immediate action. I will document these findings and plan to revoke sudo access for these high-risk accounts. <br />
<p align="center">
<img src="https://i.imgur.com/PggkFNJ.png" height="80%" width="80%" alt="Checking sudo access"/>

<h2> Step 6: Removing Sudo Access from Users in the Sudoers File </h2>
<b>Purpose: </b> To mitigate the risk of unauthorized access or privilege escalation, I will remove sudo access from users with weak passwords, ensuring that only trusted users maintain administrative privileges. <br />
<b>My Action: </b> I will carefully edit the /etc/sudoers file using a secure text editor, such as visudo, to safely remove the entries corresponding to users with weak passwords. I’ll search for user-specific lines granting sudo access and either comment them out or delete them entirely. <br />
<p align="center">
<img src="https://i.imgur.com/OEMTu2O.png" height="80%" width="80%" alt="Removing sudo access"/>
<img src="https://i.imgur.com/MqXAGCa.png" height="80%" width="80%" alt="Removing sudo access"/>

<h2> Step 7: Removing Less Access from Users in the Sudoers File </h2>
<b>Purpose: </b> To reduce unnecessary privilege escalation risks, I will remove the less access for users who should not have it and those with weak, ensuring that only authorized users can view restricted system information and preventing bad actors from accessing root privileges through the <b>less</b> command. <br />
<b>My Action: </b>  will edit the /etc/sudoers file using the <b>visudo</b> command to safely remove any entries that grant less access or similar viewing permissions to unauthorized users. I’ll search for any user-specific or group-specific configurations that allow this access and either comment them out or delete them entirely. <br />
<p align="center">
<img src="https://i.imgur.com/MqXAGCa.png" height="80%" width="80%" alt="Removing less access"/>

<h2> Step 8: Confirming Changes to the Sudoers File </h2>
<b>Purpose: </b> To ensure that the modifications made to the sudoers file are correct, effective, and error-free, preventing any disruption to legitimate system access or privilege escalation vulnerabilities. <br />
<b>My Action: </b> After editing the sudoers file, I will run a syntax check using the <b>visudo</b> command to confirm that no errors have been introduced. Additionally, I will manually review the file to ensure that only authorized users have retained the appropriate access. Once confirmed, I will check users privileges to confirm changes. <br />
<p align="center">
<img src="https://i.imgur.com/zC6YiY9.png" height="80%" width="80%" alt="Confirming changes"/>
<img src="https://i.imgur.com/COWsIh4.png" height="80%" width="80%" alt="Confirming changes"/>
<img src="https://i.imgur.com/1SNZRyS.png" height="80%" width="80%" alt="Confirming changes"/>

<h2> Step 9: Checking IDs for Every User on the System </h2>
<b>Purpose: </b> o verify the integrity of user accounts by inspecting each user’s UID (User ID) and GID (Group ID), ensuring they align with system policies and security standards.
 <br />
<b>My Action: </b> I will run the <b>id 'user'</b> command to review a list of all users and their associated UIDs and GIDs. I will check each entry to ensure that UIDs and GIDs are correctly assigned, especially for administrative accounts. <br />
<p align="center">
<img src="https://i.imgur.com/Xar9Dua.png" height="80%" width="80%" alt="Checking userID"/>


<h2> Step 10: Checking Groups Users Belong to on the System </h2>
<b>Purpose: </b> To ensure that users are assigned to the appropriate groups based on their roles and responsibilities, preventing unauthorized access to system resources or privileges. <br />
<b>My Action: </b> I will use the <b>groups</b> command for individual users to review all group memberships on the system. This will allow me to cross-check the groups that each user belongs to and identify any unauthorized or suspicious group assignments. I will pay special attention to privileged groups such as sudo or admin to confirm that only authorized accounts are included. <br />
<p align="center">
<img src="https://i.imgur.com/48pQP6r.png" height="80%" width="80%" alt="Checking groups"/>

<h2> Step 11: Removing Jack from the Sudo Group </h2>
<b>Purpose: </b> To enforce strict access controls by revoking elevated privileges from unauthorized users, ensuring that only trusted accounts remain in the <b>sudo</b> group. <br />
<b>My Action: </b> I will use the <b>usermod -G</b> command to remove Jack from the sudo group. After running the command, I will verify the change by using <b>groups jack</b> to confirm that Jack is no longer a member of the sudo group. <br />
<p align="center">
<img src="https://i.imgur.com/NfFVGA1.png" height="80%" width="80%" alt=""/>

<h2> Step 12: Removing Unauthorized Users and Groups from the System </h2>
<b>Purpose: </b> To enhance system security by identifying and removing any users or groups that are unauthorized or unnecessary, ensuring the system remains clean and free from potential security risks. <br />
<b>My Action: </b> For unauthorized users and groups, I will use the <b>deluser</b> and <b>delgroup</b> commands to remove the account and its associated files. <br />
<p align="center">
<img src="https://i.imgur.com/JUCOsSw.png" height="80%" width="80%" alt="Removing users and groups"/>

<h2> Step 13: Adding Users to the Appropriate Group </h2>
<b>Purpose: </b> To enforce proper access control by ensuring that all users are assigned to their designated groups, aligning with their roles and responsibilities. This helps streamline permissions and secures shared resources. <br />
<b>My Action: </b> I will create any missing groups using <b>addgroup</b> command. Next, I will add users to their designated groups using the <b>usermod</b> command. Then I will ensure users like Adam, Billy, Sally, and Max are part of the developers group and their own primary groups only. <br />
<p align="center">
<img src="https://i.imgur.com/7MbeNee.png" height="80%" width="80%" alt="Adding users to group"/>

<h2> Step 14: Setting File Permissions </h2>
<b>Purpose: </b> To secure critical system files by setting appropriate permissions, ensuring that sensitive data is accessible only to authorized users and preventing unauthorized modifications. <br />
<b>My Action: </b> Guided by best practices, I will adjust file permissions for key system files to enhance their security using the <b>chmod</b> command. After applying these changes, I will use <b>ls -l</b> to verify the updated permissions and document the adjustments for future reference.<br />
<p align="center">
<img src="https://i.imgur.com/mKHexpm.png" height="80%" width="80%" alt="Setting permissions"/>

<h2> Step 15: Checking for Vulnerabilities </h2>
<b>Purpose: </b> To identify and assess any existing weaknesses on the system that could be exploited by attackers, ensuring a proactive approach to securing the server. <br />
<b>My Action: </b> I will use vulnerability assessment tools such as <b>systemctl</b> to scan the system for misconfigurations, outdated software, or potential security gaps. After completing the scans, I will review the output for any identified vulnerabilities or warnings. <br />
<p align="center">
<img src="https://i.imgur.com/4xQMcbA.png" height="80%" width="80%" alt="Checking for vulnerabilities"/>
<img src="https://i.imgur.com/RvXiEA1.png" height="80%" width="80%" alt="Checking for vulnerabilities"/>
<img src="https://i.imgur.com/OT6FCNq.png" height="80%" width="80%" alt="Checking for vulnerabilities"/>

<h2> Step 16: Stopping Vulnerable Services </h2>
<b>Purpose: </b> To mitigate potential security risks by halting the operation of services identified as insecure, reducing the attack surface and preventing unauthorized access. <br />
<b>My Action: </b> After identifying vulnerable or unnecessary services during the audit, I will take immediate steps to stop them. Using the <b>systemctl stop</b> command, I will halt any flagged services. <br />
<p align="center">
<img src="https://i.imgur.com/m2TW6Uc.png" height="80%" width="80%" alt="Stopping vulnerable services"/>
<img src="https://i.imgur.com/qXZskVM.png" height="80%" width="80%" alt="Stopping vulnerable services"/>
<img src="https://i.imgur.com/v5xYq53.png" height="80%" width="80%" alt="Stopping vulnerable services"/>
<img src="https://i.imgur.com/FIXUSHP.png" height="80%" width="80%" alt="Stopping vulnerable services"/>

<h2> Step 17: Disabling Vulnerable Services </h2>
<b>Purpose: </b> To ensure vulnerable or unnecessary services do not restart during system reboots, thereby preventing them from reintroducing potential security risks. <br />
<b>My Action: </b> After stopping the flagged services, I will disable them to ensure they remain inactive. This will be accomplished using the <b>systemctl disable</b> command. <br />
<p align="center">
<img src="https://i.imgur.com/5QAs4ue.png" height="80%" width="80%" alt="Disabling vulnerable services"/>
<img src="https://i.imgur.com/KeFYGM3.png" height="80%" width="80%" alt="Disabling vulnerable services"/>

<h2> Step 18: Removing Vulnerable Services from the System </h2>
<b>Purpose: </b> To completely eliminate unnecessary or insecure services from the system, ensuring they cannot be reactivated or exploited in the future. <br />
<b>My Action: </b> After stopping and disabling the flagged services, I will uninstall them using the package management tools available on the system. <br />
<p align="center">
<img src="https://i.imgur.com/PtrInmB.png" height="80%" width="80%" alt="Removing services"/>
<img src="https://i.imgur.com/wCTSJ1r.png" height="80%" width="80%" alt="Removing services"/>
