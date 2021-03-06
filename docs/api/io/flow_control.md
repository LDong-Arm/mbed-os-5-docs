# Application flow control

We can use Blinky to explore flow control and task management in Arm Mbed OS applications. We'll look at automated actions first, then move on to handling user actions.

## Flow control for automated actions

If we want to automatically blink an LED, we have three main techniques:

1. [Wait](#wait)
1. [Ticker](#ticker)
1. [Thread](#thread)

### Wait

#### Busy wait

Busy wait is a method that blocks the processor for a period of time. This is an effective way to create time delays, but it is inefficient because it wastes processor time and keeps the processor running at full power for the duration of the wait:

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Busy-Wait)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Busy-Wait/main.cpp)

Notice `printf()`; you can enable this by uncommenting the line (remove the `//`). `printf()` prints to the terminal, so you can use it to get debug information.

<span class="tips">**Tip:** Busy wait is inefficient, and we recommend not using it. </span>

#### Suspend thread execution

A better alternative to busy wait is to suspend thread execution while waiting. Use:

 * For C++: The `ThisThread::sleep_for` API 
 * For C: The `thread_sleep_for` API.

### Ticker

Tickers and timers are another way of creating a time interval. These methods allow other code to run while you are waiting. During the wait period, if no threads are running, the idle thread can automatically put the system to sleep.

If you don't need the precision of a high-frequency timer or ticker, we recommend that you use LowPowerTimer or LowPowerTicker instead. This allows the system to be put in deep sleep mode.

Here is an example that uses a ticker object:

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Ticker)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Ticker/main.cpp)

<span class="tips">**Tip:** You may want to read the [power optimization](../tutorials/power-optimization.html) tutorial to understand how to achieve power savings. </span>

### Thread

If your application is running in RTOS mode then threads are another efficient way to blink an LED. During the waiting period, it is possible to take advantage of Mbed OS optimizations to automatically conserve power and deal with other tasks.

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Thread)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Thread/main.cpp)

## Flow control for manual actions

Let’s use a DigitalIn pin from the button to control the application. There are two ways to read input data: we can either constantly poll the button, or set an interrupt to trigger when pressed. We’ll explore these methods below.

### Active polling button

We can wait for digital input the same way we waited for time to pass - using a `while()` loop. In the example below the digital input is a button press, which causes the application to flash the LED and then wait for one second.

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Active-Polling-Button)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Active-Polling-Button/main.cpp)

We constantly poll the button to see whether it has a value that matches `BUTTON_PRESS`. If it matches, we toggle the LED and wait one second.

`BUTTON_PRESS` is used to denote what value the switch uses to represent the state *pushed*. Most switches are by default open (unpressed), so they will read as 0 while pressed. If you see your LED blinking without the button being pressed - try changing `BUTTON_PRESS` to `1`.

### Interrupt button

An alternative way to poll the button is to use an interrupt. Interrupts let you say `when that pin changes value, call this function`. In other words, we can tell the MCU to call a function when the button is pressed. In our case, that function toggles the LED:

[![View code](https://www.mbed.com/embed/?url=https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Interrupt-Button)](https://github.com/ARMmbed/mbed-os-examples-docs_only/blob/master/Tutorials_UsingAPIs/Flow-Control-Interrupt-Button/main.cpp)

In the code above a heartbeat function runs on LED2, which lets you see that your code is running. Then we connect an InterruptIn object to the button and set it so that when the button rises from 0 to 1, the toggle function is called; the function toggles LED1. This way the application can turn the LED on and off as needed, without needing to “waste” time waiting or actively polling an inactive button. The MCU is free to move on to other things .

Interrupt driven programming is one of the fundamental paradigms of microcontroller programming.
