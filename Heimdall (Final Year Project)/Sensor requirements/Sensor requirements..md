

1. Sensor requirements

Linked here are the sensor requirements for Heimdall: [[Sensor requirements.]]
Linked here are the datasheet subfolders: [[EKMB110111.pdf]]  [[HC-SR501.PDF]]
# Primary Early-Warning Sensors (The "Triggers")

These are low-power sensors that run 24/7 on the node to wake up the system when a breach occurs.

- **Passive Infrared (PIR) Sensor (e.g., HC-SR501 or Panasonic EKMC):**
    
    - _Role:_ Detects rapid changes in thermal radiation (body heat).
        
    - _Why:_ Extremely low power consumption; perfect for keeping the STM32 in sleep mode until an intruder walks past.

(After deliberation, i will be going with Panasonic EKMB110111 PaPIR as the major/lead PIR sensor) [[Primary EWS]] 
        
- **$24\text{GHz}$ Doppler Radar Module (e.g., RCWL-0516 or HLK-LD2410 or  **InnoSenT SMR-333 (or SMR-334 FMCW variant)** ):**
    
    - _Role:_ Detects physical movement through microwave reflections.
        
    - _Why:_ Unlike PIR, radar can "see" through plastic enclosures, bushes, and fog. Fusing PIR + Radar immediately eliminates 90% of false motion alarms.

The datasheets of the sensors used in this stage are linked below:
[[SMR334-314_Datasheet_SMR-3x4_2.3.pdf]] 
[[HC-SR501.PDF]]
[[EKMB110111.pdf]] 

## 2. Secondary Verification & Tracking Sensors (The "Eyes & Ears")

Once the primary sensors trigger, these confirm the exact location and nature of the threat. [[Secondary V&T Sensors]] 

- **Ultrasonic Distance Sensor (e.g., HC-SR04 or  US-100 or MatBotix LV- MaxSonar-EZ1):**
    
    - _Role:_ Calculates exact metric distance (ranging) to the object.
        
    - _Why:_ Helps Heimdall determine if the moving target is $2\text{m}$ away or $10\text{m}$ away so the gimbal camera can pre-focus accurately.
        
- **Optical Camera Module (e.g., ESP32-CAM or USB Webcam to Python):**
    
    - _Role:_ Feeds visual frames to OpenCV/YOLO for target identification (human vs. animal vs. vehicle).
        
- **Acoustic / Sound Sensor (e.g. Infineon IM69D130 (Digital XENSIV MEMS Microphone):**
    
    - _Role:_ Listens for high-decibel acoustic spikes (glass shattering, fence cutting, footsteps).

Some of the PDFs of the datasheets involved are linked below:
[

## 3. Perimeter Integrity & Tamper Sensors

These detect direct physical attacks on the Heimdall node itself. [[Perimeter Integrity & Tamper sensors]]

- **Piezoelectric Vibration / Seismic Sensor (e.g., SW-420 or LDT0-028K or Safran Colibrys VS1002 (Seismic MEMS):**
    
    - _Role:_ Detects mechanical shock and vibration.
        
    - _Why:_ Alerts the system if an intruder tries to hit, kick, or climb the post where Heimdall is mounted.
        
- **Magnetic Contact Switch (Reed Switch) / Tamper Microswitch:**
    
    - _Role:_ Mounts inside the enclosure housing.
        
    - _Why:_ Triggers an instant tamper alarm if someone opens the physical enclosure to disable the board.
        

## 4. Environmental & Context Sensors (System Health)

These ensure the system adjusts its sensitivity based on real-world conditions.

- **Light Dependent Resistor (LDR) / Photodiode:**
    
    - _Role:_ Measures ambient light levels.
        
    - _Why:_ Tells Heimdall whether to switch camera feeds to night-vision IR modes or adjust radar/PIR thresholds during high ambient heat.
        
- **Current/Voltage Sensor (e.g., INA219 IC):**
    
    - _Role:_ Monitors battery health and solar input voltage.