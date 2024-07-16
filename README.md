# Fire Fighter Robot

## Project Overview
The Fire Fighter Robot is an autonomous system designed to detect and extinguish fires. Equipped with flame sensors, a water pump, and controlled by an Arduino UNO, this robot actively scans its surroundings, alerts with a buzzer upon flame detection, and uses a water pump to extinguish detected fires.

## Operation
1. **Fire Detection:**
   - The robot continuously scans its surroundings within a designated range using three UV/IR flame sensors.
   - If no fire is detected within this range, the robot remains idle.
   - Upon detecting flames, the robot triggers an alert using a buzzer.

2. **Fire Extinguishing:**
   - The robot moves towards the fire using two DC motors controlled by a driver module.
   - The water pump, controlled by a relay module, activates to extinguish the flames.
   - The robot adjusts its direction based on the flame sensor input to position itself effectively for fire extinguishing.

## Components
- **Microcontroller:** Arduino UNO
  - <img src="https://github.com/user-attachments/assets/0f978b45-c56f-42ee-8d84-8fc0377f4104" alt="Uno board" width="300">
- **Sensors:** 3 UV/IR Flame Sensors
  - <img src="https://github.com/user-attachments/assets/6f42e4c7-3944-4311-8976-d311eccb3cfd" alt="Flame Sensor" width="230">
- **Alert System:** Buzzer (emits loud sounds for 2 seconds upon flame detection)
  - <img src="https://github.com/user-attachments/assets/076015ff-3ffa-4062-8ea2-c2fe5242776c" alt="Buzzer" width="300">
- **Motion Control:** Driver module controlling 2 DC motors
  - <img src="https://github.com/user-attachments/assets/e5455c1c-298e-48a6-8701-dbc5c8460dae" alt="Driver Module" width="300">
  - <img src="https://github.com/user-attachments/assets/580223b8-6652-4848-9d62-c51f7e91fe7d" alt="DC Motor" width="300">
- **Fire Extinguishing System:** Relay module and water pump
  - <img src="https://github.com/user-attachments/assets/5e6bf115-eb30-43f5-aa33-abb03cbb36f5" alt="Relay Module" width="300">
  - <img src="https://github.com/user-attachments/assets/9b6cc19c-fda4-4635-9aee-1cd9801cf77f" alt="Water Pump" width="300">
- **Power Supply:** 9V battery
  - 

## Implementation
The Fire Fighter Robot operates in two scenarios:
1. **Close Fire:**
   - When the fire is close, the water pump activates and extinguishes the fire based on the specified distance until the fire is out.

2. **Distant Fire:**
   - Upon detecting a distant fire, the robot:
     - Moves towards the fire source.
     - Adjusts its path based on the activated flame sensor (right, left, or front).
     - Extinguishes the fire until it is fully put out.

If no fire is detected, the robot remains silent and stationary.

## Project Structure
- `Fire Fighter Robot/Code.md`: Contains the code for the Fire Fighter Robot.
- `Fire Fighter Robot/Circuit.jpg`: Diagram of the robot's circuit.

## Getting Started
1. Clone the repository.
2. Follow the instructions in `Code.md` to upload the code to the Arduino UNO.
3. Assemble the components as shown in `Circuit.jpg`.
4. Power on the robot and observe its operation as it detects and extinguishes fires.

## Future Enhancements
- Integration of additional sensors for more robust fire detection.
- Improvements in movement algorithms for faster response times.
- Enhanced power management for longer operational periods.

---

Feel free to contribute to this project by submitting pull requests or opening issues for any bugs or feature requests.
