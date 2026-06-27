
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 单泵封闭枪
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}
[__SOURCE](1-intro/README.md)
# 1. 概述
[__SOURCE](1-intro/1-preparatory-information.md)
# 1.1 初步信息

要理解本手册，需要以下先决知识。

1. **操作 ${cont_model} 机器人控制器的知识**
2. **单泵枪的操作原理理解**
[__SOURCE](1-intro/2-monopump-func.md)
# 1.2 单泵系统


### <mark style="color:green;">1. 完整系统配置</mark>

    以下图显示了整体系统配置。单泵枪可以由机器人控制器直接控制。

![](../_assets/image18.png)

### <mark style="color:green;">2. 单泵枪组件</mark>

    以下图显示了单泵枪的组成。它由伺服电机、转子和定子组成。

![](../_assets/image19.png)
[__SOURCE](2-basic-setting/README.md)
# 2. 基本设置
[__SOURCE](2-basic-setting/1-add-axis-parameter.md)
# 2.1 附加轴参数设置

当直接控制封口枪作为机器人的附加轴时，将轴类型设置为 <Sealer>。由于单泵枪的排放量 (cc/s) 是由电机转速 (rpm) 决定的，因此必须控制轴速度。因此，将轴配置设置为 <Speed control>。

![](../_assets/image1.png)

- 如果电机是直接耦合而没有减速器，请将减速比设置为 360:1。这意味着一圈电机转动对应于机制的 360°。如果存在减速器，请设置减速器减速比，并根据排放方向设置比率的符号。 <br>

![](../_assets/image28.png)

- 加速度时间参数决定达到最大速度所需的时间，而减速度时间决定从最大速度到停止所需的时间。如果这些值对单泵枪来说很大，排放的开始/停止和回吸/补充的响应将会延迟，从而使实现所需的质量变得困难。 <br>
因此，请将这些值设置得尽可能小，以提高操作速度。
[__SOURCE](2-basic-setting/2-sealer-gun-setting.md)
# 2.2 密封枪数据设置

转到 [System] -> [4: Application Parameters] -> [20: Sealing] -> [1: Sealer Gun Settings]。
设置每个密封枪的枪类型和附加轴。您可以使用 "+" 按钮添加枪，使用 "-" 按钮删除枪。

![](../_assets/image2.png)

- 枪类型：设置为单泵枪。
- 附加轴：为枪设置轴编号。

详细的枪设置可以通过 [Properties] 按钮获得。
[__SOURCE](2-basic-setting/3-monopump-setup/README.md)
# 2.3 单泵枪设置
[__SOURCE](2-basic-setting/3-monopump-setup/1-general.md)
# 2.3.1 一般

与单泵枪相关的一般设置。

![](../../_assets/image3.png)

- 制造商: 选择单泵枪制造商。
- 排放单元: 选择用于排放接口的单位。
- 比重: 设置密封材料的比重。
- 密封命令执行模式: 作业程序中的 m_sealer 开/关命令执行排放。如果选择 <Discharge off>，作业程序将运行而不执行实际排放。
[__SOURCE](2-basic-setting/3-monopump-setup/2-flow-rate-tunning.md)
# 2.3.2 流量调节

根据单泵枪电机速度 (rpm) 设置排放速率 (cc/s)。它可以配置为最多 6 个段。<br>
流量是通过在指定速度下在天平上测量指定时间排放的量来确定的，计算公式为：“测量值 (g) * 比重 / 时间。”

![](../../_assets/image4.png)

使用 [开始手动排放] 按钮以指定速度运行单泵枪电机，持续设定时间。

![](../../_assets/image5.png)

下图显示了手动排放执行期间的状态。

![](../../_assets/image6.png)

使用 [停止手动排放] 按钮强制停止手动排放。

![](../../_assets/image7.png)

使用 [初始化] 按钮根据每次电机转动的排放量设置流量初始值。

![](../../_assets/image8.png)
[__SOURCE](2-basic-setting/3-monopump-setup/3-input-signal-assign.md)
# 2.3.3 输入信号分配

与单泵枪相关的输入信号设置到机器人控制器。

![](../../_assets/image9.png)

[Auto assign] 按钮可以根据选择的密封剂制造商自动设置信号。 <br>
    ![](../../_assets/image9_1.png)

- 密封命令执行模式：作业程序中的 m_sealer 开/关命令执行放电。然而，如果配置的信号为 ON，作业程序将在不执行实际放电的情况下运行。 <br> 
- 通信状态：检查与密封控制面板的通信状态。密封控制面板应每秒切换信号 ON/OFF。 <br>
如果信号超过 2 秒未改变状态，机器人控制器将报错 "E6319 密封设备通信错误"。 <br>
- 其他信号：检查密封控制面板的状态。如果希望机器人控制器检测这些状态并引发错误或警告，请使用用户定义的错误/警告功能。 <br>
![](../../_assets/image9_2.png)

- 压力传感器：设置压力传感器输入的信息。 <br>
	- 规格（最小 ~ 最大）：设置压力传感器的最小和最大规格值。 <br>
	- 通信（最小 ~ 最大）：设置压力传感器通过通信传送数据时的最小和最大值。 <br>
	- 信号分配：分配压力传感器的输入信号。 <br>
	- 分配的位数：设置用于压力传感器信号的位数。 <br>
	- 接口变量：设置用于接口计算压力值的变量。在这里，当前输入的计算压力值分配给 _mf4 内存。 <br>

       ![](../../_assets/image10.png)
[__SOURCE](2-basic-setting/3-monopump-setup/4-output-signal-assign.md)
# 2.3.4 输出信号分配

与单泵枪相关的来自机器人控制器的信号输出设置。

![](../../_assets/image10_5.png)

[Auto assign] 按钮可以根据选择的封口机制造商自动设置信号。 <br>
![](../../_assets/image9_1.png)

- 封口机命令执行模式：作业程序中的 m_sealer 开/关命令执行放电。然而，根据用户设置或输入信号状态，作业程序可能在不执行实际放电的情况下运行。此输出指示是否正在执行实际放电。 <br> 
- 放电：单泵枪输出其当前是否正在放电。 <br>
- 错误重置：在发生错误时用于重置封口机控制面板的输出。R1（错误重置）操作或“错误/警报信号清除”输入会导致 1 秒的 ON 脉冲输出以进行重置。 <br>
- 其他信号：使用这些信号通过机器人语言发送封口机面板状态。 <br>
[__SOURCE](3-command-condition/README.md)
# 3. 命令和密封条件

描述与密封操作相关的命令和密封条件设置。
[__SOURCE](3-command-condition/1-command/README.md)
# 3.1 命令

让我们来看看与单泵枪相关的作业程序命令。通常在 m_sealer 开启和 m_sealer 关闭之间进行放电。


{% hint style="info" %}
在手动模式下执行 m_sealer 命令时，该命令被视为已完成，但实际操作未执行。
{% endhint %}


![](../../_assets/image11.png)
[__SOURCE](3-command-condition/1-command/1-msealer-on.md)
# 3.1.1 放电启动 (m_sealer 开)

此命令启动单泵枪放电，并仅在自动模式下操作。格式如下。

#### <mark style="color:green;">命令格式</mark>
```
m_sealer on,gun=1,cnd=1,flow=0.5,od=_,ot=_
```

#### <mark style="color:green;">参数</mark>

|参数| 描述                                                                                                    |    示例    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| on   | <p>根据密封条件 (cnd) 启动枪的放电 (str)</p>   | "on" |
| gun  | <p>指定要启动放电的枪号 (int)</p>              |  1   |
| cnd  | 放电条件编号 (int)                                     | 1    |
| flow   | <p>根据密封条件的模式 (恒定、速度比例、固定量) 表现如下 (double)</p><ul><li>恒定: 以 flow 指定的速率 (cc/s) 放电，无论机器人速度如何</li><li>速度比例: 与工具尖端速度成比例放电。每 mm/s 的 cc/s 在密封条件中配置。如果未指定 flow，则使用配置的放电速率；如果 flow 是 1.3，则输出 1.3 倍的配置速率</li><li>固定量: 放电指定数量后停止；数量在密封条件中设置 (见密封条件) <br>  - 如果 od 和 ot 均未指定: 放电命令中指定的全部量，然后执行离开条件操作<br>  - 如果 od 和 ot 被指定: 在放电指定数量的同时执行后续命令，然后执行离开条件操作</li></ul>                                         | 1.3 |
| od  | 用于在机器人到达目标位置之前/之后调整命令执行的指定距离；如果未指定，则在到达目标后立即执行 (acc ok) (double)                                     | -0.5    |
| ot  | 用于在机器人到达目标位置之前/之后调整命令执行的指定时间；如果未指定，则在到达目标后立即执行 (acc ok)。如果同时指定 od 和 ot，则以 od 为先 (double)                                     | -0.5    |
[__SOURCE](3-command-condition/1-command/2-msealer-off.md)
# 3.1.2 放料停止 (m_sealer off)

此命令停止单泵枪放料。格式如下。 <br>
关闭命令在手动模式下也有效。 <br>

#### <mark style="color:green;">命令格式</mark>
```
m_sealer off,gun=1,cnd=1,od=_,ot=_
```

#### <mark style="color:green;">参数</mark>

|参数| 描述                                                                                                    |    示例    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| off   | <p>根据封口机条件 (cnd) 停止枪的放料 (str)</p>      | "off" |
| gun  | <p>指定要停止放料的枪编号 (int)</p>                  |  1   |
| cnd  | 停止放料的条件编号 (int)。停止时，首先进行回吸，然后再补充。回吸流量 (cc/s) 和时间以及补充流量 (cc/s) 和时间在封口机条件中设置 (见封口机条件) (int)                                          | 1    |
| od  | 用于在机器人到达目标位置之前/之后按指定距离调整命令执行；如果未指定，则在到达目标后立即执行 (acc ok) (double)                                     | -0.5    |
| ot  | 用于在机器人到达目标位置之前/之后按指定时间调整命令执行；如果未指定，则在到达目标后立即执行 (acc ok)。如果同时指定了 od 和 ot，则优先执行 od (double)                                     | -0.5    |
[__SOURCE](3-command-condition/2-condition/README.md)
# 3.2 封闭剂条件

封闭剂条件通过 m_sealer 的 [Properties] 按钮进行设置。您可以使用 "+" 按钮添加条件，使用 "-" 按钮删除条件。目前支持最多 8 个条件。
[__SOURCE](3-command-condition/2-condition/1-msealer-on.md)
# 3.2.1 排放开始 (m_sealer 开启)

设置 m_sealer 开启命令的排放条件。

![](../../_assets/image12.png)

- 排放模式：选择恒定、速度比例或固定量排放模式。速度比例模式根据工具尖速度自动确定流量。
- 排放量（固定模式）：在选择固定量模式时设置排放量。
- <速度-流量表>: 对于速度比例模式，按工具尖速度 (mm/s) 设置流量。最多可配置 5 个段。要设置它，请启用机器人锁并在恒定模式下运行 m_sealer 开启~关闭区域进行排放测量，然后在观察到相同排放量时设置与机器人速度对应的流量。

  ![](../../_assets/image13.png)

  如果在低速下对机器人速度和流量应用严格的比例关系，排放在开始时可能会漏掉，如下所示。 <br>
  ![](../../_assets/image26.png)

  为补偿起始时排放不足，操作时应确保即使在 0 ~ 50 mm/s 的低速下也发生一定的最小排放量，如下所示。 <br>
  ![](../../_assets/image24.png)
[__SOURCE](3-command-condition/2-condition/2-msealer-off.md)
# 3.2.2 放电停止 (m_sealer off)

当执行 m_sealer off 时，设置回吸和补充的条件。回吸在放电后去除残留材料，补充在回吸后填充喷嘴。

![](../../_assets/image14.png)

- 回吸流量：设置回吸的流量。
- 回吸时间：设置回吸的持续时间。
- 延迟时间：设置回吸与补充之间的等待时间。
- 补充流量：设置补充的流量。
- 补充时间：设置补充的持续时间。
[__SOURCE](3-command-condition/2-condition/3-stop-restart.md)
# 3.2.3 停止/重新启动

设置机器人停止（停止或紧急停止）和重新启动时的回吸和补充的条件。 <br>
在停止时，执行回吸以防止在停止位置密封剂聚集。 <br>
在重新启动时，机器人在补充后开始移动，以防止漏放。

![](../../_assets/image29.png)

<Stop>
- 回吸流量: 设置回吸的流量。
- 回吸时间: 设置回吸的持续时间。

<Restart>
- 补充流量: 设置补充的流量。
- 补充时间: 设置补充的持续时间。
[__SOURCE](4-monitoring/README.md)
# 4. 监控
[__SOURCE](4-monitoring/1-sealing-status.md)
# 4.1 密封状态

描述用于检查密封器状态的监控窗口。在[窗口设置]中选择密封状态。

![](../_assets/image15.png)

![](../_assets/image16.png)

- 流量：显示当前放电流量。
- RPM命令：与流量对应的RPM命令。
- 实际RPM：显示密封器电机的当前RPM。
- 压力：显示来自压力传感器的压力值。
- 放电量：显示自放电开始以来测量的量。
[__SOURCE](5-etc/README.md)
# 5. 杂项
[__SOURCE](5-etc/1-stop-restart.md)
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
[__SOURCE](5-etc/2-manual-oper.md)
# 5.2 手动操作 (R371)

您可以从执行 [R371: 密封剂手动操作] 时显示的屏幕手动操作单泵枪。

- 流量：设置手动操作的流量。 <br>
- 排放量：设置定量排放的排放量。 <br>

![](../_assets/image20.png)
![](../_assets/image21.png)

- 恒定排放 <br>
以设置的流量开始排放。使用 [停止排放] 按钮停止排放。 <br>
- 定量排放 <br>
以设置的流量开始排放，并在达到设置的数量时自动停止。您可以使用 [停止排放] 按钮强制停止排放。 <br>
- 停止排放 <br>
用于停止排放。 <br>

{% hint style="info" %}
停止排放时，始终根据 [off] 选项卡中设置的回吸和补充条件执行操作。
{% endhint %}
[__SOURCE](5-etc/3-license-key.md)
# 5.3 许可密钥注册

要使用此功能，需要“密封选项功能”的许可密钥。请联系我们。

![](../_assets/image17.png)
[__SOURCE](5-etc/4-system-var.md)
# 5.4 系统变量

*   <mark style="color:green;">**_sealing.flow_amount**</mark>

    ### 描述
        用于获取自放电开始以来测量的放电量。

    ### 使用示例
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #放电开始
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
    S8 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #放电停止
       print _sealing.flow_amount
       if abs(_sealing.flow_amount - 6) > 1 then
           print "放电量超出指定范围。"
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.flow_amount_cycle**</mark>

    ### 描述
        用于获取从开始到停止的一个周期内测量的放电量。

    ### 使用示例
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #放电开始
    S74 move L,spd=100mm/sec,accu=1,tool=1
    S75 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #放电停止
       print _sealing.flow_amount_cycle
       if abs(_sealing.flow_amount_cycle - 32) > 3 then
           print "1周期放电量超出指定范围。"
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.stop_seq_exe_offset_time**</mark>

    ### 描述
        这用于调整停止时的回吸动作时机（默认 0.1 [秒]）。

    ### 使用示例
    ```python
       _sealing.stop_seq_exe_offset_time=-0.2 #调整停止时的回吸时机
       m_sealer on,gun=1,cnd=1,flow=0.6 #放电开始
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #放电停止
    ```
    <br>
    <br>
[__SOURCE](5-etc/5-flow-amount-log.md)
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
[__SOURCE](5-etc/6-job-composition.md)
# 5.6 作业程序组成

作业程序布局，以便更好地匹配使用单泵枪时的放电开始和停止时机。 <br>

如果使用常见的作业布局，开始/停止点往往会错过，或者放电的量可能不足，如下所示。 <br>

![](../_assets/image27.png)

作为补偿上述现象的方法，在放电前后记录同一位置的步骤，为放电后步骤设置 accu 为 0，为放电前步骤设置 accu 为 1。然后在 m_sealer 的命令中使用 ot 或 od 来调整命令执行的时机。

![](../_assets/image25.png)

在放电停止点采用相同的方法结构命令。