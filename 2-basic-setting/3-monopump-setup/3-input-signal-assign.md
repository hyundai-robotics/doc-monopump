# 2.3.3 Input signal assignment

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

       ![](../../_assets/image10.png)