The Broadcom Value Pack (BVP) Installation Guide describes how to install the Broadcom Value Pack (BVP). The information includes step-by-step configuration instructions and suggested best practices.




## Installation of Broadcom Value Pack 


| VMware Product                              | Version               |
|:--------------------------------------------|:---------------------:|
| VMware Cloud Foundation                     |     5.2               |     
| VMware Cloud Foundation Automation          |     8.18              |
| Broadcom Value Pack by Korea CXS            |     1.0               |

---

### Steps:

### 1. Download of Broadcom Value Pack (BVP) Package
<details>
<summary>"Click to expand"</summary>

Download Broadcom Value Pack 1.0 Package file [download link ](https://my.vmware.com/web/vmware/details?downloadGroup=NSX-T-300&productId=982&rPId=45015)


<p align="center">
  <img width=75% height=75% src="/docs/assets/Graphics/2.1.step1.jpg">
</p>


</details>

---

### 2. Deployment of Broadcom Value Pack (BVP)
<details>
<summary>"Click to expand"</summary>

- **From vCenter, deploy NSX-T Unified Appliance OVA.**  
	<p align="center">
	  <img width=25% height=25% src="/docs/assets/Graphics/2.2.step1.jpg">
	</p>

- **Select OVF file.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step2.jpg">
	</p>

- **Enter NSX-T Manager VM name + vCenter folder for VM.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step3.jpg">
	</p>

- **Select ESXi to host NSX-T Manager.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step4.jpg">
	</p>

- **Review NSX-T Manager VM details.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step5.jpg">
	</p>

- **Select NSX-T Manager VM size (Small).**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step6.jpg">
	</p>

- **Select storage for NSX-T Manager VM.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step7.jpg">
	</p>

- **Select VDS Port Group for NSX-T Manager management vNIC (vCenter Managament Port Group).**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step8.jpg">
	</p>

- **Enter NSX-T Manager information (passwords, hostname, IP, DNS, NTP). Important: Rolename is "NSX Manager".**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step9.jpg">
	</p>

- **Review NSX-T Manager VM settings.**  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.2.step10.jpg">
	</p>

- **Once NSX-T Manager deployment is finished, start the VM.**  
	<p align="center">
	  <img width=40% height=40% src="/docs/assets/Graphics/2.2.step11.jpg">
	</p>
</details>

---

### 3. Register NSX-T to vCenter
<details>
<summary>"Click to expand"</summary>

*Note: NSX-T Manager requires few minutes to fully start and get all its services running.*

- **Log on NSX-T Manager UI.**  
In a browser: https://192.168.50.5/.  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.3.step1.jpg">
	</p>

- **Configuration NSX-T Licence.**  
Under "System - Settings - Licenses", click "Add".  
	<p align="center">
	  <img width=75% height=75% src="/docs/assets/Graphics/2.3.step2.jpg">
	</p>


- **Register NSX-T in vCenter (to allow the deplyment of NSX elements into vCenter/ESXi from NSX).**  
Under "System - Configuration - Fabric - Compute Managers", click "Add".  
	<p align="center">
	  <img width=50% height=50% src="/docs/assets/Graphics/2.3.step3a.jpg">
	</p>  
	<p align="center">
	  <img width=40% height=40% src="/docs/assets/Graphics/2.3.step3b.jpg">
	</p>

- **Validate NSX-T registration in vCenter.**  
Under "System - Configuration - Fabric - Compute Managers", click "Refresh" (bottom-left).
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.3.step4.jpg">
	</p>

</details>

---

### 5. Deployment of Broadcom Value Pack (BVP) in Aria Automation


<details>
<summary>"Click to expand"</summary>

*Note: If you limit your Evaluation at [Security only (no Logical Network)](/docs/3.1-Security-Only.md) and not [Logical Network + Security](/docs/3.2-LogicalNetwork-Security.md) nor [Operation Tools](/docs/3.3-Operation-Tools.md), you don't need to deploy Edge Nodes.*

#### 5.1. Creation of VDS Port Group "All VLAN"

<details>
<summary>"Click to expand"</summary>

- **Create a Port Group "All VLAN" (= VLAN Tag 0-4096) on VDS.**  
From vCenter, under "Networking", select the VDS-NSX, and right-click to "New Distributed Port Group...".
*For this lab, see the top of page for this Port Group on VDS.*  
  	<p align="center">
	  <img width=40% height=40% src="/docs/assets/Graphics/2.5.1.step1.jpg">
	</p>  
  	<p align="center">
	  <img width=70% height=70% src="/docs/assets/Graphics/2.5.1.step2.jpg">
	</p>  
  	<p align="center">
	  <img width=70% height=70% src="/docs/assets/Graphics/2.5.1.step3.jpg">
	</p>  
  	<p align="center">
	  <img width=70% height=70% src="/docs/assets/Graphics/2.5.1.step4.jpg">
	</p>  

</details>

#### 5.2. Installation of NSX Edge Node

<details>
<summary>"Click to expand"</summary>

- **Deploy 1 Edge Node on ESXi.**  
Under "System - Configuration - Fabric - Nodes - Edge Transport Nodes", click "Add Edge VM".  
*Select Form Factor Medium (useful if you want to test later Load-Balancing),  
enable SSH for admin and root if you want to try later deeper troubleshooting,  
Management and Switch (TEP) IP addresses on the top of the page), and  
Transport Zones = "nsx-overlay-transportzone" (default TZ for Overlay traffic) and "nsx-vlan-transportzone" (default TZ for VLAN traffic).*
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step1.jpg">
	</p>  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step2.jpg">
	</p>  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step3.jpg">
	</p>  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step4.jpg">
	</p>  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step5.jpg">
	</p>  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step6.jpg">
	</p>  

- **Validate Edge Node deployment.**  
Under "System - Configuration - Fabric - Nodes - Edge Transport Nodes", click "Refresh" (bottom UI)  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.2.step7.jpg">
	</p>  

</details>

#### 5.3. Creation of Edge Cluster

<details>
<summary>"Click to expand"</summary>

- **Create 1 Edge Cluster with EdgeNode1 member.**  
Under "System - Configuration - Fabric - Nodes - Edge Clusters", click "Add".  
*Select EdgeNode1 as member of that Edge Cluster.*
	<p align="center">
	  <img width=50% height=50% src="/docs/assets/Graphics/2.5.3.step1.jpg">
	</p>  

- **Validate Edge Cluster creation.**  
Under "System - Configuration - Fabric - Nodes - Edge Clusters", click "Refresh".  
	<p align="center">
	  <img width=85% height=85% src="/docs/assets/Graphics/2.5.3.step2.jpg">
	</p>  


</details>

</details>

---

[***Reference: VMware Cloud Foundation 5.2***](https://techdocs.broadcom.com/us/en/vmware-cis/vcf/vcf-5-2-and-earlier/5-2.html)

