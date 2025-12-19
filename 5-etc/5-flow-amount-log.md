# 5.5 Check discharge amount history

You can check the history of discharge amounts from recorded log files.

- date_time: date and time when the log was recorded. <br>
- job: current program number. <br>
- step: current step number. <br>
- flow_amount: cumulative discharged amount from cycle start to stop. <br>

![](../_assets/image22.png)

![](../_assets/image23.png)

{% hint style="info" %}
- A new log file is created on the first record after powering on the controller.  
- Log files are created cyclically with filenames 0 ~ 9.
{% endhint %}