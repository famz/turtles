# Generation 2: Laser Engraver Conversion

**Prerequisites**: Complete [01-pencil-turtle.md](01-pencil-turtle.md) first

**Additional Cost**: ~$100-200 | **Conversion Time**: 1-2 days | **Difficulty**: Intermediate

Convert your pencil turtle into a laser engraver with minimal mechanical changes.

## Why Laser is the Best First Upgrade

- **Minimal mechanical changes**: Just swap the tool head
- **Lightweight**: Laser module weighs less than pen holder
- **CoreXY perfect for laser**: Fast, smooth motion ideal for engraving
- **Dramatic capability increase**: From drawing to cutting and engraving
- **Same motors work great**: NEMA 17 sufficient for laser head

## Additional Parts Needed

### Laser Module & Safety Equipment

#### Laser Module (~$40-120)
- **5.5W Diode Laser** (~$40-60)
  - Engraves wood, leather, cardboard
  - Cuts paper, thin veneer
  - Good starter laser

- **10W+ Diode Laser** (~$80-120)
  - Cuts 3mm plywood
  - Engraves faster and deeper
  - Can handle acrylic
  - **Recommendation**: Start with 5.5W, upgrade later if needed

#### Safety Equipment (REQUIRED, NOT OPTIONAL)
- **Laser safety goggles** (~$15-30)
  - MUST match laser wavelength (typically 445nm for blue diode lasers)
  - OD 4+ rating minimum
  - NEVER operate laser without proper eyewear

- **Emergency stop switch** (~$5)
  - Large red mushroom button
  - Accessible from outside enclosure

- **Fire extinguisher** (~$20)
  - Keep nearby at all times
  - ABC-rated for multiple fire types

#### Enclosure Materials (~$30-50)
- Black MDF or plywood for walls
- Acrylic or polycarbonate viewing window (orange tinted for laser protection)
- Magnetic door interlocks
- Exhaust fan (120mm PC fan, ~$10)
- Flexible ducting for ventilation

#### Miscellaneous
- PWM-controlled laser driver (usually included with laser module)
- Air assist pump (optional, aquarium pump ~$15)
- Smoke/fume extraction (critical for indoor use)

**Total Additional Cost: ~$100-200**

## Conversion Process

### Step 1: Remove Pen Holder
- [ ] Remove servo and pen holder assembly
- [ ] Keep servo for future use (or use for laser Z-focus)
- [ ] Clean X-carriage mounting area

### Step 2: Mount Laser Module
- [ ] Design/cut laser mount bracket (1/4" plywood or 3D print)
- [ ] Laser should point straight down
- [ ] Ensure laser focal point at correct height (typically 10-20mm from bed)
- [ ] Mount securely to X-carriage
- [ ] Route laser power wires carefully (avoid belt interference)

### Step 3: Wiring

#### Laser PWM Control
- [ ] Connect laser PWM wire to Arduino **pin D4** (CNC Shield SpnEn pin)
- [ ] Connect laser GND to Arduino GND
- [ ] Connect laser 12V to power supply (may need separate power connection)

#### Emergency Stop
- [ ] Wire emergency stop in series with laser power
- [ ] Must cut power to laser immediately when pressed

### Step 4: Firmware Update

#### Flash GRBL Firmware
GRBL is the standard CNC/laser firmware, replacing your custom turtle firmware.

```bash
# Download GRBL 1.1h (supports laser mode)
# Use Arduino IDE to flash grbl firmware to Arduino Mega
```

#### GRBL Configuration
```
$30=1000    # Maximum spindle speed (laser PWM max)
$31=0       # Minimum spindle speed
$32=1       # Laser mode enable (important!)
```

**Laser Mode ($32=1)**:
- Turns off laser during rapid moves (G0)
- Varies laser power during curves (dynamic power)
- CRITICAL for safety and quality

### Step 5: Build Safety Enclosure

#### Enclosure Design
```
Dimensions: 500mm W x 500mm D x 300mm H
- Black interior (absorbs stray reflections)
- Viewing window (orange/amber tinted)
- Magnetic door interlock (kills laser when opened)
- Exhaust fan + ducting to outside
```

#### Critical Safety Features
- [ ] Laser CANNOT operate when door is open
- [ ] Emergency stop accessible from outside
- [ ] Viewing window protects against laser exposure
- [ ] Fume extraction vents to outside (NOT indoors)
- [ ] Fire-resistant bed material (aluminum plate)

### Step 6: Software Setup

#### G-code Senders
Choose one:
- **LightBurn** ($60, best for laser, highly recommended)
- **LaserGRBL** (free, Windows only)
- **bCNC** (free, cross-platform)
- **UGS (Universal Gcode Sender)** (free, cross-platform)

#### First Test (SAFETY CRITICAL)
```gcode
; Test pattern - 10mm square at 10% power
M3 S100       ; Turn laser on at 10% power
G1 X10 F1000  ; Move right 10mm
G1 Y10        ; Move forward 10mm
G1 X0         ; Move left 10mm
G1 Y0         ; Move back to origin
M5            ; Turn laser off
```

### Step 7: Focus and Calibration

#### Focus Laser
- [ ] Use focal point gauge (usually included with laser)
- [ ] Typical focal distance: 10-20mm from laser lens to material
- [ ] Adjust Z-height of material bed or laser mount

#### Power Calibration
Test on scrap wood:
- 10% power: Light marking
- 25% power: Medium engraving
- 50% power: Deep engraving
- 100% power: Cutting (multiple passes)

#### Speed Calibration
- Fast (3000 mm/min): Light engraving
- Medium (1500 mm/min): Standard engraving
- Slow (300-600 mm/min): Cutting

## Operating the Laser Engraver

### Workflow

1. **Design**: Create vector artwork (Inkscape, Adobe Illustrator)
2. **Import**: Load into LightBurn or LaserGRBL
3. **Set Parameters**: Power, speed, number of passes
4. **Position**: Use laser pointer or low-power mode to frame
5. **Focus**: Ensure correct focal distance
6. **Run**: Put on safety goggles, close enclosure, start job
7. **Monitor**: Watch for smoke/fire, never leave unattended

### Material Guidelines

#### Safe Materials
- ✅ Wood (pine, birch, plywood)
- ✅ Cardboard, paper
- ✅ Leather (real, not synthetic)
- ✅ Cork
- ✅ Anodized aluminum (engraving only)
- ✅ Acrylic (laser-safe, NOT all types)

#### DANGEROUS Materials (NEVER USE)
- ❌ PVC (releases chlorine gas - toxic)
- ❌ Vinyl (chlorine gas)
- ❌ ABS plastic (toxic fumes)
- ❌ Polycarbonate (discolors, catches fire)
- ❌ Fiberglass (releases particles)
- ❌ Any foam with embedded metal

## Example Projects

### Beginner Projects
1. **Wooden coasters** - Simple engraving practice
2. **Leather wallet** - Personalization
3. **Cardboard stencils** - Precise cutting
4. **Photo engraving on wood** - Grayscale lithophane

### Intermediate Projects
1. **Cutting plywood boxes** - Multiple passes, precise joints
2. **Acrylic signs** - Engraving and edge-lit effects
3. **Custom PCB stencils** - Mylar or thin plastic
4. **Leather bags** - Complex patterns

## Safety Checklist (Before Every Use)

- [ ] Safety goggles on (correct wavelength)
- [ ] Enclosure closed and interlocked
- [ ] Emergency stop accessible
- [ ] Fire extinguisher nearby
- [ ] Ventilation running (fumes exhausting outside)
- [ ] Material is laser-safe (check list above)
- [ ] No flammable materials near laser path
- [ ] Someone knows you're operating laser (don't work alone)

## Troubleshooting

### Laser won't turn on
- Check PWM connection to pin D4
- Verify GRBL laser mode enabled ($32=1)
- Test with M3 S500 command (50% power)

### Inconsistent engraving
- Check belt tension
- Verify focus distance
- Clean laser lens
- Slow down feedrate

### Smoke/flames during cutting
- Normal for wood, but monitor closely
- Add air assist (blows smoke away from cut)
- Reduce power or increase speed
- Ensure ventilation working

### Blurry or wide lines
- Laser out of focus
- Lens dirty (clean with lens cleaner)
- Belt slack causing vibration

## Maintenance

### After Each Use
- [ ] Clean laser lens (microfiber + lens cleaner)
- [ ] Vacuum out debris from bed
- [ ] Check for scorch marks or fire damage

### Weekly
- [ ] Clean ventilation fan and ducts
- [ ] Inspect belts and pulleys
- [ ] Check emergency stop functionality

### Monthly
- [ ] Deep clean enclosure interior
- [ ] Inspect laser module mounting
- [ ] Test door interlock
- [ ] Calibrate power output (compare test burns)

## Firmware: GRBL Quick Reference

### Common Commands
```gcode
M3 S1000    ; Laser ON at 100% power (S0-1000)
M5          ; Laser OFF
G0 X10 Y10  ; Rapid move (laser off automatically in laser mode)
G1 X20 F500 ; Linear move at 500mm/min (laser on)
$I          ; View GRBL info
$$          ; View all settings
$30=1000    ; Set max laser power
$32=1       ; Enable laser mode
```

### Homing (if limit switches installed)
```gcode
$H          ; Home all axes
```

## Cost Breakdown

| Item | Cost |
|------|------|
| 5.5W Laser module | $40-60 |
| Safety goggles | $15-30 |
| Enclosure materials | $30-50 |
| Emergency stop | $5 |
| Fire extinguisher | $20 |
| Ventilation fan | $10 |
| Air assist (optional) | $15 |
| **Total** | **$135-190** |

**LightBurn Software** (optional): $60 (recommended, very worth it)

## Next Steps

After mastering laser engraving:

- **See**: [03-3d-printer.md](03-3d-printer.md) - Add Z-axis for 3D printing (~$150-250)
- **Or**: Keep laser setup and build separate machine for 3D printing

## Resources

### Software
- **LightBurn**: [lightburnsoftware.com](https://lightburnsoftware.com/)
- **LaserGRBL**: [lasergrbl.com](https://lasergrbl.com/)
- **GRBL Firmware**: [github.com/gnea/grbl](https://github.com/gnea/grbl)

### Safety
- OSHA Laser Safety: Search "OSHA laser safety guidelines"
- Laser Safety Goggles Guide: Search "laser safety OD rating calculator"

### Community
- Reddit: r/lasercutting
- Facebook: "Laser Engraver Owners Group"
- YouTube: "Maker's Muse Laser Safety"

### Material Testing
- Test on scrap first ALWAYS
- Keep material database with power/speed settings
- Document everything (helps troubleshoot later)

**REMEMBER**: Lasers are NOT toys. They can cause permanent eye damage in milliseconds and start fires. Always prioritize safety over convenience.
