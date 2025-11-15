# Kiosk lock

## Overview

The Kiosk Lock app provides a robust set of tools for streamlined Android device management in Kiosk mode. This documentation is tailored to guide device administrators through the functionalities and security measures of the app, ensuring efficient day-to-day operations.

Administrators can leverage the Kiosk Lock app through Lunar Control Center serving as the interface for remote management.



<figure><img src="broken-reference" alt=""><figcaption><p>Lunar Control Center interacts with devices through the Kiosk Lock application installed on Lunar Hardware devices. It communicates through a set of APIs.</p></figcaption></figure>

Delivering the Kiosk Lock services involves the following components:&#x20;

* **Kiosk Lock app:** Android application optionally installed on Lunar Hardware with system application level privilege. It enforces Kiosk mode on devices. It also includes a user interface for on-site operators.
* **Kiosk Lock API:** a set of services provided to organizations to enable managing Kiosk Mode on devices.

Kiosk Mode does not rely on any third party infrastructure of services. It delivers its functionality through services hosted by the organization.

## Functionality

### Kiosk mode

Administrators can trigger entering in Kiosk mode remotely through Lunar Control Center. Exiting Kiosk mode can be initiated by the device administrator remotely via Lunar Control Center or by initiated by a device user through entering a Kiosk exit PIN in the Kiosk Lock app.

<details>

<summary><strong>Single App Mode</strong></summary>

In Single App Mode, administrators can lock devices to a specific application, restricting user access to only that application.&#x20;

**Use case:** Self-service kiosks, trade show displays, or public information points.

</details>

<details>

<summary><strong>Multi App Mode</strong></summary>

Multi-App Mode allows administrators to define a curated set of approved applications that users can access. This provides controlled flexibility while maintaining a restricted environment, ensuring only authorized applications are available.

**Use case:** Educational kiosk, Guest in-room entertainment.

</details>

### Device management

Administrators are able to control additional device settings when in Kiosk mode remotely. In addition, usage reports are available with insights on how users interact with the device.

<details>

<summary>Configuration Profiles</summary>

Admins can create and apply configuration profiles to devices in Kiosk mode, enabling the management of various settings including:

* restriction of notifications, status bar, and navigation bar
* scheduling turning off and on of Kiosk mode
* switching between portrait and landscape orientation
* disable sleep mode

</details>

<details>

<summary>Usage reports</summary>

Administrators can access detailed reports on device usage, including:

* Data usage - shows usage of wi-fi or mobile data;
* Location - shows last known location of the device;
* Kiosk mode duration - shows the duration in which the Kiosk mode has been active and any interuptions made by on-site operators.

The reports can be extracted for a specific date range.&#x20;

</details>

<details>

<summary>Kiosk Verification</summary>

To ensure that the device is used as intended, a verification flow is in place. If the user somehow manages to exit Kiosk mode, a verification flow will render the device useless, blocking it from further use.  &#x20;

</details>
