# Arduino Buzzwire Game

test

## Overview

This project is a handheld Buzzwire reaction game built using an Arduino. Players guide a metal wand through a wire maze without making contact. Each time the wand touches the wire, the player loses a life, and the game ends once all lives are lost or the timer runs out. A photoresistor gate at the start of the maze begins the game, and a second photoresistor gate at the end triggers a win.

## Features

* 3-life system
* Collision detection with a cooldown so a single touch can't drain all lives at once
* Photoresistor start/finish gates to automatically begin and win the game
* Adjustable time limit using a potentiometer (10–30 seconds)
* Half-time audio warning so the player knows when they're running low on time
* Red and green LED feedback
* Buzzer alerts for hits, timer beeps, wins, and losses
* An enable switch to turn the whole system on/off

## Technologies Used

* Arduino Uno
* Embedded C/C++
* Basic electronic circuit design

## Components

* Arduino Uno
* 2x Photoresistors (start and finish gates)
* Potentiometer (time control)
* Buzzer
* Red LED and Green LED
* Pushbutton / enable switch
* Breadboard and jumper wires
* Metal wire maze
* Wand probe

## How It Works

The wand and the wire maze form an electrical contact when they touch. The Arduino reads this contact on a digital input and decreases the player's remaining lives. Photoresistors at each end of the maze detect when the wand passes through, starting the game at the entrance and winning it at the exit. A potentiometer sets how long the player has to finish, and the buzzer plus LEDs give real-time feedback throughout the round.

## Challenges Faced

This project came with a number of hardware and software problems I had to work through:

* **Short circuits after soldering.** Once I soldered my connections, some of the wires were touching each other and causing short circuits. I fixed this by carefully separating the wires so they no longer made unintended contact.
* **Designing the hit/cooldown system.** Getting the collision logic right was tricky. I wanted a cooldown built into the hit detection so that a single touch wouldn't instantly cost the player all 3 lives at once. I implemented a timer-based cooldown that ignores additional hits for a short window after each registered contact.
* **Balancing the maze and wand difficulty.** Designing the physical maze and wand was harder than expected because I didn't want the game to be frustratingly hard or boringly easy. It took some trial and error to find a difficulty that felt fair and fun.
* **False triggers.** I ran into a lot of false triggers from the contact and sensors. I debugged my code to filter these out so the game only reacted to genuine contact.
* **Extending the wiring to fit the enclosure.** The wires coming off my breadboard weren't long enough to comfortably reach across the box I mounted everything on. I had to extend them so the layout fit the enclosure properly.
* **Faulty equipment.** I frequently ran into faulty components. I solved this by thoroughly testing each part before soldering it down, so I wasn't permanently committing to a broken piece.

## What I Learned

* Arduino programming and embedded logic
* Electronics prototyping
* Hardware debugging and troubleshooting
* Game logic implementation (lives, timer, win/lose states)
* Soldering and managing physical wiring

## Engineering Design Process

* **Problem:** Build an engaging reaction game that reliably detects contact without being unfair to the player.
* **Brainstorming:** Decided on a buzzwire concept with lives, a timer, and sensor-based start/finish gates.
* **Prototype:** Built the circuit on a breadboard and wrote the initial game loop.
* **Testing:** Found false triggers, short circuits, and difficulty-balance issues during testing.
* **Improvements:** Added a hit cooldown, separated shorting wires, debugged false triggers, extended wiring for the enclosure, and pre-tested components before soldering.

## Future Improvements

* LCD display for score and time
* Selectable difficulty levels
* More sound effects
* Fully portable enclosure
* Wireless score tracking

## Demo Video

https://drive.google.com/drive/folders/1r7lEVZtdQMxgW3w8Rurrsi0q8c3hj3i0?usp=sharing

## Author

Ayaan Ahmed
Grade 11 Student
Interested in Engineering and STEM Projects

