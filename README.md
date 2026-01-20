# SELFiSSH - Solar-Powered Data Acquisition System

<details open>
<summary> <b>Brief Review</b></summary>

**SELFiSSH** (Self-Contained, Low-power, Flexible, Intelligent Sampling and Storage Hardware) is a solar-powered, self-contained data acquisition and logging system designed for environmental monitoring and remote sensing applications. This hardware project includes complete Eagle CAD schematics, PCB board layouts, Gerber manufacturing files, and a comprehensive bill of materials.

The system features an ATmega168 microcontroller running at 11.0592 MHz, integrated solar charging capability with LiPo battery backup, RS-232 serial communication, and innovative daisy-chaining connectors that allow multiple units to be networked together. The power management system uses a BQ24202 charger IC to intelligently manage power from both solar and battery sources.

**Key capabilities:**
- Solar-powered with battery backup (3.7V LiPo)
- Autonomous operation with minimal external infrastructure
- Modular daisy-chain architecture for distributed sensor networks
- Comprehensive power management and conditioning
- Multiple communication interfaces (RS-232, inter-unit daisy-chain)

Below you can see the PCB design visualization:

<p align="center">
<img src = "eagleUp/eagleUp_SELFiSSH_board_top.png?raw=true" width="45%"/>
<img src = "eagleUp/eagleUp_SELFiSSH_board_bottom.png?raw=true" width="45%"/>
</p>

<p align="center">
<img src = "eagleUp/SELFiSSH.png?raw=true" width="60%"/>
</p>

</details>

<details open>
<summary> <b>Project Structure</b></summary>

The project is organized into several key directories and files:

```
SELFiSSH/
├── SELFiSSH.sch              # Main schematic file (Eagle CAD)
├── SELFiSSH.brd              # PCB board layout file (Eagle CAD)
├── CLAUDE.md                 # Claude Code guidance document
├── eagle.epf                 # Eagle project settings
│
├── BOM/
│   └── SELFiSSH.bom          # Bill of Materials (component list)
│
├── Gerbers/                  # Manufacturing files for PCB production
│   ├── SELFiSSH.GTL          # Top copper layer
│   ├── SELFiSSH.GBL          # Bottom copper layer
│   ├── SELFiSSH.GTS          # Top solder mask
│   ├── SELFiSSH.GBS          # Bottom solder mask
│   ├── SELFiSSH.GTO          # Top silkscreen
│   ├── SELFiSSH.GBO          # Bottom silkscreen
│   ├── SELFiSSH.GML          # Milling/edge cuts
│   ├── SELFiSSH.dri          # Drill file
│   ├── SELFiSSH.gpi          # Pick and place
│   └── SELFiSSH.TXT          # Manufacturing notes
│
├── eagleUp/                  # 3D renderings and visualizations
│   ├── eagleUp_SELFiSSH_board_top.png
│   ├── eagleUp_SELFiSSH_board_bottom.png
│   ├── eagleUp_SELFiSSH_top_silk.png
│   ├── eagleUp_SELFiSSH_bottom_silk.png
│   ├── SELFiSSH.png
│   └── SEL-FiSSH.skp         # SketchUp 3D model
│
└── [Archived versions]       # SELFiSH.s#*, SELFiSH.b#*, etc.
    # (Previous design iterations managed by Eagle)
```

</details>

<details open>
<summary> <b>Hardware Architecture</b></summary>

### System Overview

SELFiSSH is built around an ATmega168 microcontroller and is designed as a modular, expandable data acquisition platform. The system architecture emphasizes low power consumption, autonomous operation, and network scalability through daisy-chaining.

### Core Components

| Component | Model | Function |
|-----------|-------|----------|
| **Microcontroller** | ATmega168 | 8-bit processing and data acquisition |
| **Oscillator** | 11.0592 MHz Crystal | Timing reference (standard UART baud rate divisor) |
| **Charger IC** | BQ24202 | Solar/battery power management |
| **Communication** | RS-232 Level Shifter | Serial PC interface via DB9 connector |
| **Power Input** | 5.5V Barrel Jack | External DC power option |
| **Solar Input** | 5.5V JST Connector | Solar panel charging |
| **Battery** | 3.7V LiPo (JST) | Primary energy storage |

### Functional Blocks

**Power Management System**
- Solar input regulation (5.5V input via SOLAR connector)
- Battery charging management (BQ24202 charger IC with intelligent priority switching)
- Multiple decoupling capacitors (0.1µF, 1µF, 10µF, 4.7µF) for supply stability
- Ferrite beads filtering for noise suppression
- Battery backup via 3.7V LiPo (BATT connector)

**Communication Interface**
- RS-232 level shifter subcircuit (provides PC connectivity)
- DB9 male connector (standard serial port interface)
- Programmable baud rate selection via DIP switch (IR_BAUD_SEL)
- 2-pin connector for baud rate configuration

**Data Acquisition & Networking**
- CHAIN-IN and CHAIN-OUT connectors (M03 pads, W237-103 devices)
- Supports daisy-chaining architecture for multi-unit deployments
- 3-pin inter-unit communication links

**Design Quality Indicators**
- Distributed power supply filtering (multiple capacitors across different voltage rails)
- Analog signal conditioning (presence of ferrite beads suggests analog sensor integration)
- Professional manufacturing approach (Gerber files, DFM considerations)

</details>

<details open>
<summary> <b>Design Files & Tools</b></summary>

### Primary Design Files

All design files are in **Eagle CAD format** (version 6.2 or compatible):

- **SELFiSSH.sch** - The main schematic containing all electrical connections and component specifications
- **SELFiSSH.brd** - The PCB layout file with component placement, trace routing, and manufacturing specifications

Both files are **XML-based text formats** with the following characteristics:
- Can be version controlled and diffed via Git
- Compatible with programmatic XML parsing for automation
- Long line lengths (up to 426+ characters) - be prepared when viewing

### Manufacturing Output

The **Gerbers/** directory contains industry-standard Gerber files ready for PCB manufacturing:

- **Copper layers**: GTL (top), GBL (bottom) - actual circuit traces
- **Solder mask**: GTS (top), GBS (bottom) - solder resist areas
- **Silkscreen**: GTO (top), GBO (bottom) - component labels and reference designators
- **Milling file** (GML) - PCB edge cuts and outline
- **Drill file** (.dri) - Via and through-hole specifications
- **Pick & place file** (.gpi) - Component locations for assembly automation

### Visualization & Documentation

- **eagleUp/** folder contains 3D renderings of the board design
- **SEL-FiSSH.vsd** - Visio diagram for system architecture documentation
- **SELFiSSH.eup** - EagleUp 3D project file

### Required Tools

| Tool | Purpose | Version |
|------|---------|---------|
| **Eagle CAD** | Schematic and PCB design editing | 6.2+ |
| **Git** | Version control and design history tracking | Any recent version |
| **Gerber Viewer** (optional) | Manufacturing file visualization | Various (gerbv, ViewMaster, etc.) |
| **SketchUp** (optional) | 3D model review (SEL-FiSSH.skp) | 2016+ |

</details>

<details open>
<summary> <b>Working with This Repository</b></summary>

### Viewing the Design

1. **For schematic review**: Open `SELFiSSH.sch` in Eagle CAD to view electrical connections and component values
2. **For board layout**: Open `SELFiSSH.brd` in Eagle CAD to see component placement and routing
3. **For manufacturing files**: View Gerber files using a Gerber viewer (free online viewers available)
4. **For 3D visualization**: Open files in `eagleUp/` folder to see rendered board images, or open `SEL-FiSSH.skp` in SketchUp

### Making Design Changes

#### Updating Schematics
1. Open `SELFiSSH.sch` in Eagle CAD
2. Make electrical modifications as needed
3. Run **ERC** (Electrical Rule Check) to verify circuit integrity
4. Save the file

#### Updating PCB Layout
1. Open `SELFiSSH.brd` in Eagle CAD
2. Modify component placement and/or trace routing
3. Run **DRC** (Design Rule Check) to verify manufacturing compatibility
4. Verify trace widths, clearances, and layer assignments
5. Save the file

#### Generating Manufacturing Files
After layout changes, regenerate Gerber files:
1. In Eagle: **File → CAM Job**
2. Use the provided `.cam` configuration or create new job
3. Target the `Gerbers/` directory for output
4. Verify all required layers are exported:
   - GTL, GBL (copper)
   - GTS, GBS (mask)
   - GTO, GBO (silkscreen)
   - GML (milling)
   - .dri (drill)

#### Updating Bill of Materials
After schematic changes:
1. In Eagle: **File → Export → Partlist**
2. Export as CSV or text format
3. Verify part numbers match component specifications
4. Update `BOM/SELFiSSH.bom` with the new list

#### Version Control Workflow

When making design modifications:

```bash
# Check current status
git status

# Make your changes in Eagle CAD, then stage them
git add SELFiSSH.sch SELFiSSH.brd

# If updating manufacturing files
git add Gerbers/*

# If updating BOM
git add BOM/SELFiSSH.bom

# Create a descriptive commit
git commit -m "Update: [description of changes]"

# Example commits:
# git commit -m "Fix: Corrected voltage divider ratio on sensor input"
# git commit -m "Update: Improved power supply decoupling"
# git commit -m "Refactor: Reorganized communication interface layout"
```

**Note**: Eagle CAD automatically manages design iteration archives (`.s#*`, `.b#*` files). Do not manually edit these - they are snapshots for reference.

</details>

<details open>
<summary> <b>Component Details</b></summary>

### Power Supply Components

- **Charging IC**: BQ24202 (U3) - Solar power management and battery charging
- **Battery Connector**: 3.7V LiPo via JST 2-pin connector (BATT)
- **Solar Connector**: 5.5V input via JST 2-pin connector (SOLAR)
- **External Power**: 5.5x2.1mm barrel jack (J1)

### Decoupling & Filtering

Multiple capacitor values ensure clean power delivery:
- 0.1µF ceramic (high-frequency noise rejection)
- 1µF tantalum/ceramic (mid-frequency filtering)
- 10µF electrolytic (low-frequency bulk storage)
- 4.7µF ceramic (localized supply stabilization)

Ferrite beads on power rails suppress conducted EMI and provide additional filtering.

### Communication Components

- **Connector**: DB9 male (standard RS-232 port)
- **Level Shifter**: Converts 3.3V/5V logic to ±12V RS-232 levels
- **Baud Rate Selection**: DIP switch allows runtime baud rate configuration

### Data Acquisition Connectors

- **Chain-In**: 3-pin M03 connector for daisy-chain input
- **Chain-Out**: 3-pin M03 connector for daisy-chain output
- Supports inter-unit communication and power distribution in networked deployments

### Oscillator

**11.0592 MHz Crystal (Y1)**
- Standard frequency for microcontroller applications
- Enables clean UART baud rate generation
- Common choice for ATmega microcontrollers

</details>

<details open>
<summary> <b>Specifications & Ratings</b></summary>

### Operating Conditions

- **Microcontroller**: ATmega168 (8 MHz nominal, running at 11.0592 MHz with external crystal)
- **Battery Voltage**: 3.7V nominal (LiPo chemistry)
- **Solar Input**: 5.5V maximum
- **External Power**: 5.5V nominal
- **Serial Communication**: RS-232 logic levels (±12V)

### Physical Design

- **PCB Layers**: 2 layers (top and bottom copper)
- **Connector Types**: JST (power), DB9 (serial), M03/W237-103 (daisy-chain)
- **Oscillator**: 11.0592 MHz, crystal-based timing

### Power Management

- **Charger IC**: BQ24202 - Handles solar charging and battery management
- **Priority Logic**: Solar charging when available; automatic battery backup
- **Supply Regulation**: Distributed capacitance for stable 3.3V/5V rails

</details>

<details open>
<summary> <b>Project History & Licensing</b></summary>

**Version**: 1.0 (Current Release)

**Design Timeline**: The project tracks design iterations through Eagle CAD versioning. Previous versions are preserved as snapshots (`.s#*` and `.b#*` files) for reference and revision control.

**Licensing**: This design is released under **Creative Commons License** (as indicated by CC_TEXT labels in the schematic). Refer to the original schematic for specific license terms.

**Design Philosophy**: SELFiSSH represents an open, modular approach to data acquisition hardware, emphasizing:
- Autonomous, solar-powered operation
- Scalability through daisy-chaining
- Accessibility through standard interfaces (RS-232)
- Professional PCB design standards

</details>

<details open>
<summary> <b>Future Development & Improvements</b></summary>

Potential areas for enhancement:

- **Wireless Communication**: Add Bluetooth or LoRaWAN modules for remote data transmission
- **Expanded Sensor Support**: Develop standardized connector interfaces for various sensors
- **Firmware Development**: Create embedded firmware for common data acquisition patterns
- **Advanced Power Management**: Implement MPPT (Maximum Power Point Tracking) for improved solar efficiency
- **Memory Expansion**: Add external flash storage for extended logging capability
- **3G/4G Connectivity**: Integrate cellular modem for cloud data synchronization

</details>

<details open>
<summary> <b>Contributing & Support</b></summary>

This is an open-source hardware project. Contributions are welcome!

### How to Contribute

1. Fork the repository
2. Create a feature branch for your improvements
3. Make your changes to the design files
4. Document your modifications clearly
5. Submit a pull request with a detailed description of changes

### Reporting Issues

If you find design issues, manufacturing problems, or have suggestions for improvement:
- Check existing design archives for historical context
- Document the issue clearly with references to specific components or sections
- Include Eagle schematic/layout screenshots if applicable

### For Questions or Collaboration

This project welcomes collaboration and questions. When working with the design:
- Refer to `CLAUDE.md` for development guidance and best practices
- Consult Eagle CAD documentation for CAM job and manufacturing workflows
- Review the BOM carefully before ordering components
- Verify DRC/ERC rules pass before manufacturing

</details>

<details open>
<summary> <b>License</b></summary>

<p align = "center">
<img src= "https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by-sa.svg" />
</p>

This project is licensed under the **Creative Commons Attribution-ShareAlike License**. You are free to use, modify, and distribute this design, provided you:
- Give appropriate credit to the original designers
- Share derivative works under the same license

For full license details, see the Creative Commons website: https://creativecommons.org/licenses/by-sa/4.0/

</details>
