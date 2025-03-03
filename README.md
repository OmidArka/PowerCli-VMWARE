Install-Module VMware.PowerCLI -Scope AllUsers -Force -SkipPublisherCheck -AllowClobber
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Import-Module VMware.VimAutomation.Core -Verbose
Set-PowerCLIConfiguration -InvalidCertificateAction Ignore
connect-viserver -server <Vcenter IP | ESXI IP>


# PowerCLI Installation Guide for Windows

## Introduction
PowerCLI is a command-line tool for managing VMware environments using PowerShell. This guide provides step-by-step instructions for installing PowerCLI on **Windows**.

---

## Prerequisites
Before installing PowerCLI, ensure you meet the following requirements:

- **Windows OS**: Windows 10/11 or Windows Server 2016/2019/2022  
- **PowerShell Version**: PowerShell 5.1 or later (preferably PowerShell 7)  
- **Internet Access**: Required to download PowerCLI modules  
- **Administrative Privileges**: Required for system-wide installation  

---

## Step 1: Check PowerShell Version
To check your PowerShell version, open PowerShell and run:

```powershell
$PSVersionTable.PSVersion
```

- If your version is **5.1 or later**, proceed to the next step.  
- If not, download and install the latest version of [PowerShell](https://aka.ms/powershell-release?tag=stable).

---

## Step 2: Install PowerCLI
### **Using PowerShell Gallery (Recommended)**
PowerCLI is available as a module from the PowerShell Gallery. To install it, open PowerShell as **Administrator** and run:

```powershell
Install-Module -Name VMware.PowerCLI -Scope CurrentUser -AllowClobber -Force
```

- `-Scope CurrentUser` installs the module for the current user only.  
- `-AllowClobber` allows overwriting existing versions.  
- `-Force` automatically accepts installation prompts.  

> 💡 To install system-wide, use `-Scope AllUsers` (Requires Admin Privileges).

---

## Step 3: Verify Installation
To verify that PowerCLI is installed correctly, run:

```powershell
Get-Module -Name VMware.PowerCLI -ListAvailable
```

If the module appears in the list, the installation was successful.

---

## Step 4: Set Execution Policy
PowerCLI scripts require an appropriate execution policy. Set it to `RemoteSigned` using:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

> ⚠️ **Security Note:** Setting the execution policy to `RemoteSigned` allows local scripts to run while requiring remote scripts to be signed.

---

## Step 5: Import the PowerCLI Module
To start using PowerCLI, import the module into your PowerShell session:

```powershell
Import-Module VMware.PowerCLI
```

To check the installed version, run:

```powershell
Get-PowerCLIVersion
```

---

## Step 6: Disable SSL Certificate Warnings (Optional)
By default, PowerCLI may show SSL certificate warnings. To disable them, run:

```powershell
Set-PowerCLIConfiguration -InvalidCertificateAction Ignore -Confirm:$false
```

---

## Step 7: Connect to vCenter or ESXi
To connect to a VMware environment, use:

```powershell
Connect-VIServer -Server <vCenter-Hostname> -User <Username> -Password <Password>
```

Example:

```powershell
Connect-VIServer -Server vcenter.example.com -User admin -Password "P@ssw0rd!"
```

---

## Updating PowerCLI
To update PowerCLI to the latest version, run:

```powershell
Update-Module -Name VMware.PowerCLI -Scope CurrentUser -Force
```

---

## Uninstalling PowerCLI
If you need to remove PowerCLI, run:

```powershell
Uninstall-Module -Name VMware.PowerCLI
```

---

## Troubleshooting
### **1. Execution Policy Error**
If you encounter an execution policy error, try:

```powershell
Set-ExecutionPolicy Unrestricted -Scope CurrentUser -Force
```

### **2. PowerCLI Command Not Found**
Ensure the module is installed by running:

```powershell
Get-Module -Name VMware.PowerCLI -ListAvailable
```

If not found, reinstall it.

### **3. Connection Issues to vCenter**
If you cannot connect to vCenter, ensure:
- The **vCenter hostname/IP** is correct.  
- Your **username and password** are correct.  
- Your network allows access to **vCenter (port 443)**.  

---

## Conclusion
You have successfully installed **PowerCLI on Windows**. Now, you can automate VMware tasks efficiently.  

For more advanced usage, refer to the official [VMware PowerCLI Documentation](https://developer.vmware.com/powercli).
