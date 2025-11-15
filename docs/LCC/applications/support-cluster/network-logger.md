# Network logger

## Overview

The Network Logger application is a critical tool for support teams, enabling them to troubleshoot network connectivity issues on Lunar Hardware devices remotely. By collecting detailed connectivity logs, this application offers vital insights into the device's network behavior. It is designed to help support professionals with the tools to diagnose, analyze, and resolve connectivity-related issues efficiently.

<figure><img src="broken-reference" alt=""><figcaption><p>The Network Logger application is a system application installed on Lunar Hardware devices. It fetches network logs from devices and shares them with the Lunar Control Center via API call.</p></figcaption></figure>

Delivering the Network Logger services involves the following components:&#x20;

* **Network Logger app:** Android application installed on Lunar Hardware with system application level privilege. The application doesn't have a user interface. It works in the background, ensuring that the device operations are not disturbed.&#x20;
* **Network Logger API:** a set of services provided to facilitate the collection of logs in the Lunar Control Center console.

## Functionality

### Network activity logs

{% hint style="info" %}
The Network Activity Logs functionality enhances the Network Logger by capturing detailed events from applications utilizing the Android network libraries. It focuses on two primary types of events: DNS lookups and Network connections.
{% endhint %}

<details>

<summary>DNS Lookup</summary>

Network Logger records an event for DNS lookups that are part of system network requests. The logs capture each DNS request that resolves a hostname to an IP address.

**Purpose:** Facilitate analysis of DNS-related issues, aiding support teams in understanding application behavior and potential network configuration problems.

</details>

<details>

<summary>Network connections</summary>

Logs every network connection established by applications, encompassing both incoming and outgoing connections. Includes data such as source and destination addresses, connection type (e.g., TCP, UDP), timestamp, and connection duration.

**Purpose:** Provide support teams with insights into the network interactions of applications, aiding in diagnosing connectivity issues and ensuring network security.

</details>

### Connectivity logs

{% hint style="info" %}
Network Logger records each connection to various networks, including Wi-Fi networks and tower connectivity for mobile networks.
{% endhint %}

<details>

<summary>Wi-fi Connectivity</summary>

Logs events related to Wi-Fi network connections, including connection establishment, disconnection, and changes between different Wi-Fi networks. Includes Wi-Fi network name (SSID), connection status, signal strength, and timestamps.

**Purpose:** Helps with analysis of connectivity-related issues when connected to Wi-Fi.

</details>

<details>

<summary>Cellular Connectivity</summary>

Records tower connectivity events, tracking the device's connection to cellular towers for mobile network data.

Includes device APN, SIM number, tower ID, signal strength, connection status, and timestamps.

**Purpose**_**:**_ Assists support teams in troubleshooting mobile network-related issues.

</details>

### Data consumption logs

{% hint style="info" %}
The Network Logger records the data consumed by device applications. This includes system applications, third-party applications, and data consumed in browsing sessions.
{% endhint %}

<details>

<summary>App consumption</summary>

The application logs data consumption events initiated by applications. Includes data usage statistics, timestamps, and application identifiers.

_**Purpose:**_ Enable analysis of data consumption patterns for applications.

</details>

<details>

<summary>Browsing consumption</summary>

The application logs data consumption events while online surfing. Includes data usage statistics, timestamps, and website identifiers.

_**Purpose:**_ Enable analysis of data consumption patterns when browsing.

</details>
