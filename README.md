# Active-Directory-GPO-Project-Automated-Application-Launch

An educational lab demonstrating the implementation of **Active Directory Domain Services (AD DS)** and **Group Policy Objects (GPO)** to automate software delivery and centralized management.

## 📌 Project Overview
The objective of this project is to configure a Windows Server 2025 environment where a specific application (Microsoft Edge) is automatically launched upon user logon across all domain-joined workstations. This simulates real-world enterprise automation and policy enforcement.

## 🏗️ Lab Infrastructure
* **Hypervisor:** Oracle VirtualBox
* **Domain Controller:** Windows Server 2025 (`corp.santo.com`)
* **Client Machine:** Windows 10 Pro
* **Network:** Isolated Internal Network with DHCP and DNS services.

---

## 🛠️ Implementation Steps

### 1. Group Policy Object (GPO) Creation
1.  Navigate to **Server Manager** > **Tools** > **Group Policy Management**.
2.  Expand your Forest and Domain (e.g., `corp.santo.com`).
3.  Right-click the **Group Policy Objects** container and select **New**.
4.  Name the GPO: `Auto-Start Edge Policy`.

### 2. Configuring the Startup Policy
1.  Right-click the new GPO and select **Edit** to open the Group Policy Management Editor.
2.  Navigate to:
    `User Configuration` > `Policies` > `Administrative Templates` > `System` > `Logon`
3.  Find and double-click the setting: **"Run these programs at user logon"**.
4.  Select **Enabled**.
5.  Click **Show...** and enter the following executable path:
    `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe`
6.  Click **OK** and **Apply**.

### 3. Linking the GPO
1.  Locate your target **Organizational Unit (OU)** (e.g., `USERS`).
2.  Right-click the OU and select **Link an Existing GPO**.
3.  Select `Auto-Start Edge Policy` and click **OK**.

---

## 🧪 Testing & Validation
To verify that the policy is working correctly on the Windows 10 client:

1.  **Force Update:** Open Command Prompt as Administrator and run:
    ```cmd
    gpupdate /force
    ```
2.  **Verify Application:** Run the following command to see if the policy is applied:
    ```cmd
    gpresult /r
    ```
3.  **User Experience:** Log out and log back in. Microsoft Edge should launch automatically upon reaching the desktop.

---

## 🔍 Common Challenges & Troubleshooting

| Issue | Potential Cause | Resolution |
| :--- | :--- | :--- |
| **GPO Not Applying** | Replication delay or link status. | Run `gpupdate /force` and ensure "Link Enabled" is checked in GPMC. |
| **Domain Connection** | Incorrect DNS configuration. | Ensure the client's DNS points directly to the DC IP. |
| **Path Errors** | Incorrect file path. | Verify the `msedge.exe` path exists on the local client disk. |
| **IP Conflict** | DHCP Scope overlap. | Check DHCP exclusions to ensure static IPs aren't being assigned to clients. |
| **VM Performance** | Resource exhaustion. | Adjust RAM allocation in VirtualBox settings for the Server and Client. |

---

## 🎓 Conclusion
This project demonstrates the efficiency of **centralized management**. By using Group Policy, administrators can ensure a uniform work environment, improve security, and reduce manual configuration time for every machine in the network.

---
*Developed by Silent Mucharira - January 2026*
