This process sets up two virtual machines (Windows 10 and Linux Ubuntu) within the same Azure Virtual Network (VNet) to ensure connectivity. Below are the detailed steps:

https://imgur.com/xYQZhkm
<p class="demoTitle">&nbsp; &nbsp; &nbsp;</p>
<h3><strong>Step 1: Create a Resource Group</strong></h3>
<ol>(https://github.com/user-attachments/assets/4e416ed7-27ec-4ec5-a94f-bc878dc578e8)

<li>Go to the <a href="https://portal.azure.com/" target="_new" rel="noopener">Azure Portal</a>.</li>
<li>In the left-hand menu, select <strong>Resource groups</strong>.</li>
<li>Click <strong>Create</strong> and enter:
<ul>
<li><strong>Subscription</strong>: Select your active subscription.</li>
<li><strong>Resource Group Name</strong>: Example &ndash; <code>MyResourceGroup</code></li>
<li><strong>Region</strong>: Choose a preferred region (e.g., <code>East US</code>).</li>
</ul>
</li>
<li>Click <strong>Review + Create</strong>, then <strong>Create</strong>.</li>
</ol>
<p>&nbsp;</p>
<h3><strong>Step 2: Create a Windows 10 Virtual Machine</strong></h3>
<ol>
<li>
<p>In the <strong>Azure Portal</strong>, go to <strong>Virtual Machines</strong> and click <strong>Create</strong> &rarr; <strong>Azure Virtual Machine</strong>.</p>(https://github.com/user-attachments/assets/f5836f07-eb68-472c-8e89-fbfe011c0869)

</li>
<li>
<p>Under the <strong>Basics</strong> tab:</p>
<ul>
<li><strong>Resource Group</strong>: Select <code>MyResourceGroup</code>.</li>
<li><strong>Virtual Machine Name</strong>: Example &ndash; <code>Win10-VM</code></li>
<li><strong>Region</strong>: Select the same region as the Resource Group.</li>
<li><strong>Image</strong>: Choose <strong>Windows 10</strong>.</li>
<li><strong>Size</strong>: Choose an appropriate size (e.g., <code>Standard_B2ms</code>).</li>
<li><strong>Administrator Account</strong>:
<ul>
<li><strong>Username</strong>: <code>winadmin</code></li>
<li><strong>Password</strong>: Set a strong password.</li>
</ul>
</li>
<li><strong>Public Inbound Ports</strong>: Allow <strong>RDP (3389)</strong>.</li>
</ul>
</li>
<li>
<p>Under <strong>Networking</strong>:</p>
<ul>
<li><strong>Virtual Network</strong>: Select <strong>Create new</strong>.</li>
<li><strong>Subnet</strong>: Let it create a default subnet.</li>
</ul>
</li>
<li>
<ol>
<li>
<p>Click <strong>Review + Create</strong>, then <strong>Create</strong>.</p>
</li>
</ol>
<hr />
<h3><strong>Step 3: Create a Linux (Ubuntu) Virtual Machine</strong></h3>
<ol>
<li>
<p>In the <strong>Azure Portal</strong>, go to <strong>Virtual Machines</strong> and click <strong>Create</strong> &rarr; <strong>Azure Virtual Machine</strong>.</p>
</li>
<li>
<p>Under the <strong>Basics</strong> tab:</p>
<ul>
<li><strong>Resource Group</strong>: Select <code>MyResourceGroup</code>.</li>
<li><strong>Virtual Machine Name</strong>: Example &ndash; <code>Ubuntu-VM</code></li>
<li><strong>Region</strong>: Select the same region.</li>
<li><strong>Image</strong>: Choose <strong>Ubuntu LTS</strong>.</li>
<li><strong>Size</strong>: Choose an appropriate size (e.g., <code>Standard_B2ms</code>).</li>
<li><strong>Authentication Type</strong>: Select <strong>Username &amp; Password</strong>.
<ul>
<li><strong>Username</strong>: <code>linuxadmin</code></li>
<li><strong>Password</strong>: Set a strong password.</li>
</ul>
</li>
</ul>
</li>
<li>
<p>Under <strong>Networking</strong>:</p>
<ul>
<li><strong>Virtual Network</strong>: Select the <strong>same VNet</strong> created with the Windows VM.</li>
<li><strong>Subnet</strong>: Use the existing subnet.</li>
<li><strong>Public Inbound Ports</strong>: Allow <strong>SSH (22)</strong>.</li>
</ul>
</li>
<li>
<p>Click <strong>Review + Create</strong>, then <strong>Create</strong>.</p>
</li>
</ol>
<hr />
<h2><strong>Part 2: Observing ICMP Traffic</strong></h2>
<h3><strong>Step 1: Connect to Windows 10 VM</strong></h3>
<ol>
<li>Go to <a href="https://portal.azure.com/" target="_new" rel="noopener">Azure Portal</a>.</li>
<li>Retrieve the <strong>public IP address</strong> of your <strong>Windows 10 VM</strong>.</li>
<li><strong>Mac Users:</strong> Install <a href="https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12" target="_new" rel="noopener">Microsoft Remote Desktop</a>.</li>
<li>Use <strong>RDP</strong> to connect to <strong>Windows 10 VM</strong>.</li>
</ol>
<h3><strong>Step 2: Install and Use Wireshark</strong></h3>
<ol>
<li>On <strong>Windows 10 VM</strong>, download and install <strong>Wireshark</strong>.</li>
<li>Open <strong>Wireshark</strong>, select your <strong>active network adapter</strong>, and start <strong>packet capture</strong>.</li>
<li>In the <strong>Wireshark filter bar</strong>, enter:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-plaintext">icmp </code></div>
</div>
This filters only <strong>ICMP (ping) traffic</strong>.</li>
</ol>(https://github.com/user-attachments/assets/468fea85-4810-4411-b7b1-2e83a0ae0bd6)

<h3><strong>Step 3: Ping Ubuntu VM</strong></h3>
<ol>(https://github.com/user-attachments/assets/0334ea46-cfda-4ba9-b868-a818e1ba5cbe)

<li>Retrieve the <strong>private IP address</strong> of your <strong>Ubuntu VM</strong> from the Azure portal.</li>
<li>Open <strong>Command Prompt (cmd) or PowerShell</strong> on <strong>Windows 10 VM</strong>.</li>
<li>Run:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">ping &lt;Ubuntu_VM_Private_IP&gt; </code></div>
</div>
</li>
<li>Observe the <strong>ICMP request and reply packets</strong> in Wireshark.</li>
</ol>
<h3><strong>Step 4: Ping a Public Website</strong></h3>
<ol>
<li>In <strong>Windows 10 VM</strong>, ping Google:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">ping www.google.com </code></div>
</div>
</li>
<li>Observe <strong>ICMP traffic</strong> in <strong>Wireshark</strong>.</li>
</ol>
<hr />
<h2><strong>Part 3: Configuring a Firewall (Network Security Group)</strong></h2>
<h3><strong>Step 1: Block ICMP (Ping) Traffic</strong></h3>
<ol>
<li>Initiate <strong>continuous ping</strong> to <strong>Ubuntu VM</strong> from <strong>Windows 10 VM</strong>:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>C:\Users\Win-10-Pro\Desktop\networking Azure
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">ping &lt;Ubuntu_VM_Private_IP&gt; -t </code></div>
</div>
</li>
<li>Go to <strong>Azure Portal &rarr; Network Security Groups (NSG)</strong>.</li>
<li>Select the <strong>NSG associated with Ubuntu VM</strong>.</li>
<li>Under <strong>Inbound Security Rules</strong>, <strong>deny ICMP traffic</strong>.</li>
<li>Back in <strong>Windows 10 VM</strong>, observe that the <strong>ping requests now fail</strong> in both <strong>cmd and Wireshark</strong>.</li>
</ol>
<h3><strong>Step 2: Re-enable ICMP Traffic</strong></h3>
<ol>
<li>In <strong>Azure NSG</strong>, allow <strong>ICMP inbound traffic</strong>.</li>
<li>Observe in <strong>Windows 10 VM</strong> that the <strong>ping resumes</strong> in <strong>cmd and Wireshark</strong>.</li>
<li>Stop the ping using <strong>CTRL + C</strong>.</li>
</ol>
<hr />
<h2><strong>Observe SSH Traffic</strong></h2>
<h3><strong>Step 1: Capture SSH Traffic in Wireshark</strong></h3>
<ol>
<li>In <strong>Wireshark</strong>, enter the filter:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-plaintext">ssh </code></div>
</div>
</li>
<li>Start <strong>Wireshark packet capture</strong>.</li>
</ol>
<h3><strong>Step 2: SSH into Ubuntu VM</strong></h3>
<ol>
<li>Open <strong>PowerShell</strong> in <strong>Windows 10 VM</strong>.</li>
<li>Run:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">ssh labuser@&lt;Ubuntu_VM_Private_IP&gt; </code></div>
</div>
</li>
<li>Enter the <strong>password</strong> when prompted.</li>
<li>Run basic <strong>Linux commands</strong> (<code>ls</code>, <code>pwd</code>, <code>whoami</code>).</li>
<li>Observe <strong>SSH packets</strong> appearing in <strong>Wireshark</strong>.</li>
<li>Exit SSH:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-plaintext">exit </code></div>
</div>
</li>
</ol>
<hr />
<h2><strong>Observe DHCP Traffic</strong></h2>
<h3><strong>Step 1: Capture DHCP Traffic in Wireshark</strong></h3>
<ol>
<li>In <strong>Wireshark</strong>, enter:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-plaintext">dhcp </code></div>
</div>
</li>
<li>Start <strong>Wireshark packet capture</strong>.</li>
</ol>
<h3><strong>Step 2: Renew DHCP Lease</strong></h3>
<ol>
<li>Open <strong>PowerShell</strong> in <strong>Windows 10 VM</strong> as <strong>Administrator</strong>.</li>
<li>Run:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">ipconfig /renew </code></div>
</div>
</li>
<li>Observe <strong>DHCP packets</strong> in <strong>Wireshark</strong>, showing <strong>DHCP Discover, Offer, Request, and Acknowledge</strong>.</li>
</ol>
<hr />
<h2><strong>Observe DNS Traffic</strong></h2>
<h3><strong>Step 1: Capture DNS Traffic in Wireshark</strong></h3>
<ol>
<li>In <strong>Wireshark</strong>, enter:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-plaintext">dns </code></div>
</div>
</li>
<li>Start <strong>Wireshark packet capture</strong>.</li>
</ol>
<h3><strong>Step 2: Perform DNS Lookup</strong></h3>
<ol>
<li>Open <strong>Command Prompt or PowerShell</strong> in <strong>Windows 10 VM</strong>.</li>
<li>Run:
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950">
<div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">powershell</div>
<div class="sticky top-9 md:top-[5.75rem]">
<div class="absolute bottom-0 right-2 flex h-9 items-center">
<div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1">Copier</button></span><span class="" data-state="closed"><button class="flex select-none items-center gap-1">Modifier</button></span></div>
</div>
</div>
<div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-powershell">nslookup google.com nslookup disney.com </code></div>
</div>
</li>
<li>Observe <strong>DNS query and response packets</strong> in <strong>Wireshark</strong>.</li>
</ol>
