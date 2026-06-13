
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 单泵密封枪
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

要理解本手册，需要以下先前知识。

1. **操作 ${cont_model} 机器人控制器的知识**
2. **对单泵枪操作原理的理解**
[__SOURCE](1-intro/2-monopump-func.md)
# 1.2 单泵系统

### <mark style="color:green;">1. 完整的系统配置</mark>

    下图显示了整体系统配置。单泵枪可以直接由机器人控制器控制。

![](../_assets/image18.png)

### <mark style="color:green;">2. 单泵枪组件</mark>

    下图显示了单泵枪的组成。它由伺服电机、转子和定子组成。

![](../_assets/image19.png)
[__SOURCE](2-basic-setting/README.md)
# 2. 基本设置
[__SOURCE](2-basic-setting/1-add-axis-parameter.md)
# 2.1 额外轴参数设置

当直接将封闭枪作为机器人的额外轴进行控制时，将轴类型设置为 <Sealer>。由于单泵枪的排出量（cc/s）由电机速度（rpm）决定，因此必须控制轴速度。因此，将轴配置设置为 <Speed control>。

![](../_assets/image1.png)

- 如果电机直接与无齿轮减速器耦合，则将减速比设置为 360:1。这意味着一个电机旋转对应于机制的 360°。如果存在减速器，则设置减速器减速比，并根据排出方向设置比率的符号。 <br>

![](../_assets/image28.png)

- 加速时间参数决定达到最大速度的时间，而减速时间决定从最大速度到停止的时间。如果这些值对于单泵枪来说过大，排出启动/停止以及回吸/补充的响应将会延迟，从而使实现所需质量变得困难。 <br>
因此，将这些值设置得尽可能小以提高操作速度。
[__SOURCE](2-basic-setting/2-sealer-gun-setting.md)
# 2.2 密封枪数据设置

前往 [System] -> [4: Application Parameters] -> [20: Sealing] -> [1: Sealer Gun Settings]。
为每个密封枪设置枪类型和附加轴。您可以通过 "+" 按钮添加枪，使用 "-" 按钮移除。

![](../_assets/image2.png)

- 枪类型：设置为单泵枪。
- 附加轴：为枪设置轴编号。

详细的枪设置可以通过 [Properties] 按钮访问。
[__SOURCE](2-basic-setting/3-monopump-setup/README.md)
# 2.3 单泵枪设置
[__SOURCE](2-basic-setting/3-monopump-setup/1-general.md)
# 2.3.1 一般

与单泵枪相关的一般设置。

![](../../_assets/image3.png)

- 制造商：选择单泵枪制造商。
- 排放单元：选择用于排放接口的单元。
- 比重：设定密封材料的比重。
- 密封命令执行模式：作业程序中的 m_sealer 开/关命令执行排放。如果选择了 <排放关闭>，作业程序将在不执行实际排放的情况下运行。
[__SOURCE](2-basic-setting/3-monopump-setup/2-flow-rate-tunning.md)
# 2.3.2 流量调节

根据单泵枪电机速度（rpm）设置排放速率（cc/s）。它可以配置为最多6个段落。<br>
流量通过在指定速度下、在指定时间内在称量秤上测量排放量来确定，计算方式为：“测得值（g）* 比重 / 时间。”

![](../../_assets/image4.png)

使用 [启动手动排放] 按钮以指定速度运行单泵枪电机，持续设定时间。

![](../../_assets/image5.png)

下图显示了手动排放执行期间的状态。

![](../../_assets/image6.png)

使用 [停止手动排放] 按钮强制停止手动排放。

![](../../_assets/image7.png)

使用 [初始化] 按钮根据每次电机旋转的数量设置流量初始值。

![](../../_assets/image8.png)
[__SOURCE](2-basic-setting/3-monopump-setup/3-input-signal-assign.md)
# 2.3.3 输入信号分配

与单泵枪相关的输入信号设置。

![](../../_assets/image9.png)

[自动分配] 按钮可以根据所选的密封剂制造商自动设置信号。 <br>
![](../../_assets/image9_1.png)

- 密封剂命令执行模式：作业程序中的 m_sealer 开/关命令执行排放。然而，如果配置的信号为 ON，则作业程序将运行而不执行实际排放。 <br>
- 通信状态：检查与密封剂控制面板的通信状态。密封剂控制面板应每秒切换信号 ON/OFF。 <br>
如果信号超过 2 秒未改变状态，机器人控制器将抛出错误 "E6319 密封设备通信错误"。 <br>
- 其他信号：检查密封剂控制面板的状态。如果您希望机器人控制器检测这些状态并抛出错误或警告，请使用用户定义的错误/警告功能。 <br>
![](../../_assets/image9_2.png)

- 压力传感器：设置压力传感器输入的信息。 <br>
	- 规格 (最小 ~ 最大)：设置压力传感器的最小和最大规格值。 <br>
	- 通信 (最小 ~ 最大)：设置当压力传感器通过通信传输数据时的最小和最大值。 <br>
	- 信号分配：分配压力传感器的输入信号。 <br>
	- 分配比特计数：设置用于压力传感器信号的比特计数。 <br>
	- 接口变量：设置用于接口计算的压力值的变量。在这里，来自当前输入的计算压力值被分配给 _mf4 内存。 <br>

       ![](../../_assets/image10.png)
[__SOURCE](2-basic-setting/3-monopump-setup/4-output-signal-assign.md)
# 2.3.4 输出信号分配

与单泵枪相关的机器人控制器输出信号设置。

![](../../_assets/image10_5.png)

[自动分配]按钮可以根据选择的封闭器制造商自动设置信号。 <br>
![](../../_assets/image9_1.png)

- 封闭器命令执行模式：工作程序中的m_sealer开/关命令执行排放。然而，根据用户设置或输入信号状态，工作程序可能会在不执行实际排放的情况下运行。此输出指示是否正在执行实际排放。 <br> 
- 正在排放：单泵枪输出当前是否正在排放。 <br>
- 错误复位：在发生错误时用于重置封闭器控制面板的输出。R1（错误复位）操作或“错误/警报信号清除”输入会导致1秒的ON脉冲输出以进行复位。 <br>
- 其他信号：使用这些信号通过机器人语言发送封闭器面板状态的输出信号。 <br>
[__SOURCE](3-command-condition/README.md)
# 3. 命令和密封条件

描述与密封操作相关的命令和密封条件设置。
[__SOURCE](3-command-condition/1-command/README.md)
# 3.1 命令

让我们看看与单泵枪相关的作业程序命令。通常，放电在 m_sealer 打开和 m_sealer 关闭之间进行。


{% hint style="info" %}
在手动模式下执行 m_sealer 命令时，该命令被视为已完成，但实际操作并不会执行。
{% endhint %}


![](../../_assets/image11.png)
[__SOURCE](3-command-condition/1-command/1-msealer-on.md)
# 3.1.1 放电开始 (m_sealer on)

该命令启动单泵枪放电，仅在自动模式下操作。格式如下。

#### <mark style="color:green;">命令格式</mark>
```
m_sealer on,gun=1,cnd=1,flow=0.5,od=_,ot=_
```

#### <mark style="color:green;">参数</mark>

|参数| 描述                                                                                                    |    示例    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| on   | <p>根据密封条件 (cnd) 启动枪的放电 (str)</p>   | "on" |
| gun  | <p>指定要启动放电的枪的编号 (int)</p>              |  1   |
| cnd  | 放电的条件编号 (int)                                     | 1    |
| flow   | <p>根据密封条件的模式 (恒定、速度成比例、固定数量) 按如下方式操作 (double)</p><ul><li>恒定：以 flow 指定的速率 (cc/s) 放电，无论机器人速度如何</li><li>速度成比例：根据工具尖端速度成比例放电。每 mm/s 的 cc/s 在密封条件中配置。如果未指定 flow，则使用配置的放电速率；如果 flow 为 1.3，则输出配置速率的 1.3 倍</li><li>固定数量：放电指定的数量后停止；数量在密封条件中设置（参见密封条件） <br>  - 如果未指定 od 和 ot：放电在命令中指定的全部数量，然后执行关闭条件操作<br>  - 如果指定了 od 和 ot：在放电指定数量的同时执行后续命令，然后执行关闭条件操作</li></ul>                                         | 1.3 |
| od  | 用于在机器人到达目标位置之前/之后按指定距离调整命令执行；如果未指定，则在目标达到后立即执行 (acc ok) (double)                                     | -0.5    |
| ot  | 用于在机器人到达目标位置之前/之后按指定时间调整命令执行；如果未指定，则在目标达到后立即执行 (acc ok)。如果同时指定了 od 和 ot，则以 od 为准 (double)                                     | -0.5    |
[__SOURCE](3-command-condition/1-command/2-msealer-off.md)
# 3.1.2 停止排放 (m_sealer off)

该命令停止单泵枪排放。格式如下。 <br>
停用命令在手动模式下也有效。 <br>

#### <mark style="color:green;">命令格式</mark>
```
m_sealer off,gun=1,cnd=1,od=_,ot=_
```

#### <mark style="color:green;">参数</mark>

|参数| 描述                                                                                                            |    示例    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| off   | <p>根据密封条件 (cnd) 停止枪的排放 (str)</p>      | "off" |
| gun  | <p>指定要停止排放的枪的编号 (int)</p>                  |  1   |
| cnd  | 停止排放的条件编号 (int)。停止时首先执行回吸，然后进行补充。回吸流量 (cc/s) 和时间以及补充流量 (cc/s) 和时间在密封条件中设置 (请参阅密封条件) (int)                                          | 1    |
| od  | 用于在机器人到达目标位置之前/之后按指定距离调整命令执行；如果未指定，在达到目标后立即执行 (acc ok) (double)                                     | -0.5    |
| ot  | 用于在机器人到达目标位置之前/之后按指定时间调整命令执行；如果未指定，在达到目标后立即执行 (acc ok)。如果同时指定 od 和 ot，则以 od 为准 (double)                                     | -0.5    |
[__SOURCE](3-command-condition/2-condition/README.md)
# 3.2 密封剂条件

密封剂条件通过 m_sealer 的 [Properties] 按钮设置。您可以使用 "+" 按钮添加条件，并使用 "-" 按钮删除条件。目前支持最多 8 个条件。
[__SOURCE](3-command-condition/2-condition/1-msealer-on.md)
# 3.2.1 排放启动 (m_sealer 开)

设置 m_sealer 开命令的排放条件。

![](../../_assets/image12.png)

- 排放模式：选择恒定、速度比例或固定量排放模式。速度比例会根据工具尖端速度自动确定流量。
- 排放量（固定模式）：选择固定量模式时设置排放量。
- <速度-流量表>: 对于速度比例模式，根据工具尖端速度（mm/s）设置流量。最多可配置 5 个段。要设置它，请启用机器人锁定并以恒定模式运行 m_sealer 开~关区域以测量排放，然后设置与观察到的相同排放量对应的机器人速度的流量。

  ![](../../_assets/image13.png)

  如果在低速度下应用机器人速度与流量之间严格的比例关系，启动时可能会错过排放，如下所示。 <br>
  ![](../../_assets/image26.png)

  为了补偿起始时排放不足，请操作以使在低速 0 ~ 50 mm/s 时也会发生一定的最小排放量，如下所示。 <br>
  ![](../../_assets/image24.png)
[__SOURCE](3-command-condition/2-condition/2-msealer-off.md)
# 3.2.2 排放停止 (m_sealer 关闭)

执行 m_sealer 关闭时，设置回吸和补充的条件。回吸在排放后去除残留材料，补充则在回吸后填充喷嘴。

![](../../_assets/image14.png)

- 回吸流量：设置回吸的流量。
- 回吸时间：设置回吸的持续时间。
- 延迟时间：设置回吸和补充之间的等待时间。
- 补充流量：设置补充的流量。
- 补充时间：设置补充的持续时间。
[__SOURCE](3-command-condition/2-condition/3-stop-restart.md)
# 3.2.3 停止/重新启动

设置机器人停止（停止或紧急停止）和重新启动时的回吸和补充的条件。 <br>
在停止时，执行回吸以防止密封剂在停止位置凝聚。 <br>
在重新启动时，机器人在补充后开始移动，以防止错过排放。 

![](../../_assets/image29.png)

<Stop>
- 回吸流速：设置回吸流速。
- 回吸时间：设置回吸持续时间。

<Restart>
- 补充流速：设置补充流速。
- 补充时间：设置补充持续时间。
[__SOURCE](4-monitoring/README.md)
# 4. 监控
[__SOURCE](4-monitoring/1-sealing-status.md)
# 4.1 密封状态

描述用于检查密封器状态的监控窗口。在[窗口设置]中选择密封状态。

![](../_assets/image15.png)

![](../_assets/image16.png)

- 流量：显示当前的放电流量。
- RPM命令：与流量对应的RPM命令。
- 实际RPM：显示密封器电机的当前RPM。
- 压力：显示来自压力传感器的压力值。
- 放电量：显示自放电开始以来测量的量。
[__SOURCE](5-etc/README.md)
# 5. 其他
[__SOURCE](5-etc/1-stop-restart.md)
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
[__SOURCE](5-etc/2-manual-oper.md)
# 5.2 手动操作 (R371)

您可以从执行 [R371: 密封剂手动操作] 时显示的屏幕手动操作单泵枪。

- 流量：设置手动操作的流量。 <br>
- 放电量：设置固定放电的放电量。 <br>

![](../_assets/image20.png)
![](../_assets/image21.png)

- 恒定放电 <br>
以设置的流量开始放电。使用 [停止放电] 按钮停止放电。 <br>
- 固定放电 <br>
以设置的流量开始放电，当达到设置的放电量时自动停止。您可以使用 [停止放电] 按钮强行停止放电。 <br>
- 停止放电 <br>
使用此按钮停止放电。 <br>

{% hint style="info" %}
停止放电时，将始终根据 [关闭] 选项卡中设置的回吸和补充条件执行操作。
{% endhint %}
[__SOURCE](5-etc/3-license-key.md)
# 5.3 许可证密钥注册

使用“密封选项功能”需要许可证密钥。请与我们联系。

![](../_assets/image17.png)
[__SOURCE](5-etc/4-system-var.md)
# 5.4 系统变量

*   <mark style="color:green;">**_sealing.flow_amount**</mark>

    ### 描述
        用于获取自排放开始以来测量的排放量。

    ### 用例示例
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #排放开始
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
    S8 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #排放停止
       print _sealing.flow_amount
       if abs(_sealing.flow_amount - 6) > 1 then
           print "排放量超出规定范围。"
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.flow_amount_cycle**</mark>

    ### 描述
        用于获取从开始到停止的一个周期内测量的排放量。

    ### 用例示例
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #排放开始
    S74 move L,spd=100mm/sec,accu=1,tool=1
    S75 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #排放停止
       print _sealing.flow_amount_cycle
       if abs(_sealing.flow_amount_cycle - 32) > 3 then
           print "1周期排放量超出规定范围。"
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.stop_seq_exe_offset_time**</mark>

    ### 描述
        用于调整停止时回吸动作的时机（默认 0.1 [秒]）。
### 使用示例
    ```python
       _sealing.stop_seq_exe_offset_time=-0.2 #调整停止时的回吸时机
       m_sealer on,gun=1,cnd=1,flow=0.6 #排放开始
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #排放停止
    ```
    <br>
    <br>
[__SOURCE](5-etc/5-flow-amount-log.md)
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
[__SOURCE](5-etc/6-job-composition.md)
# 5.6 作业程序组成

作业程序布局以更好地匹配使用单泵枪时放电的开始和停止时机。 <br>

如果使用常用的作业布局，开始/停止点通常会错过，或放电量可能不足，如下所示。 <br>

![](../_assets/image27.png)

作为补偿上述现象的方法，在放电前后记录相同位置的步骤，将放电后步骤的 accu 设置为 0，将放电前步骤的 accu 设置为 1。然后在 m_sealer 上命令中使用 ot 或 od 来调整命令执行的时机。

![](../_assets/image25.png)

使用相同的方法在放电停止点构造命令。