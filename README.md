<h1>Configuring DNS A and CNAME Records</h1>

<h2>Overview</h2>
<p>Create and verify DNS A and CNAME records on a Windows Server DNS in Azure to enable host-to-IP resolution and hostname aliases.</p>

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (VMs, DNS)</li>
  <li>Windows Server (DNS Manager)</li>
  <li>Remote Desktop, PowerShell</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2019/2022</li>
  <li>Windows 10 (client)</li>
</ul>

<h2>High-Level Steps</h2>
<ol>
  <li>Log into DNS server VM and open DNS Manager.</li>
  <li>Create A-records mapping hostnames to private IPs.</li>
  <li>Create CNAME records to alias hostnames as needed.</li>
  <li>Validate using <code>ping</code> and <code>nslookup</code> from client VM.</li>
</ol>

<h2>Actions and Observations</h2>
<p><img src="https://i.imgur.com/DJmEXEB.png" width="80%" alt="DNS Manager A Records"/></p>
<p>A-records successfully created for multiple internal hosts.</p>

<p><img src="https://i.imgur.com/DJmEXEB.png" width="80%" alt="CNAME Aliases"/></p>
<p>CNAME records allowed alternative hostnames for easy access.</p>

<p><img src="https://i.imgur.com/DJmEXEB.png" width="80%" alt="nslookup Test"/></p>
<p><code>nslookup</code> verified accurate name resolution across both record types.</p>
