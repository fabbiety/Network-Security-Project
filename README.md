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

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
