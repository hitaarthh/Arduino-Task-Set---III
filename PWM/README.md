<div>
<a href="https://www.arduino.cc/"><img src="https://img.shields.io/badge/MicroController%3A-Arduino%20UNO%203-green[700]"height="25" align="left"></a>
<a href="https://www.tinkercad.com/things/6sPd7v0lE5K?sharecode=bRUlGeeJrNxdif_1R4nE3-BGLVqJF6D2BW3rW7xpatg"><img src="https://img.shields.io/badge/Simulation:-Click%20to%20Simulate -blue" height="25"></a>
<a href="https://www.microchip.com/en-us/product/ATmega328P"><img src="https://img.shields.io/badge/Processor%3A-Atmega328P-black" height="25" align="right"></a>
</div>

<div align="center">
   <h1>Observing PWM Behaviour Using Tinkercad Oscilloscope</h1>
</div>

### --> What is a PWM and how exactly it works!? 🤔
- PWM stands for <a href="https://www.theengineeringprojects.com/2018/10/introduction-to-pwm-pulse-width-modulation.html">Pulse Width Modulation</a> which is a process to control average power supplied by the electrical signal. It is a method in which digital outputs are used to control analogue devices. This phenomenon is widely used to control inertial loads such as the speed of the motor, the brightness of the light, and the temperature of the heating elements.

- Using PWM, the average power (in the perspective of the value of current or voltage) applied to the load is controlled by a turning switch that stands between the load and supply. PWM doesn’t offer true analogue output, it provides power in pulses, instead. This means you won’t be getting current continuously delivered to the load, you’ll receive power in on and off pulses.

### --> Duty Cycle:

- The total power applied to the load is directly proportional to the time in which the switch remains turned ON. The percentage of the digital signal in which it is turned ON is called the duty cycle. Thus, controlling the ON phase of the digital signal over a consistent time interval controls the average voltage applied to the device. The time duration at which pulse remains in the On/Off state is called the width of the pulse wave.

- Known that the electrical device controlled by PWM shows behaviour that is the result of the average of wave pulses.

<div align="center">
<img src="https://res.cloudinary.com/rs-designspark-live/image/upload/c_limit,w_758/f_auto/v1/article/pwm1_5b5a238f95dc10f912bb0a66419d19884fbdd5e6"  >
</div>

### --> Simulation Diagram:

<a href="https://www.tinkercad.com/things/6sPd7v0lE5K?sharecode=bRUlGeeJrNxdif_1R4nE3-BGLVqJF6D2BW3rW7xpatg"><img width="953" alt="Simulation diagram" src="https://user-images.githubusercontent.com/91147942/167164354-de51d842-3ecf-42fc-92b6-7d1288430020.png">
</a>