# 5.4 시스템 변수

*   <mark style="color:green;">**_sealing.flow_amount (토출량)**</mark>

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
           print "토출량이 지정된 범위를 벗어났습니다."
           stop
       endif
    ```

