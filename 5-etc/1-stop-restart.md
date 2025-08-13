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

