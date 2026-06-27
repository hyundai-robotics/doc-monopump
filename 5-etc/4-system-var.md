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