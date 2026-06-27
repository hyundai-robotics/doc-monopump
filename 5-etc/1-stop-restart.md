# 5.1 在封口器开启区域的停止/重新启动

解释当机器人在封口器开启区域停止/重新启动时单泵枪的行为。

![](../_assets/image30.png)

- 停止：执行回吸以防止在停止位置封口器堵塞。
- 重新启动：机器人在执行停止条件的加注后开始移动，以防止漏排。

{% hint style="info" %}
参考
- [3.2.3 停止/重新启动](../3-command-condition/2-condition/3-stop-restart.md)<br>
- 系统变量 ([_sealing.stop_seq_exe_offset_time](./4-system-var.md))
{% endhint %}