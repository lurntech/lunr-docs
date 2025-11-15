# Action logger

## Overview

The Action Logger application is a comprehensive monitoring tool designed to provide detailed insights into user interactions with the device. By collecting detailed activity logs, this application offers insights into how the device is used by the user. It is designed to help support teams with the tools to diagnose, analyze, and resolve connectivity-related issues efficiently.

<figure><img src="broken-reference" alt=""><figcaption><p>The Action Logger application is a system application installed on Lunar Hardware devices. It records activity on devices and shares them with the Lunar Control Center via API call.</p></figcaption></figure>

Delivering the Action Logger services involves the following components:&#x20;

* **Action Logger app:** Android application installed on Lunar Hardware with system application level privilege. The application doesn't have a user interface. It works in the background, ensuring that the device operations are not disturbed.&#x20;
* **Network Logger API:** a set of services provided to facilitate the collection of logs in the Lunar Control Center console.

## Functionality

{% hint style="info" %}
The Action Logger collects activity logs from user actions on the device.&#x20;
{% endhint %}

<details>

<summary>Key logger</summary>

The Key Logger functionality records each keystroke made on the device, capturing alphanumeric characters, special symbols, and function keys. Timestamps are associated with each keystroke, creating a chronological log of textual input.

**Purpose:** The Key Logger helps monitor and audit user input. It facilitates troubleshooting by providing a detailed record of all textual interactions within applications, aiding in the identification of specific actions and potential issues.

</details>

<details>

<summary>App acitivity logger</summary>

The App Activity Logger captures and logs the usage time of applications on the device. It records the start and end times of each application session, offering a comprehensive overview of how users interact with different applications.

**Purpose:** The App Activity Logger is designed to facilitate the monitoring and optimization of application usage. By tracking the duration of sessions, it helps administrators make informed decisions about device performance and usage preferences.

</details>
