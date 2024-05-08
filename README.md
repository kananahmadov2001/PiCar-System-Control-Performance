<div align="center">
    <h1 id="Header">PiCar-System-Control-Performance</h1>
</div>

PiCar is a robotic platform that uses Raspberry Pi, a small single-board computer, as its primary control unit. The PiCar we built for the Final Module included the sensors: Camera, DC Motor, Servos(s), Analog-to-Digital Converter, and Ultrasonic sensors.

<div align="center">
    <b>Description details:</b>
    <p style="margin-top:10px;"></p>
</div>

    1. Introduction: Sensors used on the PiCar and Power
    2. Methods: 
    3. Analysis and Results: 
    4. Conclusion

<div align="center">
    <h2 id="Header">Introduction: Sensors used on the PiCar and Power</h2>
</div>

The PiCar has the Ultrasonic sensor for the eyes and the Camera as its mouth. The Ultrasonic Sensor also has a builtin voltage divider to convert the 5 V for the Echo down to 3.3 V input to the Raspberry Pi. The DC motor is installed on the back of the PiCar; the motor has a rear-wheel drive connected to some gears underneath that drive the wheels. The Analogto-Digital Converter (ADC) is also connected to the back end of the car next to the motor. The ADC was also connected to a photoresistor at channel 0 and an LED light that pointed at the inside of the left back wheel where the black and white disk is installed. Regarding the Servo(s), our PiCar has three servomotors on it:
* Nod servomotor (for tilting the head up and down)
* Swivel servomotor (for twisting the head left and right)
* Steer servomotor (for steering the front wheels left and
