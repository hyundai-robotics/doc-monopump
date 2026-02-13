
[__SOURCE](README.md)
# ${cont_model} 제어기 기능설명서 - 모노펌프 실러건

[__SOURCE](0-about-this-manual/precautions.md)
# 사전 주의사항

{% include url="https://hrcontentsrelay-bmgae5hdbzapc4bc.koreacentral-01.azurewebsites.net/api/proxy?path=doc-common-pages/ko/precautions.md" %}

[__SOURCE](1-intro/README.md)
# 1. 개요


[__SOURCE](1-intro/1-preparatory-information.md)
# 1.1 사전 필요 정보

이 설명서를 이해하기 위해서는 다음과 같은 사전 정보가 필요합니다.

1. **${cont_model} 로봇 제어기 조작 지식**
2. **모노펌프 건의 동작 원리**

[__SOURCE](1-intro/2-monopump-func.md)
# 1.2 모노펌프 시스템


### <mark style="color:green;">1. 전체 시스템 구성 </mark>

    하기의 그림은 전체 시스템 구성을 나타냅니다. 로봇 제어기로 모노펌프 건을 직접 제어할 수 있습니다.

![](../_assets/image18.png)

### <mark style="color:green;">2. 모노펌프건 구성</mark>

    하기의 그림은 모노펌프 건의 구성을 나타냅니다. 서보모터, 로터, 스테이트로 구성되어 있습니다.

![](../_assets/image19.png)


[__SOURCE](2-basic-setting/README.md)
# 2. 기본 설정


[__SOURCE](2-basic-setting/1-add-axis-parameter.md)
# 2.1 부가축 파라미터 설정

실러 건을 로봇의 부가축으로 직접 제어할 때는 축 사양을 <실러>로 설정합니다. 또한 모노펌프 건의 토출량(cc/s)은 해당 모터의 회전속도(rpm)에 따라 결정되기 때문에 해당 축의 속도를 제어해야 합니다. 이에 따라 축 구성을 <속도제어>로 설정합니다.

![](../_assets/image1.png)


- 감속기를 사용하지 않고 모터와 직결한다면 감속비를 360:1으로 설정합니다. 이는 모터 1회전에 실제 기구는 360deg 회전함을 의미합니다. 감속기가 존재한다면 해당 감속기의 감속비를 설정하고 또한 토출이 진행되는 방향을 고려하여 감속비 부호를 설정합니다. <br>

![](../_assets/image28.png)

- 가감속 파라미터의 가속시간은 최고속에 도달하는 시간을 감속시간은 최고속에서 정지까지 시간을 결정하는 파라미터로 모노펌프건에서 이 설정값이 크면 토출 시작과 종료시, 석백과 리필 동작시 반응이 늦기 때문에 원하는 품질을 확보하기 어렵습니다.<br>
따라서 가능한 범위에서 작게 설정하여 동작속도를 높여서 사용합니다.


[__SOURCE](2-basic-setting/2-sealer-gun-setting.md)
# 2.2 실러건 데이터 설정

[시스템] -> [4: 응용 파라미터] -> [20: 실링] -> [1: 실러건 설정] 화면에 집입합니다.
실러건에 따른 건의 타입과 부가축을 설정합니다. "+"버튼에 의한 건의 추가, "-"버튼에 의한 건의 삭제가 가능합니다.

![](../_assets/image2.png)

- 건 타입 : 모노펌프 건으로 설정합니다.
- 부가축 : 해당 건의 부가축 번호를 설정합니다.

[속성] 버튼에 의한 상세한 건의 설정이 가능합니다.

[__SOURCE](2-basic-setting/3-monopump-setup/README.md)
# 2.3 모노펌프건 설정


[__SOURCE](2-basic-setting/3-monopump-setup/1-general.md)
# 2.3.1 일반

모노펌프 건과 관련된 일반적인 설정입니다.

![](../../_assets/image3.png)

- 제조사 : 모노펌프 건의 제조사를 선택합니다.
- 토출비 단위 : 토출비 인터페이스를 위한 단위를 선택합니다.
- 비중 : 실러 물질의 비중을 설정합니다.
- 실러명령 실행방식 : 작업 프로그램에서 msealer on/off 명령문을 실행하여 토출을 수행합니다. 그런데 <토출 off>를 선택하면 실제 토출은 수행하지 않고 작업 프로그램을 실행할 수 있습니다. 


[__SOURCE](2-basic-setting/3-monopump-setup/2-flow-rate-tunning.md)
# 2.3.2 토출비 튜닝

모노펌프 건의 모터 회전속도(rpm)에 따른 토출비(cc/s)를 설정합니다. 최대 6단계의 구간으로 나누어 설정이 가능하도록 구성되어 있습니다.<br>
토출비는 지정 시간동안 지정 속도로 토출된 양을 저울에서 계측한 후 "계측값(g) * 비중 / 시간"의 계산값으로 설정합니다. 

![](../../_assets/image4.png)


[수동 토출 시작] 버튼을 이용하여 해당 모노펌프 건의 모터를 지정된 속도로 설정된 시간동안만 구동할 수 있습니다.

![](../../_assets/image5.png)


하기의 그림은 수동 도출 실행에 대한 진행 상태를 표시합니다.

![](../../_assets/image6.png)


[수동 토출 정지] 버튼을 이용하여 수동 토출 실행을 강제로 정지시킬 수 있습니다.

![](../../_assets/image7.png)


[초기화] 버튼을 이용하여 모터 1회전에 대한 토출량을 기준으로 토출비를 초기값으로 설정할 수 있습니다.

![](../../_assets/image8.png)



[__SOURCE](2-basic-setting/3-monopump-setup/3-input-signal-assign.md)
# 2.3.3 입력 신호 할당

모노펌프 건과 관련하여 로봇제어기로 입력되는 신호에 대한 설정입니다.

![](../../_assets/image9.png)

[자동할당] 버튼에 의하여 선택된 실러건 제조사에 따른 신호의 자동 설정이 가능합니다. <br>
    ![](../../_assets/image9_1.png)

- 실러명령 실행방식 : 작업 프로그램에서 msealer on/off 명령문을 실행하여 토출을 수행합니다. 그런데 설정된 신호가 on 상태이면 실제 토출은 수행하지 않고 작업 프로그램을 실행할 수 있습니다. <br> 
- 통신 상태 : 실러 제어반과의 통신 상태를 확인합니다. 실러 제어반은 해당 신호를 1초마다 on/off 반복하도록 제어하면 됩니다. <br>
로봇 제어기는 해당 신호의 상태가 2초 이상 변경되지 않으면 "E6319 실링 장비 통신이상" 에러를 발생합니다. <br>
- 그 외 신호 : 실러 제어반의 상태를 확인합니다. 로봇 제어기에서 해당 상태를 검지하여 에러나 경고를 발생하고자 할 때에는 사용자 정의 에러/경고 기능을 사용하십시오. <br>
![](../../_assets/image9_2.png)

- 압력 센서 : 압력 센서 입력에 대한 정보를 설정합니다. <br>
	- 사양(최소 ~ 최대) :압력 센서 사양의 최소값과 최대값을 설정합니다. <br>
	- 통신(최소 ~ 최대) :압력 센서의 데이터가 통신으로 전달될 때 이에대한 최소값과 최대값을 설정합니다. <br>
	- 신호 할당 :압력 센서에서 입력되는 신호를 설정합니다. <br>
	- 할당된 비트 수 : 압력 센서에서 사용되는 신호의 비트수를 설정합니다. <br>
	- 인터페이스 변수 : 계산된 압력값의 인터페이스를 위한 변수값을 설정합니다. 여기서는 현재 입력되는 압력으로 계산된 압력값이 _mf4의 메모리에 대입됩니다. <br>

       ![](../../_assets/image10.png)


[__SOURCE](2-basic-setting/3-monopump-setup/4-output-signal-assign.md)
# 2.3.4 출력 신호 할당

모노펌프 건과 관련하여 로봇제어기에서 출력하는 신호에 대한 설정입니다.

![](../../_assets/image10_5.png)

[자동할당] 버튼에 의하여 선택된 실러건 제조사에 따른 신호의 자동 설정이 가능합니다. <br>
![](../../_assets/image9_1.png)

- 실러명령 실행방식 : 작업 프로그램에서 msealer on/off 명령문을 실행하여 토출을 수행합니다. 그런데 사용자 설정이나 입력신호 상태에 의해서 실제 토출을 수행하지 않고 작업 프로그램을 실행할 수 있습니다. 실제 토출의 수행 여부에 대한 출력입니다. <br> 
- 토출 중 : 모노펌프 건이 실러의 토출 여부를 출력합니다. <br>
- 에러 리셋 : 실러 제어반에 이상이 발생한 경우에 이를 리셋하기 위한 출력입니다.  <br>
  R1(에러 리셋) 동작이나 "에러/경보 신호 클리어" 신호가 입력되면 동작하는데 동작은 1초 동안 on되는 펄스 신호로 출력됩니다.<br>
- 그 외 신호 : 로봇언어에서 신호출력으로 실러 제어반에 상태를 전달할 때 사용하십시오. <br>


[__SOURCE](3-command-condition/README.md)
# 3. 명령문과 실러조건

실링 작업과 관련된 명령문과 실러조건 설정에 대해 설명합니다.


[__SOURCE](3-command-condition/1-command/README.md)
# 3.1 명령문

job 프로그램에서 모노펌프 건과 관련된 명령문에 대해서 알아봅시다.일반적으로 토출은 m_sealer on에서 m_sealer off의 구간내에서 수행됩니다.


{% hint style="info" %}
수동모드에서 m_sealer 명령문을 실행할 때는 명령문은 실행 완료로 처리하지만 실제 동작은 수행하지 않습니다.
{% endhint %}


![](../../_assets/image11.png)


[__SOURCE](3-command-condition/1-command/1-msealer-on.md)
# 3.1.1 토출 시작 (m_seler on)

모노펌프 건의 토출을 시작하는 명령문으로 형식은 다음과 같으며 자동모드에서만 동작합니다.

#### <mark style="color:green;">명령문 형식</mark>
```
m_sealer on,gun=1,cnd=1,flow=0.5,od=_,ot=_
```

#### <mark style="color:green;">파라미터</mark>

|파라미터| 설명                                                                                                    |    사용 예    |
| :---: | ------------------------------------------------------------------------------------------------------- | :-------: |
| on   | <p>실러 조건(cnd)의 설정에 따라 해당 건의 토출을 시작(str)</p>   | "on" |
| gun  | <p>토출을 시작할 모노펌프 건의 번호를 지정(int)</p>              |  1   |
| cnd  | 토출을 위한 조건 번호(int)                                     | 1    |
| flow   | <p>실러 조건(cnd)에 설정된 정속, 속도비례, 정액의 토출 모드 설정에 따라 하기와 같이 동작(double)</p><ul><li>정속 : 로봇의 속도에 무관하게 flow에 지정한 토출비(cc/s)로 토출</li><li>속도비례 : 로봇의 툴 끝 이동속도에 비례한 토출을 수행합니다. 로봇의 툴 끝 이동속도(mm/s)에 대한 토출비(cc/s)는 실러 조건에서 설정. (실러조건 참고) flow를 지정하지 않은 경우는 설정된 토출비의 1배로 토출되며 flow가 1.3으로 지정된 경우는 설정된 토출비의 1.3배로 출력</li><li>정액 : 지정된 토출량만 출력한 후 토출을 종료하며 이때 토출량은 실러 조건에서 설정(실러조건 참고) <br>  - od와 ot가 모두 기록되지 않은 경우 : 해당 명령문에서 지정된 토출량을 모두 토출한 후 off 조건에 대한 동작을 수행<br>  - od와 ot가 기록된 경우 : 이후의 명령문들을 수행하면서 지정된 토출량을 토출한 후 off 조건에 대한 동작을 수행</li></ul>                                         | 1.3 |
| od  | 로봇이 목표위치 도달 전/후에 지정된 거리만큼 명령문의 실행을 조정하고자 할 때 사용하며 지정되지 않은 경우는 목표위치 도달(acc ok)후 바로 실행(double)                                     | -0.5    |
| ot  | 로봇이 목표위치 도달 전/후에 지정된 시간만큼 명령문의 실행을 조정하고자 할 때 사용하며 지정되지 않은 경우는 목표위치 도달(acc ok)후 바로 실행. 만약 od와 ot가 모두 기록된 경우 od를 우선으로 적용(double)                                     | -0.5    |


[__SOURCE](3-command-condition/1-command/2-msealer-off.md)
# 3.1.2 토출 종료 (m_seler off)

모노펌프 건의 토출을 종료하는 명령문으로 형식은 다음과 같습니다. <br>
off 명령문은 수동모드에서도 동작합니다. <br>

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


[__SOURCE](3-command-condition/2-condition/README.md)
# 3.2 실러조건

실러조건은 m_sealer on이나 off 명령문에서 [속성]버튼에 의해 설정합니다. "+"버튼에 의한 조건의 추가, "-"버튼에 의한 조건의 삭제가 가능하며 현재 최대 8개의 조건을 지원합니다.  


[__SOURCE](3-command-condition/2-condition/1-msealer-on.md)
# 3.2.1 토출 시작 (m_seler on)

m_sealer on 명령을 수행할 때 토출 조건을 설정합니다.

![](../../_assets/image12.png)

- 토출 모드 : 정속, 속도비례, 정액의 토출 모드를 선택합니다. 속도비례는 로봇의 툴 끝 이동속도에 따라 자동으로 토출비가 결정됩니다.
- 토출량(정액 모드) : 토출 모드가 정액인 경우 토출량을 설정합니다.
- <속도-토출비 테이블> : 토출 모드가 속도비례인 경우 로봇 툴 끝의 이동속도(mm/s)에 따른 토출비를 설정합니다. 최대 5단계의 구간으로 나누어 설정이 가능하도록 구성되어 있습니다. 설정하는 방법은 로봇 Lock을 유효로 설정한 상태에서 하기의 그림과 같이 m_sealer on ~ off 구간을 정속 모드로 실행하여 토출량을 확인합니다. 동일한 토출량이 되었을 때 해당 로봇속도에 따른 토출비를 설정합니다.

  ![](../../_assets/image13.png)

  로봇의 속도가 낮은 구간에서 로봇 속도에 따른 토출비을 정비례 관계로 적용한다면 하기의 그림과 같이 토출 시작시 토출이 누락되는 현상이 발생합니다. <br>
  ![](../../_assets/image26.png)

  상기 토출 시작시 부족한 토출량을 보상하기 위해서는 하기의 그림과 같이 로봇의 속도가 0 ~ 50mm/s의 저속에서도 일정량 이상의 토출이 되도록 운용하는 것이 필요합니다. <br>
  ![](../../_assets/image24.png)

[__SOURCE](3-command-condition/2-condition/2-msealer-off.md)
# 3.2.2 토출 종료 (m_seler off)

m_sealer off명령문 수행시 석백 및 리필을 위한 동작 조건을 설정합니다. 석백은 토출이 끝난 후 잔량 제거를 위한 동작이며 리필은 석백이 끝나고 노즐에 실러를 충진하는 동작입니다. 

![](../../_assets/image14.png)

- 석백 토출비 : 석백 동작을 위한 토출비를 설정합니다.
- 석백 시간 : 석백 동작 시간을 설정합니다.
- 지연 시간 : 석백과 리필 사이에 대기 시간을 설정합니다.
- 리필 토출비 : 리필을 위한 토출비를 설정합니다.
- 리필 시간 : 리필 동작 시간을 설정합니다.


[__SOURCE](3-command-condition/2-condition/3-stop-restart.md)
# 3.2.3 정지/재기동 (stop/restart)

정지나 비상정지 입력으로 로봇이 정지하고 재기동할때 석백 및 리필을 위한 동작 조건을 설정합니다. <br>
정지시에는 석백 동작을 수행하여 정지 위치에서 실러가 뭉치는것을 방지합니다. <br>
재기동시는 토출 누락을 방지하기 위해 리필 동작 수행 이후에 로봇이 이동을 시작합니다. 

![](../../_assets/image29.png)

<정지>
- 석백 토출비 : 석백 동작을 위한 토출비를 설정합니다.
- 석백 시간 : 석백 동작 시간을 설정합니다.

<재기동>
- 리필 토출비 : 리필을 위한 토출비를 설정합니다.
- 리필 시간 : 리필 동작 시간을 설정합니다.


[__SOURCE](4-monitoring/README.md)
# 4. 모니터링


[__SOURCE](4-monitoring/1-sealing-status.md)
# 4.1 실링 상태

실러 상태를 확인하기 위한 모니터링창에 대해서 설명합니다. [창조정]에서 실링 상태를 선택합니다.

![](../_assets/image15.png)

![](../_assets/image16.png)

- 토출비 : 현재 토출되는 토출비를 표시합니다.
- RPM 지령값 : 토출비에 해당하는 실러 모터의 RPM 지령값입니다.
- RPM 현재값 : 실러 모터의 RPM 현재값을 표시합니다.
- 압력 : 압력 센서에 의해 입력되는 압력값을 표시합니다.
- 토출량 : 토출 시작부터 계측된 토출양을 표시합니다.


[__SOURCE](5-etc/README.md)
# 5. 기타

[__SOURCE](5-etc/1-stop-restart.md)
# 5.1 실러 on구간 정지/재기동

실러 on구간에서 로봇이 정지/재기동시 모노펌프 건의 동작에 대해서 설명합니다.

![](../_assets/image30.png)

- 정지 : stop 조건의 석백 동작을 수행하여 정지 위치에서 실러가 뭉치는것을 방지합니다..
- 재기동 : 토출 누락을 방지하기 위해 stop 조건의 리필 동작 수행 이후에 로봇이 이동을 시작합니다.


{% hint style="info" %}
참고내용
- [3.2.3 정지/재기동 (stop/restart)](../3-command-condition/2-condition/3-stop-restart.md)<br>
- 시스템 변수 ([_sealing.stop_seq_exe_offset_time](./4-system-var.md))
{% endhint %}


[__SOURCE](5-etc/2-manual-oper.md)
# 5.2 수동 운전(R371)

[R371 : 실러 수동 운전]을 수행했을 때 표시되는 화면에서 모노펌프 건을 수동 운전할 수 있습니다.

- 토출비 : 수동 운전을 위한 토출비를 설정합니다. <br>
- 토출량 : 정량토출 동작시 토출량을 설정합니다. <br>

![](../_assets/image20.png)
![](../_assets/image21.png)

- 정속토출 <br>
 설정된 토출비로 토출을 시작합니다. 토출을 정지하기 위해서는 [토출정지] 버튼을 별도로 수행하여야 합니다. <br>
- 정량토출  <br>
 설정된 토출비로 토출을 시작한 후 설정된 토출량에 도달하면 자동으로 토출을 정지합니다. [토출정지] 버튼으로 강제로 토출을 정지할 수 있습니다. <br>
- 토출정지 <br>
 토출을 정지하기 위해 사용합니다. <br>

{% hint style="info" %}
토출 정지시에는 항상 [off] 탭에 설정된 석백과 리필 조건에 따른 동작이 수행됩니다.
{% endhint %}


[__SOURCE](5-etc/3-license-key.md)
# 5.3 라이선스키 등록

본 기능을 사용하기 위해서는 "실링 옵션 기능"에 대한 라이선스키가 필요합니다. 당사에 문의하십시오.

![](../_assets/image17.png)

[__SOURCE](5-etc/4-system-var.md)
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


[__SOURCE](5-etc/5-flow-amount-log.md)
# 5.5 토출량 이력확인

기록된 로그 파일로 토출량의 이력을 확인할 수 있습니다.

- date_time : 로그 기록시의 날짜와 시간입니다. <br>
- job : 현재 프로그램 번호입니다. <br>
- step : 현재 스텝의 번호입니다. <br>
- flow_amount : 사이클 시작부터 종료까지 누적된 토출량입니다. <br>

![](../_assets/image22.png)

![](../_assets/image23.png)

{% hint style="info" %}
- 제어기 전원 투입 후 첫번째 기록시에 새로운 로그 파일이 생성됩니다.  
- 로그 파일은 0 ~ 9의 파일명이 순환하면서 생성됩니다.
{% endhint %}


[__SOURCE](5-etc/6-job-composition.md)
# 5.6 작업 프로그램 구성

모노펌프 건으로 토출의 시작 시점과 종료 시점을 보다 쉽게 맞추기 위한 작업 프로그램 구성 방법입니다. <br>

일반적으로 사용하는 작업 프로그램 형태를 사용한다면 하기의 그림과 같이 토출의 시작/종료 시점에서 누락이 발생하거나 토출량이 부족한 현상으로 나타납니다. <br>

![](../_assets/image27.png)

상기 현상을 보완하기 위한 방법으로 하기의 그림과 같이 토출전 스텝과 토출후의 스텝을 동일한 위치로 기록한 상태에서 토출후의 스텝에는 accu를 0으로 설정하고 토출전 스텝에는 accu를 1로 설정합니다. 이후에 m_sealer on 명령문에서 ot나 od 명령문을 사용하여 명령문을 실행하는 시점을 조정합니다.

![](../_assets/image25.png)

토출 종료 지점에서도 동일한 방식으로 명령문을 구성하여 사용합니다. 
