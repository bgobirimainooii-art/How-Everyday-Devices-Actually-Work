# How-Everyday-Devices-Actually-Work
A plain-English technical reference for the physics and engineering behind 8 common consumer devices. Built as a TechPulse companion reference.
Memory Cards (NAND Flash Storage)
How data is stored:
Floating-gate transistor
├── Control Gate (top)
├── Oxide insulation
├── Floating Gate (trapped electrons live here)
├── Oxide insulation
└── Channel (substrate)

Electrons trapped in floating gate = 0
No electrons in floating gate      = 1
Why data survives without power: Electrons are physically trapped between two layers of insulating oxide material. There is no electrical path for them to escape. This is fundamentally different from RAM.
Write/erase: Applying a high voltage forces electrons through the oxide via quantum tunneling (Fowler-Nordheim tunneling). Erase applies opposite voltage to pull electrons out.
Endurance limit: Each write/erase cycle slightly degrades the oxide. Consumer NAND typically rated 3,000-10,000 program/erase cycles. Enterprise SLC NAND: 100,000+ cycles.
RAM (Dynamic RAM — DRAM)
How data is stored:
Memory cell = 1 transistor + 1 capacitor
Charged capacitor   = 1
Discharged capacitor = 0
Why data disappears on power loss:
Capacitors leak charge within milliseconds
Memory controller must refresh every cell ~64,000 times per second (every 64ms)
Cut power → refresh stops → charge drains → all data lost
Refresh overhead: In DDR4, refresh operations consume ~1-2% of available bandwidth.
DRAM vs SRAM:
DRAM	SRAM
Cell size	1T+1C (small)	6 transistors (large)
Needs refresh	Yes	No
Speed	Slower	Faster
Use case	Main memory	CPU cache
CPU — Instruction Cycle
Clock speed: 4 GHz = 4,000,000,000 cycles/second
One cycle ≈ 0.25 nanoseconds

Fetch → Decode → Execute → Write Back
  ↓         ↓         ↓          ↓
Get       Translate  ALU runs   Store
instruction  to signals  the op   result
Pipelining: Modern CPUs process multiple instructions simultaneously at different stages. A 4-stage pipeline processes 4 instructions in parallel, one at each stage.
Key components:
Control Unit: Directs the fetch-decode-execute-writeback cycle
ALU (Arithmetic Logic Unit): Performs math and logical operations
Cache (L1/L2/L3): Fast on-chip memory — L1 ~1ns, RAM ~100ns
Registers: Fastest storage (inside the CPU itself), ~0.1ns access
Why clock speed isn't everything: IPC (Instructions Per Clock) × clock frequency × core count = actual throughput.
WiFi (802.11)
Frequency bands:
Band	Range	Speed	Congestion
2.4 GHz	Long	Slower	High
5 GHz	Medium	Faster	Medium
6 GHz (WiFi 6E/7)	Short	Fastest	Low
How it works:
Router converts data → Radio waves at 2.4/5/6 GHz
Radio waves travel through air
Device antenna receives signal
Device converts radio waves → data
OFDM (Orthogonal Frequency-Division Multiplexing): WiFi doesn't use one frequency — it splits the channel into many subcarriers and transmits in parallel. WiFi 6 uses 1024-QAM and OFDMA for higher efficiency.
Note: 6 GHz band (WiFi 6E/7) added in 2021 — most "how WiFi works" explanations predate this and only mention 2.4 and 5 GHz.
Fingerprint Sensors — Three Types
1. Capacitive (Side-mounted buttons, older iPhones)
Finger ridge touches → capacitor charge changes
Finger valley (air gap) → capacitor charge unchanged
Controller maps charge differences → fingerprint image
2. Optical (Under-display, most Android phones)
Display illuminates fingertip
Camera beneath display photographs fingerprint
AI model matches against stored template
3. Ultrasonic (Samsung Galaxy S-series)
Transducer emits ultrasonic pulse through glass
Pulse reflects differently off ridge vs. valley
Sensor builds 3D map from reflection timing
Comparison:
Type	Speed	Works wet?	Security	Typical use
Capacitive	Fast	No	High	Side buttons
Optical	Medium	Limited	Medium	Under-display
Ultrasonic	Slow	Yes	Highest	Under-display
Touchscreens (Projected Capacitive)
Glass surface
    ↓
ITO (Indium Tin Oxide) grid — transparent, conductive
    ↓ carries weak AC electric field
Your finger (conductive) distorts field at contact point
    ↓
Controller chip reads distortion across all grid intersections
    ↓
Triangulates X/Y coordinates from distortion pattern
    ↓
Reports touch coordinates to processor
Multi-touch: Modern screens sample the entire grid simultaneously, detecting up to 10+ touch points in parallel.
Why gloves don't work: Standard gloves are non-conductive. Touchscreen gloves use conductive thread at fingertip positions.
Lithium-Ion Batteries
Discharge (in use):
Li+ ions: Anode (graphite) → electrolyte → cathode (LiCoO₂)
Electrons: External circuit (this is the current you use)

Charge (plugged in):
Li+ ions: Cathode → electrolyte → anode
Electrons: Forced back through external circuit
Why capacity degrades:
Lithium plating on anode (especially with fast charging)
SEI (Solid Electrolyte Interphase) layer thickens over cycles
Cathode crystal structure degrades from repeated lithium insertion/extraction
Capacity loss curve: ~20% capacity loss by 500 full cycles for most consumer cells.
Solid-state batteries: Replace liquid electrolyte with solid material → slower degradation, higher energy density, no leak risk.
QR Codes
QR Code structure:
┌─────────────────────┐
│ ██░  Finder Pattern │ ← 3 corner squares for orientation
│ ░░░  (top-left)     │
│                     │
│  ██░  Finder        │ ← Top-right
│                     │
│  Data modules ░█░█░ │ ← Black/white squares encode data
│  ░█░░█░░█░█░░       │
│                     │
│  ██░  Finder        │ ← Bottom-left
└─────────────────────┘
Error correction levels:
Level	Data recovery	Capacity
L	7%	Highest
M	15%	High
Q	25%	Medium
H	30%	Lower
Why logos in QR codes work: Adding a logo typically covers 20-30% of the data area. With Level H error correction, up to 30% of the code can be damaged or obscured and the QR code still scans correctly.
Capacity: A QR code can store up to 3KB of binary data, 7KB of numeric data, or 4KB of alphanumeric data.
Speed Reference
Technology          Operation              Typical time
──────────────────────────────────────────────────────
CPU instruction    Single cycle           0.1 ns
RAM access         Read/write             ~100 ns
RAM refresh        Controller cycle       ~10 µs
NVMe SSD read      4KB random read        ~100 µs
WiFi packet        Transmission           ~0.1 ms
Touchscreen        Touch detection        ~5 ms
Fingerprint        Scan + match           ~20 ms
QR code            Scan + decode          ~100 ms
Battery charge     Full cycle (1C rate)   ~1 hour
NAND data          Retention guarantee    ~10 years
Related Resources
TechPulse @techpulse.league
JEDEC DRAM Standards
IEEE 802.11 WiFi Specification
QR Code ISO/IEC 18004 Standard
