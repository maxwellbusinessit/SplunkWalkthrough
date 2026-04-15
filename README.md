This project demonstrates a hands-on Security Operations Center (SOC) lab using Splunk. It simulates real-world security monitoring by ingesting logs, detecting threats, and generating incident reports.
Hope it helps somebody out there to learn something new!

I am personally using linux mint for this project, so it may be different depending on which operating system or linux distribution you are using. Follow along with mint for best results.


1. Install Splunk Enterprise from their website using the free trial here: https://www.splunk.com/en_us/download/splunk-enterprise.html
                                                         OR
   Use the wget command to install it directly, results may vary depending on your operating system:

   sudo wget -O splunk-10.2.2-80b90d638de6-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.2.2/linux/splunk-10.2.2-80b90d638de6-linux-amd64.deb"

   If you recieve any errors related to dependencies you can try running: sudo apt-get install -f

   <img width="1114" height="371" alt="image" src="https://github.com/user-attachments/assets/c4790121-7b2b-4f2e-9ad7-104f5b58a0d4" />

   

3. 
