# 5.5 检查放电量历史

您可以从记录的日志文件中检查放电量的历史。

- date_time: 记录日志的日期和时间。 <br>
- job: 当前程序编号。 <br>
- step: 当前步骤编号。 <br>
- flow_amount: 从循环开始到停止的累计放电量。 <br>

![](../_assets/image22.png)

![](../_assets/image23.png)

{% hint style="info" %}
- 在控制器开机后的第一个记录上创建一个新的日志文件。  
- 日志文件以文件名 0 ~ 9 循环创建。
{% endhint %}