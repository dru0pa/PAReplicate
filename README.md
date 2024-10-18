# CyberArk Vault Replication Scheduled Task Configuration

This PowerShell script automates the creation and configuration of a scheduled task for CyberArk Vault replication on Windows servers.

## Features

* **Creates a local user:** Creates a local user account named "CyberArk-Backup" with the specified password (or resets the password if the user already exists).
* **Adds to Administrators group:** Adds the "CyberArk-Backup" user to the local Administrators group.
* **Creates a scheduled task:** Creates a scheduled task named "CyberArk Vault Replication" to run `PAReplicate.exe` with the specified arguments.
* **Schedules daily execution:** Sets the task to run daily at 2:00 AM.
* **Configures task settings:**
    * Allows the task to run on battery power.
    * Prevents the task from being stopped if the computer switches to battery power.
    * Allows multiple instances of the task to run in parallel.
* **Runs as SYSTEM:** Configures the task to run under the SYSTEM account.
* **Sets working directory:** Sets the working directory for the task to `C:\Program Files (x86)\PrivateArk\Replicate`.
* **Enables domain credential storage:** Sets the registry value `disabledomaincreds` to 0 to allow domain credentials to be stored.

## Requirements

* PowerShell: The script requires PowerShell to be installed on the target Windows server.
* Administrator Privileges: The script must be executed with administrator privileges.

## Usage

1.  Save the script: Save the script as a `.ps1` file (e.g., `Configure-CyberArkVaultReplication.ps1`).
2.  Run the script: Execute the script from an elevated PowerShell prompt:

    ```powershell
    .\Configure-CyberArkVaultReplication.ps1
    ```

3.  **Manual Configuration:** After running the script, manually edit the scheduled task to:

    *   Set the "Start in (optional)" field to `C:\Program Files (x86)\PrivateArk\Replicate`.
    *   Change the user to "CyberArk-Backup" and provide the password you entered when prompted by the script.

## Security Considerations

*   **Password Handling:** In production environments, avoid hardcoding passwords or prompting for them in plain text. Use secure methods like fetching the password from a secure vault or using a credential object.
*   **Least Privilege:** Evaluate if the task requires the high privileges of the SYSTEM account or if it can be run under a less privileged account.
*   **Error Handling:** Consider adding error handling (e.g., `try...catch` blocks) to gracefully handle potential issues.

## Disclaimer

This script is provided as-is. Use it at your own risk. It is recommended to thoroughly test the script in a non-production environment before deploying it to production servers.

## Contributing

Contributions are welcome! Feel free to submit pull requests or open issues for any bugs or feature requests.

## License

This script is licensed under the MIT License.
