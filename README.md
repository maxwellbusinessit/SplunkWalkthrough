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


   You will be prompted to log in using the username and password that you had previously set in the command line interface for the administartor account.
   Once you enter the username and password correctly you will be allowed access to the dashboard.
   (Side note: If you'd like to make splunk start on boot you can use this command in the shell: sudo /opt/splunk/bin/splunk enable boot-start)


   
   <img width="2240" height="1400" alt="image" src="https://github.com/user-attachments/assets/9f2bcd0d-2e9b-47e8-9aa2-b5fdbf1c871d" />

   

   

   
