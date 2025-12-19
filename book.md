# ${cont_model} Robot Controller Function Manual - Monopump Sealer Gun

{% hint style="warning" %}
The information provided in this product manual is the property of HD Hyundai Robotics.

No part of this manual may be reproduced or redistributed without HD Hyundai Robotics' written consent, nor may it be provided to third parties or used for other purposes.

This manual is subject to change without prior notice.


**Copyright ⓒ 2025 by HD Hyundai Robotics**
{% endhint %}# 1. 개요

# 1.1 Preliminary information

To understand this manual, the following prior knowledge is required.

1. **Knowledge of operating the ${cont_model} robot controller**
2. **Understanding of the operation principle of a monopump gun**# 1.2 Monopump system


### <mark style="color:green;">1. Complete system configuration </mark>

    The following figure shows the overall system configuration. The monopump gun can be directly controlled by the robot controller.

![](../_assets/image18.png)

### <mark style="color:green;">2. Monopump gun components</mark>

    The following figure shows the composition of the monopump gun. It consists of a servo motor, rotor, and stator.

![](../_assets/image19.png)# 2. 기본 설정

# 2.1 Additional axis parameter settings

When controlling the sealer gun directly as an additional axis of the robot, set the axis type to <Sealer>. Because the monopump gun's discharge amount (cc/s) is determined by the motor speed (rpm), you must control the axis speed. Therefore, set the axis configuration to <Speed control>.

![](../_assets/image1.png)


- If the motor is directly coupled without a gearbox, set the reduction ratio to 360:1. This means one motor revolution corresponds to 360° of the mechanism. If a gearbox exists, set the gearbox reduction ratio and set the sign of the ratio according to the discharge direction. <br>

![](../_assets/image28.png)

- The acceleration time parameter determines the time to reach maximum speed, and the deceleration time determines the time from maximum speed to stop. If these values are large for the monopump gun, the response for discharge start/stop and suck-back/refill will be delayed, making it difficult to achieve the desired quality. <br>
Therefore, set these values as small as possible to increase operating speed.# 2.2 Sealer gun data settings

Go to [System] -> [4: Application Parameters] -> [20: Sealing] -> [1: Sealer Gun Settings].
Set the gun type and additional axis for each sealer gun. You can add a gun with the "+" button and remove one with the "-" button.

![](../_assets/image2.png)

- Gun type: set to Monopump gun.
- Additional axis: set the axis number for the gun.

Detailed gun settings are available via the [Properties] button.# 2.3 Monopump gun setup# 2.3.1 General

General settings related to the monopump gun.

![](../../_assets/image3.png)

- Manufacturer: select the monopump gun manufacturer.
- Discharge unit: choose the unit used for the discharge interface.
- Specific gravity: set the specific gravity of the sealer material.
- Sealer command execution mode: The m_sealer on/off commands in the job program execute discharge. If <Discharge off> is selected, the job program runs without performing actual discharge.# 2.3.2 Flow rate tuning

Set the discharge rate (cc/s) according to the monopump gun motor speed (rpm). It can be configured in up to 6 segments.<br>
The flow rate is determined by measuring the amount discharged at a specified speed for a specified time on a scale and calculated as: "measured value (g) * specific gravity / time." 

![](../../_assets/image4.png)


Use the [Start manual discharge] button to run the monopump gun motor at the specified speed for the set time.

![](../../_assets/image5.png)


The following figure shows the status during manual discharge execution.

![](../../_assets/image6.png)


Use the [Stop manual discharge] button to forcibly stop manual discharge.

![](../../_assets/image7.png)


Use the [Initialize] button to set the flow rate initial values based on the amount per one motor revolution.

![](../../_assets/image8.png)# 2.3.3 Input signal assignment

Settings for signals input to the robot controller related to the monopump gun.

![](../../_assets/image9.png)

The [Auto assign] button can automatically set signals based on the selected sealer manufacturer. <br>
    ![](../../_assets/image9_1.png)

- Sealer command execution mode: The m_sealer on/off commands in the job program perform discharge. However, if the configured signal is ON, the job program will run without performing actual discharge. <br> 
- Communication status: Check communication status with the sealer control panel. The sealer control panel should toggle the signal ON/OFF every second. <br>
The robot controller raises the error "E6319 Sealing equipment communication error" if the signal does not change state for more than 1 second. <br>
- Other signals: Check the state of the sealer control panel. If you want the robot controller to detect these states and raise errors or warnings, use the user-defined error/warning function. <br>
![](../../_assets/image9_2.png)

- Pressure sensor: Set information for pressure sensor input. <br>
	- Spec (min ~ max): set the minimum and maximum specification values for the pressure sensor. <br>
	- Communication (min ~ max): set the min and max values when the pressure sensor delivers data via communication. <br>
	- Signal assignment: assign the input signal for the pressure sensor. <br>
	- Assigned bit count: set the bit count used for the pressure sensor signal. <br>
	- Interface variable: set the variable for interfacing the calculated pressure value. Here, the calculated pressure value from current input is assigned to _mf4 memory. <br>

       ![](../../_assets/image10.png)# 2.3.4 Output signal assignment

Settings for signals output from the robot controller related to the monopump gun.

![](../../_assets/image10_5.png)

The [Auto assign] button can automatically set signals based on the selected sealer manufacturer. <br>
![](../../_assets/image9_1.png)

- Sealer command execution mode: The m_sealer on/off commands in the job program perform discharge. However, depending on user settings or input signal states, the job program may run without performing actual discharge. This output indicates whether actual discharge is being performed. <br> 
- Discharging: The monopump gun outputs whether it is currently discharging. <br>
- Error reset: Output used to reset the sealer control panel in case of an error. R1 (error reset) operation or "Error/Alarm signal clear" input causes a 1-second ON pulse output for reset. <br>
- Other signals: Use these to send sealer panel states via output signals in robot language. <br># 3. Commands and sealer conditions

Describes commands and sealer condition settings related to sealing operations.# 3.1 Commands

Let's look at the job program commands related to the monopump gun. Usually discharge is performed between m_sealer on and m_sealer off.


{% hint style="info" %}
When executing the m_sealer command in manual mode, the command is treated as completed but actual operation is not performed.
{% endhint %}


![](../../_assets/image11.png)# 3.1.1 Discharge start (m_sealer on)

This command starts monopump gun discharge and operates only in automatic mode. The format is as follows.

#### <mark style="color:green;">Command format</mark>
```
m_sealer on,gun=1,cnd=1,flow=0.5,od=_,ot=_
```

#### <mark style="color:green;">Parameters</mark>

|Parameter| Description                                                                                                    |    Example    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| on   | <p>Starts discharge for the gun according to the sealer condition (cnd) (str)</p>   | "on" |
| gun  | <p>Specifies the gun number to start discharge (int)</p>              |  1   |
| cnd  | Condition number for discharge (int)                                     | 1    |
| flow   | <p>Depending on the sealer condition's mode (constant, speed-proportional, fixed amount), behaves as follows (double)</p><ul><li>Constant: discharges at the rate (cc/s) specified by flow, regardless of robot speed</li><li>Speed-proportional: discharges proportionally to tool-tip speed. The cc/s per mm/s is configured in the sealer condition. If flow is not specified, uses the configured discharge rate; if flow is 1.3, outputs 1.3 times the configured rate</li><li>Fixed amount: discharges the specified amount and then stops; the amount is set in sealer condition (see sealer conditions) <br>  - If both od and ot are not specified: discharges the full amount specified in the command then performs off-condition actions<br>  - If od and ot are specified: performs subsequent commands while discharging the specified amount and then performs off-condition actions</li></ul>                                         | 1.3 |
| od  | Use this to adjust command execution by a specified distance before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok) (double)                                     | -0.5    |
| ot  | Use this to adjust command execution by a specified time before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok). If both od and ot are specified, od takes precedence (double)                                     | -0.5    |# 3.1.2 Discharge stop (m_sealer off)

This command stops monopump gun discharge. The format is as follows. <br>
The off command works in manual mode as well. <br>

#### <mark style="color:green;">Command format</mark>
```
m_sealer off,gun=1,cnd=1,od=_,ot=_
```

#### <mark style="color:green;">Parameters</mark>

|Parameter| Description                                                                                                    |    Example    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| off   | <p>Stops discharge for the gun according to the sealer condition (cnd) (str)</p>      | "off" |
| gun  | <p>Specifies the gun number to stop discharge (int)</p>                  |  1   |
| cnd  | Condition number for stopping discharge (int). When stopping, suck-back is performed first, followed by refill. The suck-back flow rate (cc/s) and time and the refill flow rate (cc/s) and time are set in the sealer condition (see sealer conditions) (int)                                          | 1    |
| od  | Use this to adjust command execution by a specified distance before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok) (double)                                     | -0.5    |
| ot  | Use this to adjust command execution by a specified time before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok). If both od and ot are specified, od takes precedence (double)                                     | -0.5    |# 3.2 Sealer conditions

Sealer conditions are set via the [Properties] button in the m_sealer on/off commands. You can add conditions with the "+" button and remove them with the "-" button. Up to 8 conditions are currently supported.# 3.2.1 Discharge start (m_sealer on)

Set discharge conditions for the m_sealer on command.

![](../../_assets/image12.png)

- Discharge mode: select constant, speed-proportional, or fixed-amount discharge modes. Speed-proportional automatically determines flow according to tool-tip speed.
- Discharge amount (fixed mode): set the discharge amount when fixed-amount mode is selected.
- <Speed-Flow table>: For speed-proportional mode, set the flow by tool-tip speed (mm/s). It can be configured in up to 5 segments. To set it, enable robot Lock and run an m_sealer on~off region in constant mode to measure discharge, then set the flow corresponding to the robot speed when the same discharge amount is observed.

  ![](../../_assets/image13.png)

  If you apply a strictly proportional relationship between robot speed and flow at low speeds, discharge may be missed at the start as shown below. <br>
  ![](../../_assets/image26.png)

  To compensate for insufficient discharge at the start, operate so that a certain minimum amount of discharge occurs even at low speeds of 0 ~ 50 mm/s as shown below. <br>
  ![](../../_assets/image24.png)# 3.2.2 Discharge stop (m_sealer off)

When executing m_sealer off, set the conditions for suck-back and refill. Suck-back removes residual material after discharge, and refill fills the nozzle after suck-back.

![](../../_assets/image14.png)

- Suck-back flow rate: set the flow rate for suck-back.
- Suck-back time: set the suck-back duration.
- Delay time: set the wait time between suck-back and refill.
- Refill flow rate: set the flow rate for refill.
- Refill time: set the duration for refill.# 3.2.3 Stop/restart

Set the conditions for suck-back and refill when the robot stops (stop or emergency stop) and restarts. <br>
On stop, perform suck-back to prevent sealer clumping at the stop position. <br>
On restart, the robot starts moving after refill to prevent missed discharge. 

![](../../_assets/image29.png)

<Stop>
- Suck-back flow rate: set the flow rate for suck-back.
- Suck-back time: set the suck-back duration.

<Restart>
- Refill flow rate: set the refill flow rate.
- Refill time: set the refill duration.# 4. Monitoring# 4.1 Sealing status

Describes the monitoring window for checking sealer status. Select Sealing Status in [Window Settings].

![](../_assets/image15.png)

![](../_assets/image16.png)

- Flow rate: shows the current discharge flow rate.
- RPM command: RPM command corresponding to the flow rate.
- RPM actual: shows the current RPM of the sealer motor.
- Pressure: shows the pressure value from the pressure sensor.
- Discharged amount: shows the amount measured since discharge start.# 5. Miscellaneous# 5.1 Stop/Restart in sealer ON region

Explains monopump gun behavior when the robot stops/restarts in a sealer ON region.

![](../_assets/image30.png)

- Stop: perform suck-back for the stop condition to prevent sealer clumping at the stop position.
- Restart: the robot starts moving after performing the stop-condition refill to prevent missed discharge.


{% hint style="info" %}
Reference
- [3.2.3 Stop/restart](../3-command-condition/2-condition/3-stop-restart.md)<br>
- System variables ([_sealing.stop_seq_exe_offset_time](./4-system-var.md))
{% endhint %}# 5.2 Manual operation (R371)

You can manually operate the monopump gun from the screen shown when performing [R371: Sealer manual operation].

- Flow rate: set the flow rate for manual operation. <br>
- Discharge amount: set the discharge amount for fixed-amount discharge. <br>

![](../_assets/image20.png)
![](../_assets/image21.png)

- Constant discharge <br>
 Starts discharge at the set flow rate. Use the [Stop discharge] button to stop discharge. <br>
- Fixed-amount discharge  <br>
 Starts discharge at the set flow rate and automatically stops when the set amount is reached. You can forcibly stop discharge using the [Stop discharge] button. <br>
- Stop discharge <br>
 Use this to stop discharge. <br>

{% hint style="info" %}
When stopping discharge, actions according to the suck-back and refill conditions set in the [off] tab are always performed.
{% endhint %}# 5.3 License key registration

A license key for the "Sealing option feature" is required to use this function. Please contact us.

![](../_assets/image17.png)# 5.4 System variables

*   <mark style="color:green;">**_sealing.flow_amount**</mark>

    ### Description
        Used to obtain the measured discharged amount since discharge start.

    ### Usage example
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
    S8 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
       print _sealing.flow_amount
       if abs(_sealing.flow_amount - 6) > 1 then
           print "Discharged amount is outside the specified range."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.flow_amount_cycle**</mark>

    ### Description
        Used to obtain the measured discharged amount for one cycle from start to stop.

    ### Usage example
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S74 move L,spd=100mm/sec,accu=1,tool=1
    S75 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
       print _sealing.flow_amount_cycle
       if abs(_sealing.flow_amount_cycle - 32) > 3 then
           print "1-cycle discharged amount is outside the specified range."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.stop_seq_exe_offset_time**</mark>

    ### Description
        This is used to adjust the timing of the suck-back action when stopping (default 0.1 [sec]).

    ### Usage example
    ```python
       _sealing.stop_seq_exe_offset_time=-0.2 #adjust suck-back timing on stop
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
    ```
    <br>
    <br># 5.5 Check discharge amount history

You can check the history of discharge amounts from recorded log files.

- date_time: date and time when the log was recorded. <br>
- job: current program number. <br>
- step: current step number. <br>
- flow_amount: cumulative discharged amount from cycle start to stop. <br>

![](../_assets/image22.png)

![](../_assets/image23.png)

{% hint style="info" %}
- A new log file is created on the first record after powering on the controller.  
- Log files are created cyclically with filenames 0 ~ 9.
{% endhint %}# 5.6 Job program composition

A job program layout to better match the start and stop timing of discharge when using a monopump gun. <br>

If you use a commonly used job layout, the start/stop points often miss or the discharged amount may be insufficient, as shown below. <br>

![](../_assets/image27.png)

As a method to compensate for the above phenomenon, record the step before and after discharge at the same position, set accu to 0 for the post-discharge step and set accu to 1 for the pre-discharge step. Then use ot or od in the m_sealer on command to adjust the timing of command execution.

![](../_assets/image25.png)

Use the same method to structure commands at the discharge stop point.