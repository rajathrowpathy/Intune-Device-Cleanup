Intune Device Cleanup Script
This PowerShell script helps identify and delete inactive Microsoft Intune-managed devices that also lack a User Principal Name (UPN). This is useful for maintaining a clean Intune environment by removing stale or improperly registered devices.

🚀 Features
Connects to Microsoft Graph API: Utilizes the Microsoft Graph PowerShell SDK to interact with your Intune tenant.

Filters Inactive Devices: Identifies devices that haven't synced since a specified date.

Filters Devices without UPN: Narrows down the list to devices where the UserPrincipalName property is empty or null.

Pre-Deletion Review: Displays a table of eligible devices before performing any deletion, allowing for review.

Confirmation Prompt: Requires explicit confirmation before proceeding with device deletion.

📋 Prerequisites
Before running this script, ensure you have the following:

PowerShell 5.1 or newer: This script is designed for Windows PowerShell or PowerShell Core.

Microsoft Graph PowerShell SDK: You need to install the Microsoft.Graph.DeviceManagement.Actions module.
If you don't have it, open PowerShell as an administrator and run:

Install-Module -Name Microsoft.Graph.DeviceManagement.Actions -Force

Sufficient Permissions: The account you use to run this script must have the necessary permissions in Azure AD/Intune. The script requests DeviceManagementManagedDevices.ReadWrite.All scope, which allows reading and deleting managed devices. Ensure your account has this permission assigned (e.g., through an Intune Administrator or Global Administrator role).

💡 How to Use
Save the Script: Save the provided PowerShell code to a .ps1 file (e.g., Clean-IntuneDevices.ps1).

Open PowerShell ISE (or your preferred PowerShell editor):

Right-click on the .ps1 file and choose "Edit with PowerShell ISE" or open PowerShell ISE and navigate to the file.

Review the Script Parameters:

lastSyncDateTime Filter: The script currently filters devices that haven't synced since 2025-06-28T00:00:00Z. You should modify this date to suit your cleanup policy. Devices older than this date and missing a UPN will be considered for deletion.

$devices = Get-MgDeviceManagementManagedDevice -Filter "lastSyncDateTime lt 2025-06-28T00:00:00Z" `

Important: The date format YYYY-MM-DDTHH:MM:SSZ is UTC (Coordinated Universal Time). Adjust it accordingly.

Run the Script:

Execute the script in your PowerShell session.

When prompted by Connect-MgGraph, you will need to sign in with an account that has the required permissions.

The script will then display a list of devices that meet the criteria.

Confirm Deletion:

After the list is displayed, the script will ask: Do you want to delete these devices? (yes/no)

Carefully review the list.

Type yes and press Enter to proceed with the deletion.

Type no and press Enter to cancel the deletion.

⚠️ Important Notes
Irreversible Action: Deleting devices from Intune is an irreversible action. Once a device is deleted, it will no longer be managed by Intune, and its associated data (e.g., compliance status, installed apps) will be removed.

Test First: It is highly recommended to test this script in a non-production or test environment first to understand its behavior and impact.

Backup: Consider having a backup or a clear understanding of your device enrollment and management strategy before running cleanup scripts in production.

Permissions: Always follow the principle of least privilege. Ensure the account used has only the necessary permissions and nothing more.

Script Review: Always review any script from an external source before running it in your environment.
