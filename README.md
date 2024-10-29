# Cyber Quests Fall 2024 Challange


Part 1: Devon_Lee
What we know: Devon Lee is a 57-year-old IT technician at Palm Tree Investments, a fin-tech firm that provides investment services in South Florida.  Over a two-year period starting from February 2020, Devon decided to steal customer credit card information from the firm's internal SharePoint server to sell on the dark web.  He also harvested employee personal information – including social security numbers, birth dates, and addresses to create fake IDs, which were in turn used with fabricated pay stubs, bank statements, and tax documents to apply for loans and pay for his extravagant lifestyle.
 
Using the provided customerPII.csv file, evidence.pcap file, TLSkeys.log file, and social media post image to answer the questions
#
Q1: How many Palm Tree Investment customers were impacted?

The customerPII.csv file contains payment card data like Card Number, Expiration, CVV/CVC, etc. Excluding the first line which shows the format that the information is in, a total of 3456 customers were impacted.

![image](https://github.com/user-attachments/assets/e21fb865-fede-4cfc-b644-2f19cb456d88)
#
Q2: How many credit card issuers were impacted? and Q3: Which card issuer was the most impacted?

4 credit card issuers were impacted, VISA was the most impacted with 2104 different cards

![image](https://github.com/user-attachments/assets/150b7f8d-cb02-4238-932c-d38ca6af0bd9)
#
For questions 4-7 I used Wireshark to inspect a packet capture

Q4: Which email service was used to transfer the complete list of employees?

The email server used was Gmail, here we see a POST to mail.google.com, and a few lines below we see gmail.pinto-server

![image](https://github.com/user-attachments/assets/7b1ee29f-9e31-487a-acb0-40291134dada)
![image](https://github.com/user-attachments/assets/b7ec9396-a615-4d86-8241-379ae9d9a85e)
#
Q5: What is the name of the file that was used to POST /_/upload and exfil employee information?

looking through the Wireshark capture and following the HTTP stream (http2.streamid eq 111), the contents of the email can be seen in cleartext. This is only possible, however, because of the TLSkeys.log file. Without it the entire packet capture would be encrypted.

![image](https://github.com/user-attachments/assets/72ff239a-bcb8-4d8f-9d16-dbf767b341ab)
![image](https://github.com/user-attachments/assets/83761c78-f091-45e2-86b7-03e967e3d16b)
#
Q6: How many employees were listed in the aforementioned file?

The file contained the information of 20 employees
#
Q7: What email address was the file sent to?

Using the given hint of applying a filter to the packet capture, it leads to one packet. Looking into the HTML form shows the email was sent to Devon Lee. 

![image](https://github.com/user-attachments/assets/deac6a88-c2a1-47e2-8638-d32e123339be)
#
Q8: Which country was the "destination" image taken in? and Q9: Who is the author of the destination image?

The social media post image is that of a waterfall, a reverse image search reveals it's Anna Ruby Falls in Georgia. However, looking into the metadata of the image, reveals that its actually a screenshot of a picture. The screenshot was taken in Cambodia, by Sharon Lee. 

Q10: What is the most logical reason that Devon would choose to hide in this location?

The most likely reason Devon Lee would flee to Cambodia is the fear of being caught and charged for the crimes they committed. 
