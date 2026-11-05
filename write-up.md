NAME : FATIN BATRISYA BINTI ABDUL RAUF

STUDENT ID : 52215125437

COURSE : IKB21403 VULNERABILITY ANALYSIS

LAB : L01-B01

PREPARED FOR : Ms. Nor Adani Kamal Mohamad Nasir

Performing System Hacking of BlueMoon 2021

PENTEST MENTHODOLOGY
1. Reconnaissance - netdiscover
2. Scanning - nmap
3. Gaining Access - gobuster, ftp, metasploit, ssh
4. Privilege Escalation - sudo -l, feedback.sh
5. Maintain Access - docker
6. Clear Tracks - history -c

STEPS
1. Open Kali and BlueMoon2021. I use Oracle VirtualBox

2. Let BlueMoon2021 run in background. Log into Kali

<img width="1917" height="916" alt="image" src="https://github.com/user-attachments/assets/7c21c069-6cb9-499a-b907-4f8249cd4df8" />

3. Open Root Terminal Emulator and enter password

<img width="490" height="231" alt="image" src="https://github.com/user-attachments/assets/900b6325-48de-470c-8bb4-9bacbfbf6a43" />

4. Use ifconfig to find our (attacker's) ip address. In this case, mine is 192.168.56.105

<img width="637" height="176" alt="image" src="https://github.com/user-attachments/assets/92ef4828-c646-4230-a052-914c29dc3e34" />

5. Use netdiscover to find the target on the network

<img width="655" height="162" alt="image" src="https://github.com/user-attachments/assets/dcfb23b4-9b8e-445c-8b73-f3d01b28f278" />

6. Target is likely 192.168.56.100 or 192.168.56.104 , so let's find out which one is it using nmap.

<img width="592" height="402" alt="image" src="https://github.com/user-attachments/assets/9b16a0ce-2103-4cf5-8df7-09e15adaf29b" />

7. Based on finding above, our target ip address is likely 192.168.56.104 since there are lots open ports. Three ports were found, 21 (FTP), 22(SSH) and 80(HTTP)

8. I visited the website using http://192.168.56.104 in my browser.

<img width="1917" height="827" alt="image" src="https://github.com/user-attachments/assets/c5693a48-9988-4a8b-aaff-498925fc013d" />

9. The website looks TOO empty, so we are going to find hidden directories. Use gobuster dir -u http://192.168.56.104 \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

<img width="730" height="377" alt="image" src="https://github.com/user-attachments/assets/117be813-0283-4b38-808d-4a548c6848f3" />

10. I found a directory /hidden_text . Let's check it out.

<img width="1917" height="421" alt="image" src="https://github.com/user-attachments/assets/8fec18f0-df32-4d89-b600-4bde842bc3c2" />

11. The "Thank You" text is in blue color which means clickable. Click on it.

12. A QR code is displayed.

<img width="1917" height="592" alt="image" src="https://github.com/user-attachments/assets/fbb7a39f-0df2-496e-8b0e-fdfb32a21dd3" />

13. Decode the QR code using any online tools. I used https://www.qr-codes.com/decoder

<img width="1437" height="615" alt="va2" src="https://github.com/user-attachments/assets/6a7e9af9-ef9b-4cea-afae-23bc081bbc48" />

14. We received the USER = userftp and PASSWORD = ftpp@ssword . Next, we log into FTP using the credentials. Use ftp 192.168.56.104

15. Login is successful.

<img width="347" height="191" alt="va3" src="https://github.com/user-attachments/assets/67767665-9818-4908-b8e2-9d9a61d82854" />

17. List the files using ls

<img width="587" height="97" alt="va4" src="https://github.com/user-attachments/assets/48c18ae9-6791-4544-8dbb-7fceaaf544fc" />

18. We download both files using get information.txt and get p_lists.txt

<img width="1907" height="225" alt="va5" src="https://github.com/user-attachments/assets/58d3959c-60dd-4529-afbf-6e2db4e829fc" />

19. Exit ftp using bye

<img width="121" height="41" alt="va6" src="https://github.com/user-attachments/assets/c601583d-fe02-4c3f-beeb-3260fa79e394" />

20. Read the downloaded files in root using cat information.txt and p_lists.txt

<img width="1006" height="691" alt="va7" src="https://github.com/user-attachments/assets/6efdd4c5-75b5-4ae6-8ae4-09b15cd4b9a4" />

21. Now that we know the username is robin and file p_lists.txt contains list of passwords, I am going to use port 22 and attack SSH.

22. I used Metasploit's SSH login module using msfconsole and search ssh_login

<img width="742" height="737" alt="va8" src="https://github.com/user-attachments/assets/15e4bc8e-eb0d-4167-8e27-992f14274b6a" />

<img width="865" height="187" alt="image" src="https://github.com/user-attachments/assets/0974ca8b-3ae5-45d6-9e36-b52f06b519f7" />

22. Enter use 0 to use the module and enter show options to look at the options

<img width="1900" height="536" alt="image" src="https://github.com/user-attachments/assets/1eb92aea-6854-4398-9095-8f2b55cfc8af" />

23. Brute-force by configuring RHOSTS, USERNAME and PASS_FILE as below

<img width="1902" height="227" alt="image" src="https://github.com/user-attachments/assets/fe880ebc-40b8-43b7-99c5-b83681996737" />

24. Now we have retrieved the password which is k4rv3ndh4nh4ck3r . Let's exit using exit -y 

<img width="390" height="17" alt="image" src="https://github.com/user-attachments/assets/ebe51acd-b400-4713-8cf6-80fc0b6c8f00" />

25. Login as robin using ssh robin@192.168.56.104 and enter the password

<img width="685" height="345" alt="image" src="https://github.com/user-attachments/assets/a9ee7002-e378-483e-a775-9bdbcf152b48" />

26. We have successfully login as robin! Now let's capture the flags. List the files using ls and read using cat

<img width="360" height="125" alt="image" src="https://github.com/user-attachments/assets/fb124bce-4ea4-405f-a469-a816ee9b95e9" />

27. Use sudo -l to check what commands can user robin run as sudo

<img width="880" height="96" alt="image" src="https://github.com/user-attachments/assets/f33ab7ef-7187-492a-97d5-07d461b6d6a0" />

28. As stated above, user robin can run feedback.sh in project directory as user jerry (no password needed). So let's read the feedback.sh

<img width="555" height="207" alt="image" src="https://github.com/user-attachments/assets/cf7c3db5-264f-47f0-a562-716439203fad" />

29. Use sudo -u jerry ./feedback.sh to run as user jerry. Explore through the directory and find the second flag. This is horizontal privilege escalation (user → another user).

<img width="1041" height="456" alt="image" src="https://github.com/user-attachments/assets/d0b02885-2acb-493f-9461-622e2d4f3cc4" />

30. From here, we are going from jerry to root. Use id to check identity. We discovered that jerry is a member of "docker" group.

31. Use docker run -v /:/mnt --rm -it alpine chroot /mnt sh to bridge the container's environment with host's file system.

<img width="525" height="492" alt="image" src="https://github.com/user-attachments/assets/ac69ae15-e60c-43ff-9862-cac7bb5c1999" />

32. Clear history logs using history -c

<img width="245" height="51" alt="image" src="https://github.com/user-attachments/assets/f5e65bf1-a2ea-4346-98db-435cfb395223" />
























