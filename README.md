<div align="center">
    <h1 id="Header">PiCar-System-Control-Performance</h1>
</div>

PiCar is a robotic platform that uses Raspberry Pi, a small single-board computer, as its primary control unit. The PiCar we built for the Final Module included the sensors: Camera, DC Motor, Servos(s), Analog-to-Digital Converter, and Ultrasonic sensors.

<div align="center">
    <b>Outline:</b>
    <p style="margin-top:10px;"></p>
</div>

    1. Introduction: Sensors used on the PiCar and Power
    2. Objective 1: Control
    3. Objective 2: Movement
    4. Objective 3: Movement with Control

<div align="center">
    <h2 id="Header">Introduction: Sensors used on the PiCar and Power</h2>
</div>

The PiCar has the Ultrasonic sensor for the eyes and the Camera as its mouth. The Ultrasonic Sensor also has a built in voltage divider to convert the 5 V for the Echo down to 3.3 V input to the Raspberry Pi. The DC motor is installed on the back of the PiCar; the motor has a rear-wheel drive connected to some gears underneath that drive the wheels. The Analog-to-Digital Converter (ADC) is also connected to the back end of the car next to the motor. The ADC was also connected to a photoresistor at channel 0 and an LED light that pointed at the inside of the left back wheel where the black and white disk is installed. Regarding the Servo(s), our PiCar has three servomotors on it:
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

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/5caf4583-51ab-4efa-bcfb-fece10e241b6"> 
</p>

Kp, Ki, and Kd are the three important parameters of the PID controller to tune the controller’s behaviour. Kp is the proportional value that provides a quick adjustment when the desired and current output differ. As soon as there is a difference present between the output and the desired output, the system can instantly respond. Ki is the integral control uses the integral (or sum of all errors in the case of a digital system). So even after no error is present in the system, the integral will likely be non-zero which allows the controller to achieve zero-steady state error. Kd is the derivative control uses the derivative of the error (in a digital system, the difference between the most recent measurements). It helps to reduce the impact of quick changes in the other control components, which help reduce the overshoot of the system.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/a166aaeb-6023-408a-84d0-b56b8e424db0"> 
</p>

Picking values for Kp, Ki, and Kd was tricky. Large values resulted in quick response but also large overshoot and often instability. Therefore, we followed the general observations procedure from our Notes to choose the appropriate values for Kp and Ki:

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/27da88db-b8db-43ba-b0fd-156e09f5f633"> 
</p>

After the following the general observations procedure, we choose the Kp = 1.0, Ki = 4.0, and Kd = 0.0. While the derivative coefficient can be valuable in controlling systems with high dynamics and oscillations, it’s not always necessary. Since we were working with a simple and stable system with computational constraints, and proportional and integral control provided the desired system response, we decided that adding derivative control might not offer substantial benefits. Therefore, we choose Kd = 0. A Kp of 1.0 provided enough overshoot to ensure that our PiCar was able to overcome inertia and get movement right away. The large Ki value of 4.0 surprised us, but multiple trials proved that lower Ki values resulted in small RPS oscillations – keeping the RPS values ”stuck” at undesired outputs. Here is the usage we had for Objective 1 that contains all the command line arguments and their values we had:

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/ad107880-8322-4abc-84ff-783b036f044f"> 
</p>

We got a steady velocity-time plot for the PiCar with only Control at the RPS of 5. The strange bottom spike at the t = 2.4 sec could be due to some bad photo-resistor reading. Regarding the system performance results, we calculated the RPS of 4.929 for our plot and found the Peak RPS to be 6.240. Since calculated the RPS, then the Steady State Error is 5 - 4.929 = 0.071. The 90% of our calculated RPS is 4.436, therefore we found the Response Time to be t = 0.60 sec where the RPS value has a sharp increase to an RPS of 5.940 – past an RPS of 4.436. Finally, the OverShoot was ((6.240 – 5.000)/5.000)*100 = - 24.8%. To justify the reasoning why our real time calculations are accurate, we modified our plotting program and just examined a steady state portion of that data (power of 2 amount of data) to determine the FFT.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/5fd64270-9a65-42ce-ae2f-2afe4d377a7f"> 
</p>


<div align="center">
    <h2 id="Header">Objective 2: Movement</h2>
</div>

The goal of the second objective was to create a program that would drive the PiCar to a blue object that is positioned at least 10 feet away with the PiCar turned up to 30◦ degrees away from the blue object in either direction. The blue object we used for objective 2 and for objective 3 is shown in figure 10. There were three targets that we were challenged to meet for this objective: A speed target, a distance target, and a direction target. The speed target was to reach the blue object in less than 10 seconds. The distance target was to start the PiCar at least 10 feet away from the blue object and stopping the PiCar within 15 cm of the blue object. The direction target is to direct the PiCar to the blue object with various starting angles. Using a mixture of the logic and functions from module9b.py and module9d.py, we created objective2.py, a program that tracks the blue object to output the steer servo position and simultaneously measure the distance from the blue object to determine the appropriate pwm for the DC motors.

The image capture delay and delta value were adjusted to create an accurately responsive PiCar that makes proportional changes in steer servo direction towards the blue object. To reduce the occurrence of over-steering/over- correction, we set the steer direction straight ahead for angle measurements below 7.5 degrees in either direction. The program initialization step centers the swivel servo, sets the nod servo slightly above center, and sets the pwm of the motor to 90% for 0.5 seconds to make sure that the PiCar overcomes inertia. Past the initialization steps, the motor pwm decreases to 62% until the PiCar gets within 200 cm. For a distance range of 199- 100, 99-50, 49-10, and 9-0 cm the pwm is set to 50%, 45%, 40%, and 0% respectfully to allow for a smooth decrease in pwm as the PiCar gets closer to the blue object.


<div align="center">
    <h2 id="Header">Objective 3: Movement with Control</h2>
</div>

The goal of Objective 3 was to combine the processes of Objective 1 and Objective 2 and make the car start from a specific point and travel in a straight line to a large colored object at a specific speed determined by the instructor. The purpose was that the car should not run into the object and should ”stop” as close to the object as possible without hitting it. Our PiCar got within 3/8”. Regarding the PID coefficients, we again followed the procedure in Fig. 7. We chose the Kp = 1.5, Ki = 4.0, and Kd = 0.0. We choose the Kd = 0 again because we were working with a system that had computational constraints, and proportional and integral control provided the desired system response. Therefore, we decided that adding derivative control might not offer substantial benefits. A Kp value of 1.5 was needed because of the load that is experienced by the PiCar increases the inertia that must be overcome. Kp remained constant from objective 1 as it provided a smoother acceleration to our desired 5 RPS value compared to other values for Kp. Higher Kp caused the PiCar to accelerate too fast and lower Kp caused the PiCar to not accelerate at all. Here is the usage we had for Objective 3 that contains all the command line arguments and their values we had:

<p align="center" width="100%">
    <img width="50%" src="https://github.com/kananahmadov2001/PiCar-System-Control-Performance/assets/135070652/546e58ce-4fb0-4180-8fd1-6035fdde1a6b"> 
</p>

The velocity-time plot with Movement and Control is not as smooth as the velocity-time plot with only Control; this is due to the increased system dynamics, non-linearities, and the friction. Regarding the system performance results, we calculated the RPS of 4.812 for our plot and found the Peak RPS to be 6.450. Since calculated the RPS, then the Steady State Error is 5 - 4.812 = 0.188. The 90% of out calculated RPS is 4.331, therefore we founded Response Time to be t = 3.935 sec at RPS of 5.004. Finally, the OverShoot was ((6.450 – 5.000)/5.000)*100 = 29.0%
