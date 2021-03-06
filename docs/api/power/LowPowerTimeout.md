# LowPowerTimeout

<span class="images">![](https://os.mbed.com/docs/development/mbed-os-api-doxy/classmbed_1_1_low_power_timeout.png)<span>LowPowerTimeout class hierarchy</span></span>

Use the LowPowerTimeout interface to set up an interrupt to call a function after a specified delay. You can create any number of LowPowerTimeout objects. This allows multiple outstanding interrupts at the same time. For more information about power management, please see our [power management APIs](power-management-sleep.html).

## Notes

- No blocking code in ISR: Avoid any call to wait, infinite while loop or blocking calls in general.
- No printf, malloc or new in ISR: Avoid any call to bulky library functions. In particular, certain library functions (such as printf, malloc and new) are not re-entrant, and their behavior could be corrupted when called from an ISR.

## LowPowerTimeout class reference

[![View code](https://www.mbed.com/embed/?type=library)](https://os.mbed.com/docs/development/mbed-os-api-doxy/classmbed_1_1_low_power_timeout.html)

## LowPowerTimeout example

Set up a time out to invert an LED after a given time:

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/APIs_Drivers/lowpowerTimeout_ex_1/)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/APIs_Drivers/lowpowerTimeout_ex_1/main.cpp)

## Related content

- [Power management APIs](power-management-sleep.html).
