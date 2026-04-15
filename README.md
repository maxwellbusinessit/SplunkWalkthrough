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


   When prompted to set the source type, you can just set it as default and hit apply settings:
   
   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/e04f5979-d8e8-4a6a-9c9a-2ddfa622d7f1" />


   Then you can select these settings in the prompt:
   
   <img width="546" height="359" alt="image" src="https://github.com/user-attachments/assets/89692079-6d5f-49ff-8edd-4613d6f50d21" />


   Next, set the index to main and leave the host value as the default, for me it is Mint.
   
   <img width="1110" height="808" alt="image" src="https://github.com/user-attachments/assets/eea03b7c-e9e4-4edf-8de5-d96665e2342e" />
   
   The rest of the prompts for this section are pretty self explanatory, so just finish them up and you'll be done with this step.


 6. Use threat detection queries by navigating to "Search & Reporting" on the main dashboard on the left hand side:

  <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/1cd82f4b-d95e-41bd-a954-c55412e574e3" />


  Once you're there you can try entering some queries and viewing the results, in the screenshot example we're viewing all the failed login attempts in the logs.txt file, there are only a few as this is just an example. If nothing is showing up when you search, setting the time range to "All time" because these logs are dated. Since this lab uses basic log ingestion without field extraction, we analyze activity using mostly raw log patterns. This would differ from a real enterprise environment.

  <img width="2234" height="287" alt="image" src="https://github.com/user-attachments/assets/8500ad7e-4d8c-4be5-823f-b8ba6ddd8435" />

  With the query used, after hitting the search button the results appear as follows:
  
  <img width="2235" height="620" alt="image" src="https://github.com/user-attachments/assets/e2f34f05-d6db-4183-aeaa-d6d157c4106e" />


   Here are a few queries you can try: 
   
   index=main "LOGIN_FAILED" | stats count by _raw    (Shows all failed login attempts, can be useful in identifying a brute force attack when there are a ton of these in a short time frame)

   index=main "LOGIN_SUCCESS"    (Shows all successful logins)

   index=main ("LOGIN_SUCCESS" OR "LOGIN_FAILED") | stats count by _raw    (Shows both failed and successful login attempts)

   index=main "ACCESS_CONFIDENTIAL_FILE"    (Shows an event where a confidential file was accessed in our example)

   Feel free to try and construct some of your own!


 7. Create a monitoring dashboard:

   Navigate to Search & Reporting from the main dashboard > then select dashboards at the top:
   

   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/56bacee1-b589-4b9a-b88a-a0d18c2b76f5" />


   Then select "Create New Dashboard" in the top right:


  <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/b56a51c8-08ec-40bf-839a-edc6f5257261" />


   Feel free to create it however you want, but for this example I'll be using the following options and classic dashboards:


   <img width="570" height="530" alt="image" src="https://github.com/user-attachments/assets/66dd7e48-5592-4d16-a5eb-481ce8770607" />


   Once you're here you'll want to add a panel with the "+Add Panel" option on the top row beside "Edit Dashboard":
   In the "Add Panel" options, you can do many different things. This part of splunk is very flexible and allows monitoring in
   the form of graphs, events, charts, tables etc. In this example we keep it simple because our default log file is very simple:

  Select New > Events > and input the query (index=main "LOGIN_FAILED") in the "Search String" box:


  <img width="1113" height="885" alt="image" src="https://github.com/user-attachments/assets/1503c82e-80fd-4e2c-b36c-66e38c5ec020" />


  Once you add this event monitor to the dashboard, it'll show up like so:


  <img width="1116" height="429" alt="image" src="https://github.com/user-attachments/assets/a33b380b-b7d4-4705-bc33-1d52aeefb486" />



  This allows you to see all the failed login attempts from our logs.txt file. Feel free to create some other ones, you will soon find that you can make all sorts of them depending on your needs.


8. Create alerts:

     You can create alerts which will be triggered by a certain event occuring:

     Navigate to the "Search & Reporting" section once again and run a search query:


     <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/ae51022a-2755-43d7-8155-38f5357e580d" />


     In this example we use access of a confidential file, because that may be something a security operations team would want to keep track of and verify. Once you perform the search query select "Save As" and then "Alert":


   
<img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/ad2c82b0-e9e7-4f6e-a8b6-68c5f57b0429" />


  Again we are given a plethora of options to choose from, but in this example I've configured it as follows: 


  <img width="779" height="919" alt="image" src="https://github.com/user-attachments/assets/cd381234-9a98-4aa8-b1e5-828e9b906fc9" />


  This sets the alert to run on a schedule every five minutes as a cron job in order to simulate real time evaluation of logs. In a real environemnt we would use the real-time analysis feature, but that is beyond the scope of this basic project.

  After saving the alert, you can view it along with all the times that it has been triggered:


  <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/de432b4c-37b4-48ab-922b-a8c78a93995c" />


  Upon hitting the "view results" button, you can see more info about the alert and what happened:


  <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/63259a5b-993e-4902-b5ac-285e9a48a020" />









That's all for this basic walkthrough! I may expand upon this in the future by adding some EDR features using agents on virtual machines to simulate real time analysis of endpoints. Feel free to try this project out for yourself in order to get your feet wet with using splunk. If you've read this far into my project thank you very much and I appreciate your time! As always get curious, explore, learn, and most of all have fun with it!





     



  





   


     
   







   


   

   

   
