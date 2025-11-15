# LCC console (with all features)

## Overview

The Lunar Control Center Console serves as a centralized user interface for operators to efficiently manage and monitor devices remotely. The console acts as a single point of control, providing operators with a comprehensive set of tools and features to ensure seamless device management and real-time monitoring.

## Functionality

<details>

<summary>Create rules</summary>

Operators can access create, edit, and delete rules in the console using the [Rule Engine](broken-reference) functionality. In addition, operators can monitor the execution of rules through the logs.&#x20;

</details>

<details>

<summary>Account provisioning</summary>

Operators can create, suspend, or delete device accounts on demand.&#x20;

</details>

<details>

<summary>Management actions</summary>

Operators can remotely execute management actions on devices, including resetting device account passwords and wiping devices.&#x20;

</details>

<details>

<summary>Policy management</summary>

Operators can create, edit, or delete device policies which are then applied through the Policy Controller application. The policies can be managed on three levels: instance-wide (affecting all devices), group-wide (affecting a subset of devices), and specific devices (affecting a single device).

</details>

<details>

<summary>Kiosk lock management</summary>

Operators can create, edit, or delete Kiosk Lock policies which are then applied through the [Kiosk Lock](broken-reference) application.&#x20;

</details>

<details>

<summary>OTA updates</summary>

Operators manage OTA OS updates through the console, allowing them to initiate OTA updates to their fleet of devices.

</details>

<details>

<summary>Communication with devices</summary>

Operators can initiate communication with devices from the console through the [Space Link](broken-reference) application. Communication is recorded and available for audit.&#x20;

</details>

<details>

<summary>Management of app catalogue</summary>

Operators can manage app catalogs for their fleet of devices. The app catalogs can be created on three levels: instance-wide (affecting all devices), group-wide (affecting a subset of devices), and specific device (affecting a single device).

</details>

<details>

<summary>Device logs</summary>

Operators can access device logs individually for devices or aggregated in a report. The logs include network logs, action logs, and sensor logs.

</details>

<details>

<summary>Software integrity</summary>

The Lunar Control Center receives information about the local device settings through the [Policy Controller](broken-reference) application. The Software Integrity report feature compares the on-device settings with the policy configured on Lunar Control Center, including whether certain settings are enabled or disabled, and the software version the device is running on.&#x20;

Any discrepancies between configured policies and actual device settings trigger notification warnings, helping SOC teams identify any potential device security threats.&#x20;

</details>

<details>

<summary>Initiate remote ADB session</summary>

Operators can initiate remote ADB sessions from the Lunar Control Center console through the [Debug Bridge](broken-reference) application installed on devices.&#x20;

</details>

<details>

<summary>Initiate remote device control</summary>

Operators can initiate remote device control from the Lunar Control Center console through the [Mission Control](broken-reference) application installed on devices.&#x20;

</details>

<details>

<summary>Manage integrations</summary>

Administrators can set up integrations between LCC and third-party services through the console. More on the available integrations can be found in the [integrations article](broken-reference).&#x20;

</details>

<details>

<summary>LCC updates and rollback</summary>

The Console allows administrators to update the version of Lunr Control Center. Admins can decide to update to the latest version, or to a specific version. The update can be scheduled for a future date. Auto-update is available, allowing administrators to select an auto-update to the latest beta or production LCC version automatically when available.&#x20;

In addition, admins can roll back to a previous LCC version allowing them to revert in order to mitigate an issue caused by the latest update.&#x20;

</details>

<details>

<summary>Update integration modules</summary>

Administrators can set up integrations between LCC and third-party services through the console. More on the available integrations can be found in the [integrations article](broken-reference).&#x20;

</details>

<details>

<summary>Backup and restore</summary>

Operators can do a backup and restore for the following data:&#x20;

* Configurations: device, application, account, and software policies on personal, group, and default levels;
* Rule engine: automation rules;
* Settings: System settings, Notification settings, Retention policy settings, Branding;
* Device accounts: including account username, password, device UID, device S/N.

The backup can be either a full backup (all data is downloaded as a backup) or an incremental backup (only changes from the last backup event are downloaded as a backup). Backups can be triggered manually or scheduled for regular backups including daily backup, weekly backup and monthly backup.&#x20;

</details>
