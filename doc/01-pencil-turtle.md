# Generation 1: Pencil Turtle Drawing Machine

**Build Time**: 4 weeks | **Cost**: ~$217-269 | **Difficulty**: Beginner-Intermediate

A plywood-based 2-axis CNC drawing machine controlled via Python turtle interface.

## Overview

This machine uses a CoreXY mechanism to move a pen holder in 2D space (X-Y plane), controlled by stepper motors and driven by Python code that mimics the turtle graphics API.

**Key Features**:
- 300mm x 300mm working area
- Arduino Mega 2560 + CNC Shield V3 (expandable platform)
- Python turtle API for familiar programming interface
- Plywood construction (easy with basic woodworking tools)

## Bill of Materials

### Electronics & Motion Control

#### Core Controller
- **Arduino Mega 2560** (~$15-20)
  - Excellent for real-time motor control
  - 54 digital I/O pins (plenty for expansion)
  - 16 analog inputs
  - 4 UARTs for serial communication
  - Native USB connection for easy programming
  - **Recommendation**: Arduino Mega 2560 + CNC Shield V3

#### Motor Driver
- **CNC Shield V3** (~$5-8) + **DRV8825 stepper drivers** (2x, ~$4-6)
  - CNC Shield V3 mounts directly on Arduino Mega
  - A4988: Up to 2A per coil, 1/16 microstepping
  - DRV8825: Up to 2.5A per coil, 1/32 microstepping
  - **Recommendation**: DRV8825 for smoother motion and higher current

#### Motors
- **NEMA 17 Stepper Motors** (2x, ~$20-30)
  - Specifications: 1.8° step angle, 1.5-2A current, 40+ N·cm holding torque
  - Example: 17HS4401 or similar

#### Power Supply
- **12V 5A power supply** (~$12) (or 24V 3A for faster movement)
  - Must provide enough current for 2 motors simultaneously
  - Barrel jack or screw terminal connection

#### Pen Lift Mechanism
- **SG90 or MG90S Micro Servo** (1x, ~$5)
  - 180° rotation, 9g weight
  - Metal gear (MG90S) preferred for durability

#### Miscellaneous Electronics
- USB cable (A to B, ~$5)
- GT2 timing belt (6mm width, 5+ meters total, ~$8)
- GT2 pulleys (20-tooth, 5mm bore, 2x, ~$8)
- 608ZZ bearings (8x-16x for idlers, ~$10 for 10pcs)
- M3 and M5 bolts, nuts, washers (~$15 for kit)
- Wire (22 AWG stranded, various colors, ~$10)
- Limit switches (optional but recommended, 3x, ~$5)

**Electronics Subtotal: ~$117-139**

### Hardware & Mechanical

#### Linear Motion
- **Option A**: 8mm linear rods + LM8UU bearings (~$37)
  - 8mm chrome steel rods (4x, 500mm+ length, ~$25)
  - LM8UU linear bearings (4x, ~$12)

- **Option B**: MGN12H linear rails (~$60-80, more expensive but smoother)
  - MGN12H 400mm rails (2x)

- **Recommendation**: Linear rods for budget build

#### Fasteners & Hardware (~$15-20)
- M3 bolts (various lengths: 8mm, 12mm, 16mm, 20mm, 30mm)
- M3 nuts and lock nuts
- M5 bolts (for motor mounting)
- M5 T-nuts or inserts for plywood
- Wood screws (#6 or #8, 1-2" length)

**Mechanical Parts Subtotal: ~$60-70**

#### Pen Holder
- 8mm ID tube or collar (to hold standard pencil/pen)
- Small compression spring
- Cork or foam padding

### Plywood & Wood Materials (~$30-40)
- **3/4" (18mm) plywood** - base and frame (2'x2' sheet, ~$15-20)
- **1/2" (12mm) plywood** - gantry and moving parts (2'x2' sheet, ~$10-15)
- **1/4" (6mm) plywood** - smaller brackets and pen holder (1'x1' sheet, ~$5)

### Miscellaneous (~$10-20)
- Sandpaper, wood glue, zip ties, etc.

## **TOTAL PROJECT COST: ~$217-269**

### Tools You'll Use
- Table saw (cutting plywood to size)
- Drill press or hand drill (precise holes for rods/bolts)
- Forstner bits (clean holes for bearings)
- Circular saw (breaking down sheet goods)
- Band saw (curves and intricate cuts)
- Chisels and planes (fine-tuning fit)
- Screwdrivers and hex keys
- Clamps
- Square and measuring tape
- Sandpaper (120 and 220 grit)

## Mechanical Design

### Recommended Mechanism: CoreXY

CoreXY uses two motors and a single continuous belt in a specific configuration to achieve independent X and Y motion.

**Advantages**:
- Both motors remain stationary (reduces moving mass)
- Good speed and accuracy
- Efficient belt routing

**Dimensions**:
- Working area: 300mm x 300mm (approximately 12" x 12")
- Overall footprint: 450mm x 450mm x 200mm tall

### Key Mechanical Components to Build

#### 1. Base Frame (3/4" plywood)
- Dimensions: 450mm x 450mm
- Mount for motors (2 corners)
- Mounting points for Y-axis rails/rods

#### 2. Y-Axis Gantry (1/2" plywood)
- Two vertical supports that ride on Y-axis rails
- Mounting for X-axis rails
- Belt routing channels

#### 3. X-Axis Carriage (1/2" plywood)
- Rides on X-axis rails
- Holds pen lift servo
- Belt attachment points

#### 4. Pen Holder Assembly (1/4" plywood)
- Spring-loaded pen holder
- Servo arm connection
- Vertical sliding mechanism

## Step-by-Step Build Plan

### Phase 1: Planning & Procurement (Week 1)

#### Day 1-2: Finalize Design
- [ ] Choose CoreXY vs H-Bot mechanism
- [ ] Sketch out belt routing diagram
- [ ] Create cutting list for plywood
- [ ] Download Arduino IDE from arduino.cc

#### Day 3-5: Order Parts
- [ ] Review complete Bill of Materials above
- [ ] Create shopping cart from BOM (see costs inline with each part)
- [ ] Order electronics from Amazon/AliExpress (Electronics Subtotal: ~$117-139)
- [ ] Order mechanical parts (Mechanical Subtotal: ~$60-70)
- [ ] Visit local hardware store for plywood (~$30-40)

#### Day 6-7: Prepare Workshop
- [ ] Clear workspace
- [ ] Gather and organize your tools
- [ ] Test power tools and sharpen blades
- [ ] Purchase plywood sheets locally

### Phase 2: Frame Construction (Week 2)

#### Day 1: Base Frame
- [ ] Cut base plate: 450mm x 450mm (3/4" plywood)
- [ ] Mark and drill motor mounting holes (corners)
- [ ] Create bearing/idler mounting holes
- [ ] Sand all edges smooth

#### Day 2: Linear Motion System - Y Axis
- [ ] Cut and mount Y-axis rod supports (vertical pieces)
- [ ] Drill 8mm holes for rod mounting (use drill press for precision)
- [ ] Install Y-axis rods (ensure parallel with spacers)
- [ ] Test fit LM8UU bearings on rods

#### Day 3: Y-Axis Gantry
- [ ] Cut gantry side plates (2x, 1/2" plywood)
- [ ] Drill holes for X-axis rods
- [ ] Create bearing mounts for Y-axis
- [ ] Cut and attach gantry crossbar
- [ ] Install bearings and test Y-axis sliding

#### Day 4: Linear Motion System - X Axis
- [ ] Install X-axis rods on gantry
- [ ] Cut X-axis carriage plate
- [ ] Drill and install X-axis bearings
- [ ] Verify smooth motion on both axes

#### Day 5: Belt System Planning
- [ ] Install motor mounts and motors
- [ ] Install belt idler pulleys (608ZZ bearings)
- [ ] Create belt routing diagram (tape on frame)
- [ ] Cut and shape belt attachment points on carriage

### Phase 3: Pen Mechanism (Week 3, Days 1-2)

#### Pen Lift Assembly
- [ ] Cut servo mounting bracket
- [ ] Design pen holder with vertical slots
- [ ] Create spring-loaded pen grip
  - Drill 8mm hole through holder
  - Add compression spring
  - Create servo arm linkage
- [ ] Mount servo to X-carriage
- [ ] Test pen lift (up = 45°, down = 90° servo position)
- [ ] Add felt/cork to pen holder for grip

### Phase 4: Electronics Integration (Week 3, Days 3-5)

#### Day 3: Motor Wiring
- [ ] Mount Arduino Mega to base (use standoffs or bracket)
- [ ] Install DRV8825 drivers on CNC Shield V3
  - Driver orientation: potentiometer faces away from Arduino
  - X-axis driver in first socket, Y-axis in second socket
- [ ] Set microstepping jumpers under drivers (all 3 jumpers = 1/32 step)
- [ ] Mount CNC Shield V3 onto Arduino Mega pins
- [ ] **DO NOT power on yet**

#### Day 4: Controller Wiring
- [ ] Wire motors to CNC Shield terminal blocks
  - X-axis motor to X terminals (2B 2A 1A 1B)
  - Y-axis motor to Y terminals (2B 2A 1A 1B)
  - Note motor coil pairs (use multimeter for continuity)
- [ ] Connect servo to D11 pin (or designated servo pins on shield)
  - Orange/Yellow (signal) to D11
  - Red (5V) to 5V
  - Brown/Black (GND) to GND
- [ ] Connect 12V power supply to CNC Shield
  - Red (+12V) to positive terminal
  - Black (GND) to negative terminal
- [ ] Connect USB cable from Arduino to computer

#### Day 5: Initial Power-On & Testing
- [ ] Double-check all wiring
- [ ] Adjust driver current limit (potentiometer on DRV8825)
  - Vref = (Motor Current × 8 × Rsense)
  - For 1.5A motor: Vref ≈ 1.2V
  - Use multimeter to measure between pot and GND
- [ ] Upload test sketch to Arduino (simple blink test first)
- [ ] Power on 12V supply
- [ ] Upload motor test sketch (single axis movement)
- [ ] Test individual motor rotation (no belt)
- [ ] Test servo sweep

### Phase 5: Belt Installation & Calibration (Week 3, Days 6-7)

#### Belt Routing (CoreXY)
- [ ] Route belt following CoreXY pattern
- [ ] Attach belt to carriage with zip ties or clamps
- [ ] Tension belt (should "twang" when plucked)
- [ ] Verify carriage moves smoothly when motors turn
- [ ] Check for belt skipping

#### Mechanical Calibration
- [ ] Mark 100mm distance on frame
- [ ] Command 100mm movement
- [ ] Measure actual distance
- [ ] Calculate steps/mm calibration value
- [ ] Repeat for both axes

### Phase 6: Software Development (Week 4)

#### Day 1-2: Arduino Firmware
- [ ] Install Arduino IDE libraries:
  - AccelStepper library (for smooth acceleration)
  - Servo library (built-in)
- [ ] Write Arduino firmware (`turtle_firmware.ino`):
  - AccelStepper setup for both motors
  - CoreXY kinematics (convert X,Y to motor steps)
  - Servo control for pen up/down
  - Serial command parser (G-code-like or custom protocol)
  - Command examples: `G1 X100 Y50`, `M3` (pen down), `M5` (pen up)
- [ ] Upload firmware and test with Serial Monitor
- [ ] Test basic movements (square, circle)

#### Day 3-4: Python Host Software (Turtle Interface)
- [ ] Install Python libraries:
  ```bash
  pip install pyserial
  ```
- [ ] Create `TurtleMachine` class with API:
  ```python
  turtle = TurtleMachine(port='/dev/ttyACM0')  # or COM3 on Windows
  turtle.forward(100)
  turtle.left(90)
  turtle.penup()
  turtle.pendown()
  turtle.goto(x, y)
  turtle.circle(50)
  ```
- [ ] Implement coordinate transformation
- [ ] Add boundary checking (300x300mm limits)
- [ ] Send commands to Arduino via serial

#### Day 5: Testing & Examples
- [ ] Test with Python turtle examples:
  - Spirals
  - Fractals (Koch snowflake)
  - Geometric patterns
- [ ] Create demo scripts
- [ ] Fine-tune speed and acceleration

#### Day 6-7: Polish & Features
- [ ] Add homing routine (if limit switches installed)
- [ ] Implement proper shutdown
- [ ] Add error handling and status feedback
- [ ] Create user documentation

## Software Architecture

### Two-Part System: Arduino Firmware + Python Host

#### Arduino Firmware (runs on Arduino Mega)
Handles real-time motor control, receives commands via serial.

#### Python Host Software (runs on your PC/Mac)
Provides turtle API, sends commands to Arduino via USB serial.

### Directory Structure
```
turtle_machine/
├── firmware/
│   └── turtle_firmware/
│       └── turtle_firmware.ino    # Arduino sketch
├── python/
│   ├── src/
│   │   ├── serial_comm.py         # Serial communication
│   │   ├── kinematics.py          # CoreXY math
│   │   └── turtle_machine.py      # Main turtle API
│   ├── examples/
│   │   ├── square.py
│   │   ├── spiral.py
│   │   └── fractal.py
│   └── config.py                  # Calibration values
└── README.md
```

### Arduino Firmware Configuration (turtle_firmware.ino)
```cpp
// Pin definitions (from CNC Shield V3)
#define X_STEP_PIN 54
#define X_DIR_PIN 55
#define X_ENABLE_PIN 38

#define Y_STEP_PIN 60
#define Y_DIR_PIN 61
#define Y_ENABLE_PIN 56

#define SERVO_PIN 11

// Calibration
#define STEPS_PER_MM 80.0  // Adjust after calibration
#define MAX_SPEED 3000.0   // steps/second
#define ACCELERATION 500.0 // steps/second^2

// Workspace limits
#define MAX_X 300  // mm
#define MAX_Y 300  // mm

// Pen positions
#define PEN_UP_ANGLE 45
#define PEN_DOWN_ANGLE 90
```

### Python Configuration (config.py)
```python
# Serial port (auto-detect or specify)
# macOS: /dev/tty.usbmodem* or /dev/cu.usbmodem*
# Linux: /dev/ttyACM0 or /dev/ttyUSB0
# Windows: COM3, COM4, etc.
SERIAL_PORT = 'AUTO'  # or specify like '/dev/ttyACM0'
BAUD_RATE = 115200

# Workspace (should match Arduino firmware)
MAX_X = 300  # mm
MAX_Y = 300  # mm

# Drawing speed
DEFAULT_SPEED = 2000  # mm/min
```

## Testing Protocol

### Mechanical Tests
1. **Smooth Motion Test**: Push carriage by hand across full range
2. **Belt Tension Test**: Check for even tension, no sagging
3. **Perpendicularity Test**: Use square to verify X/Y axes are 90°
4. **Backlash Test**: Move back and forth, check for play

### Electrical Tests
1. **Continuity Test**: Verify all connections with multimeter
2. **Motor Phase Test**: Check motor coils before wiring
3. **Power Test**: Verify voltage at drivers (12V)
4. **Single Motor Test**: Test each motor independently

### Software Tests
1. **Single Axis Test**: Move X only, then Y only
2. **Square Test**: Draw 100mm square, measure accuracy
3. **Circle Test**: Draw circle, check roundness
4. **Repeat Position Test**: Return to origin 10x, check error

## Troubleshooting

### Motor doesn't move
- Check driver enable pin (should be LOW)
- Verify power supply voltage
- Check current limit on driver
- Test with manual step pulses

### Motor moves wrong direction
- Swap DIR signal logic (invert in code)
- Or swap one motor coil pair

### Belt skips
- Increase belt tension
- Reduce acceleration
- Check pulley set screws

### Inaccurate drawings
- Recalibrate steps/mm
- Check belt tension
- Verify pulley teeth aren't worn
- Add acceleration ramping

### Pen doesn't lift properly
- Adjust servo angles in config
- Check servo power (needs 5V, 1A)
- Verify linkage isn't binding
- Add weight/spring to pen holder

## Safety Notes

- Always disconnect power before working on wiring
- Wear safety glasses when cutting plywood
- Keep fingers away from moving belts and pulleys
- Use proper ventilation when soldering
- Secure loose clothing/hair around power tools
- Mount power supply securely with strain relief

## Next Steps

Once you've successfully built and tested your pencil turtle, you're ready to expand:

**See**: [02-laser.md](02-laser.md) - Easiest upgrade path (~$100-200)

## Resources

### Tutorials & Guides
- CoreXY kinematics: [corexy.com](http://corexy.com/theory.html)
- Stepper motor basics: Search "How stepper motors work"
- Arduino AccelStepper library: [airspayce.com/mikem/arduino/AccelStepper](http://www.airspayce.com/mikem/arduino/AccelStepper/)
- CNC Shield V3 pinout: Search "CNC Shield V3 pinout diagram"
- PySerial documentation: [pyserial.readthedocs.io](https://pyserial.readthedocs.io/)

### Suppliers
- **Electronics**: Amazon, AliExpress, Adafruit, SparkFun
- **Mechanical**: Amazon, OpenBuilds, RobotShop
- **Plywood**: Local hardware store (Home Depot, Lowe's)

### CAD Files
- Create your own using measurements above
- Or adapt open-source CNC designs (QueenBee, MPCNC)

Good luck with your build! This is a challenging but rewarding project that combines woodworking, electronics, and programming.
