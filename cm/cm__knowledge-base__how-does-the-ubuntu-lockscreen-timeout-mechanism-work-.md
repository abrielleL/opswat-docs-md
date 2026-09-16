<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-does-the-ubuntu-lockscreen-timeout-mechanism-work- -->

# How does the Ubuntu Lockscreen Timeout Mechanism Work?

The lock screen timeout calculation mechanism for Ubuntu involves two key parameters: "Blank Screen Delay" and "Automatic Screen Lock Delay". These parameters determine the duration of user inactivity before the screen turns off without locking, and the subsequent duration before the user's session is automatically locked. The combined time of these two delays results in the overall lock screen timeout.

1. **Blank Screen Delay**: The "Blank Screen Delay" refers to the duration of time in which there are no user actions. During this period, the screen remains active and on, but without any user interaction. It represents the time interval before the screen turns off without locking the user session.
2. **Automatic Screen Lock Delay**: The "Automatic Screen Lock Delay" represents the time interval after the "Blank Screen Delay" has started. Once the "Blank Screen Delay" has passed, the system initiates the countdown for the "Automatic Screen Lock Delay". If the user remains inactive during this period, the system will automatically lock the user's session and require reauthentication.

**Calculation of Lock Screen Timeout**: The total lock screen timeout is calculated by summing up the "Blank Screen Delay" and the "Automatic Screen Lock Delay". The process can be summarized as follows:

Lock Screen Timeout = Blank Screen Delay + Automatic Screen Lock Delay

By adding these two durations together, the system determines how long the screen will remain active and unlocked before it turns off and locks the user's session.

This mechanism ensures that the system provides a balance between energy conservation (turning off the screen during periods of inactivity) and security (automatically locking the user session after extended periods of inactivity). The user has control over these parameters, allowing them to configure the screen timeout settings according to their preferences.

Overall, the lock screen timeout calculation mechanism in Ubuntu considers both the "Blank Screen Delay" and the "Automatic Screen Lock Delay" to determine the total duration of user inactivity before the screen is turned off and the session is locked. This approach helps maintain a secure yet user-friendly experience on the Ubuntu operating system.
