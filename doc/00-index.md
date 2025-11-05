# Turtle Drawing Machine: 4-Generation Evolution

A modular plywood-based CNC platform that evolves from drawing machine to laser engraver, 3D printer, and beyond.

## Overview

This project is designed as an **expandable platform** using industry-standard components (Arduino Mega + CNC Shield V3) that can grow with your skills and needs.

**Key Philosophy**:
- Start simple (drawing machine)
- Learn motion control fundamentals
- Expand capabilities incrementally
- Reuse electronics across generations

## The Four Generations

### [Generation 1: Pencil Turtle](01-pencil-turtle.md)
**Cost**: ~$217-269 | **Time**: 4 weeks | **Difficulty**: ⭐⭐☆☆☆

A plywood-based 2-axis drawing machine with Python turtle interface.

**What You Build**:
- CoreXY mechanism
- 300x300mm work area
- Arduino Mega + CNC Shield V3
- NEMA 17 motors
- Python turtle API

**What You Learn**:
- Motion control basics
- Stepper motor tuning
- Belt tensioning
- CoreXY kinematics
- Serial communication

**Start here**: [01-pencil-turtle.md](01-pencil-turtle.md)

---

### [Generation 2: Laser Engraver](02-laser.md)
**Additional Cost**: ~$100-200 | **Time**: 1-2 days | **Difficulty**: ⭐⭐⭐☆☆

**Easiest upgrade path**: Swap pen for laser module.

**What You Add**:
- 5-10W diode laser
- GRBL firmware
- Safety equipment (goggles, enclosure)
- Fume extraction

**What You Learn**:
- GRBL configuration
- Laser safety protocols
- G-code senders
- Material testing
- Power/speed relationships

**Capabilities**:
- Engrave wood, leather, cardboard
- Cut thin plywood (3mm)
- Create custom signs and artwork
- PCB stencils

**Prerequisites**: Complete Gen 1

**Start here**: [02-laser.md](02-laser.md)

---

### [Generation 3: 3D Printer](03-3d-printer.md)
**Additional Cost**: ~$150-250 | **Time**: 2-3 weeks | **Difficulty**: ⭐⭐⭐⭐☆

Add Z-axis, hotend, and heated bed for 3D printing.

**What You Add**:
- Z-axis with lead screw
- E3D hotend
- Heated bed
- Extruder motor
- Marlin firmware

**What You Learn**:
- Marlin configuration
- PID tuning
- Slicing software
- 3D printing troubleshooting
- Temperature control

**Capabilities**:
- Print PLA, PETG, ABS
- ~200x200x250mm build volume
- Functional prototypes
- Custom parts

**Reality Check**:
⚠️ Plywood frame may limit print quality (ringing/ghosting). Consider frame reinforcement or dedicated printer build.

**Prerequisites**: Complete Gen 1

**Start here**: [03-3d-printer.md](03-3d-printer.md)

---

### [Generation 4: CNC Mill](04-cnc-mill.md)
**Cost**: ~$400-800 | **Time**: 4-6 weeks | **Difficulty**: ⭐⭐⭐⭐⭐

**⚠️ REQUIRES FRAME REBUILD**: Plywood NOT suitable for milling.

**What You Actually Build**:
- New aluminum extrusion frame
- Linear rails (MGN15)
- NEMA 23 motors
- Spindle motor (500W-1kW)
- Ball screws

**What You Reuse**:
- Arduino Mega + CNC Shield V3
- Stepper drivers (may need upgrade)
- Electronics knowledge

**What You Learn**:
- Mechanical rigidity requirements
- Spindle control (VFD)
- CAM software (Fusion 360)
- Feeds and speeds
- Work holding

**Capabilities**:
- Mill wood, MDF, plastics
- Light aluminum work
- PCB milling
- Custom enclosures

**Honest Recommendation**:
Build dedicated CNC (MPCNC, Shapeoko) instead of "converting". Plywood frame is fundamentally incompatible with milling forces.

**Prerequisites**: Understand Gen 1 limitations

**Start here**: [04-cnc-mill.md](04-cnc-mill.md)

---

## Recommended Build Path

### Path A: Drawing → Laser (Recommended for Most)
1. Build Gen 1 (pencil turtle) - Learn fundamentals
2. Add Gen 2 (laser) - Minimal changes, huge capability gain
3. Keep using laser for projects

**Total investment**: ~$317-469
**Time**: 5 weeks
**Result**: Versatile laser engraver with drawing capabilities

---

### Path B: Drawing → 3D Printing
1. Build Gen 1 (pencil turtle)
2. **Optional**: Add Gen 2 (laser) for learning
3. Add Gen 3 (3D printer) with frame reinforcement

**Total investment**: ~$367-519 (or ~$467-719 with laser)
**Time**: 6-7 weeks
**Result**: Budget 3D printer (with quality limitations)

**Alternative**: Build dedicated 3D printer (Prusa, Voron)

---

### Path C: Ultimate DIY Journey
1. Build Gen 1 (pencil turtle) - Learn fundamentals
2. Add Gen 2 (laser) - Expand capabilities
3. Build separate Gen 4 (CNC mill) - Dedicated machine
4. **Optional**: Build separate Gen 3 (3D printer) - Dedicated machine

**Total investment**: ~$1,100-1,800
**Time**: 12-16 weeks
**Result**: Complete maker workshop (drawing, laser, CNC, 3D printing)

---

## Why This Platform Design?

### Arduino Mega + CNC Shield V3
- **Industry standard**: Used in GRBL CNC, Marlin 3D printers
- **Expandable**: 4-axis support (X, Y, Z, A/E)
- **Well-documented**: Massive community
- **Firmware options**: GRBL, Marlin, or custom
- **Affordable**: ~$20-30 total

### CoreXY Mechanism
- **Fast**: Both motors stationary (low moving mass)
- **Accurate**: Good for laser and drawing
- **Scalable**: Easy to make larger
- **Educational**: Learn kinematics

### Modular Tool Head
- Easy to swap between pen, laser, extruder
- Quick-change system possible
- Encourages experimentation

## Common Components Across All Generations

**Electronics** (Buy once, use in all generations):
- Arduino Mega 2560
- CNC Shield V3
- DRV8825 stepper drivers
- 12V power supply (may need upgrade for Gen 3/4)

**Mechanical** (Gen 1 → Gen 2 reuse):
- Frame, motors, belts, pulleys
- Linear motion system
- CoreXY belt routing

**Skills** (Build progressively):
- Gen 1: Motion control, Python, Arduino basics
- Gen 2: GRBL, laser safety, G-code
- Gen 3: Marlin, temperature control, 3D printing
- Gen 4: Rigidity, CAM, machining theory

## What Tools You Need

**Essential Woodworking**:
- Table saw or circular saw
- Drill press (or hand drill + patience)
- Measuring tape, square
- Clamps
- Sandpaper

**Essential Electronics**:
- Soldering iron (for occasional connections)
- Multimeter
- Wire strippers
- Screwdrivers, hex keys

**Software**:
- Arduino IDE (free)
- Python (free)
- GRBL sender (free)
- CAM software (Fusion 360 free for hobbyists)

## Budget Summary

| Generation | Incremental Cost | Total Cost |
|------------|-----------------|------------|
| Gen 1: Pencil Turtle | $217-269 | $217-269 |
| Gen 2: Laser (+Gen 1) | +$100-200 | $317-469 |
| Gen 3: 3D Printer (+Gen 1) | +$150-250 | $367-519 |
| Gen 4: CNC Mill (rebuild) | ~$800-1,300 | $800-1,300 |

## Safety First

Each generation has specific safety requirements:

**Gen 1 (Drawing)**: Basic electrical safety
**Gen 2 (Laser)**: Eye protection (CRITICAL), fire safety, fume extraction
**Gen 3 (3D Printer)**: Fire risk (heated bed/hotend), thermal runaway protection
**Gen 4 (CNC Mill)**: Flying chips, noise, dust, spindle danger

**Always**:
- Wear appropriate PPE
- Never bypass safety features
- Keep fire extinguisher accessible
- Don't leave machines unattended

## Getting Started

Ready to begin? Start with Generation 1:

**→ [01-pencil-turtle.md](01-pencil-turtle.md)**

This will teach you the fundamentals and give you a working platform to expand from.

## Community & Support

### Resources
- **GRBL**: [github.com/gnea/grbl](https://github.com/gnea/grbl)
- **Marlin**: [marlinfw.org](https://marlinfw.org/)
- **Arduino**: [arduino.cc](https://arduino.cc)

### Forums
- Reddit: r/hobbycnc, r/lasercutting, r/3Dprinting
- Arduino forums
- RepRap forums

### YouTube Channels
- Teaching Tech (3D printing, calibration)
- NYC CNC (machining fundamentals)
- Maker's Muse (general making)

## FAQ

**Q: Can I skip Gen 1 and go straight to Gen 2/3/4?**
A: Technically yes, but Gen 1 teaches critical fundamentals. The $217 investment in learning is worth it.

**Q: NEMA 17 or NEMA 23 motors?**
A:
- **Gen 1 & 2 (Drawing/Laser)**: NEMA 17 perfect (lightweight tool head)
- **Gen 3 (3D Printer)**: NEMA 17 works well
- **Gen 4 (CNC Mill)**: NEMA 23 required (cutting forces much higher)

Starting with NEMA 23 adds ~$30-40 and no real benefit for Gen 1/2. Save money, learn with NEMA 17, upgrade when needed.

**Q: How long does each generation take to build?**
A:
- Gen 1: 4 weeks (if building weekends)
- Gen 2: 1-2 days (conversion)
- Gen 3: 2-3 weeks (mechanical + tuning)
- Gen 4: 4-6 weeks (essentially new machine)

**Q: What if I only want [laser/3D printer/CNC]?**
A: You can build Gen 1 and jump to your target, but Gen 1 is the best learning platform. It's forgiving, cheap, and teaches fundamentals you'll use in later gens.

**Q: Is the plywood frame strong enough?**
A:
- ✅ Gen 1 (Drawing): Yes
- ✅ Gen 2 (Laser): Yes (lightweight laser head)
- ⚠️ Gen 3 (3D Printer): Marginal (may need reinforcement)
- ❌ Gen 4 (CNC Mill): No (frame rebuild required)

**Q: Can I use [different controller/motors/etc]?**
A: Sure! This guide uses proven, affordable components. You can substitute, but you'll need to adapt instructions.

---

Good luck with your build journey! Start with Gen 1 and work your way up. Each generation teaches new skills while building on what you've learned.

**Happy making! 🛠️**
