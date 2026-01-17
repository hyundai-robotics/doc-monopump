# 3.1.1 Discharge start (m_sealer on)

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
| ot  | Use this to adjust command execution by a specified time before/after the robot reaches the target position; if not specified, executes immediately after target is reached (acc ok). If both od and ot are specified, od takes precedence (double)                                     | -0.5    |