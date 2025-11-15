# Sensor logger

## Overview

The Sensor Logger application is a tool designed to provide accurate data on device sensor metrics. By collecting accurate information from device sensors, this application helps support teams with troubleshooting and resolving device issues related to the device sensors.

<figure><img src="broken-reference" alt=""><figcaption><p>The Sensor Logger application is a system application installed on Lunar Hardware devices. It collects sensor values from devices and shares them with the Lunar Control Center via API call.</p></figcaption></figure>

Delivering the Sensor Logger services involves the following components:&#x20;

* **Sensor Logger app:** Android application installed on Lunar Hardware with system application level privilege. The application doesn't have a user interface. It works in the background, ensuring that the device operations are not disturbed.&#x20;
* **Sensor Logger API:** a set of services provided to facilitate the collection of logs in the Lunar Control Center console.

## Functionality

{% hint style="info" %}
The application's sole purpose is to collect sensor values from devices.&#x20;
{% endhint %}

<details>

<summary>Accelerometer sensor</summary>

Records the value of the accelerometer sensor used to measure the acceleration force in m/s2 that is applied to a device on all three physical axes (x, y, and z), including the force of gravity.

</details>

<details>

<summary>Ambient temperature sensor</summary>

Records the value of the ambient temperature sensor used to measure the ambient room temperature in degrees Celsius (°C).

</details>

<details>

<summary>Geomagnetic field sensor</summary>

Records the value of the geomagnetic field sensor used to measure the ambient geomagnetic field for all three physical axes (x, y, z) in μT.

</details>

<details>

<summary>Gravity sensor</summary>

Records the value of the gravity sensor used to measure the force of gravity in m/s2 that is applied to a device on all three physical axes (x, y, z).

</details>

<details>

<summary>Gyroscope sensor</summary>

Records the value of the gyroscope sensor used to measure a device's rate of rotation in rad/s around each of the three physical axes (x, y, and z).

</details>

<details>

<summary>Light sensor</summary>

Records the value of the light sensor used to measure the ambient light level (illumination) in lx.

</details>

<details>

<summary>Linear acceleration sensor</summary>

Records the value of the linear acceleration sensor used to measure the acceleration force in m/s2 that is applied to a device on all three physical axes (x, y, and z), excluding the force of gravity.

</details>

<details>

<summary>Orientation sensor</summary>

Records the value of the orientation sensor used to measure degrees of rotation that a device makes around all three physical axes (x, y, z).&#x20;

</details>

<details>

<summary>Pressure sensor</summary>

Records the value of the pressure sensor used to measure the ambient air pressure in hPa or mbar.

</details>

<details>

<summary>Relative humidity sensor</summary>

Records the value of the humidity sensor used to measure the relative ambient humidity in percent (%).

</details>

<details>

<summary>Temperature sensor</summary>

Records the value of the temperature sensor used to measure the temperature of the device in degrees Celsius (°C).

</details>
