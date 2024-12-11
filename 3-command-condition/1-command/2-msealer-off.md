﻿# 3.1.2 토출 종료 (m_seler off)

모노펌프 건의 토출을 종료하는 명령문으로 형식은 다음과 같으며 자동모드에서만 동작합니다.

#### <mark style="color:green;">명령문 형식</mark>
```
m_sealer off,gun=1,cnd=1,od=_,ot=_
```

#### <mark style="color:green;">파라미터</mark>

|파라미터| 설명                                                                                                    |    사용 예    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| off   | <p>실러 조건(cnd)의 설정에 따라 해당 건의 토출을 종료(str)</p>      | "off" |
| gun  | <p>토출을 종료할 모노펌프 건의 번호를 지정(int)</p>                  |  1   |
| cnd  | 토출 종료를 위한 조건 번호(int). 토출 종료시 먼저 석백이 수행되며 그 후 리필동작이 수행. 석백 동작을 위한 토출비(cc/s)와 시간 그리고 리필 동작을 위한 토출비(cc/s)와 시간은 실러 조건에서 설정(실러조건 참고)(int)                                          | 1    |
| od  | 로봇이 목표위치 도달 전/후에 지정된 거리만큼 명령문의 실행을 조정하고자 할 때 사용하며 지정되지 않은 경우는 목표위치 도달(acc ok)후 바로 실행(double)                                     | -0.5    |
| ot  | 로봇이 목표위치 도달 전/후에 지정된 시간만큼 명령문의 실행을 조정하고자 할 때 사용하며 지정되지 않은 경우는 목표위치 도달(acc ok)후 바로 실행. 만약 od와 ot가 모두 기록된 경우 od를 우선으로 적용(double)                                     | -0.5    |
