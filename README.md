<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory: Group Policy & Account Management in the Cloud (Azure)(4/4)</h1>
This tutorial outlines common functions in Active Directory that are used to manage user, admin, and group permissions in Active Directory.  Using the virtual machines dc-1 and client-1 in the previous 3 guides, we will test permissions in Active Directory and demonstrate how to modify them.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Users & Computers

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>High-Level Permissions Management Steps</h2>

- Creating folders to assign separate permissions
- Assigning "Read-only" Permissions for Users
- Assigning "Read/Write" Permissions for Users
- Assigning "Read/Write" Permissions for Admins
- Observing Access in Client-1 via "bat.cop" User
- Creating an "ACCOUNTANTS" Group in Active Directory
- Assigning "ACCOUNTANTS" Permissions as a group
- Adding "bat.cop" User to "ACCOUNTANTS"
- Observe "bat.cop" User's permissions change


<h2>Permissions Management Steps</h2>

<p>
1) Log into dc-1 and create the following 4 folders: <br />
  <strong>- read-access <br />
  - "write-access" <br />
  - "no-access" <br />
  - "accounting"</strong> <br />
  <br />
  <br />
<img src="https://i.imgur.com/8N9IybO.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
2) To begin allocating permissions, navigate to: <strong>[Right-Click] read-access > Properties > Sharing > Share</strong>.<br />
  <br />
<img src="https://i.imgur.com/ChfzJYQ.png" height="60%" width="40%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/k0USdbk.png" height="60%" width="40%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/Z6WpZu0.png" height="60%" width="40%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
3) If <strong>"Read"</strong> permissions were allocated successfully, in <strong>Client-1</strong> (our test user), we should have access to the <strong>"read-access"</strong> folder.<br />
  <br />
<img src="https://i.imgur.com/svaH8NV.png" height="60%" width="40%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
4) Once here, add <strong>"Domain Users"</strong> and give them <strong>"Read/Write"</strong> permissions by clicking on the dropdown as seen below.<br />
  <br />
<img src="https://i.imgur.com/a1bWXJU.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/FAALtXa.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
5) If <strong>"Read/Write"</strong> permissions were allocated successfully, in <strong>Client-1</strong> (our test user), we should have access to the <strong>"write-access"</strong> folder. <br />
  <br />
<img src="https://i.imgur.com/MWphZa7.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
6) Open the command prompt as an administrator, and type <strong>"gpupdate /force"</strong>.  As you can see, the updates should complete successfully.<br />
  <br />
<img src="https://i.imgur.com/nyNmjWe.png" height="60%" width="100%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/SQWk3VC.png" height="60%" width="100%" alt="Disk Sanitization Steps"/> <br />

  
</p>
<br />
<br />
<br />
<br />

<p>
7) If "Read/Write" permissions were allocated successfully to only admins, in Client-1 (our test user), we should NOT have access to the "no-access" folder, since we are logged onto Client-1 as a user and not an admin. <br />
  <br />
<img src="https://i.imgur.com/orEfnz4.png" height="60%" width="100%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
8) Now, we will create a new "ACCOUNTANTS" group in dc-1 to assign permissions to the "accounting" folder. Navigate to Active Directory Users & Computers > [Right Click] mydomain.com > New > Organizational Unit. Name the new Organizational Unit "_GROUPS", this is where the "ACCOUNTANTS" group will be located. <br />
  <br />
<img src="https://i.imgur.com/Lya01lw.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />



<p>
9) Next, navigate to: Active Directory Users & Computers > mydomain.com > [Right Click] Groups > New > Group. Name the group "ACCOUNTANTS".<br />
  <br />
  <br />
<img src="https://i.imgur.com/J1gt5Py.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/CmrZU2y.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br /> 
</p>
<br />
<br />
<br />
<br />


<p>
10) Next, navigate to the "accounting" folder we created in dc-1 and select properties.  Give "Read/Write" permissions to the "ACCOUNTANTS" group as shown below.<br />.
  <br />
<img src="https://i.imgur.com/U1mxqJE.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/aa0o4bP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
11) If "Read/Write" permissions were allocated successfully to only "ACCOUNTANTS", in Client-1 (our test user), we should NOT have access to the "accounting" folder, since we are logged onto Client-1 as a user which has NOT been added to the "ACCOUNTANTS" group in Active Directory. <br />
  <br />
<img src="https://i.imgur.com/jqn4kX2.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
12) To add our test user "bat.cop" to the "_USERS" group, navigate to Active Directory Users and Computers > mydomain.com > _GROUPS > [Double Click] ACCOUNTANTS.  Then, select "Add" and add "bat.cop" as a user, giving them ACCOUNTANTS group permissions. <br />
  <br />
<img src="https://i.imgur.com/gSvLELe.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/O6PjBn4.png" height="60%" width="40%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
13) As seen below, in the event viewer, you can see all logon attempts and make security decisions based off of them.  Here, we see all login attempts by <strong>bat.cop</strong> and can see where access was restored in the lab environment.</strong><br />
  <br />
<img src="https://i.imgur.com/rVMANvx.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

14) Log into <strong>dc-1</strong> as an administrator, navigate to the search bar, and type <strong>"run"</strong>. Then, type <strong>"gpmc.msc"</strong>. <br />
  <br />
<img src="https://i.imgur.com/qnmxkSn.png" height="40%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
