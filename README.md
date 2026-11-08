# Domain-Controller-IT-Support-Project
Windows Server Active Directory home lab with Group Policy, file share permissions, and a Jira Service Management helpdesk workflow with TeamViewer remote support.


---


## 1. Lab Environment


---


<img width="1085" height="604" alt="1" src="https://github.com/user-attachments/assets/f7900826-e7dc-41ee-b084-3005d4f7c521" />

Figure_1:VM dashboard showing all three machines running: one Windows Server (Domain Controller) and two Windows 11 Pro client PCs.


---


<img width="1024" height="711" alt="2" src="https://github.com/user-attachments/assets/ad2b664e-ea59-4f7d-820b-9cf8b7c86f4e" />

Figure_2:Server Manager dashboard on the Domain Controller, showing the installed server roles and the overall health of the server.


---


<img width="532" height="591" alt="3" src="https://github.com/user-attachments/assets/f9cf0ed6-6bf3-4c86-a43e-74f88f581c2d" />

Figure_3:System Properties on the server, showing the full computer name and the domain name, which confirms the server is configured as the domain controller.


---


## 2. Active Directory Structure


---


<img width="718" height="457" alt="4" src="https://github.com/user-attachments/assets/d14aacbb-e1eb-4f29-9041-a70488f04c39" />


Figure_4:The "Company Groups" OU in Active Directory Users and Computers, containing four security groups, one for each department. These groups are used to control access to shared folders.


---


<img width="675" height="417" alt="5" src="https://github.com/user-attachments/assets/fcd9b4de-d2a8-474f-bc3b-75f6b9b00902" />


Figure_5:The "Company Computers" OU containing both client PCs (PC1 and PC02), so computer-level Group Policies can be applied to them.


---


<img width="717" height="410" alt="6" src="https://github.com/user-attachments/assets/2a028c55-d924-409f-acc9-722dc597a483" />


Figure_6:The "Departments" OU with four department OUs: Finance, HR, IT and Marketing. Each department's users are kept separate so policies and permissions can be managed per department.


---


<img width="649" height="504" alt="7" src="https://github.com/user-attachments/assets/89e8637e-815b-41c2-a2ee-20569563af5c" />


Figure_7:The HR OU containing two HR user accounts.


---


<img width="640" height="506" alt="8" src="https://github.com/user-attachments/assets/b75ed7e7-656d-4a37-9c3c-53ac58bb1038" />


Figure_8:The IT OU containing two IT user accounts. These are the support staff who handle tickets.


---


<img width="410" height="466" alt="9" src="https://github.com/user-attachments/assets/9dfd9f1f-094d-40a4-bc2b-5e72af487e5b" />


Figure_9:System Properties on PC02, showing its full computer name and that it is joined to the domain.


---


<img width="1600" height="836" alt="10" src="https://github.com/user-attachments/assets/755b99e3-8307-463d-9f97-69fc8e447ffc" />


Figure_10:Windows 11 login screen with a domain user, Alex Costa from the IT department, signing in. This confirms domain authentication works on the client PC.


---


## 3. Group Policy


---


<img width="448" height="622" alt="11" src="https://github.com/user-attachments/assets/0207ca4f-82f0-47d0-a561-95e100718b75" />


Figure_11:Group Policy Management Console showing one GPO linked to the Company Computers OU and two GPOs linked to the HR OU.


---


<img width="947" height="652" alt="12" src="https://github.com/user-attachments/assets/789054bd-3642-449e-bbe2-e7a5950ee1f7" />


Figure_12:HR GPO that sets a single wallpaper on all HR desktops. Users cannot change it.


---


<img width="893" height="669" alt="13" src="https://github.com/user-attachments/assets/3d968157-c169-4a91-b71b-d72c734d9c17" />


Figure_13:Company Computers GPO with an account lockout policy: accounts lock for 30 minutes after 5 invalid logon attempts. This protects against password guessing.


---


<img width="886" height="652" alt="14" src="https://github.com/user-attachments/assets/adc48308-f64a-48bb-a482-539e248b235a" />


Figure_14:HR GPO that prohibits access to Control Panel and PC Settings, so HR users cannot change system settings.


---


<img width="663" height="807" alt="15" src="https://github.com/user-attachments/assets/8e5c56fc-4460-480e-8a03-29922c7156f4" />


Figure_15:`gpresult /r` run in Command Prompt on the client PC, confirming that the HR Wallpaper and Disable Control Panel GPOs are applied.


---


<img width="1685" height="860" alt="16" src="https://github.com/user-attachments/assets/d14251f3-55fa-4b99-b1aa-76ba7b88a327" />


Figure_16:HR user's desktop with the wallpaper applied by the admin GPO, which verifies the policy works.


---


## 4. File Shares and Permissions


---


<img width="699" height="445" alt="17" src="https://github.com/user-attachments/assets/2db766a1-09ad-41df-a3dc-bc318625794f" />


Figure_17:Shared folders on the Domain Controller, one for each department: Finance, HR, IT and Marketing.


---


<img width="831" height="682" alt="18" src="https://github.com/user-attachments/assets/34a404da-ce7d-45eb-bd06-83bf33c6b098" />


Figure_18:Sharing tab of the HR folder Properties, showing the network path `\\DC01\HR_FILE`.


---


<img width="830" height="677" alt="19" src="https://github.com/user-attachments/assets/c5ee3629-60a5-42a6-b951-1412d27539ec" />


Figure_19:Security tab of the HR folder, with permissions assigned to the HR security group, so only HR members can access it.


---


<img width="638" height="588" alt="20" src="https://github.com/user-attachments/assets/cbc18bfa-d7da-4c3b-9946-9a8bbbc74f7c" />


Figure_20:HR user opening the HR folder successfully.


---


<img width="1111" height="642" alt="21" src="https://github.com/user-attachments/assets/0b7917f7-6f26-4555-b300-1851e0d74357" />


Figure_21:The same HR user trying to open the Finance folder and getting "Windows cannot access \\DC01\Shares\FINANCE_FILE". This confirms department access is properly restricted.


---


<img width="1633" height="813" alt="22" src="https://github.com/user-attachments/assets/abd9fd89-a87b-4f82-8678-309350850734" />


Figure_22:Jira Service Management, "Support" project, Queue Overview. This is where IT staff see and manage tickets raised by users.


---


## 5. Scenario 1: Password Reset


---


<img width="1598" height="805" alt="23" src="https://github.com/user-attachments/assets/d4ce80c1-38d1-4a60-bbde-737c3490a42b" />


Figure_23:Ticket assigned to the IT technician: "Request to Change Password", because the user forgot their old password.


---


<img width="865" height="696" alt="24" src="https://github.com/user-attachments/assets/96cedc55-ad79-40eb-ab72-0a0368c180c0" />


Figure_24:The HR user's original ticket, "Request to Change Password", raised through Jira after forgetting the old password.


---


<img width="814" height="544" alt="25" src="https://github.com/user-attachments/assets/cafbad2b-dbca-431f-90f1-148ea544bd92" />


Figure_25:IT technician logs into the Domain Controller, opens Active Directory Users and Computers and finds the user Pooja Saxena.


---


<img width="749" height="521" alt="26" src="https://github.com/user-attachments/assets/e06ce8b0-f16e-4db4-9a4d-8d541f35335d" />


Figure_26:Reset Password window with a new temporary password entered and confirmed, and "User must change password at next logon" ticked.


---


<img width="1395" height="842" alt="29" src="https://github.com/user-attachments/assets/6da692f1-c739-4184-8a68-0984ba612757" />


Figure_29:Login screen for Pooja Saxena showing that the password must be changed before signing in. The temporary password was shared through a separate messaging channel, not in the ticket.


---


<img width="1343" height="833" alt="30" src="https://github.com/user-attachments/assets/188a800c-f901-4584-aa74-f78bea2ee563" />


Figure_30:Pooja Saxena enters her own new password and gets the message "Your password has been changed". Ticket resolved.


---


## 6. Scenario 2: Folder Access Request


---


<img width="870" height="704" alt="31" src="https://github.com/user-attachments/assets/34cd4830-1524-4c33-8602-e3f632020694" />


Figure_31:New Jira ticket, "Access Request": the user needs access to the HR Confidential folder after a promotion.


---


<img width="1636" height="810" alt="49" src="https://github.com/user-attachments/assets/c5cb0ea9-ee9a-47ea-88b2-b56478f099c8" />


Figure_49:Jira Queue Overview showing the new Access Request ticket in the queue.


---


<img width="1600" height="805" alt="50" src="https://github.com/user-attachments/assets/91b34dc9-4c77-4ecb-8557-affa17185583" />


Figure_50:IT technician clicks "Assign to me" to take ownership of the ticket.


---


<img width="805" height="696" alt="32" src="https://github.com/user-attachments/assets/83660915-c36f-40ae-9393-2c756b9dccfa" />


Figure_32:On the Domain Controller, the IT technician opens the HR Confidential folder Properties, Security tab. Only one senior HR user currently has access.


---


<img width="857" height="699" alt="33" src="https://github.com/user-attachments/assets/b5d7330f-f39d-4506-b3b3-8483539582d6" />


Figure_33:Permissions window for HR Confidential, with the Add option visible.


---


<img width="973" height="696" alt="34" src="https://github.com/user-attachments/assets/4120329a-b9c9-490b-93ce-718078ea2f91" />


Figure_34:Add user window with Pooja Saxena selected, then OK.


---


<img width="839" height="694" alt="35" src="https://github.com/user-attachments/assets/09013b42-00a1-4a9c-90e7-18b3f5ba8e9d" />


Figure_35:Permissions for HR Confidential now list two users, including Pooja Saxena.


---


<img width="1633" height="805" alt="36" src="https://github.com/user-attachments/assets/499eee6b-fef4-4fcf-9318-f14bdbf2b12e" />


Figure_36:IT technician replies in Jira: the permission has been changed and the user can now access the HR Confidential folder.


---


<img width="780" height="642" alt="37" src="https://github.com/user-attachments/assets/2ada085f-40c0-4997-a992-bc9d44e8f412" />


Figure_37:Pooja Saxena opens the HR Confidential folder successfully, which confirms the fix.


---


## 7. Scenario 3: Software Installation with Remote Support


<img width="1562" height="796" alt="38" src="https://github.com/user-attachments/assets/354ac48b-d686-4523-a8ca-62757461cefe" />


Figure_38:HR user downloads Notepad++ from the internet and clicks Open File.


---


<img width="661" height="735" alt="39" src="https://github.com/user-attachments/assets/d5d68fcd-982b-4b2f-8e6f-c903e7e589fb" />


Figure_39:User Account Control popup asking for an admin username and password. The HR user does not have admin credentials, so the install is blocked. This is expected behavior for standard users.


---


<img width="780" height="691" alt="40" src="https://github.com/user-attachments/assets/dd4c3eb3-3086-40f9-8a7a-4c7ad6b81d55" />


Figure_40:HR user raises a Jira ticket: "Need Admin Access to Install Notepad++".


---


<img width="1636" height="805" alt="41" src="https://github.com/user-attachments/assets/daccabb1-5687-4ef7-97c2-306fdd370721" />


Figure_41:IT technician sees the ticket in the Jira Queue Overview.


---


<img width="1598" height="805" alt="42" src="https://github.com/user-attachments/assets/31057c9b-c4a6-4f60-a496-ea826e9c4dfd" />


Figure_42:IT technician assigns the ticket to themselves.


---


<img width="1685" height="860" alt="43" src="https://github.com/user-attachments/assets/ec53b439-9327-4b9e-ad63-6fcc7f247813" />


Figure_43:IT technician connects to the HR computer through TeamViewer, using a link sent by email.


---


<img width="1685" height="860" alt="44" src="https://github.com/user-attachments/assets/58335260-a69c-42ac-aebd-e3ea97c9e173" />


Figure_44:The same admin credentials popup appears on the HR computer during the remote session.


---


<img width="1685" height="860" alt="45" src="https://github.com/user-attachments/assets/bc8871b6-9a2b-468e-b920-b6e5150849dd" />


Figure_45:IT technician enters the admin username and password and clicks Yes.


---


<img width="1685" height="860" alt="46" src="https://github.com/user-attachments/assets/2966ff5e-c352-41ff-b917-b839bca71677" />


Figure_46:Notepad++ installation popup.


---


<img width="1685" height="860" alt="47" src="https://github.com/user-attachments/assets/15f677ab-75db-42de-a8f0-a3fabc9b3dff" />


Figure_47:Installation finishes. Click Finish.


---


<img width="1024" height="768" alt="48" src="https://github.com/user-attachments/assets/cee4ddd9-e773-48f2-a2e1-f0f1f0a2ba1a" />


Figure_48:HR user opens Notepad++ and the dashboard loads, confirming the install worked.
