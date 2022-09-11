<h1>Implemetation of Network Security and Testing</h1>


<h2>Description</h2>
The process by which network is shielded and against an unauthorized access and detection of attacks on the network is known as network security. There are five main concepts defined with respect to Network security which are listed as follows: <br/><br/>
- <b>Confidentiality:</b> this is the concept of preventing or minimizing the access of unauthorized users to the network.<br/>
- <b>Integrity:</b> this is to ensure that there is no unauthorized data change is allowed and information remain undistorted.<br/>
- <b>Availability:</b> this concept ensures that data is available for accessing continuously as at when required.<br/>
- <b>Authentication:</b> it ensures the source of the information is accurate and the identity is not forged.<br/>
- <b>Nonrepudiation:</b> this concept ensures the sender, and the recipient of the message cannot deny their role.<br/> <br/>

I will review some modern security threats and attacks and also demonstrate how some attacks are actualized and provide recommended solutions for preventing and mitigating the attacks.

<br />


<h2>Design Prototypes</h2>

<h4>Vulnerable Network Design</h4> 

Three virtual machines were used to implement the network design prototype. 

The first virtual machine is a Kali Linux machine with the IP address of 192.168.81.128 represented the attacking VM, since it is already preconfigured with some penetrating tools.

Ubuntu Mate 18.04 is the operating system installed on the second VM. Also installed, was Snort tool for intrusion detection and prevention. This VM also serve as the gateway for the network with the IP address of 192.168.81.135.

Metasploitable 2 Linux is the third VM serving as the vulnerable machine on the network, where web application server and open ports exist. The IP address is 192.168.81.131.

For the project, VMware tool was use for the virtualization on which the virtual machines were created. Appropriate resources were allocated for each VMs according to the expected task. 

<p align="center">
Vulnerable Network: <br/>
<img src="https://i.imgur.com/pRc5rrR.png" height="80%" width="80%" alt="Vulnerable Network"/> 
<br />
</p>

<h4>Secured Network Architecture </h4>

The figure below shows the security implementation proposed for the network. Intrusion detection and prevention system (IDS/IPS), the unused ports on the vulnerable server were closed and the security level of the web server raised to high.

<p align="center">
Secured Network: <br/>
<img src="https://i.imgur.com/XFDywMc.png" height="80%" width="80%" alt="Secured Network Architecture "/> 
<br />
</p>

<h2>Information Gathering </h2>

To obtain details regarding the network topology, operating systems on the network nodes, the ports and their status, the IP addresses of the machines information gathering technique is deployed.
The tools used in this work are Network Mapper (Nmap) and Zenmap (the GUI of Nmap). The Zenmap was used to get understanding of the topology and obtain IP addresses of the host in the network. While Nmap was used to further investigate the vulnerable host on the network and open ports, services information was obtained.


<h4>Identifying Vulnerabilities in the target network</h4>

Using Zenmap tool for “intense scan” the network at initial stage as shown below. The topology reveals all the IP addresses active on the network and vulnerable node was detected and coloured red with the IP address 192.168.81.131 (this is the Metasploitable 2 VM).

<p align="center">
Network Topology: <br/>
<img src="https://i.imgur.com/ywBh5Iy.png" height="80%" width="80%" alt="Network Topology"/> 
<br />
</p>

Further checks revealed other valuable information of each identified hosts, like the OS on each host, the MAC, the number of opened and closed ports.

<p align="center">
Zenmap scan output: <br/>
<img src="https://i.imgur.com/vnhG9di.png" height="80%" width="80%" alt="Zenmap scan output"/> 
<br />
</p> <br/>


<h4>Identifying Vulnerabilities in the target Host</h4>

For a more specific scan, Nmap was used to specifically scan the vulnerable machine to obtain detailed exploitable services by using the command nmap -Sv -p- 192.168.81.131. Screenshot below.<br/>
It is worth noting that the information gathering was carried out on Kali Linux machine which is the attacking machine (192.168.81.128).

<p align="center">
Nmap Output: <br/>
<img src="https://i.imgur.com/3mEnTj8.png" height="80%" width="80%" alt="Nmap Output"/> 
<br />
</p> <br/>


<h3>Brute Force Attack </h3>

To obtain the credentials of the vulnerable machine, brute force attack was launched from the attacker’s machine using HYDRA. Hydra is a tool which has been pre-installed on Kali Linux. The techniques use dictionary attack, therefore a file that contain series of possible username and password was used. Command used was hydra -L rockyou.txt -P rockyou.txt 192.168.81.131 ftp.
The process retrieved usernames and password for exploitation of the vulnerable node. Result below shows that four credentials were obtained, username and password same: msfadmin, service, postgres and user.

<p align="center">
Brute Force Attack Using HYDRA: <br/>
<img src="https://i.imgur.com/6DIE5Z9.png" height="80%" width="80%" alt="Brute Force Attack Using HYDRA"/> 
<br />
</p> <br/>

While the brute-force attack was on going, Wireshark installed on the VM2 (gateway device), captured the FTP traffic and series of credential that were tested were captured.

<p align="center">
Brute Force Attack Wireshark Capture: <br/>
<img src="https://i.imgur.com/W89DNRN.png" height="80%" width="80%" alt="Brute Force Attack Wireshark Capture "/> 
<br />
</p> <br/>

<h3>Smiley Face Attack</h3>

FTP vsftpd 2.3.4 version is vulnerable to an attack known as Smiley face attack. The username and password are formulated by the attacker. However, the username is followed by smiley symbol ie :) This opens up the listener on port 6200 which was not initially part of the opened ports (Shimpi, 2019). The connection hang after the password is entered and the target shell can be targeted using Netcat tool.

<p align="center">
Smiley Attack: <br/>
<img src="https://i.imgur.com/2lFH14L.png" height="80%" width="80%" alt="Smiley Attack "/> 
<br />
</p> <br/>

<p align="center">
Exploiting Metasploitable2 using Netcat: <br/>
<img src="https://i.imgur.com/hWY2gtC.png" height="80%" width="80%" alt="Exploiting Metasploitable2 using Netcat "/> 
<br />
</p> <br/>

<p align="center">
confirmation of content in webserver: <br/>
<img src="https://i.imgur.com/Bw2GVLI.png" height="80%" width="80%" alt="confirmation of content in webserver "/> 
<br />
</p> <br/>


<h3>Secure Shell Exploit</h3> 
<b>The Process</b>

<p align="center">
Exploiting using Secure Shell. Access was gained into Metasploit framework: <br/>
<img src="https://i.imgur.com/zYMnwv0.png" height="80%" width="80%" alt="Exploiting using Secure Shell "/> 
<br />
</p> <br/>

Also in this scenario, the file containing list of usernames and passwords was used and SSH was opened for all the credentials that were cracked.

<p align="center">
Interacting with the auxiliary: <br/>
<img src="https://i.imgur.com/x6eL0js.png" height="80%" width="80%" alt="Interacting with the auxiliary"/> 
<br />
</p> <br/>

<p align="center">
Exploiting SSH: <br/> 
<img src="https://i.imgur.com/lmpkfA5.png" height="80%" width="80%" alt="Exploiting SSH"/> 
<br />
</p> <br/> 

The msfadmin was used to gain SSH access into the vulnerable machine and attacker continue with the affect stage.

<p align="center">
Access Breach using SSH: <br/> 
<img src="https://i.imgur.com/1F5h74C.png" height="80%" width="80%" alt="Access Breach using SSH"/> 
<br />
</p> <br/> 

The action below demonstrates private and public keys of the admin obtained from the machine. When this is retrieved by an attacker, several other exploit can be carried out. 

<p align="center">
Compromising target data: <br/> 
<img src="https://i.imgur.com/QZigiH4.png" height="80%" width="80%" alt="Compromising target data"/> 
<br />
</p> <br/> 

<h3>SQL Injection Attack</h3>

Since almost every website has a database behind it containing confidential data and secretes, sql injection remain very popular method of attack on web sites. It involves the use of SQL rules to retrieving hidden information or modifying them using SQL query (Hackers-Arise, 2021). 
An open-source penetrating testing tool known as SQLmap was used to find and exploit the SQL injection vulnerabilities. Sqlmap has been pre-installed in Kali Linux VM. While DVWA web application server has been pre-installed in the Metasploitable 2 machine. The security level of the dvwa web server was set to “low”, navigated to the SQL injection and a random user ID was provided to obtain a response from the database. http://192.168.81.131/dvwa/vulnerabilities/sqli/?id=234&Submit=Submit#  

<p align="center">
Web-Server response: <br/> 
<img src="https://i.imgur.com/DeyK9nC.png" height="80%" width="80%" alt="Web-Server response"/> 
<br />
</p> <br/> 

Exploring the server using sqlmap command below exposed the type of database in the backend, the number of tables inside the database.

<p align="center">
Information gathering: <br/> 
<img src="https://i.imgur.com/5rAWhEm.png" height="80%" width="80%" alt="Information gathering"/> 
<img src="https://i.imgur.com/UO21wtv.png" height="80%" width="80%" alt="Information gathering"/> 
<br />
</p><br/>

<p align="center">
Revealing Database Structure: <br/> 
<img src="https://i.imgur.com/PrCAMQG.png" height="80%" width="80%" alt="Revealing Database Structure"/> 
<img src="https://i.imgur.com/ibsRGLB.png" height="80%" width="80%" alt="Revealing Database Structure"/> 
<img src="https://i.imgur.com/b5mcnVE.png" height="80%" width="80%" alt="Revealing Database Structure"/>
<img src="https://i.imgur.com/TCcy3ue.png" height="80%" width="80%" alt="Revealing Database Structure"/>
<img src="https://i.imgur.com/3DvbJX3.png" height="80%" width="80%" alt="Revealing Database Structure"/>
<br />
</p><br/>

The content of the database was dump using  the command sqlmap -u "http://192.168.81.131/dvwa/vulnerabilities/sqli/?id=2344&Submit=Submit" --cookie="PHPSESSID=4879ad207639768562c942606d370a97; security=low" --columns -T users –batch
This revealed the not only the first name, last name, username, and password but also the hash of the passwords as captured below. 

<p align="center">
Database Dump: <br/> 
<img src="https://i.imgur.com/awt04vg.png" height="80%" width="80%" alt="Database Dump"/> 
<img src="https://i.imgur.com/vHDFBHq.png" height="80%" width="80%" alt="Database Dump"/> 
<br />
</p><br/>


<h3>Flood attack</h3>

<b>Using Hping3</b>
This attack shows the Distributed Denial of Service (DDOS) attack which involves overloading target machine with a large quantity and size of packets using Hping3 tool on the attacker’s machine. The effect of the flood was captured on the gateway machine which has snort installed on it.

<p align="center">
Initializing Flood Attack: <br/> 
<img src="https://i.imgur.com/KdNcJia.png" height="80%" width="80%" alt="Initializing Flood Attack"/> 
<br />
</p> <br/> 

From the result captured below, t could be seen that 44.987% was dropped due to the flood. The resource utilization was also captured, and the memory and CPU increased exponentially.

<p align="center">
Snort Capture: <br/> 
<img src="https://i.imgur.com/vjMJNLO.png" height="80%" width="80%" alt="Snort Capture"/> 
<br />
</p> <br/> 

<b>Synflood</b>

<p align="center">
Using Metasploit framework to initiate syn flood: <br/> 
<img src="https://i.imgur.com/pYhYAz2.png" height="80%" width="80%" alt="Using Metasploit framework to initiate syn flood"/> 
<br />
</p> <br/>

<p align="center">
Degraded computer resources: <br/> 
<img src="https://i.imgur.com/T1af6mK.png" height="80%" width="80%" alt="Degraded computer resources"/> 
<br />
</p> <br/>

<h2>Evaluation of Test Outcomes</h2>

It is of good practice and standard regulation that all used ports are to be closed. Opened ports increase the risk of being exploited. On the remote DVWA web server, all traffic of telnet, FTP, SSH were denied using the uncomplicated firewall. The test carried out thereafter from the attacker’s VM indicated that the remote access was denied, therefore, resolving the vulnerabilities.

<p align="center">
Implementing UFW: <br/> 
<img src="https://i.imgur.com/9dw7j8A.png" height="80%" width="80%" alt="Implementing UFW"/> 
<br />
</p> <br/>

<p align="center">
Secured port: <br/> 
<img src="https://i.imgur.com/kXcUTr9.png" height="80%" width="80%" alt="Secured port"/> 
<br />
</p> <br/>

Also, the Security level on the web server was raised to “high”, thereby denying the revelation of database content when sqlmap tool was used.

Furthermore, snort local rules were configured to display alerts, drop icmp traffics to void against DDOS attacks. The configuration was done on the gateway device. The outcome indicated that all the icmp packets were dropped originating from kali VM through the gateway vm. 

<p align="center">
Snort Rule configuration: <br/> 
<img src="https://i.imgur.com/RrI9GnO.png" height="80%" width="80%" alt="Snort Rule configuration"/> 
<br />
</p> <br/>

<h4>Other Recommendations to secure the network</h4>

In modern network design, implementation of automated intrusion detection and prevention system are used to ensure that the network is secured, and it is aware of latest available threats. Therefore, the use of Software Defined Networking (SDN) for network security is receiving attention. With this system, constant monitoring to guard against Zero-day attack and all other already known attacks are instantly reported. Since it is connected not only the application layers but also to other security devices on the network, vulnerabilities are also check and reported in real-time. This will no doubt enhance the overall network security especially for the SDN-Network Intrusion Detection system (NIDS) using Machine learning (ML). <br/>

Data Encryption is another way to secure data. This will provide additional level of security even if there is a successful breach, the attacker will not be able to use the data thereby ensuring the integrity of the system. Unlike the incident in the SSH attack performed, where the public and private keys were retrieved from the target machine. Cloud providers makes storing secretes more convenience with the key vault, and other data encryption features on their platform. This will ensure that data protection is assured to a higher level. <br/>

Role Base Access control technique will enable compromised credential to be restricted to only the resources that are needed to function and access can be easily revoke when the compromise is detected. This process defines the authorization of the system and limit system exposure to attacks.

One aspect that is often neglected is the continuous training of users on the network to sharpen their skills and create awareness with respect to the development in cyber activities. System administrator and other technical team requires periodic cybersecurity training. Likewise, the staff of the organization, who are the weakest link, need information security awareness on password protection, Social Engineering, file access and sharing, phishing identification etc.



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
