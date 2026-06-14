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

# The game ties together several small systems that each handle one job, and the Arduino runs them together in a continuous loop. Here's how each part contributes.

# 

# \*\*Start and finish photoresistors\*\*

# 

# Two photoresistors act as invisible "gates" that mark the beginning and end of the maze. A photoresistor changes its resistance based on how much light reaches it, and each one is wired into a voltage divider so the Arduino can read that change as a number on an analog pin (A0 for the start, A1 for the finish). When the wand passes the start gate and the reading drops below a set threshold, the game begins automatically. When the wand reaches the finish gate and that reading drops, the win sequence triggers. This means the player never has to press a button to start or end a round; the act of physically moving the wand through the maze is what drives the game forward.

# 

# \*\*The wand and the hit system\*\*

# 

# The metal wand and the wire maze are the core of the game. The maze wire is connected to a digital input pin (D5) that the Arduino holds HIGH by default using its internal pull-up resistor. The wand is connected to ground. As long as the wand isn't touching the wire, the pin stays HIGH and nothing happens. The instant the wand touches the wire, it completes a path to ground and pulls the pin LOW, which the Arduino reads as a hit. On each hit the player loses one life, the red LED flashes, and the buzzer plays a tone.

# 

# The tricky part of the hit system is the cooldown. Without it, a single touch lasting even a fraction of a second would register dozens of hits in a row, because the loop runs thousands of times per second, and the player would lose all three lives instantly. To prevent this, the code records the time of each hit and ignores any new contact for a short window (about 300 milliseconds) afterward. This way one touch always equals exactly one lost life, no matter how long the wand stays against the wire, which keeps the game fair.

# 

# \*\*The adjustable timer\*\*

# 

# The potentiometer lets the player set the difficulty before starting. A potentiometer is a knob that outputs a variable voltage depending on how far it's turned, and the Arduino reads that voltage on pin A2. The code maps that reading onto a finish time between 10 and 30 seconds, so turning the knob one way gives a relaxed round and turning it the other way creates tight time pressure. Once the game starts, the Arduino counts up one second at a time using its internal clock (rather than freezing the whole program with delays), so the rest of the game stays responsive while the timer runs. If the player reaches the halfway point of their time, the buzzer plays a distinct warning tone so they know the clock is running down. If the timer reaches the finish time before the player completes the maze, the game ends as a loss.

# 

# \*\*Feedback: LEDs and buzzer\*\*

# 

# The red and green LEDs and the piezo buzzer give the player constant feedback so they always know what's happening. The red LED and a low buzzer tone fire on every hit and during the lose sequence, while the green LED and a higher tone celebrate a win. The buzzer also handles the start tone, the regular per-second timer beeps, and the half-time warning, so the game communicates its full state through sound and light without needing a screen.

# 

# \*\*The enable switch\*\*

# 

# A switch wired to pin D4 acts as a master on/off control for the whole system. When the switch is in the enabled position, the Arduino runs the full game loop, checking the gates, the wand, and the timer. When it's off, the system idles. This makes it easy to reset or pause the setup between players without unplugging anything.

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

* # \*\*Arduino programming and embedded logic.\*\* I learned how to structure a program that runs continuously and reacts to inputs in real time, breaking the game into separate functions for starting, running, winning, and losing.



* # \*\*Electronics prototyping.\*\* Building the circuit on a breadboard first taught me how to plan a layout, test connections, and change my design quickly before committing to anything permanent.



* # \*\*Hardware debugging and troubleshooting.\*\* I learned to track down problems that could come from either the code or the physical circuit, which meant testing systematically instead of guessing.



* # \*\*Game logic implementation (lives, timer, win/lose states).\*\* I learned how to manage game state, tracking lives, time, and whether a round is active, and how to transition cleanly between those states.



* # \*\*Soldering and managing physical wiring.\*\* I built real soldering skill and learned how easily neighboring connections can short if they aren't kept separated.



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

* # \*\*LCD display for score and time.\*\* Adding a small screen would let players see their remaining lives and the countdown directly, instead of relying only on the buzzer and LEDs.



* # \*\*Selectable difficulty levels.\*\* Preset modes like easy, medium, and hard could adjust the time limit and number of lives automatically.



* # \*\*More sound effects.\*\* Adding distinct tones or short melodies for different events would make the game more lively and satisfying to play.



* # \*\*Fully portable enclosure.\*\* Mounting everything in a self-contained case with its own power source would make the game easy to carry and demo anywhere.



* # \*\*Wireless score tracking.\*\* Sending results to a phone or computer over Bluetooth or Wi-Fi would let scores be logged and compared over time.



# \## Demo Video

# 

# https://drive.google.com/drive/folders/1r7lEVZtdQMxgW3w8Rurrsi0q8c3hj3i0?usp=sharing

# 

# \## Author

# 

# Ayaan Ahmed

# Grade 11 Student

# Interested in Engineering and STEM Projects

