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

<img width="869" height="730" alt="DNS 1" src="https://github.com/user-attachments/assets/d812aceb-3364-4357-b882-69a04cb9caf6" />

First, start the VMs and RDP into Client1. Open PowerShell as an administrator and attempt to ping "mainframe." This will fail because "mainframe" is not found in the local cache, the hosts file, or the DNS server.

<img width="875" height="733" alt="DNS 2" src="https://github.com/user-attachments/assets/d0b145aa-f163-48c3-ac38-d1e42bf35df7" />

Next, run the command ipconfig /displaydns. You'll notice there is no entry for "mainframe" in the DNS cache.

<img width="874" height="314" alt="DNS 3" src="https://github.com/user-attachments/assets/8aef9427-6892-465b-8da6-a4c0da35e790" />


After that, run the command nslookup mainframe. Once again, you'll find that no results are returned.

<img width="1187" height="657" alt="DNS 4" src="https://github.com/user-attachments/assets/f6eff9c8-96fc-414f-8808-36ca96171ddf" />

Next, we'll create a DNS A-record on DC-1 for "mainframe" and point it to DC-1's private IP address. On the DC-1 VM, search for Administrative Tools and open DNS. Navigate to DC-1 > Forward Lookup Zones > mydomain.com, then right-click inside mydomain.com and select New Host (A or AAAA). In the Name field, enter mainframe, and in the IP Address field, input DC-1's private IP address. Save the record.

<img width="863" height="311" alt="DNS 5" src="https://github.com/user-attachments/assets/747e1ad2-8bb1-4690-90d5-f22b669f4c35" />

Now, return to Client1 and try pinging "mainframe" in PowerShell again. This time, the ping will succeed because we created a DNS A-record on DC-1 pointing to its private IP address.


<img width="756" height="526" alt="DNS 6" src="https://github.com/user-attachments/assets/ff14b1b3-f59d-4679-8621-45206d0a78ba" />
<img width="858" height="296" alt="DNS 7" src="https://github.com/user-attachments/assets/4b8cc84f-5db2-4b5e-ae30-815c83b6e187" />
<P>
  
</P>
Now, go back to DC-1 and update the DNS A-record for "mainframe" to point to the IP address 8.8.8.8. After making this change, return to the Client1 VM and ping "mainframe" again. You'll notice it still pings the old IP address.


<img width="859" height="604" alt="DNS 8" src="https://github.com/user-attachments/assets/dbaf8b20-a236-4fd6-b0d3-bf2e45d8b6d6" />



Use the command ipconfig /displaydns on Client1 and locate the entry for "mainframe." You'll see that the A-record still points to 10.0.0.4, providing a more detailed view of the cached DNS entry.
<img width="879" height="227" alt="DNS 9" src="https://github.com/user-attachments/assets/0accc309-3796-484c-b5bb-39b4b84fba0e" />


To ensure that the new IP address from the updated A-record is reflected, use the command ipconfig /flushdns to clear the DNS cache. The new IP address will be shown when you use ipconfig /displaydns.

<img width="874" height="315" alt="DNS 10" src="https://github.com/user-attachments/assets/27eb52bb-2e31-4980-b8fb-546757c68700" />

Now, attempt to ping "mainframe" one more time from Client1. You'll notice that it successfully pings the new IP address 8.8.8.8, reflecting the updated A-record.

<img width="757" height="523" alt="DNS 11" src="https://github.com/user-attachments/assets/9f0cfc03-043b-4e7b-ac3f-8f2477da0b1c" />

Next, go back to the DC-1 VM and create a CNAME record that points the host "explore" to "www.google.com". To do this, navigate to the DNS Manager, right-click mydomain.com under Forward Lookup Zones, and select New Alias (CNAME). In the Alias name field, enter explore, and in the Fully Qualified Domain Name (FQDN) field, enter www.google.com. Save the record.

<img width="868" height="303" alt="DNS 12" src="https://github.com/user-attachments/assets/df741a6d-a3c4-4e80-9122-7775f0982e84" />


Go back to the Client1 VM and ping "explore." You should observe that the ping is successfully resolved to www.google.com, as the CNAME record you created points "explore" to that address.


<img width="868" height="303" alt="DNS 12" src="https://github.com/user-attachments/assets/df741a6d-a3c4-4e80-9122-7775f0982e84" />

Lastly, run the command nslookup explore on Client1. The results should show that "explore" resolves to www.google.com, indicating the CNAME record is working as expected.
