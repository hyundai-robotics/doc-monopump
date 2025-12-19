# 5.6 Job program composition

A job program layout to better match the start and stop timing of discharge when using a monopump gun. <br>

If you use a commonly used job layout, the start/stop points often miss or the discharged amount may be insufficient, as shown below. <br>

![](../_assets/image27.png)

As a method to compensate for the above phenomenon, record the step before and after discharge at the same position, set accu to 0 for the post-discharge step and set accu to 1 for the pre-discharge step. Then use ot or od in the m_sealer on command to adjust the timing of command execution.

![](../_assets/image25.png)

Use the same method to structure commands at the discharge stop point.