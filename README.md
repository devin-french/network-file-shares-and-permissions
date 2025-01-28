# network-file-shares-and-permissions
<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" alt="Permissions Photo"/>
</p>

<h1>Understanding File Permissions</h1>
This lab focuses on file permissions and shares within an Active Directory domain. I'm logged in as Jane Doe (admin) on the domain controller VM and as a regular user on the client VM, building on a previous lab where the client was joined to the domain.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>


<img width="1280" alt="Screenshot 2025-01-26 at 5 15 05 PM" src="https://github.com/user-attachments/assets/c553ad10-0503-41d7-8690-185f9817f40b" />
<img width="1280" alt="Screenshot 2025-01-26 at 5 18 52 PM" src="https://github.com/user-attachments/assets/ca62c3ea-274e-4e6b-911c-e14ef8ba9275" />


Logged in as admin on the domain controller VM, I created 4 folders on the C:\ drive. To share and set permissions, I opened each folder’s Properties and used the Sharing tab. I set the following permissions:

- Domain Users: Read access on the read-access folder, Read/Write on the write-access folder.
- Domain Admins: Read/Write on the no-access folder (this will be updated later for the accounting folder).

<img width="1280" alt="Screenshot 2025-01-27 at 1 25 55 AM" src="https://github.com/user-attachments/assets/90e15bc6-0376-4340-ab9f-58f6322dc715" />

On the client VM, I navigated to the shared folders at \\dc-1. Some folders only allow viewing, others restrict access entirely. This is due to the folder permissions set for the Security Groups and the user's group membership.

<img width="1280" alt="Screenshot 2025-01-27 at 1 35 53 AM" src="https://github.com/user-attachments/assets/c4a85a98-e04a-4700-9e7d-9a16ec14d7f9" />
<img width="1280" alt="Screenshot 2025-01-27 at 1 38 26 AM" src="https://github.com/user-attachments/assets/3ff77641-fa44-49a9-a75c-d40c46ad6a27" />

On the domain controller, I created a new Security Group called ACCOUNTANTS in Active Directory. Then, I assigned Read/Write permissions for the ACCOUNTANTS group to the accounting folder.


<img width="1280" alt="Screenshot 2025-01-27 at 1 43 14 AM" src="https://github.com/user-attachments/assets/8831184c-83f2-4bef-86f3-54ae91af239e" />
<img width="1280" alt="Screenshot 2025-01-27 at 1 48 03 AM" src="https://github.com/user-attachments/assets/c00bcd90-684b-433c-b695-c224b49f62bf" />


The user couldn't access the accounting folder because they weren’t in the ACCOUNTANTS group. I logged off the client, added bon.rovej to the ACCOUNTANTS group in Active Directory, then logged back in. Bon.rovej can now access the accounting folder.

<h2>Lessons Learned </h2>

This lab helped me understand file permissions in Windows/Active Directory. In a real-world scenario, I would set permissions to ensure users only access what they need for their work, avoiding unnecessary permissions.
