# Debug bridge

## Overview

The Debug Bridge application is a powerful tool designed to facilitate remote debugging, monitoring, and control of Lunar Hardware devices through the Android Debug Bridge protocol. This application is particularly useful for developers, administrators, and support teams who need to manage and troubleshoot Android devices remotely.

<figure><img src="broken-reference" alt=""><figcaption><p>The Debug Bridge application is a system application installed on Lunar Hardware devices. It allows admins to run shell commands remotely. The Debug Bridge application can be enabled by default, removing the need to physically enable it on devices. </p></figcaption></figure>

Operators can utilize the Debug Bridge services through the Lunar Control Center console. The connection with devices can be established as long as the device is connected to the internet.&#x20;

## Functionality

{% hint style="info" %}
The Debug Bridge application utilizes the Android Debug Bridge protocol, enabling all ADB functions to be executed remotely.&#x20;
{% endhint %}

<details>

<summary>Install applications</summary>

Remotely install applications on the device using a shell command. You can install or multiple applications with the same command.

</details>

<details>

<summary>Set up port forwarding</summary>

Set up arbitrary port forwarding, which forwards requests on a specific host port to a different port on a device.

This could be useful if you are trying to determine what is being sent to a given port on the device.

</details>

<details>

<summary>Copy files to and from a device</summary>

Copy files to and from a device. Unlike the install applications command, which only copies an APK file to a specific location, this functionality lets you copy arbitrary directories and files to any location in a device.

</details>

<details>

<summary>Trigger activity</summary>

Issue commands to perform various system actions, such as start an activity, force-stop a process, broadcast an intent, modify the device screen properties, and more.

</details>

<details>

<summary>Record a video</summary>

A shell utility for recording the display of devices. The utility records screen activity to an MPEG-4 file.&#x20;

</details>
