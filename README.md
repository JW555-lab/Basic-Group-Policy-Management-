# Basic-Group-Policy-Management-
Group Policy Object creation and deployment in Active Directory - Restricting Control Panel access for a domain OU using PowerShell

In this project, I extended my existing Active Directory lab by creating and deploying a GPO to restrict Control Panel access for users in the sales organizational unit.

Actions and Observations:

This project builds on my existing joellab.local domain from the AD-Home-Lab project. Before I could apply a policy to Client01, it needed to be joined to the domain, which meant it first had to be pointed at DC1 for DNS resolution, since domain lookups depend on it.


1. I set Client01's DNS server to DC1's address and confirmed it with ipconfig /all. This shows the DNS Server correctly set to 192.168.10.1 alongside the client's own static IP.


<img width="1919" height="901" alt="1" src="https://github.com/user-attachments/assets/8fa09159-5dde-41df-9599-317faa63494f" />


2. With DNS pointed correctly, I joined Client01 to the domain. After the join and a restart, the System > About page confirmed the change, the Full device name now reads Client01.joellab.local instead of just a standalone workgroup machine.


<img width="1919" height="880" alt="2  Ipconfig" src="https://github.com/user-attachments/assets/f4bbd4c4-ee2b-4067-8399-7582c2b8efee" />


3. With Client01 domain joined, I moved to DC1 to build the actual policy. First, I created a new, empty GPO to hold the setting.
   ( New-GPO -Name "Restrict-ControlPanel" )


<img width="1919" height="933" alt="3  Join Client01 to the domain" src="https://github.com/user-attachments/assets/76c06e11-5c61-4e36-b57f-bfc34fe0816c" />


4. Next, I configured the actual policy setting inside that GPO a registry based policy that hides Control Panel from any user it applies to.


<img width="1919" height="871" alt="4  DC1 GPO created" src="https://github.com/user-attachments/assets/994f8d5a-e5ff-444f-acf3-53689557582e" />


5. Finally, I linked the GPO to the Sales OU, so the restriction applies to every user account in that department rather than the whole domain.


<img width="1918" height="911" alt="5  DC1 Configure the policy setting" src="https://github.com/user-attachments/assets/f3d680da-60a3-4f4b-8b38-aa7f30d4e231" />


6. The output confirms the link was created, the GPO is enabled, and it's targeting the correct OU.


<img width="1919" height="888" alt="6  Linked GPO to sales OU" src="https://github.com/user-attachments/assets/832e87a1-a60a-4ec0-8bb6-bc552d23681e" />


Summary:

This project shows the workflow behind centralized policy management in a Windows domain joining a workstation to a domain, building a GPO, configuring a setting inside it, and scoping it to a specific department using an OU link. 
