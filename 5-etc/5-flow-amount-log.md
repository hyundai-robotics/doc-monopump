# 5.5 检查排放量历史

您可以查看记录日志文件中的排放量历史。

- date_time: 记录日志的日期和时间。 <br>
- job: 当前程序编号。 <br>
- step: 当前步骤编号。 <br>
- flow_amount: 从循环开始到停止的累计排放量。 <br>

![](../_assets/image22.png)

![](../_assets/image23.png)

{% hint style="info" %}
- 在控制器通电后第一次记录时，会创建新的日志文件。  
- 日志文件以文件名 0 ~ 9 循环创建。
{% endhint %}