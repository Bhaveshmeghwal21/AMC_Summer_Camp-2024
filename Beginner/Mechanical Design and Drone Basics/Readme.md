# Drone Basics 
We have already conducted a workshop on drone basics, before moving ahead just go through [Drone-101](https://github.com/Bhaveshmeghwal21/Drone-101/tree/main)




# Mechanical Design
If you have not installed Solidworks then you can install it from here

UAVs are complex machines that require careful consideration when it comes to design. By understanding the key design principles involved in UAV technology, including aerodynamics, propulsion, material selection, and control systems, designers can create efficient and reliable machines that can complete their missions safely and effectively. These principles ensure that UAVs are able to perform their tasks with accuracy and precision, while also adhering to necessary safety guidelines.

As UAV technology continues to advance, it is essential for designers to remain knowledgeable of these fundamental design principles in order to create the most effective UAVs.

## Designing drone frame
The mechanical design of a drone frame plays a crucial role in its overall performance, stability, and durability. Let’s explore why it’s so important:

1.**Aerodynamics and Efficiency:**
- Aerodynamic design directly impacts how efficiently a drone moves through the air. By optimizing the shape and structure of the frame, manufacturers can reduce drag and improve overall flight efficiency1.
- A well-designed frame minimizes air resistance, allowing the drone to fly longer distances with less energy consumption.

2. **Structural Integrity and Stability:**
- The strength and rigidity of the frame are critical for maintaining stability during flight. A weak or poorly designed structure can lead to mechanical failure, resulting in a loss of control or damage to the drone2.
- The frame must withstand various forces, including those during takeoff, landing, and maneuvers. Proper mechanical design ensures the frame can handle these stresses.

3. **Weight Optimization:**
- Drone frames need to bear significant loads while remaining lightweight. Less material means reduced weight, which directly affects flight performance.
- Topology optimization techniques, such as using ANSYS, can help optimize frame designs to achieve a balance between strength and weight3. Lighter frames allow for longer flight times and better maneuverability.

4. **Component Integration:**
- The frame serves as the foundation for integrating other components, such as motors, propellers, batteries, and sensors.
- Proper mechanical design ensures that these components fit securely and are positioned optimally for balanced weight distribution and stability.

5. **Material Selection:**
- Choosing the right materials for the frame is essential. Low-weight yet rigid materials (such as carbon fiber or lightweight alloys) are commonly used.
- The frame material affects overall drone weight, durability, and crash resistance.


### Task 1 
For this you have to design a quadcopter frame, you can watch this [tutorial](https://youtu.be/SU8QDIEdPk0?si=piGcGou45qyMqABW&t=2)

The tasks aims to design a versatile and robust drone using SolidWorks software, tailored for applications such as aerial photography, surveillance, and delivery services. The design will focus on creating a quadcopter model with the following specifications:

Size and Weight: The drone should have a compact and lightweight frame, with a maximum diagonal size of 500mm and a weight limit of 1.5kg including the battery and payload.
Payload Capacity: Capable of carrying a minimum payload of 500g.
Flight Time: A minimum flight time of 20 minutes on a single charge.
 Frame Geometry: Ensure a symmetrical X or H frame design for stability, with arm lengths of 250mm.
Motor Mounts: Design motor mounts to fit standard motor sizes, typically M3 or M4 screw mounting patterns.
Propeller Size: Use propellers with a diameter of 9 to 12 inches, matching the motor’s specifications for optimal thrust.
Electronic Speed Controllers (ESC): Allocate space for ESCs that can handle the current requirements of the motors.
Camera Mount: Include an adjustable camera mount capable of holding standard action cameras with vibration dampening.
Antenna Placement: Designate positions for RF and GPS antennas to avoid signal interference.
Landing Gear: Incorporate retractable or fixed landing gear with a height of at least 75mm to protect the camera and sensors during landing.
Battery Compartment: Design a secure battery compartment that can accommodate batteries up to 150mm x 50mm x 30mm.
Arm Thickness: Aim for an arm thickness of 10mm to provide strength while minimizing drag.
Body Height: Keep the body height around 50mm to accommodate electronics while maintaining a low profile.
Propeller Clearance: Ensure at least 20mm clearance between propellers to prevent airflow interference.
Flight Controller Bay: Design a bay for the flight controller with a standard 30.5mm mounting hole pattern.

For submission just screenrecord the any part of 5 min of designing in solidworks and submit the CAD file & video in [link](https://docs.google.com/forms/d/e/1FAIpQLSeKhWzEIBl4Nn6bGHmLxqT-Xwug2iRiWKuPCz4XnJUj1gHCqg/viewform?usp=sf_link)

**NOTE** 
- When you choose a BLDC motor, you can find a thrust-current relation in their official website so that you can get your current draw with your payload. For eg check out [emax-mt2213 935kv](https://emaxmodel.com/products/emax-mt2213-935kv-multicopter-brushless-motor)
- Also for flight time assume it is hovering and current drawn by motor only.
-  If any data missing then you can choose appropriate data for making efficient drone.







