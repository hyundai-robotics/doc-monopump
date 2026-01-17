# 3.2.1 Discharge start (m_sealer on)

Set discharge conditions for the m_sealer on command.

![](../../_assets/image12.png)

- Discharge mode: select constant, speed-proportional, or fixed-amount discharge modes. Speed-proportional automatically determines flow according to tool-tip speed.
- Discharge amount (fixed mode): set the discharge amount when fixed-amount mode is selected.
- <Speed-Flow table>: For speed-proportional mode, set the flow by tool-tip speed (mm/s). It can be configured in up to 5 segments. To set it, enable robot Lock and run an m_sealer on~off region in constant mode to measure discharge, then set the flow corresponding to the robot speed when the same discharge amount is observed.

  ![](../../_assets/image13.png)

  If you apply a strictly proportional relationship between robot speed and flow at low speeds, discharge may be missed at the start as shown below. <br>
  ![](../../_assets/image26.png)

  To compensate for insufficient discharge at the start, operate so that a certain minimum amount of discharge occurs even at low speeds of 0 ~ 50 mm/s as shown below. <br>
  ![](../../_assets/image24.png)