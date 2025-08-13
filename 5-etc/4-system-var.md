# 5.4 시스템 변수

*   <mark style="color:green;">**_sealing.flow_amount**</mark>

    ### 설명
        토출 시작부터 계측된 토출량을 얻기위해 사용합니다.

    ### 사용 예
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #토출시작
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
    S8 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #토출종료
       print _sealing.flow_amount
       if abs(_sealing.flow_amount - 6) > 1 then
           print "토출량이 지정한 범위를 벗어났습니다."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.flow_amount_cycle**</mark>

    ### 설명
        1 사이클에 대한 토출 시작부터 계측된 토출량을 얻기위해 사용합니다.

    ### 사용 예
    ```python
       m_sealer on,gun=1,cnd=1,flow=0.6 #토출시작
    S74 move L,spd=100mm/sec,accu=1,tool=1
    S75 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #토출종료
       print _sealing.flow_amount_cycle
       if abs(_sealing.flow_amount_cycle - 32) > 3 then
           print "1사이클 토출량이 지정한 범위를 벗어났습니다."
           stop
       endif
    ```
    <br>
    <br>

*   <mark style="color:green;">**_sealing.stop_seq_exe_offset_time**</mark>

    ### 설명
        정지시에는 stop 조건에 따라 석백 동작을 수행하는데 이 석백 동작의 타이밍을 조정하기 위해서 사용합니다. (기본값 0.1[sec])

    ### 사용 예
    ```python
       _sealing.stop_seq_exe_offset_time=-0.2 #정지시 석백타이밍 시간 조정
       m_sealer on,gun=1,cnd=1,flow=0.6 #토출시작
    S4 move L,spd=100mm/sec,accu=1,tool=1
    S5 move L,spd=100mm/sec,accu=1,tool=1
    S6 move L,spd=100mm/sec,accu=1,tool=1
    S7 move L,spd=100mm/sec,accu=1,tool=1
       m_sealer off,gun=1,cnd=1 #토출종료
    ```
    <br>
    <br>

