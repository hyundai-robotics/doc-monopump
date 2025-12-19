# 2.1 Additional axis parameter settings

When controlling the sealer gun directly as an additional axis of the robot, set the axis type to <Sealer>. Because the monopump gun's discharge amount (cc/s) is determined by the motor speed (rpm), you must control the axis speed. Therefore, set the axis configuration to <Speed control>.

![](../_assets/image1.png)


- If the motor is directly coupled without a gearbox, set the reduction ratio to 360:1. This means one motor revolution corresponds to 360° of the mechanism. If a gearbox exists, set the gearbox reduction ratio and set the sign of the ratio according to the discharge direction. <br>

![](../_assets/image28.png)

- The acceleration time parameter determines the time to reach maximum speed, and the deceleration time determines the time from maximum speed to stop. If these values are large for the monopump gun, the response for discharge start/stop and suck-back/refill will be delayed, making it difficult to achieve the desired quality. <br>
Therefore, set these values as small as possible to increase operating speed.