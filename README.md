<h1>Active-Directory-HomeLab-Creating-Windows-Clients</h1>

<h2>Description</h2>
This project is a continuation of using PowerShell to create users in my previous project/repository and I will focus on making the clients (computers) on a VM to be added to the domain. See diagram below for reference/network information.

<br>
<br/>

<b>ALL CREDITS ON THIS PROJECT GOES TO JOSH MADAKOR. <b> 

<br/>
<img src="https://imgur.com/yibftVW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h2>Languages and Utilities Used</h2>

- <b>None
  
<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows Server 2016</b>
- <b>Oracle VirtualBox</b>

<h2>Lab walk-through/details:</h2>

<p align="center">

Go to your Oracle VB Console and find "New." Name it CLIENT1, with Windows 10 and 64-Bit set. Hit next; for the RAM, keep it at 2GB unless you know and can supply 4GB. Continue all the way through and create the VM. <br/>
<img src="https://imgur.com/w7TT5Me.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Right click on the Client1 vm, Settings, Advanced tab and enable the drop down to Bidirectional for Shared Clipboard and Drag'n'Drop. </b>
<img src="https://imgur.com/6uxcWEf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Go to the System Tab and adjust the CPU accordingly (if you don't know, keep it less. In this example I am using 4). </b>
<img src="https://imgur.com/GkP0PYS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Go to the Network tab and make adapter 1 NAT internal. This will allow our client to receive an IP address from the DHCP server, emulating a corporate/live production IT environment. </b>
<img src="https://imgur.com/ByAwDyi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
This could have been during the 1st step, but find the Windows 10 ISO on your computer and mount it onto the VM. If you do not have it or recall, you will need to grab one via Microsoft https://www.microsoft.com/en-us/software-download/windows10ISO before proceeding. </b>
<img src="https://imgur.com/sTUV4ve.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Continue with Next, Install Now, "I don't have a product key." </b>
<img src="https://imgur.com/mWyWqbY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
For the Windows version, do NOT pick Windows 10 Home. You will not be able to join it to the domain. Select and proceed with Windows 10 Pro. </b>
<img src="https://imgur.com/QfKTRT0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Accept the license agreement, Custom install, then next. It will begin installing and restart. Similarly to setting up your server, do NOT "press any key to continue" on the black screen or you'll have to redo the setup again. </b>
<img src="https://imgur.com/ZdUJ1Ft.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Set your appropriate region, keyboard layout and skip adding a second keyboard. </b>
<img src="https://imgur.com/a9qufdx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the organization management option. This emulating a real-life environment of having a domained, organization controlled and joined computer. </b>
<img src="https://imgur.com/S4oiAjs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select Domain join instead (bottom left corner area). </b>
<img src="https://imgur.com/gPIAMsT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, make the name User, with no password afterwards and not now. On the Choose privacy settings, UNCHECK ALL options. It'll depend on the organization but most opt to keep the location option checked for recovery purposes if lost physically ie a laptop. </b>
<img src="https://imgur.com/QWEOBkW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Skip customize experience and Not Now for Cortana. You should be initializing and eventually will reach the home desktop page. </b>
<img src="https://imgur.com/AEP18By.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Open your command prompt and try to ping Google and mydomain.com. (Google: 8.8.8.8) ping 8.8.8.8 and ping mydomain.com. Since the domain join option in the previous setup was available, our client can "talk" and communicate with the internet. DNS server should be working if we can ping to the internet, so from setting up the RAS, NAT, and DHCP everything in the infrastructure should be working. </b>
<img src="https://imgur.com/AEP18By.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We will change the name. Right click start menu, go to system, scroll down, advanced system settings, and click the Change button. Go to Computer Name tab and rename it to Client1. Then, select the Domain option under Member of and enter mydomain.com </b>
<img src="https://imgur.com/XJGjShN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Press Ok and it'll prompt administrator credentials to authorize the join. Use the administrator account you created when on the root/server account. (If that doesn't work, try your root/server account credentials). </b>
<img src="https://imgur.com/bPKYgUx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
You should be presented with a prompt stating "Welcome to mydomain.com domain." Press Ok, close out the window, and restart now for the client. </b>
<img src="https://imgur.com/c2myYEo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The client computer should have restarted and is now part of the domain you created. Navigate back to your DC and review the DHCP settings via the Tools (top right of the Server Manager). Go to the DHCP server, expand the Scope, and expand the Address Lease. You should see your client with an IP address assigned to it, which was given from the DHCP server when the client was being setup and connected to our internal network (RAS, NAT and DHCP doing their services in conjuction to provide the utilities to your client computer).  </b>
<img src="https://imgur.com/EcIGgj2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
While on your DC, go back to Active Directory Users and Computers. Under mydomain.com, go to Computers. You'll see that Client1 is now listed as an active computer under your domain from being domain joined during the setup process. If you were to delete that computer off of Active Directory, then it would be normal computer and you cannot use your credentials earlier to sign back on, since it's no longer part of the enterprise. But since it's now part of the domain, the administrator account and the 1000 users listed on Active Directory could sign on to that client computer with their credentials.  </b>
<img src="https://imgur.com/s08PdG6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Try logging in with one of the user accounts available on Active Directory. The passwords are all the same, being Password1. You should be able to sign on. For example, I used abirk below.  </b>
<img src="https://imgur.com/vB1YIvJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
For another check/confirmation: Once logged in with a random account, (or yours that you created, not the admin one), open the Command Prompt and type in whoami. It should come back with information referencing the username and the domain. 
<img src="https://imgur.com/L71amFX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
This concludes the lab(s), to include from the previous repositories creating AD DC, installing RAT, NAS, DHCP, users using PowerShell and joining a client computer to a domain. Feel free play around and experiment on your lab and reference supplemental sources as needed for assistance/troubleshooting.  
<img src="https://imgur.com/LdYZmCj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
