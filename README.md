# \# Arduino Buzzwire Game

# 

# \## Overview

# 

# This project is a handheld Buzzwire reaction game built using an Arduino. Players guide a metal wand through a wire maze without making contact. Each time the wand touches the wire, the player loses a life, and the game ends once all lives are lost or the timer runs out. A photoresistor gate at the start of the maze begins the game, and a second photoresistor gate at the end triggers a win.

# 

# \## Features

# 

# \- 3-life system

# \- Collision detection with a cooldown so a single touch can't drain all lives at once

# \- Photoresistor start/finish gates to automatically begin and win the game

# \- Adjustable time limit using a potentiometer (10–30 seconds)

# \- Half-time audio warning so the player knows when they're running low on time

# \- Red and green LED feedback

# \- Buzzer alerts for hits, timer beeps, wins, and losses

# \- An enable switch to turn the whole system on/off

# 

# \## Technologies Used

# 

# \- Arduino Uno

# \- Embedded C/C++

# \- Basic electronic circuit design

# 

# \## Components

# 

# \- Arduino Uno

# \- 2x Photoresistors (start and finish gates)

# \- Potentiometer (time control)

# \- Buzzer

# \- Red LED and Green LED

# \- Pushbutton / enable switch

# \- Breadboard and jumper wires

# \- Metal wire maze

# \- Wand probe

# 

# \## How It Works

# 

# The wand and the wire maze form an electrical contact when they touch. The Arduino reads this contact on a digital input and decreases the player's remaining lives. Photoresistors at each end of the maze detect when the wand passes through, starting the game at the entrance and winning it at the exit. A potentiometer sets how long the player has to finish, and the buzzer plus LEDs give real-time feedback throughout the round.

# 

# \## Challenges Faced

# 

# This project came with a number of hardware and software problems I had to work through:

# 

# \- \*\*Short circuits after soldering.\*\* Once I soldered my connections, some of the wires were touching each other and causing short circuits. I fixed this by carefully separating the wires so they no longer made unintended contact.

# 

# \- \*\*Designing the hit/cooldown system.\*\* Getting the collision logic right was tricky. I wanted a cooldown built into the hit detection so that a single touch wouldn't instantly cost the player all 3 lives at once. I implemented a timer-based cooldown that ignores additional hits for a short window after each registered contact.

# 

# \- \*\*Balancing the maze and wand difficulty.\*\* Designing the physical maze and wand was harder than expected because I didn't want the game to be frustratingly hard or boringly easy. It took some trial and error to find a difficulty that felt fair and fun.

# 

# \- \*\*False triggers.\*\* I ran into a lot of false triggers from the contact and sensors. I debugged my code to filter these out so the game only reacted to genuine contact.

# 

# \- \*\*Extending the wiring to fit the enclosure.\*\* The wires coming off my breadboard weren't long enough to comfortably reach across the box I mounted everything on. I had to extend them so the layout fit the enclosure properly.

# 

# \- \*\*Faulty equipment.\*\* I frequently ran into faulty components. I solved this by thoroughly testing each part before soldering it down, so I wasn't permanently committing to a broken piece.

# 

# \- \*\*End photoresistor not triggering.\*\* When the wand reached the finish gate, the end photoresistor wouldn't trigger the win condition because the light level wasn't changing enough to drop below my threshold. I fixed this by attaching a small piece of paper to the end of the wand, which blocked enough light to lower the photoresistor's reading enough to reliably trigger the end-game function.

# 

# \## What I Learned

# 

# \- Arduino programming and embedded logic

# \- Electronics prototyping

# \- Hardware debugging and troubleshooting

# \- Game logic implementation (lives, timer, win/lose states)

# \- Soldering and managing physical wiring

# 

# \## Engineering Design Process

# 

# \*\*Problem.\*\* The goal was to build an engaging reaction game that reliably detects when the wand touches the wire, without being unfair to the player. The core challenge is that a buzzwire game lives or dies on its sensing: if contact detection is too sensitive it punishes the player for nothing, and if it's not sensitive enough the game feels broken. On top of that, I wanted the game to actually feel like a game, with lives, a sense of urgency from a timer, and clear feedback, rather than just a circuit that beeps when two wires touch. Defining the problem this way, around reliability and fairness, shaped every decision that came after.

# 

# \*\*Brainstorming.\*\* I settled on a buzzwire concept built around a few interacting systems rather than a single mechanic. The player would have a limited number of lives, a countdown timer to create pressure, and automatic start and finish detection so the game could begin and end on its own without me pressing buttons. I decided to use photoresistor gates at the entrance and exit of the maze to detect when the wand passed through, a potentiometer to let the time limit be adjusted on the fly, and a buzzer plus LEDs to give the player immediate audio and visual feedback. Planning these features out ahead of time helped me understand which components I'd need and how they'd have to talk to each other.

# 

# \*\*Prototype.\*\* I built the circuit on a breadboard first so I could change things easily before committing to anything permanent. I wired up the photoresistors, the potentiometer, the buzzer, both LEDs, and the wand contact, then wrote the initial version of the game loop to tie them together. This first build let me confirm the basic logic worked, with the game able to start, count down, register hits, and reach a win or lose state, even though plenty of rough edges still needed fixing. Prototyping on the breadboard meant I could iterate quickly instead of being locked into early mistakes.

# 

# \*\*Testing.\*\* Once the prototype was running, testing exposed a series of real problems that weren't obvious on paper. I found that the contact was producing false triggers, that some of my soldered wires were shorting against each other, that the difficulty of the physical maze needed tuning, and that the end photoresistor wasn't reliably detecting the wand when it reached the finish. Each of these only showed up once I was actually playing the game repeatedly, which reinforced how important hands-on testing is compared to just assuming the design will work.

# 

# \*\*Improvements.\*\* Based on what testing revealed, I made a round of targeted fixes. I added a cooldown to the hit detection so a single touch couldn't drain all three lives at once, separated the wires that were shorting after soldering, debugged my code to filter out the false triggers, and extended the wiring so the layout fit comfortably inside the enclosure. To fix the unreliable finish gate, I attached a small piece of paper to the end of the wand so it would block enough light to trigger the end photoresistor. I also got into the habit of thoroughly testing each component before soldering it, so I wouldn't permanently commit to a faulty part. Each improvement came directly out of a specific problem I'd seen during testing, which is exactly the kind of iterate-and-refine loop that engineering is about.

# 

# \## Future Improvements

# 

# \- LCD display for score and time

# \- Selectable difficulty levels

# \- More sound effects

# \- Fully portable enclosure

# \- Wireless score tracking

# 

# \## Demo Video

# 

# https://drive.google.com/drive/folders/1r7lEVZtdQMxgW3w8Rurrsi0q8c3hj3i0?usp=sharing

# 

# \## Author

# 

# Ayaan Ahmed

# Grade 11 Student

# Interested in Engineering and STEM Projects

