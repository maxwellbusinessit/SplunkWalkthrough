This project demonstrates a hands-on Security Operations Center (SOC) lab using Splunk. It simulates real-world security monitoring by ingesting logs, detecting threats, and generating incident reports.
Hope it helps somebody out there to learn something new!

I am personally using linux mint for this project, so it may be different depending on which operating system or linux distribution you are using. Follow along with mint for the best results.


1. Download Splunk Enterprise from their website using the free trial here: https://www.splunk.com/en_us/download/splunk-enterprise.html
                                                         OR
   Use the wget command to install it directly, results may vary depending on your operating system:

   sudo wget -O splunk-10.2.2-80b90d638de6-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.2.2/linux/    splunk-10.2.2-80b90d638de6-linux-amd64.deb"


   <img width="1114" height="371" alt="image" src="https://github.com/user-attachments/assets/c4790121-7b2b-4f2e-9ad7-104f5b58a0d4" />
   

2. Install splunk by changing your working directory to Downloads with: cd ~/Downloads
   Then running: sudo dpkg -i splunk.deb (The file name won't actually be as short as splunk.deb, but it could vary depending on the version.)
    If you recieve any errors related to dependencies you can try running: sudo apt-get install -f

   <img width="1108" height="327" alt="image" src="https://github.com/user-attachments/assets/39a84d10-ddbb-4fe5-8fac-d7a9695f5621" />
  

3. Start splunk by first using chown to give your user account the permission it needs for this process:
    sudo chown -R $USER:$USER /opt/splunk
   Then run:
    /opt/splunk/bin/splunk start --accept-license


   <img width="473" height="48" alt="image" src="https://github.com/user-attachments/assets/1f5684a6-9a62-4e96-9e43-9c2afa9fdc73" />

   
   <img width="1111" height="1357" alt="image" src="https://github.com/user-attachments/assets/26324d1a-450d-4b4f-917a-c0e909f4df93" />

   

   You will be prompted to set a user name and password for the administrator account, because I already have an administrator account created I was not prompted to do so in these screenshots. You can set the login to whatever you please.


4. Access splunk via the web user interface with: http://localhost:8000
   It will differ depending on your localhost for example mine is depicted in the above screenshot as http://Mint:8000
   

   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/63043001-0292-459b-8708-06dceeb55f99" />


   You will be prompted to log in using the username and password that you had previously set in the command line interface for the administrator account.
   Once you enter the username and password correctly you will be allowed access to the dashboard.
   (Side note: If you'd like to make splunk start on boot you can use this command in the shell: sudo /opt/splunk/bin/splunk enable boot-start)


   
   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/9f2bcd0d-2e9b-47e8-9aa2-b5fdbf1c871d" />


   From here on you can do whatever you'd like, but if you want to try ingesting some sample logs and experimenting with them follow the next few steps:


5. Create a sample log (logs.txt) and populate it with the following data (Or you can use logs from the internet for extra brownie points):

   2026-04-15 10:01:23 LOGIN_SUCCESS user1 192.168.1.10
   2026-04-15 10:02:10 LOGIN_FAILED user1 192.168.1.10
   2026-04-15 10:02:15 LOGIN_FAILED user1 192.168.1.10
   2026-04-15 10:02:20 LOGIN_FAILED user1 192.168.1.10
   2026-04-15 10:05:00 ACCESS_CONFIDENTIAL_FILE user2


    Navigate to Settings > Add Data in the top right corner


   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/6c9bdcfe-62b3-4108-927a-bcec61d15de7" />


    Then select upload from my computer and select your logs.txt file:


   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/17938589-c14a-4789-85f4-bd05c99b5376" />


   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/f4a1406f-683f-4a0d-a3af-905f0ab81d5b" />


   When prompted to set the source type, you can just set it as default and hit apply settings:
   
   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/e04f5979-d8e8-4a6a-9c9a-2ddfa622d7f1" />


   Then you can select these settings in the prompt:
   
   <img width="546" height="359" alt="image" src="https://github.com/user-attachments/assets/89692079-6d5f-49ff-8edd-4613d6f50d21" />


   Next, set the index to main and leave the host value as the default, for me it is Mint.
   
   <img width="1110" height="808" alt="image" src="https://github.com/user-attachments/assets/eea03b7c-e9e4-4edf-8de5-d96665e2342e" />
   
   The rest of the prompts for this section are pretty self explanatory, so just finish them up and you'll be done with this step.





   


   

   

   
