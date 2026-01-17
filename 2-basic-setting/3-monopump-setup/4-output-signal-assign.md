# 2.3.4 Output signal assignment

Settings for signals output from the robot controller related to the monopump gun.

![](../../_assets/image10_5.png)

The [Auto assign] button can automatically set signals based on the selected sealer manufacturer. <br>
![](../../_assets/image9_1.png)

- Sealer command execution mode: The m_sealer on/off commands in the job program perform discharge. However, depending on user settings or input signal states, the job program may run without performing actual discharge. This output indicates whether actual discharge is being performed. <br> 
- Discharging: The monopump gun outputs whether it is currently discharging. <br>
- Error reset: Output used to reset the sealer control panel in case of an error. R1 (error reset) operation or "Error/Alarm signal clear" input causes a 1-second ON pulse output for reset. <br>
- Other signals: Use these to send sealer panel states via output signals in robot language. <br>