# Rule engine

## Overview

The Lunar Control Center Rule Engine is a powerful tool that enables the creation of customized workflows based on various triggers. This feature allows for the automation of device management tasks, enhancing efficiency and responsiveness. In addition, operators can set additional conditions for the rule.&#x20;

Rule engine logs are available for monitoring the execution of rules allowing teams to track and troubleshoot automation-related issues.&#x20;

Rules can be applied to one or more devices. The scope can be defined as:

* Single device, by providing it's account username
* Group of devices, identified by their visibility or permission group
* All devices of the instance
* A group of devices, identified by a rule group

### Triggers

{% hint style="info" %}
Triggers are what start the processing of an automation rule. Triggers can be an event or a specific device state.
{% endhint %}

<details>

<summary>Time triggers</summary>

Workflows can be scheduled to execute at a selected time. Including:

* every 1 hour
* once a day
* once a week
* once a month
* on a selected date and time

</details>

<details>

<summary>Policy triggers</summary>

Workflows can be scheduled to execute if a single or multiple device policies do not match actual device settings after sync.&#x20;

</details>

<details>

<summary>Network triggers</summary>

Workflows can be scheduled to execute based on network activity events, including:

* app or browsing data consumption exceeding a threshold
* device lost connectivity

</details>

<details>

<summary>Action triggers</summary>

Workflows can be scheduled to execute based on user activity events, including:

* a particular message is typed
* application usage time exceeds a threshold

</details>

<details>

<summary>Location triggers</summary>

Workflows can be scheduled to execute based on location-related events, including:

* the device has left a pre-set location perimeter
* the device has entered a pre-set location perimeter

</details>

<details>

<summary>Sensor triggers</summary>

Workflows can be scheduled to execute based on sensor values. The rule can be set to trigger if a certain sensor value goes above or under a set value.

</details>

<details>

<summary>Update triggers</summary>

Workflows can be scheduled to execute based on an update event, including successful or failed OS updates, and successful or failed application updates.

</details>

<details>

<summary>Enrollment triggers</summary>

Workflows can be scheduled to execute based on an enrollment event, including successful or failed device enrollment.

</details>

### Conditions

{% hint style="info" %}
Conditions are optional for automation rules. Setting conditions can prevent an automation action from executing unless certain conditions are met. Once the trigger event occurs, all conditions are getting checked. If true, the automation action is executed.&#x20;
{% endhint %}

<details>

<summary>Zone conditions</summary>

Zone conditions check if a device is in a certain zone. GPS enabled is required for the condition to work as designed.

</details>

<details>

<summary>Time conditions</summary>

The time condition checks if the time of trigger is at a specified time or day, or if it is after or before a specified time.

</details>

### Actions

{% hint style="info" %}
The action of an automation rule is what is being executed when a rule fires.
{% endhint %}

<details>

<summary>Device Notifications</summary>

Automated notifications can be sent to devices, including text notifications, rich notifications, voice notifications, and toast notifications.

</details>

<details>

<summary>Email Notifications</summary>

Automated email notifications can be sent to a list of email recipients. The notifications can include custom variables to describe the reason for the notification to the recipients.&#x20;

</details>

<details>

<summary>Management actions</summary>

Management actions can be automatically executed, including device wipe, device sleep mode, device turn on, and device reboot.&#x20;

</details>

<details>

<summary>Policy change</summary>

Automatically change the device(s) policy through the [Policy Controller applicaiton](broken-reference).

</details>

<details>

<summary>Network restriction</summary>

Includes DNS-based restrictions through URL whitelisting or blacklisting, preventing users of devices from surfing prohibited sites.

This action does not require a trigger. It can be set as a permanent rule.

</details>

<details>

<summary>App restriction</summary>

Restricts the use of specific applications. Applications can be selected by specifying the APK package name or choosing a category of applications (e.g. entertainment, social media, etc.)

</details>

<details>

<summary>Webhook</summary>

Facilitates communication with third-party applications by sending instant web notifications every time the trigger event occurs.

</details>



Created rules have one of 2 statuses:

* Draft - a rule that is not turned on. While it is saved, it will not execute;
* Live - a rule that is turned on and will execute when triggered.&#x20;
