# Cyber Quests Fall 2024 Challange


<h3>Part 1: Devon Lee</h3>

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

![image](https://github.com/user-attachments/assets/8b286c12-be92-461a-adcd-0f444d5381e5)

Q10: What is the most logical reason that Devon would choose to hide in this location?

The most likely reason Devon Lee would flee to Cambodia is the fear of being caught and charged for the crimes they've committed. 
#
<h3>Part 2: Donathan Koebee</h3>

Donathan Koebbe is a 43-year-old engineer who helps build nuclear-powered aircraft carriers for the United States Navy.  Donathan was recently suspected of creating a plot to transmit information relating to the design of nuclear ships to a foreign nation.  He sold information known as “Restricted Data” concerning the design of nuclear-powered warships to a person he believed was a representative of a foreign power. In actuality, that person was an undercover FBI agent. Donathan has been charged in a criminal complaint alleging violations of the Atomic Energy Act. You are being asked to decrypt the blueprint file that was provided by Donathan to the agent and help answer questions regarding the process by which Donathan was able to acquire the aircraft blueprints.

The provided files are the evidence_dk.pcap, the email messages between Donathan (Alice Hill) and the FBI agent (Bob Burns), and the encrypted blueprint file
#
Q11: What blueprint did Bob Burns request from Alice Hill?

Based on the email exchange the FBI agent requested the blueprints for the "CV-60 Large Aircraft Carrier"
#
Q12: Which tool did Alice use to encrypt the blueprint file?

GnuPG allows you to encrypt and sign, data and communications
#
Q13: How many pages does the encrypted blueprint file contain?
The passwrod for the encyrpted file is LIBERTEEGALITEFRATERNITE, these were the words included in the image file named key.png
After using GPG to decrypt the file with the password, I saw that the file was 19 pages long
#
Q14: What network utility was downloaded through HTTP and used to exfil the PDF blueprint?

ncat Was used to exfiltrate the data.

![image](https://github.com/user-attachments/assets/91a09c95-e58b-48ca-b502-4e7853c9bf56)
#
Q15: Which server tool was used to host the network utility used to exfil the PDF blueprint?

Python SimpleHTTP server is used to host ncat

![image](https://github.com/user-attachments/assets/072d2150-6aee-4484-acdc-0a7a07de7703)
#
Q16: What tool was used to download the exfil tool?

cURL: cURL can be used to download files, in this case it was used to download ncat from another host.
#
Q17: Recover the PDF blueprint that Donathan exfiltrated.  When were the blueprints prepared?
Based on when the  cv-60 large aircraft carrier was built I chose a date before then, 5 January 1947. The most recent date in the files was June 25th, 2007
#
Q18: A file called "calc_target_offsets" was recovered from the computer hosting the blueprints.  What CVE was likely used by Donathan to gain access to the blueprints? and Q19: What is the name given to the security vulnerability Donathan used?

Based on the file that was recovered, the security vulnerability Donathan Koebbe exploited was the CoronaBlue exploit (CVE-2020-0796), this is an SMBv3 remote code execution vulnerability.

![image](https://github.com/user-attachments/assets/8097649a-c718-416c-a9e6-eb37c3898531)
#
Q20: What version of Windows was the computer hosting the blueprints likely running?

Windows 10 1903/1909 are two of the 4 known affected versions, the other two are Windows server 2016 1903/1909

![image](https://github.com/user-attachments/assets/6767d484-aa91-4ef2-b103-b1fe7e1c1695)
#
<h3>Part 3</h3>

As a new SOC analyst, you are being asked to analyze the log.txt file from an Apache server and answer the following questions:
#
Q21: How many POST requests are there?

5499
#
Q22: How many GET requests are there?

1040
#
Q23: How many unique client-requested resources are there?


#
Q24: Which client-requested resource is the most common/had the most requests?

#
Q25: How many different HTTP response status codes are represented in this log?

I saw 7 different response codes, 200, 301-3, 400, 404, and 500.
#
Q26: How many times does the most commonly appearing HTTP response code in the log file appear?

The 200 HTTP response code had appeared 2036 times

![image](https://github.com/user-attachments/assets/170a73f1-f45f-449f-80ed-551dfd009615)
#
Q27: What is the entire URI of the most common referer (without quotes)?

This URL: http://192.168.4.161/DVWA is the most common
#
<h3>Part 4</h3>

You are a new security analyst at a bank and are being asked to identify the 7 Social Security Numbers from the ssn.txt file that do not conform to the below requirements from the Social Security Administration. Based on the rule stated find the SSN that doesn't belong.
#
Q28: SSA will only issue SSNs which are 9 digits in the format XXX-XX-XXXX, Which SSN fails this rule?
117-3-8427

![image](https://github.com/user-attachments/assets/768b82ed-a2f7-4ff3-bcfb-7af30c1c6a8d)

Q29: SSA will not issue SSNs which are duplicates, Which SSN fails this rule?


Q30: SSA will not issue SSNs beginning with the number "9", Which SSN fails this rule?
995-99-5192

![image](https://github.com/user-attachments/assets/de391565-ba91-401b-b41f-9e4f0f92ac24)


Q31: SSA will not issue SSNs beginning with the number "666" in positions 1 - 3, Which SSN fails this rule?
666-37-3885

![image](https://github.com/user-attachments/assets/ec557b39-e20d-46b8-b361-6476eab6cbc9)


Q32: Which SSA will not issue SSNs beginning with the number "000" in positions 1 - 3, SSN fails this rule?
000-97-7549

![image](https://github.com/user-attachments/assets/8f7dc2f1-aaaa-4240-bf41-3d3d8d186813)


Q33: SSA will not issue SSNs with the number "00" in positions 4 - 5, Which SSN fails this rule?
378-00-7651

![image](https://github.com/user-attachments/assets/a33914d5-e340-458e-a98f-d97c36440c7c)

Q34: SSA will not issue SSNs with the number "0000" in positions 6 - 9, Which SSN fails this rule?
571-63-0000

![image](https://github.com/user-attachments/assets/910994b1-62ed-4c38-aadb-97adc973d85e)


