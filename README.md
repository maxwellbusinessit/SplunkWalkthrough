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



4. 
   
