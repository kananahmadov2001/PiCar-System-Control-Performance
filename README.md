<div align="center">
    <h1 id="Header">PiCar-System-Control-Performance</h1>
</div>

PiCar is a robotic platform that uses Raspberry Pi, a small single-board computer, as its primary control unit. The PiCar we built for the Final Module included the sensors: Camera, DC Motor, Servos(s), Analog-to-Digital Converter, and Ultrasonic sensors.

<div align="center">
    <b>Description details:</b>
    <p style="margin-top:10px;"></p>
</div>

    1. Introduction: Sensors used on the PiCar and Power
    2. Objective 1: Control
    3. Objective 1: Movement
    4. Objective 3: Movement with Control

<div align="center">
    <h2 id="Header">Introduction: Sensors used on the PiCar and Power</h2>
</div>

The PiCar has the Ultrasonic sensor for the eyes and the Camera as its mouth. The Ultrasonic Sensor also has a builtin voltage divider to convert the 5 V for the Echo down to 3.3 V input to the Raspberry Pi. The DC motor is installed on the back of the PiCar; the motor has a rear-wheel drive connected to some gears underneath that drive the wheels. The Analog-to-Digital Converter (ADC) is also connected to the back end of the car next to the motor. The ADC was also connected to a photoresistor at channel 0 and an LED light that pointed at the inside of the left back wheel where the black and white disk is installed. Regarding the Servo(s), our PiCar has three servomotors on it:
* Nod servomotor (for tilting the head up and down)
* Swivel servomotor (for twisting the head left and right)
* Steer servomotor (for steering the front wheels left and

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/28984a60-a50c-4976-ba48-2b17961fa3f6"> 
</p>

Other than the sensors, the PiCar’s Power component is also essential. The Power LEDs and switch is located on the PWM HAT, which sits on top of the Raspberry Pi. The up/down switch controlls the power from the batteries located under the PiCar, and the four LEDs indicates how much power was left in the batteries.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/fec7c5b2-c88e-4d00-b544-056300e7df36"> 
</p>


<div align="center">
    <h2 id="Header">Objective 1: Control</h2>
</div>

The main goal of objective 1 was designing a control system for the car similar to what was used for the motor.



<div align="center">
    <h2 id="Header">Objective 2: Movement</h2>
</div>



<div align="center">
    <h2 id="Header">Objective 1: Movement with Control</h2>
</div>
