<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Active Directory (Part 4 Network File Sharing)</h1>
I will be demonstrating how you can assign permissions to various file types.

<h2>Walkthrough</h2>

- Log into Server(the windows server VM) and create several folders on your VMs c: drive (In this case I created 4 and named them; read access, write access, no access, and accounting). 

<img width="865" alt="Screenshot 2025-02-07 at 15 15 58" src="https://github.com/user-attachments/assets/2c990089-5910-43a7-b53d-a3361c63c1f8" />

- For the read access folder, I assigned it to Domain Users and gave it read-only permission. For the write access folder, I also assigned it to Domain Users and gave it a read-write permission.

<img width="953" alt="Screenshot 2025-02-07 at 15 16 55" src="https://github.com/user-attachments/assets/2d43a282-d05d-44ce-803a-3687f37a243d" />

<img width="945" alt="Screenshot 2025-02-07 at 15 18 08" src="https://github.com/user-attachments/assets/52daf65a-cd12-4b0d-b178-c4fba96a40d4" />

- For the no-access folder, I assigned it to Domain Admins and gave it read-write permission (Haven't done anything with the accounting folder yet).

<img width="894" alt="Screenshot 2025-02-07 at 15 18 52" src="https://github.com/user-attachments/assets/227cdb6a-1752-480d-9922-2f90499c646d" />

- Log into User(the windows 10 VM) with one of the users created in active directory users & computers to view the folders.

<img width="637" alt="Screenshot 2025-02-07 at 15 22 01" src="https://github.com/user-attachments/assets/31ce1072-9456-43a7-be4e-001b878999ad" />

<img width="1714" alt="Screenshot 2025-02-07 at 15 22 19" src="https://github.com/user-attachments/assets/461506c9-cb5b-4636-b2a8-0371f08364ad" />

- The read-access folder can be viewed but can not have any changes made to it since the permission was set to read-only, however, changes can be made to the write-access since it was given a read-write permission.

<img width="1128" alt="Screenshot 2025-02-07 at 15 22 54" src="https://github.com/user-attachments/assets/58ad3cbb-c836-45c2-af5e-a836965420f2" />

<img width="1138" alt="Screenshot 2025-02-07 at 15 23 03" src="https://github.com/user-attachments/assets/97d3b584-0c52-4dcb-876e-8cb5384be6ec" />

<img width="986" alt="Screenshot 2025-02-07 at 15 23 26" src="https://github.com/user-attachments/assets/1a388df8-aea6-4e66-b386-0fa151122047" />

<img width="887" alt="Screenshot 2025-02-07 at 15 23 50" src="https://github.com/user-attachments/assets/7ff83c64-9571-46cf-bbe5-82e25a2d3b82" />

- The no-access folder can not be viewed nor edited despite having the read-write permission and that's because it was assigned to Domain Admins and not Domain Users, and the users created in ADUC only fall under Domain Users.

<img width="1012" alt="Screenshot 2025-02-07 at 15 24 19" src="https://github.com/user-attachments/assets/6b1fde4c-b1dd-425d-a30b-1037a6d1f09c" />

- Now it's time to handle the accounting folder.

- Log back into Server and then go to active directory users & computers and create a new organisational unit(I called it GROUPS).

<img width="752" alt="Screenshot 2025-02-07 at 15 25 15" src="https://github.com/user-attachments/assets/8a1e9603-0487-4379-81a0-af65ef3ecafe" />

<img width="755" alt="Screenshot 2025-02-07 at 15 26 45" src="https://github.com/user-attachments/assets/cc32f0cf-7859-4c54-9d93-0394c97c925f" />

- Within the new organisational unit create a new security group(I called it ACCOUNTANTS).

<img width="755" alt="Screenshot 2025-02-07 at 15 28 12" src="https://github.com/user-attachments/assets/891cf38c-d308-470a-8a6b-5c64b3f73361" />

- Go to the accounting folder created earlier and assign it to the accountants security group that was just created and also give it the read-write permission. 

<img width="886" alt="Screenshot 2025-02-07 at 15 29 57" src="https://github.com/user-attachments/assets/127f5e65-d984-4300-bd59-d6cc6e51ca71" />

- If you log into User the accounting folder will now show up however you won't be able to view it nor make changes to it since the user account we logged in with is not part of the accountant security group.

<img width="1003" alt="Screenshot 2025-02-07 at 15 30 47" src="https://github.com/user-attachments/assets/670cd8b2-11a2-4b45-802e-7eba9c2ec970" />

- We can go back to active directory users and computers choose a user account and make it a part of the accountants' security group.

<img width="752" alt="Screenshot 2025-02-07 at 15 34 19" src="https://github.com/user-attachments/assets/d4b234a2-3b16-46df-ac44-25d0ff2a7cbd" />

<img width="400" alt="Screenshot 2025-02-07 at 15 34 58" src="https://github.com/user-attachments/assets/67eb387e-67e2-4bd0-a51e-44dc3c062663" />

<img width="755" alt="Screenshot 2025-02-07 at 15 35 21" src="https://github.com/user-attachments/assets/b92cc577-4bde-4bd4-a1a9-452e92040dbd" />
 
- If we log back into User with the user account that was just assigned to the accountant security group then we can now view and make changes to the accounting folder.

<img width="1157" alt="Screenshot 2025-02-07 at 15 36 32" src="https://github.com/user-attachments/assets/62641b98-4dd7-4735-adb2-994b3ca0e647" />

<img width="764" alt="Screenshot 2025-02-07 at 15 37 42" src="https://github.com/user-attachments/assets/9f87c385-0e54-4a3d-a8c0-37a8d796ace0" />

- And that's it.
