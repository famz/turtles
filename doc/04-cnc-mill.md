# Generation 4: CNC Mill Conversion

**Prerequisites**: Understand [01-pencil-turtle.md](01-pencil-turtle.md) limitations

**Additional Cost**: ~$400-800 | **Rebuild Time**: 4-6 weeks | **Difficulty**: Expert

**⚠️ IMPORTANT**: This is essentially building a new machine. Plywood frame is NOT suitable for milling operations.

## Reality Check: Why This is NOT a Simple Conversion

### Plywood Frame Problems for CNC Milling
- **Insufficient rigidity**: Plywood flexes under cutting forces
- **Chatter**: Vibration ruins surface finish and damages tools
- **Accuracy**: Frame flex = dimensional inaccuracy
- **Safety**: Unexpected tool movement is dangerous

### What "Conversion" Actually Means
You're keeping:
- Arduino Mega + CNC Shield V3 ✅
- Stepper drivers ✅
- Power supply (may need upgrade)
- GRBL firmware concept ✅

You're replacing:
- **EVERYTHING ELSE** ❌

### Honest Recommendation
**Build a dedicated CNC mill** using proven designs:
- **MPCNC (Mostly Printed CNC)** - ~$400, good for wood/aluminum
- **Shapeoko** - ~$1200-2400, commercial quality
- **X-Carve** - ~$1500-3000, good community
- **Custom aluminum extrusion build** - ~$600-1200

These designs solve the rigidity problem from the ground up.

## If You Insist on Converting: Full Rebuild Plan

### Frame Rebuild (~$200-300)

#### Materials
- **2020 Aluminum Extrusion** (15-20 meters, ~$150-200)
- **Corner brackets** (20-30pcs, ~$20)
- **T-nuts and M5 bolts** (100+ pcs, ~$15)
- **Angle brackets** (10-15pcs, ~$15)
- **Gantry plates** (aluminum 6mm, ~$40)

#### Design Requirements
- Triangulated frame (no cantilevers)
- Bolted joints (not wood screws)
- Heavy base (mass dampens vibration)
- Rigid gantry (no plywood)

### Motion System Upgrade (~$150-250)

#### Linear Rails (Required)
- **MGN15H or HGR15** linear rails (4x, ~$100-150)
- Much stiffer than rods
- Lower friction
- Better accuracy

#### Ball Screws (Optional, Better)
- Replace GT2 belts with ball screws (~$80-120)
- Zero backlash
- Better for milling forces
- Slower but more accurate

### Motors & Drivers (~$80-120)

#### NEMA 23 Motors (Required)
- 3x NEMA 23 (X, Y, Z, ~$60-90)
- Higher torque for cutting forces
- NEMA 17 will stall under load

#### Driver Upgrade (May Be Needed)
- CNC Shield V3 DRV8825 can handle NEMA 23 (2.5A)
- May need external drivers (TB6600, ~$30-40) for higher current

### Spindle System (~$80-200)

#### Options

**Budget: Trim Router** (~$50-80)
- DeWalt DW660 or similar
- 1/8" collets
- ~30,000 RPM
- Good for wood, soft plastics
- Loud!

**Better: Spindle Motor** (~$100-150)
- 500W-1kW ER11 spindle
- Variable speed (VFD controlled)
- Water or air cooled
- Quieter than router
- Better for aluminum

#### VFD (Variable Frequency Drive) (~$30-60)
- Controls spindle speed
- PWM control from Arduino (pin D11)
- 110V or 220V input

### Z-Axis (~$80-120)

#### Requirements
- 150-200mm travel
- Very rigid (takes all cutting forces)
- Ball screw recommended (lead screw acceptable)

#### Components
- Linear rails (2x MGN15H, ~$40)
- Ball screw (1605 or 1610, ~$30)
- NEMA 23 motor (~$20)
- Z-carriage plate (aluminum, custom cut)

### Work Holding (~$40-80)

#### Bed
- Aluminum plate (10mm thick, ~$40)
- T-track or T-slot for clamping
- Wasteboard (MDF, replaceable)

#### Clamps
- T-track clamps (~$20)
- Toe clamps (~$10)
- Vise (optional, ~$50-100)

### Dust Collection (~$50-100)

#### Requirements
- CNC milling generates TONS of dust/chips
- Dust everywhere without collection
- Health hazard (silica dust from MDF)

#### System
- Shop vac (~$40-60)
- Dust shoe/shroud (~$20, 3D print or buy)
- Hose and fittings (~$10)

### Electronics Additions (~$30-50)

#### Spindle Control
- Relay or SSR to turn router on/off (~$10)
- VFD for variable speed spindle (~$30-60)

#### Emergency Stop
- Large mushroom button (~$5-10)
- Cuts power immediately

#### Enclosure (Highly Recommended)
- Contains noise, dust, and chips
- MDF or plywood walls (~$50-100)
- Clear viewing window (~$20)

## Assembly Process

### Phase 1: Frame Construction (Weeks 1-2)
- [ ] Design frame in CAD (Fusion 360, OnShape)
- [ ] Cut aluminum extrusion to length
- [ ] Assemble base frame (use square for accuracy)
- [ ] Build Y-axis gantry
- [ ] Install linear rails on all axes
- [ ] Verify squareness (critical for accuracy)

### Phase 2: Motion System (Week 3)
- [ ] Install X-axis linear rails on gantry
- [ ] Install Y-axis rails on base
- [ ] Install Z-axis rails on X-carriage
- [ ] Mount ball screws (if using)
- [ ] Couple motors to screws (rigid couplers)
- [ ] Test motion (should be smooth, zero binding)

### Phase 3: Spindle Mount (Week 4)
- [ ] Design Z-carriage with spindle mount
- [ ] Mount spindle securely
- [ ] Add dust shoe around spindle
- [ ] Wire spindle (VFD or relay)
- [ ] Test spindle at various speeds

### Phase 4: Electronics (Week 5)
- [ ] Mount Arduino + CNC Shield
- [ ] Wire NEMA 23 motors
- [ ] Set driver current (2-3A for NEMA 23)
- [ ] Wire spindle control
- [ ] Add emergency stop
- [ ] Add limit switches (homing required for CNC)

### Phase 5: Calibration & Testing (Week 6)
- [ ] Flash GRBL firmware
- [ ] Set steps/mm for each axis
- [ ] Tune acceleration/jerk
- [ ] Run air cuts (no material)
- [ ] Test with foam or soft wood
- [ ] Graduate to hardwood
- [ ] Finally test aluminum (if needed)

## GRBL Configuration for CNC

### Key Settings
```
$100=200    ; X steps/mm (depends on ball screw pitch)
$101=200    ; Y steps/mm
$102=200    ; Z steps/mm

$110=2000   ; X max rate (mm/min)
$111=2000   ; Y max rate
$112=500    ; Z max rate (slower for Z)

$120=250    ; X acceleration (mm/sec^2)
$121=250    ; Y acceleration
$122=100    ; Z acceleration (slower)

$20=1       ; Soft limits (enable)
$21=1       ; Hard limits (enable, requires limit switches)
$22=1       ; Homing cycle (enable)

$30=24000   ; Max spindle speed (RPM)
$31=0       ; Min spindle speed
$32=0       ; Laser mode (disable for CNC)
```

## CAM Software (Toolpath Generation)

### What is CAM?
CAM (Computer-Aided Manufacturing) converts 3D models into G-code toolpaths.

### Recommended CAM Software

**Free Options**:
1. **Fusion 360** (free for hobbyists)
   - Integrated CAD + CAM
   - Industry standard
   - Excellent toolpath generation
   - Steep learning curve

2. **FreeCAD + Path Workbench** (free, open-source)
   - Fully free
   - Learning curve
   - Active community

**Paid Options**:
1. **VCarve** (~$350-700)
   - Very popular in hobbyist CNC
   - Easy to learn
   - 2.5D machining focus

2. **Carbide Create** (free) + Carbide Create Pro ($180)
   - Simple interface
   - Good for Shapeoko/Nomad

### Basic CAM Workflow
1. Import 3D model (STL, STEP)
2. Set up stock material
3. Choose cutting tools
4. Generate toolpaths (roughing, finishing)
5. Simulate (catch errors before cutting)
6. Post-process to G-code
7. Load into GRBL sender (bCNC, UGS, CNCjs)

## Cutting Parameters

### Speeds and Feeds (Critical for Success)

#### Chipload Formula
```
Chipload = Feedrate / (RPM × Number_of_Flutes)

Example for 1/8" 2-flute endmill in wood:
- RPM: 18,000
- Feedrate: 1000 mm/min
- Chipload: 1000 / (18000 × 2) = 0.028mm (good for wood)
```

#### Material Guidelines

**Softwood (Pine)**:
- Endmill: 1/8" 2-flute
- RPM: 18,000
- Feedrate: 1000-1500 mm/min
- Depth of cut: 3-5mm

**Hardwood (Oak, Maple)**:
- Endmill: 1/8" 2-flute
- RPM: 18,000
- Feedrate: 800-1200 mm/min
- Depth of cut: 2-3mm

**MDF**:
- Endmill: 1/8" or 1/4" up-cut spiral
- RPM: 18,000-24,000
- Feedrate: 1500-2000 mm/min
- Depth of cut: 4-6mm (takes very aggressive cuts)

**Aluminum (6061)**:
- Endmill: 1/8" 2-flute carbide
- RPM: 12,000-15,000
- Feedrate: 400-600 mm/min
- Depth of cut: 0.5-1mm (many passes)
- **Coolant/lubrication required**

### Climb vs Conventional Milling
- **Climb milling**: Cutter moves with feedrate direction (better finish)
- **Conventional milling**: Cutter moves against feedrate (safer for rigid machines)
- Use climb milling for better surface finish

## Safety (CRITICAL)

### Before Every Cut
- [ ] Safety glasses (flying chips)
- [ ] Hearing protection (routers are LOUD)
- [ ] Dust mask or respirator (MDF/aluminum dust hazardous)
- [ ] Secure all clamps (loose workpiece = dangerous projectile)
- [ ] Check tool tightness in collet
- [ ] Clear work area of loose objects
- [ ] Emergency stop accessible

### During Operation
- [ ] Never reach into cut area while spindle running
- [ ] Keep hands away from collet/bit
- [ ] Watch for tool breakage (stop immediately)
- [ ] Monitor for fires (friction can ignite dust)
- [ ] Never leave machine unattended

### Tool Breakage
- Broken endmills become shrapnel
- Causes: wrong feeds/speeds, dull tool, crash
- Prevention: conservative settings, proper speeds

## Maintenance

### After Each Use
- [ ] Vacuum all chips and dust
- [ ] Clean linear rails (blow off dust)
- [ ] Check tool for damage
- [ ] Inspect work holding

### Weekly
- [ ] Lubricate linear rails (light oil)
- [ ] Grease ball screws
- [ ] Check belt tension (if using belts)
- [ ] Inspect spindle mount for vibration loosening

### Monthly
- [ ] Re-tram spindle (check perpendicularity)
- [ ] Check all frame bolts for tightness
- [ ] Calibrate steps/mm
- [ ] Sharpen or replace dull endmills

## Troubleshooting

### Chatter (Vibration Lines)
- Reduce depth of cut
- Increase feedrate (sometimes)
- Reduce spindle RPM
- Sharpen tool
- Increase machine rigidity (add mass)

### Inaccurate Cuts
- Check belt tension
- Verify steps/mm calibration
- Check work holding (part moving?)
- Measure repeatability (return to zero test)

### Tool Breakage
- Too aggressive depth/feedrate
- Dull tool (replace)
- Crash (operator error)

### Motor Stalling
- Cutting forces too high
- Reduce depth/feedrate
- Upgrade to NEMA 23 (if not already)
- Check driver current setting

## Cost Breakdown (Full Rebuild)

| Category | Cost |
|----------|------|
| Aluminum extrusion frame | $200-300 |
| Linear rails (MGN15) | $100-150 |
| Ball screws (optional) | $80-120 |
| NEMA 23 motors (3x) | $60-90 |
| Spindle (500W-1kW) | $100-150 |
| VFD controller | $30-60 |
| Z-axis components | $80-120 |
| Work holding & bed | $40-80 |
| Dust collection | $50-100 |
| Endmills & tooling | $50-100 |
| Miscellaneous | $50-100 |
| **Total** | **$840-1,370** |

**Reuse from Gen 1**:
- Arduino Mega + CNC Shield (~$25 saved)
- Power supply (may need upgrade)
- Stepper drivers (~$6 saved)

**Effective new cost: ~$800-1,300**

## Alternative: Dedicated CNC Designs

### MPCNC (Mostly Printed CNC) - ~$400
**Pros**:
- Well-documented build
- Large community
- Parts available as kits
- Can cut wood, soft aluminum

**Cons**:
- Slower than commercial machines
- Some printed parts wear over time

### Shapeoko 4 - ~$1,500-2,400
**Pros**:
- Commercial quality
- Excellent support
- Carbide 3D ecosystem
- Ready to cut out of box

**Cons**:
- Expensive
- Limited customization

### Custom Aluminum Extrusion Build - ~$600-1,200
**Pros**:
- Fully customizable
- Can scale to any size
- Proven design patterns available
- Very rigid

**Cons**:
- Requires CAD skills
- More planning needed
- No single BOM to follow

## Bottom Line

**Do NOT try to mill on the plywood turtle frame.**

Instead:
1. Keep Gen 1 (pencil turtle) as-is
2. Add Gen 2 (laser) to Gen 1 (easy conversion)
3. Build dedicated CNC mill from scratch (MPCNC or custom)
4. Reuse Arduino + CNC Shield + drivers from Gen 1 if desired

**Time investment**:
- Plywood conversion (inevitably fails): 4-6 weeks + frustration
- MPCNC build: 3-4 weeks + working machine
- Custom build: 4-8 weeks + optimized machine

**Choose wisely.**

## Resources

### Designs
- **MPCNC**: [v1engineering.com](https://www.v1engineering.com/)
- **Shapeoko Community**: [community.carbide3d.com](https://community.carbide3d.com/)
- **OpenBuilds**: [openbuilds.com](https://openbuilds.com/)

### CAM Software
- **Fusion 360**: [autodesk.com/products/fusion-360](https://www.autodesk.com/products/fusion-360)
- **VCarve**: [vectric.com](https://www.vectric.com/)

### Community
- **CNCZone Forums**: [cnczone.com](https://www.cnczone.com/)
- Reddit: r/hobbycnc
- YouTube: NYC CNC (excellent tutorials)

### Safety
- **Machinery's Handbook** (machining reference bible)
- OSHA Machinery Safety Guidelines

Good luck, and remember: **Rigidity is king in CNC milling.** Don't compromise on the frame.
