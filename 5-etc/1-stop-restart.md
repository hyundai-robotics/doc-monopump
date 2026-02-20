# 5.1 在密封器开启区域停止/重启

解释当机器人在密封器开启区域停止/重启时，单泵枪的行为。

![](../_assets/image30.png)

- 停止：执行回吸以防止在停止位置密封剂凝聚。
- 重启：在执行停止条件补充后，机器人开始移动以防止漏放。

{% hint style="info" %}
参考
- [3.2.3 停止/重启](../3-command-condition/2-condition/3-stop-restart.md)<br>
- 系统变量 ([_sealing.stop_seq_exe_offset_time](./4-system-var.md))
{% endhint %}