<h1>Implementing VPC Peering on AWS</h1>


<h2>Description</h2>
In this live environment, you will learn how to create, and configure VPC peering within AWS. VPC peering is a feature of AWS which allows cross-VPC communication, without additional hardware, or software solutions. VPC peering is a feature you will use daily in production environments, and it's useful to know for all of the AWS exams.<br />
<br />
The environment is split into three stages. There is an architectural overview first, followed by the creation and configuration of a VPC peer, and finally the live environment will finish by demonstrating the limitations of VPC peering and some advanced features.<br />
<br />
By the end of the lab, you will be able to comfortably implement VPC peering, know it's limitations, and perhaps more importantly understand when and why you would use the feature.
<br />

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>AWS</b>
  
<h2>Program walk-through:</h2>

In INSTANCE1, ping the public IP address for INSTANCE2:<br/>
ping <INSTANCE2_PUBLIC_IP_ADDRESS>

<br/>
 
<p align="center">
<img src="https://i.imgur.com/GGj5FUp.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the AWS Console, navigate to the VPC Dashboard.
2. Click Network ACLs.
3. Select Public2-NACL.
4. In the tab at the bottom of the page, select Inbound Rules.
5. Click Edit.
6. For rule 104, enter the following in the Source field:
- 10.0.0.0/13
7. Click Save
<br/>
 
<p align="center">
<img src="https://i.imgur.com/rSiat6k.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the AWS Console, navigate back to the VPC Dashboard.
2. Under, Virtual Private Cloud, click Peering Connections.
3. Click Create Peering Connection.
4. For VPC (Requester), select VPC1.
5. For VPC (Accepter), select VPC2.
6. Click Create Peering Connection.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/kbEikOD.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

At the top of the page, click Actions, and select Accept Request.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/9DrNn3A.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
<img src="https://i.imgur.com/srEYrxU.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Click Route Tables, and select Public1-RT.
2. At the bottom of the page, select the Routes tab, and click Edit.
3. Click Add another route.
4. For Destination, enter the <VPC2_IPV4_CIDR>, and in the Target box, select the target starting with pcx.
5. Click Save


<br/>
 
<p align="center">
<img src="https://i.imgur.com/TzjaAzC.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Repeat these steps for Private1-RT

<br/>
 
<p align="center">
<img src="https://i.imgur.com/wHYlTDn.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Click Public2-RT.
2. At the bottom of the page, select the Routes tab, and click Edit.
3. Click Add another route.
4. For Destination, enter the <VPC1_IPV4_CIDR>, and in the Target box, select the target starting with pcx.
5. Click Save


<br/>
 
<p align="center">
<img src="https://i.imgur.com/8Iqmckm.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Repeat these steps for Private2-RT
<br/>
 
<p align="center">
<img src="https://i.imgur.com/K2B59rB.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Back in INSTANCE1, ping the public IP address for INSTANCE2 again:
ping <INSTANCE2_PUBLIC_IP_ADDRESS><br/>
There should be communication.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/PogWjQ5.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the VPC Dashboard, under, Virtual Private Cloud, click Peering Connections.
2. Click Create Peering Connection.
3. For VPC (Requester), select VPC2.
4. For VPC (Accepter), select VPC3.
5. Click Create Peering Connection.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/456KmJ6.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Select the pending connection and at the top of the page, click Actions, and select Accept Request.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/5fBTmcd.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In Route Tables, and select Public2-RT.
2. At the bottom of the page, select the Routes tab, and click Edit.
3. Click Add another route.
4. For Destination, enter the <VPC3_IPV4_CIDR>, and in the Target box, paste the <PEERING_CONNECTION_ID>.
5. Click Save.
6. Repeat these steps for Private2-RT.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/9TbimCf.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Select Public3-RT.
2. At the bottom of the page, select the Routes tab, and click Edit.
3. Click Add another route.
4. For Destination, enter the <VPC2_IPV4_CIDR>, and in the Target box, paste the <PEERING_CONNECTION_ID>.
5. Click Save.
6. Repeat these steps for Private3-RT.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/3mWQ4A7.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Back in INSTANCE1, ping the public IP address for INSTANCE3. There shouldn’t be any communication. 

<br/>
 
<p align="center">
<img src="https://i.imgur.com/KDeHyeg.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the AWS Console, navigate to the VPC Dashboard.
2. Click Network ACLs.
3. Select Private3-NACL.
4. In the tab at the bottom of the page, select Inbound Rules.
5. Click Edit.
6. Click Add another rule, and enter the following:
- Rule #: 100
- Type: All ICMP
- Source: 10.0.0.0/13
7. Click Save.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/WjzLv7m.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Click the Outbound Rules tab, and repeat these steps.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/JN7l9G4.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the VPC Dashboard, under, Virtual Private Cloud, click Peering Connections.
2. Click Create Peering Connection.
3. For VPC (Requester), select VPC1.
4. For VPC (Accepter), select VPC3.
5. Click Create Peering Connection.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/siLySrM.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Select the pending connection.
At the top of the page, click Actions, and select Accept Request.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/RyaCjaX.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Copy the Peering Connection Id for the third connection.
2. In Route Tables, and select Public1-RT.
3. At the bottom of the page, select the Routes tab, and click Edit.
4. Click Add another route.
5. For Destination, enter the <VPC3_IPV4_CIDR>, and in the Target box, paste the <PEERING_CONNECTION_ID> for the third connection.
6. Click Save

<br/>
 
<p align="center">
<img src="https://i.imgur.com/EwqAORM.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Repeat these steps for Private1-RT

<br/>
 
<p align="center">
<img src="https://i.imgur.com/VFfpvKK.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Select Public3-RT.
2. At the bottom of the page, select the Routes tab, and click Edit.
3. Click Add another route.
4. For Destination, enter the <VPC1_IPV4_CIDR>, and in the Target box, paste the <PEERING_CONNECTION_ID>.
5. Click Save.
6. Repeat these steps for Private3-RT


<br/>
 
<p align="center">
<img src="https://i.imgur.com/8MbqAwv.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

In the INSTANCE1 terminal, ping the public IP address for INSTANCE3 again

<br/>
 
<p align="center">
<img src="https://i.imgur.com/SJTUlyC.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the AWS Console, navigate to the EC2 Dashboard.
2. Select Instance2.
3. Copy the Public DNS (IPv4) URL.
4. In the INSTANCE1 terminal, ping the Instance2 URL:
- ping <INSTANCE2_PUBLIC_DNS><br/>
There should not be any communication


<br/>
 
<p align="center">
<img src="https://i.imgur.com/4jqMYZ5.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the VPC Dashboard, click Peering Connections.
2. Select the connection that connects VPC1 and VPC2, and in the Actions menu, click Edit DNS Settings.
3. Check both boxes under DNS Resolution, and click Save.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/Fh4mBXU.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

In the INSTANCE1 terminal, ping the Instance2 URL and there should be communication this time.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/v8bmRJH.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />
