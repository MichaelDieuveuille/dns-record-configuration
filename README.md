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
<img width="2559" height="1292" alt="Screenshot 2025-11-07 112630" src="https://github.com/user-attachments/assets/7881ad87-118b-4da9-9963-99baa5b8fc35" />

<p>A-records successfully created for multiple internal hosts.</p>

<img width="2559" height="1293" alt="Screenshot 2025-11-07 112912" src="https://github.com/user-attachments/assets/a0d7fc80-d52e-4021-b6f6-fcc1d6ff15cf" />

<p>CNAME records allowed alternative hostnames for easy access.</p>

<img width="2559" height="1217" alt="Screenshot 2025-11-07 112942" src="https://github.com/user-attachments/assets/35467e41-d383-4858-9f4f-6651ad6cfeb7" />

<p><code>nslookup</code> verified accurate name resolution across both record types.</p>
