# Managing-Security-Groups-Mapped-Drives-Personal-Drive-Configuration

This part of my home lab documentation is dedicated to the management of **Security Groups**, **Mapped Drives**, and **Personal Drives** within a domain environment. The project illustrates the process of creating and configuring security groups to manage permissions, establishing mapped drives for network access, and setting up personal drives for individual user storage.

<h2>Goals</h2>

- Establish and set up **Security Groups** within Active Directory to regulate access to resources and network drives.
- Configure **Mapped Drives** to allow users to automatically access shared resources throughout the network.
- Set up **Personal Drives** for each user to securely store data within the domain environment.
- Apply best practices for **permission management** by utilizing security groups and ensuring proper access control for both mapped and personal drives.

<h2>Walkthrough</h2>

In this home lab, our focus will be on setting up **Security Groups**, **Mapped Drives**, **Personal Drives**, and **Drive Letter Mapping**. To begin, open **Server Manager** on your **Windows Server 2022**. Next, choose **File and Storage Services** from the left sidebar, then click on **Shares**. Right-click and choose **New Share**.



1. <p align="center">
   <img src="https://i.imgur.com/FSKvUaW.png" height="80%" width="80%"/>
   <br />
   <br />
</p>

Proceed by clicking Next until you arrive at the Specify Share Name screen. Assign the name HR to the share, then keep clicking Next until you reach the Create button. Click Create to complete the setup of the shared folder.

2. <p align="center">
   <img src="https://i.imgur.com/B71gKKb.png" height="80%" width="80%"/>
   <br />
   <br />
</p>

Repeat the procedure, but this time label the share as Personal. Click Next, then select Create to finalize the setup for the second shared folder.

3. <p align="center">
   <img src="https://i.imgur.com/kNKY5S0.png" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now that our shared folders are set up, navigate to File Explorer → This PC → Local C Drive → Shares to access them.

4. <p align="center">
   <img src="https://i.imgur.com/tmU0KEy.png" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now, navigate to Active Directory Users and Computers → right-click on Users → choose New → then select Group to establish a new security group.

5. <p align="center">
   <img src="https://i.imgur.com/nwXhsij.png" height="80%" width="80%"/>
   <br />
   <br />
</p>

Designate the group as "HR".



Now, let's double-click on "HR" → select "Managed By" → click on "Change" and then input "Helpdesk".

7. <p align="center">
   <img src="https://i.imgur.com/uHzHAvS" height="80%" width="80%"/>
   <br />
   <br />
</p>

We will establish another group in the same manner and designate it as "Personal," which will also be overseen by Helpdesk.

8. <p align="center">
   <img src="https://i.imgur.com/pYlxE1E" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now, return to the shared folders. Right-click on Personal → choose Properties, then proceed to the Sharing tab. Highlight the path \SERVER2022\Personal, right-click, and select Copy. After that, paste this path into the Description field of the Personal properties in Active Directory Users and Computers.

9. <p align="center">
   <img src="https://imgur.com/gptqzvU" height="80%" width="80%"/>
   <br />
   <br />
</p>

10. <p align="center">
   <img src="https://imgur.com/shfwwTd" height="80%" width="80%"/>
   <br />
   <br />
</p>

Repeat the procedure for the HR shared folder. After completing that, access the HR group in Active Directory Users and Computers and navigate to the Members tab. Click on Add, then search for and include Bob in the group.

11. <p align="center">
    <img src="https://imgur.com/RlJnFhS" height="80%" width="80%"/>
   <br />
   <br />
</p>

Repeat the procedure for the Personal share folder. Access the Personal group within Active Directory Users and Computers, click on the Members tab, choose Add, and subsequently include Bob in the group.

12. <p align="center">
  <img src="https://imgur.com/ecpTcLQ" width="800">
   <br />
   <br />
</p>

To confirm, choose the HR organizational unit within the domain, then double-click on Bob. After that, navigate to the Member Of tab to ensure that Bob is part of the HR group.

13. <p align="center">
   <img src="https://imgur.com/W2QXIfW" height="60%" width="60%"/>
  <br />
   <br />
</p>

Now, we will concentrate on setting up the appropriate permissions. To achieve this, go to the Personal share folder, right-click on it, and choose Properties. In the Security tab, click on Advanced, and then select Disable Inheritance.

   14. <p align="center">
   <img src="https://imgur.com/IY0pAr1" height="60%" width="60%"/>
   <br />
   <br />
</p>

   Choose the initial option "Covert inherited permissions..."

15. <p align="center">
   <img src="https://imgur.com/4KCOHdW" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now eliminate both "Users". This action will exclude any users who lack access to this personal folder.

16. <p align="center">
   <img src="https://imgur.com/al39hom" height="80%" width="80%"/>
   <br />
   <br />
</p>

Click on Add, then choose Select a principal. Include the Helpdesk group and grant the Modify permission in the basic permissions section.

17. <p align="center">
   <img src="https://imgur.com/RdkiAjr" height="80%" width="80%"/>
   <br />
   <br />
</p>
   
Repeat the procedure and include the Personal group, making sure that the Modify permission is activated in the basic permissions section.

18. <p align="center">
   <img src="https://imgur.com/PB3NM75r" height="80%" width="80%"/>
   <br />
   <br />
</p>

Currently, in the properties of the Personal folder, go to the Sharing tab → select Share... → right-click on Personal → opt for Read/Write, and then click Share.

19. <p align="center">
   <img src="https://imgur.com/XAzL02X" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now, proceed with the same steps on the **HR** folder:

1. Right-click on **HR** → select the **Security** tab → click on **Advanced**.
2. Choose **Disable Inheritance** → opt for **Convert inherited permissions...**.
3. Remove the two **Users** permissions.
4. Click on **Add**, then **Select a Principal**, and include **Helpdesk**.
5. Activate **Modify** for basic permissions.
6. Click **OK**, followed by **Apply**.



20. <p align="center">
   <img src="https://imgur.com/eoIj7Sp" height="80%" width="80%"/>
   <br />
   <br />
</p>

Now, let's go through the same procedure for the **HR** folder:

1. Right-click on **HR** → choose the **Security** tab → click on **Advanced**.
2. Click on **Add**, then **Select a Principal**, and include **HR**.
3. Activate **Modify** for basic permissions.
4. Click **OK**, then **Apply**.

This will grant **HR** group members access to the HR shared folder with the appropriate permissions.

21. <p align="center">
   <img src="https://imgur.com/zBFEKe2" height="80%" width="80%"/>
   <br />
   <br />
</p>

To guarantee that the **HR** group has "Read/Write" access in the sharing settings, please follow these instructions:

1. Right-click on the **HR** folder.
2. Choose **Properties** and navigate to the **Sharing** tab.
3. Click on **Share…**.
4. In the **Network Access** window, verify that **HR** is included.
5. Right-click on **HR** and select **Read/Write**.
6. Click **Share** to finalize the settings.

This process ensures that members of the **HR** group possess the appropriate permissions to read and write to the HR shared folder.

22. <p align="center">
   <img src="https://imgur.com/7Jumo55" height="80%" width="80%"/>
   <br />
   <br />
</p>

To verify Bob's access to the **HR** folder on Desktop2:

1. Sign in as **Bob** on the **Desktop2** account.
2. Launch **File Explorer**.
3. In the **File Explorer** search bar, enter the following network path: `\Server2022\HR`
4. Hit **Enter** to access the **HR** shared folder.

As Bob is a member of the **HR** group, he should have the necessary access to this folder. You ought to be able to view the contents of the **HR** folder. If the permissions were configured correctly, Bob should possess **Read/Write** access to this folder.

23. <p align="center">
   <img src="https://imgur.com/QMUXuhE" height="80%" width="80%"/>
   <br />
   <br />
</p>

- **Copy the network path** for the HR folder: \Server2022\HR
- Right-click on **This PC** in **File Explorer** and choose **Map this Network drive**.
- In the **Map Network Drive** window:
- **Drive letter**: Select a drive letter, for example, **Z:**
- **Folder**: Insert the network path \Server2022\HR into the folder field.
- Tick the box for **Reconnect at sign-in** if you wish for the drive to be automatically remapped upon login.
- Click **Finish**

24. <p align="center">
   <img src="https://imgur.com/ylU8W9q" height="80%" width="80%"/>
   <br />
   <br />
</p>



25. <p align="center">
   <img src="https://imgur.com/5hRA2Xl" height="80%" width="80%"/>
   <br />
   <br />
</p>

An alternative way to map a personal drive is to log into your Windows Server 2022 account and copy the network path found in the "Personal Properties" section of the shared folders.

26. <p align="center">
   <img src="https://imgur.com/9Karr6e" height="80%" width="80%"/>
   <br />
   <br />
</p>

Next, launch Active Directory Users and Computers, look for "Bob," right-click on his name, and choose "Properties." After that, navigate to the "Profile" tab and under "Home Folder," select "Connect" and assign the drive letter P:. Insert the network path for the drive: \SERVER2022\Personal%username% (ensure to include "%username%"). Lastly, click "Apply." This action will establish a personal folder in Bob's directory.

27. <p align="center">
   <img src="https://imgur.com/cezcR8g" height="80%" width="80%"/>
   <br />
   <br />
</p>

After logging into Desktop2 as Bob, we will observe that both the Personal and HR drives are mapped.

28. <p align="center">
   <img src="https://imgur.com/E1L8rFI" height="80%" width="80%"/>
   <br />
   <br />
</p>

Congratulations we have successfully configured on how to implement Security Groups, Map Drives, Personal Drives and Map Letter.
