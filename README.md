# cereal_oldest
The capnp struct definitions used across the comma ecosystem

The "cereal" repository by comma.ai is a specialized messaging specification and high-performance inter-process communication (IPC) system designed for robotics systems. It functions as a pub-sub (publisher-subscriber) messaging system, where a single publisher sends messages to multiple subscribers. This is particularly useful in scenarios where, for example, a sensor process reads gyro measurements from an IMU and publishes a `sensorEvents` packet, which can then be subscribed to by other processes like a calibration or localization process for various uses【7†source】.

In terms of implementation, cereal uses Cap'n proto for its message types. It defines a structure called `Event` which contains `logMonoTime` and `valid` fields, and a union to define the packet type. All fields in the messages must describe quantities in SI units and be unambiguous and easy to plot and human-readable with minimal parsing【7†source】. The system is designed to maintain backward compatibility so that old logs can still be parsed with new versions of cereal, generally achieved by adding structs or members to structs【8†source】.

For custom forks, especially those of openpilot, it’s possible to modify certain reserved events in cereal without breaking compatibility with the mainline versions of cereal and openpilot【9†source】. Cereal supports two backends for messaging: one based on ZeroMQ and another custom pub-sub based on shared memory, which doesn't require the bytes to pass through the kernel【10†source】. There are also Python examples provided in the repository to illustrate the use of these messaging systems in subscriber and publisher roles【11†source】.

Openpilot, on the other hand, is an open source driver assistance system developed by comma.ai that performs functions like Adaptive Cruise Control (ACC), Automated Lane Centering (ALC), Forward Collision Warning (FCW), and Lane Departure Warning (LDW). It supports over 250 car makes and models and includes a camera-based Driver Monitoring (DM) system to alert drivers who are distracted or asleep【15†source】.

To use openpilot in a car, you need a supported device (comma 3/3X), the openpilot software, a supported car, and a car harness to connect the device to the car. Openpilot can also run on PCs for development or experimentation, using recorded or simulated data. It can be run in simulation with the CARLA simulator, and a PC running openpilot can control a vehicle if connected to the appropriate hardware【16†source】【17†source】.

The openpilot community encourages contributions and bug fixes, and the documentation provides guides for adding support for new car makes and models. The openpilot system uploads driving data to comma.ai's servers by default, which is used to train models and improve the system. However, users have the option to disable this data collection【18†source】【19†source】.

In terms of safety and testing, openpilot adheres to ISO26262 guidelines and has various software-in-the-loop and hardware-in-the-loop tests to ensure reliability and safety. The code that enforces the safety model is part of the panda system and is written in C【20†source】.

The directory structure of the openpilot repository shows the organization of the codebase into various components like cereal (for messaging), common (library-like functionality), docs, opendbc (interpreting data from cars), panda (CAN communication), third-party libraries, system (generic services), and selfdrive (code needed to drive the car)【21†source】. 

Cereal's messaging system plays a crucial role in openpilot's architecture, facilitating communication between different components of the system, like sensor data collection, logging, and the various driving assistance functionalities.
