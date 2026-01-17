# 3.1.2 Discharge stop (m_sealer off)

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
| ot  | Use this to adjust command execution by a specified time before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok). If both od and ot are specified, od takes precedence (double)                                     | -0.5    |