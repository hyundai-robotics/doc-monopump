# 5.4 System variables

*   <mark style="color:green;">**_sealing.flow_amount**</mark>

    ### Description
        Used to obtain the measured discharged amount since discharge start.

    ### Usage example
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
    S8 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
       print _sealing.flow_amount
       if abs(_sealing.flow_amount - 6) > 1 then
           print "Discharged amount is outside the specified range."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.flow_amount_cycle**</mark>

    ### Description
        Used to obtain the measured discharged amount for one cycle from start to stop.

    ### Usage example
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S74 move L,spd=100mm/sec,accu=1,tool=1
    S75 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
       print _sealing.flow_amount_cycle
       if abs(_sealing.flow_amount_cycle - 32) > 3 then
           print "1-cycle discharged amount is outside the specified range."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.stop_seq_exe_offset_time**</mark>

    ### Description
        This is used to adjust the timing of the suck-back action when stopping (default 0.1 [sec]).

    ### Usage example
    ```python
       _sealing.stop_seq_exe_offset_time=-0.2 #adjust suck-back timing on stop
       m_sealer on,gun=1,cnd=1,flow=0.6 #discharge start
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #discharge stop
    ```
    <br>
    <br>