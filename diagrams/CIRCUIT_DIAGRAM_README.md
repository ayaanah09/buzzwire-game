# Buzzwire Game: Circuit Diagram & Component Reference

This folder has the circuit diagram for the Arduino Buzzwire Game. The main image is `buzzwire_circuit_diagram.jpg`, a high-resolution picture of the full schematic that's ready to drop straight into the project README or print out. There's also an editable `.svg` version of the same diagram if you ever want to move parts around or recolor anything, since in the SVG every component, wire, resistor, and label is its own separate element.

## How to import into Tinkercad

If you want to edit the diagram yourself, use the `.svg` file, which imports straight into a Tinkercad design/canvas project (Tinkercad treats SVG as 2D editable shapes). The `.jpg` is just a flat image, so it's perfect for viewing and sharing but can't be edited the same way. It's worth knowing that `.stl` and `.obj` won't work here either; those are 3D mesh formats meant for solid objects, so they can't represent wiring. SVG is really the right format for an editable schematic.

If you'd rather have a version you can actually simulate, the easiest path is to rebuild the same connections inside Tinkercad Circuits using the wiring table below. Between the diagram and that table, you've got everything you need to place each part and run it.

## Pin assignments (from the Arduino sketch)

| Arduino pin | Mode          | Connects to                            |
|-------------|---------------|----------------------------------------|
| A0          | INPUT         | Start photoresistor divider (LDR1)     |
| A1          | INPUT         | End photoresistor divider (LDR2)       |
| A2          | INPUT         | Potentiometer wiper                    |
| D4          | INPUT_PULLUP  | Enable switch (other side to GND)      |
| D5          | INPUT_PULLUP  | Wand contact (maze wire; wand to GND)  |
| D6          | OUTPUT        | Piezo buzzer (+)                       |
| D7          | OUTPUT        | Red LED (via 220 Ω)                    |
| D8          | OUTPUT        | Green LED (via 220 Ω)                  |
| 5V          | power         | + rail (LDRs, potentiometer)           |
| GND         | ground        | - rail (everything's return path)      |

## Wiring table (node by node)

| From                     | To                        | Notes                          |
|--------------------------|---------------------------|--------------------------------|
| 5V                       | + power rail              | main supply                    |
| GND                      | - ground rail             | common ground                  |
| LDR1 leg A               | + rail                    | top of start divider           |
| LDR1 leg B               | A0 **and** 10 kΩ → GND    | divider midpoint feeds A0      |
| LDR2 leg A               | + rail                    | top of end divider             |
| LDR2 leg B               | A1 **and** 10 kΩ → GND    | divider midpoint feeds A1      |
| Pot terminal 1           | + rail                    |                                |
| Pot terminal 3           | GND                       |                                |
| Pot wiper (terminal 2)   | A2                        | sets finish time 10-30 s       |
| D7                       | 220 Ω → Red LED anode     | LED cathode → GND              |
| D8                       | 220 Ω → Green LED anode   | LED cathode → GND              |
| D6                       | Buzzer (+)                | buzzer (-) → GND               |
| D5                       | Maze wire                 | wand → GND; touching = LOW     |
| D4                       | Switch terminal 1         | switch terminal 2 → GND        |

## Brief description of the critical components

**Arduino Uno** is the microcontroller running the game. It reads the sensors on its analog and digital inputs and drives the LEDs and buzzer as outputs, handling all the lives, timer, and win/lose logic.

**Photoresistors (LDR1, LDR2)** are light-dependent resistors, meaning their resistance drops as more light hits them. Each one is wired with a 10 kΩ resistor as a voltage divider, so the Arduino can read a changing voltage on A0/A1 as the light level changes. LDR1 sits at the maze entrance and starts the game, while LDR2 at the exit triggers the win. (Blocking the light onto LDR2 with a small paper flag on the wand is what finally made the finish trigger reliably.)

**10 kΩ resistors** are the pull-down half of each photoresistor divider. They give the analog pin a defined voltage to read instead of leaving it floating.

**Potentiometer (10 kΩ)** is a knob you turn by hand to set the difficulty. Its wiper feeds A2, and the code maps that reading to a finish time somewhere between 10 and 30 seconds, so you can change how long a round lasts without touching the code.

**Wand & wire maze** is really the heart of a buzzwire game. The maze wire connects to D5, which the Uno holds HIGH with its internal pull-up. When the metal wand touches the wire, it completes a path to GND and pulls D5 LOW, and the code reads that as a hit and takes away a life. A short cooldown in software keeps a single touch from draining all the lives at once.

**Red & green LEDs** handle the visual feedback. The red LED (D7) flashes on a hit and during the lose sequence, and the green LED (D8) flashes on a win. Each one uses a 220 Ω series resistor to limit the current and protect both the LED and the pin.

**Piezo buzzer** handles the audio feedback on D6. It plays different tones for the game start, the timer beeps, the half-time warning, and the hit, win, and lose moments.

**Enable switch** connects to D4 using the internal pull-up. When it's closed (reading LOW) the whole game is active, so it basically works as a master on/off.

**Power & ground rails** tie everything together. The 5V rail feeds the photoresistor dividers and the potentiometer, and the ground rail is the shared return path for everything else, including the LED cathodes, the buzzer's negative leg, the wand, and the switch.
