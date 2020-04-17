# Mbed OS bare metal profile

There are many use cases for IoT devices. Different use cases require different configurations, connectivity and security. They also have different requirements for resource consumption. Many products must operate in ultraconstrained environments on tiny MCUs with low memory and compute power available. We created the Mbed OS bare metal profile for IoT devices that require ultraconstrained resources.

<span class="images">![Mbed OS bare metal profile block diagram](../../images/bare_metal_block_diagram.png)<span>Mbed OS bare metal profile block digram</span></span>

The Mbed OS bare metal profile is a compact profile of Mbed OS without an RTOS. The Mbed OS bare metal profile is API compatible with Mbed OS and supports a subset of Mbed OS features and components as listed below:

| Features/Components | Mbed OS bare metal  | Mbed OS |
| --- | ---  | --- |
| 802.15.4_RF | Not Available | Available |
| PSA | Not Available | Available |
| Wifi | Not Available | Available |
| Drivers | Available(except USBCDC_ECM) | Available |
| Events | Available | Available |
| Cellular | Not Available | Available |
| Cryptocell | Available | Available |
| Device key | Available | Available |
| BLE  | Available(except Nordic cordio target) | Available |
| Development tools<br> (For example, Mbed CLI, Mbed Studio, Mbed Online Compiler, GCC, Arm Compiler 6 and so on) | Available | Available |
| Lorawan | Available | Available |
| Lwipstack | Not Available | Available |
| Mbed TLS | Not Available | Available |
| Nonostack | Not Available | Available |
| Netsocket | Not Available | Available |
| NFC | Available | Available |
| Storage | Available | Available |
| HAL APIs | Available | Available |
| Platform APIs | Available | Available |
| RTOS | Not available | Available |
| RTOS APIs | Available | Available |

To begin using the Mbed OS bare metal profile from Mbed OS 2, please follow our [instructions](../tutorials/migrating-to-mbed-os-5.html).
