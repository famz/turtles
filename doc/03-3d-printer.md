# Generation 3: 3D Printer Conversion

**Prerequisites**: Complete [01-pencil-turtle.md](01-pencil-turtle.md) first

**Additional Cost**: ~$150-250 | **Conversion Time**: 2-3 weeks | **Difficulty**: Advanced

Convert your pencil turtle into a 3D printer by adding a Z-axis, hotend, and heated bed.

## Important Considerations

### Frame Rigidity Warning
**Plywood may not be rigid enough for reliable 3D printing**. Consider:
- Reinforcing frame with aluminum angle brackets
- Upgrading to aluminum extrusion (2020 profile)
- Accepting some print quality limitations (ringing, ghosting)

### Why 3D Printer is More Challenging
- Heavier moving parts (extruder + hotend)
- High temperatures require careful wiring
- More complex firmware (Marlin)
- Rigidity requirements higher than laser/pen
- Vibration from extruder motor

### Realistic Expectations
This conversion will produce **functional prints** but may not match commercial 3D printer quality due to:
- Plywood flex/vibration
- Open-loop control (no print monitoring)
- Budget components

**For serious 3D printing**: Consider building a dedicated printer (Prusa, Voron, etc.)

## Additional Parts Needed

### Z-Axis Motion System (~$40-60)

#### Lead Screw Option (Recommended)
- T8 lead screw, 300mm length, 2mm pitch (~$10)
- T8 anti-backlash nut (~$5)
- 5mm to 8mm flexible coupler (~$5)
- NEMA 17 motor for Z-axis (~$10)
- Linear rods for Z-axis (2x 8mm x 300mm, ~$15)
- LM8UU bearings for Z-axis (2x, ~$6)

#### Belt Option (Alternative)
- GT2 belt and pulleys (~$10)
- Counterweight or dual Z-motors

### Extruder System (~$40-80)

#### Budget Option
- Bowden extruder kit (~$15)
- Longer PTFE tube run from extruder to hotend

#### Better Option (Recommended)
- BMG clone extruder (~$25)
- Better grip on filament
- Handles flexible filaments better

### Hotend (~$30-70)

#### Budget Option
- E3D V6 clone (~$15-25)
- Works but temperature control may drift

#### Recommended Option
- Genuine E3D V6 (~$60-70)
- Better quality control
- Reliable temperature
- Longer lifespan

### Heated Bed (~$20-40)

#### Options
- 12V 200x200mm silicone heater (~$15)
- 12V 200x200mm aluminum PCB heater (~$20-30)
- **Note**: May need to upgrade power supply for heated bed

### Build Surface (~$10-20)
- PEI sheet (~$15, best adhesion)
- Glass plate (~$10, flat surface)
- BuildTak sheet (~$12, good adhesion)

### Electronics Additions

#### Temperature Sensors
- Thermistors (100K, 2x, ~$2)
- Thermistor wiring and connectors

#### Cooling
- 40mm cooling fan for hotend (12V, ~$5)
- 50mm radial fan for part cooling (12V, ~$5)

#### Power Upgrade
- **May need 12V 15A+ power supply** (~$25)
  - Heated bed draws 8-10A
  - Motors + hotend + fans ~5A
  - Total: 13-15A minimum

### Miscellaneous (~$20-30)
- PTFE tubing (Bowden, 1m)
- Kapton tape (high-temperature insulation)
- Wire extensions (higher temperature rated)
- Cable management (drag chain recommended)
- Build plate clips or magnetic base

**Total Additional Cost: ~$150-250**

## Mechanical Modifications

### Z-Axis Construction

#### Design Requirements
- 200-250mm of vertical travel
- Stable platform for heated bed
- Minimal wobble (lead screw concentricity critical)

#### Build Steps
- [ ] Design Z-axis frame (mounted to base)
- [ ] Install Z-axis lead screw and motor
- [ ] Mount Z linear rods (parallel and perpendicular to bed)
- [ ] Build bed carriage with LM8UU bearings
- [ ] Attach anti-backlash nut to bed carriage
- [ ] Couple motor to lead screw (flexible coupler critical)
- [ ] Test Z-axis movement (should be smooth, no binding)

### Carriage Modifications

#### Add Extruder Mount
- [ ] Remove pen holder/laser mount
- [ ] Design mounting plate for hotend
- [ ] Add mounting bracket for part cooling fan
- [ ] Ensure hotend nozzle clears bed at Z=0

#### Weight Considerations
- Hotend + extruder adds ~200-400g to carriage
- May need to slow down speeds (reduce acceleration)
- Check belt tension (more weight = more tension needed)

### Heated Bed Installation

#### Mounting
- [ ] Attach silicone heater to aluminum bed plate
- [ ] Insulate bottom of heater (cork or foam)
- [ ] Attach thermistor to bed (center, under heater)
- [ ] Mount bed to Z-carriage (allow for leveling adjustment)
- [ ] Apply build surface (PEI, glass, or BuildTak)

#### Leveling System
- [ ] Install leveling screws at 3-4 corners
- [ ] Use springs for tension
- [ ] Ensure bed can tilt for leveling

## Electronics & Wiring

### Wiring Overview

#### New Connections to CNC Shield
- **Z-axis motor** → Z terminal on CNC Shield
- **Extruder motor** → A (4th axis) terminal on CNC Shield
- **Hotend heater** → D8 or D9 (PWM pins)
- **Bed heater** → D10 (or external MOSFET if >10A)
- **Hotend thermistor** → Analog pin A13
- **Bed thermistor** → Analog pin A14
- **Cooling fans** → 12V rail with MOSFETs for control

#### High-Current Wiring (CRITICAL)
- Heated bed draws 8-10A → Use 14-16 AWG wire minimum
- Route high-current wires separately from signal wires
- Use external MOSFET if bed current >10A (recommended)

### External MOSFET for Heated Bed
```
Recommended: MOSFET breakout board (~$5)
- Protects Arduino from high current
- Better reliability
- Easier replacement if fails
```

## Firmware: Marlin 2.x

### Why Marlin?
- Industry standard for 3D printers
- Supports heated bed, extruder, temperature control
- G-code compatible with all slicers
- Extensive configuration options

### Marlin Configuration

#### Configuration.h Key Settings
```cpp
// Machine type
#define COREXY

// Stepper motors
#define X_DRIVER_TYPE  DRV8825
#define Y_DRIVER_TYPE  DRV8825
#define Z_DRIVER_TYPE  DRV8825
#define E0_DRIVER_TYPE DRV8825

// Steps per mm (calibrate these!)
#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 400, 93 }
// X, Y (same as drawing machine)
// Z: 400 for T8 lead screw (2mm pitch)
// E: 93 for BMG extruder (calibrate!)

// Max feedrates
#define DEFAULT_MAX_FEEDRATE { 200, 200, 5, 25 }
// X, Y: 200mm/s (slower than laser for quality)
// Z: 5mm/s
// E: 25mm/s

// Build volume
#define X_BED_SIZE 200
#define Y_BED_SIZE 200
#define Z_MAX_POS 250

// Temperatures
#define TEMP_SENSOR_0 1        // Hotend (100K thermistor)
#define TEMP_SENSOR_BED 1      // Heated bed (100K thermistor)
#define HEATER_0_MAXTEMP 275   // Hotend safety limit
#define BED_MAXTEMP 120        // Bed safety limit

// PID tuning (run auto-tune after build)
#define PIDTEMP
#define PIDTEMPBED
```

### PID Auto-Tuning (REQUIRED)
```gcode
; Auto-tune hotend (target 200°C)
M303 E0 S200 C8

; Auto-tune bed (target 60°C)
M303 E-1 S60 C8

; Save results
M500
```

## Slicing Software

### Recommended Slicers
1. **Cura** (free, beginner-friendly)
2. **PrusaSlicer** (free, advanced features)
3. **Simplify3D** ($150, professional)

### Initial Slicer Settings

#### Cura Profile
```
Printer:
- Build volume: 200 x 200 x 250mm
- Nozzle: 0.4mm
- GCode flavor: Marlin

Print Settings (conservative):
- Layer height: 0.2mm
- Wall thickness: 1.2mm (3 walls)
- Infill: 20%
- Print speed: 40mm/s (slow for plywood flex)
- Travel speed: 80mm/s

Temperatures:
- PLA: 200°C hotend, 60°C bed
- PETG: 230°C hotend, 80°C bed
- ABS: 240°C hotend, 100°C bed (not recommended on plywood)
```

## Calibration Process

### Step 1: E-steps Calibration
```gcode
; Mark filament 120mm from extruder
M302 P1           ; Allow cold extrusion (testing only)
G91               ; Relative positioning
G1 E100 F100      ; Extrude 100mm
M302 P0           ; Disable cold extrusion

; Measure actual distance extruded
; If only 95mm extruded:
; New E-steps = (100 / 95) * current_steps
; Example: (100/95) * 93 = 98 steps/mm

M92 E98           ; Set new E-steps
M500              ; Save to EEPROM
```

### Step 2: Bed Leveling
```gcode
G28               ; Home all axes
G1 Z0.1           ; Lower to near bed
; Use paper under nozzle
; Adjust bed screws until slight drag on paper
; Check all 4 corners + center
```

### Step 3: First Layer Calibration
- Print single-layer square
- Check squish (filament should be slightly flattened)
- Adjust Z-offset if needed

### Step 4: Temperature Tower
- Print temperature tower model
- Find optimal temperature for your filament
- Adjust slicer profile

## First Print Workflow

1. **Preheat**: M104 S200 (hotend), M140 S60 (bed)
2. **Home**: G28
3. **Level bed**: Manual or mesh bed leveling
4. **Load filament**: Heat hotend, push filament through
5. **Slice model**: Use conservative settings
6. **Start print**: Monitor first layer closely
7. **Watch for issues**: Bed adhesion, warping, layer shifts

## Common 3D Printing Issues

### Poor Bed Adhesion
- Clean bed with IPA (isopropyl alcohol)
- Level bed more carefully
- Increase bed temperature (+5-10°C)
- Slow down first layer (50% speed)
- Apply glue stick or hairspray (if needed)

### Layer Shifting
- Check belt tension (too loose or too tight)
- Reduce acceleration in firmware
- Reduce print speed
- **Likely cause**: Plywood flex under motion forces

### Stringing
- Reduce temperature
- Enable retraction in slicer (4-6mm for Bowden)
- Increase retraction speed

### Warping
- Increase bed temperature
- Add brim or raft in slicer
- Enclose printer (helps with ABS, not for PLA)

### Ringing/Ghosting
- **Expected with plywood frame**
- Reduce acceleration
- Reduce jerk settings
- Add mass to frame (not ideal)
- Upgrade to aluminum extrusion frame

## Maintenance

### Daily (During Active Use)
- [ ] Check bed adhesion before each print
- [ ] Verify hotend temperature stability
- [ ] Clean nozzle tip

### Weekly
- [ ] Clean build plate thoroughly
- [ ] Check belt tension
- [ ] Inspect wiring for damage
- [ ] Grease Z-axis lead screw

### Monthly
- [ ] Re-calibrate E-steps
- [ ] Check bed leveling
- [ ] Inspect hotend for clogs
- [ ] Tighten any loose screws
- [ ] Check driver current settings

## Safety Considerations

- **Fire hazard**: Heated bed + hotend can ignite if fault occurs
- **Thermal runaway protection**: MUST be enabled in Marlin
- **Never leave unattended**: Especially during first few hours
- **Smoke detector**: Install near printer
- **Fire extinguisher**: Keep accessible

### Thermal Runaway Protection (Marlin)
```cpp
#define THERMAL_PROTECTION_HOTENDS
#define THERMAL_PROTECTION_BED
```
This MUST be enabled - it prevents fires if thermistor fails.

## Upgrade Path

### Phase 1: Basic Prints (Weeks 1-4)
- Print simple models (calibration cubes, benchy)
- Learn slicer settings
- Troubleshoot common issues

### Phase 2: Frame Reinforcement (Optional)
- Add aluminum angle brackets
- Install linear rails (MGN12H)
- Dampen vibrations (rubber feet)

### Phase 3: Advanced Features (Optional)
- Auto bed leveling (BLTouch, ~$40)
- Direct drive extruder (better quality)
- All-metal hotend (print high-temp materials)
- Enclosure (for ABS printing)

## Cost Breakdown

| Item | Cost |
|------|------|
| Z-axis mechanics | $40-60 |
| Hotend (E3D V6 clone) | $15-25 |
| Extruder (BMG clone) | $25 |
| Heated bed | $20-40 |
| Build surface | $10-20 |
| Thermistors & wiring | $10 |
| Cooling fans | $10 |
| Power supply upgrade | $25 |
| MOSFET board | $5 |
| Misc (PTFE, wire, etc.) | $15 |
| **Total** | **$175-235** |

## Realistic Assessment

### Pros of This Conversion
- Learn CoreXY 3D printing
- Reuse existing X/Y mechanics
- Lower cost than dedicated printer
- Satisfying DIY project

### Cons of This Conversion
- Plywood frame = quality limitations
- Time investment for troubleshooting
- May need frame rebuild for serious use
- Not competitive with commercial printers

### Bottom Line
**This is a learning platform, not a production machine.**

For serious 3D printing, consider:
- Prusa MK4 (~$800, assembled)
- Bambu Lab P1P (~$600)
- Voron 2.4 (DIY kit, ~$800-1200, aluminum frame)

## Next Steps

- **See**: [04-cnc-mill.md](04-cnc-mill.md) - CNC mill conversion (requires frame rebuild)
- **Or**: Build dedicated 3D printer with aluminum extrusion frame

## Resources

### Firmware
- **Marlin**: [marlinfw.org](https://marlinfw.org/)
- **Marlin Configuration Guide**: Search "Marlin 2.x configuration guide"

### Slicing Software
- **Cura**: [ultimaker.com/software/ultimaker-cura](https://ultimaker.com/software/ultimaker-cura)
- **PrusaSlicer**: [github.com/prusa3d/PrusaSlicer](https://github.com/prusa3d/PrusaSlicer)

### Community
- Reddit: r/3Dprinting
- Marlin Discord
- RepRap forums

### Calibration
- Teaching Tech Calibration: [teachingtechyt.github.io/calibration.html](https://teachingtechyt.github.io/calibration.html)

Good luck! 3D printing is incredibly rewarding but requires patience and troubleshooting. Don't get discouraged by initial failures - every maker goes through them.
