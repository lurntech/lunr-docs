# Space Link

## Overview

The Space Link application serves as a communication bridge between support agents and devices, offering a range of features to enhance remote support and interaction. Designed to facilitate seamless communication, this application enables support agents to send messages in both voice and text format to devices.

<figure><img src="broken-reference" alt=""><figcaption><p>The Space Link application is a system application installed on Lunar Hardware devices. It allows Lunar Control Center operators to communicate seamlessly with devices. </p></figcaption></figure>

Space Link empowers support teams to deliver timely and personalized support, troubleshoot issues effectively, and maintain a seamless communication channel with users.&#x20;

## Functionality

<details>

<summary>Notifications</summary>

Allows sending of text notifications to the device in the form of a notification. Notifications pop on the screen and stay in the notification panel until acknowledged. The notifications can include text, special symbols, emojis, and website links and rich notifications such as a choice-form (single and multi-choice)

As an extension to the function, Lunar Control Center operators can see whether the notification has been acknowledged by the device user.&#x20;

**Purpose:** Communicate urgent updates or announcements to users in text format.

</details>

<details>

<summary>Voice recording</summary>

Allows sending playing a voice recording on the device. The voice recording appears in the notification panel of the user, allowing them to play the voice recording.&#x20;

As an extension to the function, Lunar Control Center operators can see whether the voice recording has been played.&#x20;

**Purpose:** Communicate urgent updates or announcements to users in voice format.

</details>

<details>

<summary>Intercommunication</summary>

Allows initiation of a 2-way VoIP communication between the Lunar Control Center console and the Lunar Hardware device. Lunar Control Center operators can force the intercommunication to start or prompt the device user to accept the initiated call. In addition, the device camera can be enabled during the call to provide live visual feed.

Initiated calls are recorded and available to be replayed from the Lunar Control Center.

**Purpose:** Troubleshoot issues in real time through verbal communication with the device user.

</details>



{% hint style="info" %}
Space Link functionalities require the installation of third-party services including [Openfire](broken-reference), [Kamalio](broken-reference), and [RTPEngine](broken-reference).
{% endhint %}
