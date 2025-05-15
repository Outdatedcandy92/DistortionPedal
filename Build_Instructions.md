# Build Instructions

### 📦 What You Need

- PCB 

- Electronic Components (See component table below)

- Soldering tools: Soldering iron, solder, tweezers

- DC Power Supply (9V)

- Aluminium Enclosure (125B)

- Optional: Multimeter and Oscilloscope for troubleshooting

### Component List

| Component(s)                         | Value / Part Number                     |
|-------------------------------------|-----------------------------------------|
| C1, C3                              | 47n                                     |
| C2, C8, C9                          | 0.47u                                   |
| C4                                  | 250p                                    |
| C5                                  | 68n                                     |
| C7                                  | 100p                                    |
| C10                                 | 0.01u                                   |
| C11                                 | 0.022u                                  |
| C12                                 | 0.1u                                    |
| C13                                 | 0.047u                                  |
| C14                                 | 1u                                      |
| C15                                 | 47uF                                    |
| C23                                 | 100uF                                   |
| D1                                  | 1N4004                                  |
| D4, D5, D8                           | D1N4148                                 |
| Q1, Q2, Q3                          | 2SC2240                                 |
| R1, R22                             | 1K                                      |
| R2, R7                              | 470K                                    |
| R3, R8, R18, R21, R24, R25          | 10K                                     |
| R4, R5, R10, R11, R23               | 100K                                    |
| R9                                  | 22                                      |
| R13                                 | 4.7K                                    |
| R14, R15                            | 2.2K                                    |
| R16, R17                            | 6.8K                                    |
| R39                                 | 47K                                     |
| R19, R20                            | 1M                                      |
| U1                                  | NJM4558          |
| VR1, VR2                            | 100KB                                   |
| VR3                                 | 20KB                                    |
| J1, J2                              | 6.35mm Jacks                            |


## 🔧 1. Populate the PCB (Section by Section)

We'll populate the circuit in logical stages, following the signal path from input to output. This approach helps with troubleshooting and gives a better understanding of how the pedal works.
### 🎛️ 1.1 Input Buffer Stage

This section conditions your guitar signal before it hits the gain stages.

    Resistors:

        R1, R2, R3

    Capacitors:

        C1, C2

➡️ Tip: Double-check resistor values before soldering using a multimeter or color code.
### ⚡ 1.2 Transistor Boost (Q2 Pre-Gain Stage)

This stage boosts the signal before it hits the op-amp.

    Transistor:

        Q2 (2SC2240)

    Resistors:

        R4, R5, R6, R7, R8

    Capacitors:

        C3, C4, C5

### 🎚️ 1.3 Op-Amp Clipping Stage

This is the main distortion stage using U1. It amplifies the signal and clips it via feedback diodes.

    IC:

        U1 (NJM3404A, M5223AL, or BA728N)

        Use a socket for easy replacement

    Resistors:

        R9, R10, R11

    Capacitors:

        C6, C7, C8, C9

    Diodes:

        D4, D5 (1N4148)

### 📐 1.4 Tone Control Stage

Filters the distorted signal for tone shaping.

    Resistors:

        R13, R14, R15

    Capacitors:

        C10, C11, C12, C13

    Potentiometer (not wired yet):

        VR2 (100KB - TONE)

### 🔉 1.5 Output Amplifier & Level Control

Boosts the final signal and lets you control the output level.

    Transistor:

        Q1, Q3 (2SC2240)

    Resistors:

        R16, R17, R18, R19, R20, R21

    Capacitors:

        C14, C15

    Potentiometer (not wired yet):

        VR3 (20KB - LEVEL)

### 🔋 1.6 Power Supply Filtering & Bypass

This section smooths the power input and manages circuit grounding.

    Diode:

        D1 (1N4004) – reverse polarity protection

    Capacitors:

        C23 (100uF bulk filtering)

    Resistors:

        R22, R23, R24, R25

    Extra:

        R39 (pull-down to prevent pop noise)

    Diode:

        D8 (1N4148 – protection or logic switching)

### 🧠 1.7 Final Touches – Leave for Later

DO NOT solder these yet. Wait until you’ve mounted the board in your enclosure:

    Potentiometers (wired off-board):

        VR1 (100KB – DISTORTION)

        VR2 (100KB – TONE)

        VR3 (20KB – LEVEL)

    Power Input (DC jack):

        9V center-negative

    Guitar Input/Output Jacks:

        J1, J2 (6.35mm mono jacks)

    3PDT Footswitch and LED wiring (if using true bypass)


## 🧰 2. Mounting and Wiring the Enclosure

Once your PCB is fully populated (excluding off-board parts), it’s time to mount everything in the enclosure and wire the final connections.
### 📦 2.1 Drill the Enclosure

Before mounting any components, prepare your enclosure:

    Drill holes for:

        3 potentiometers (VR1–VR3)

        2 mono 6.35mm jacks (input and output)

        9V DC power jack

        Footswitch (typically a 3PDT)

        Optional: LED indicator and vent holes

Use the PCB as a reference to space things properly and avoid cramping.
### 🛠️ 2.2 Mount the Off-Board Components

Install these components into the enclosure:

    Potentiometers:

        VR1 (Distortion)

        VR2 (Tone)

        VR3 (Level)

    Footswitch:

        3PDT for true bypass

    Jacks:

        J1 (Input), J2 (Output), both mono

        DC jack for 9V power (center-negative)

    Optional:

        LED indicator with a current-limiting resistor (~4.7kΩ or 2.2kΩ for brightness)

### 🔌 2.3 Wiring Connections
2.3.1 Potentiometers

    Wire VR1–VR3 to the PCB using flexible stranded wire.

    Keep wires short but not tight to reduce strain.

### 2.3.2 3PDT Footswitch Wiring (True Bypass)

    Standard layout:

        Middle row: IN → PCB IN, OUT → PCB OUT

        One side: Guitar input jack → switch, switch → PCB input

        Other side: PCB output → switch, switch → output jack

        Optional: Connect LED cathode to switch for status indication

### 2.3.3 Jacks

    Input jack:

        Tip → footswitch

        Sleeve → Ground

    Output jack:

        Tip → footswitch

        Sleeve → Ground

    DC Jack:

        +9V → PCB power input (through D1)

        GND → Common ground with jacks and PCB

### 🧪 2.4 Final Testing

Before closing the enclosure:

    Check continuity of all wires and grounds.

    Plug in your guitar and amp.

    Power the pedal with 9V and test:

        Bypass mode passes clean signal.

        Effect mode adds distortion.

        All knobs affect the sound as expected.

### 🪛 2.5 Closing It Up

    Once fully tested, carefully fit the PCB and wires into the enclosure.

    Secure the PCB if needed using standoffs, foam, or hot glue (avoid metal contact).

    Tighten the nuts on jacks, footswitch, and pots.

    Add knobs to the pots and label controls:
    Distortion, Tone, and Level.    