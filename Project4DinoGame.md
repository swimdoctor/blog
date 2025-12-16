# Arduino Dino Game Post-Mortem

A couple of months ago, when I first heard that our final project was open-ended, I knew that I wanted to take another attempt at a makeshift handheld game. I made a version of Tetris during a hackathon with my roommates about a year ago, and wanted to try it again. I knew I could use a more advanced screen, but decided to try and utilize the 2x16 LCD display as an added limitation, especially once I learned you could have up to 8 special characters. While hanging out with a friend, I started prototyping 5x8 sprites on paper, and brainstorming simple games that could work on such a small display. I settled on the dino game as a game that was simple enough yet still dynamic with the limited sprite count.


The goal was to build a playable game with:

- A controllable dino that can jump
- Randomly spawning cacti with fair spacing
- Basic player animations
- Piezo buzzer sound effects

![Sprites](./Images/Project4c.png)

---

## Project Narrative

When I began implementing the project, I first created the four dino frames and two cactus frames as custom LCD characters. I tested these frames on the 2x16 display to ensure that the small sprites would be readable and convey motion clearly. Below is my intial sprites vs the ones I settled on for the final game.

![Sprites](./Images/Project4a.png)

Each Sprite is then represented by a byte table that gets given to the LCD

```
byte dinoChar0[8] = {
  B00000,
  B00000,
  B00000,
  B00110,
  B01011,
  B11110,
  B01110,
  B10001
};
```

Next, I wired a push button to the Arduino to serve as the jump control. I then programmed a basic animation loop, cycling through the dino frames while running, and only showing a single leaping frame on the row above while jumping.

```
//Draw Bird
if(jumpDelay == 0) {
lcd.setCursor(1, 0);
lcd.write(' ');
lcd.setCursor(1, 1);
lcd.write(byte(animState));
}
```

For obstacles, I used a string buffer to represent the scrolling floor and added logic for controlled random cactus generation. This ensured that the obstacles were always spaced so the player had time to react, with occasional pairs of two cactus to make wider obstacles.

I also implemented a scoring system, incrementing points each time the dino passed an obstacle. Every 500 points, it does a little tune and speeds up the game by shortening the delay per frame. The buzzer was also used for jumps and game-over feedback, with a series resistor added to prevent interference with the LCD (More on this later).

Finally, I went and added collision detection to see if the player was overlapping a cactus, and if so, end the game and show a basic Game Over screen before reseting and going back to the Menu.

---

## Some Challenges I faced

### LCD Flicker with Buzzer:
- Using the buzzer initially caused the LCD to flicker and the data on the screen to corrupt.
- I did some googling and realized that the problem was usually caused by low power. 
- Adding a 100–220 Ω resistor in series with the buzzer solved the problem by limiting current.

### Limited Custom Characters:
- The LCD supports only 8 custom characters at a time.
- Handled by reusing cactus frames and careful management of animation states.
- I went and found the proper design documentation for the LCD display, to see what fonts there were and how many custom characters were allowed.

---

## Results/Conclusion

The final project is a fully playable Dino game on the 2x16 LCD, featuring:

- 6 Sprites
- 3 Sounds
- 1 Button
- Questionable Ergonomics
- Sleek 'Techy' Exposed Hardware
- A Functional Game Loop
- Increasing Difficulty

See gameplay here: <https://youtube.com/shorts/RSkeWy7UfqI?feature=share>

## Parts List

- Arduino Uno
- 2x16 LCD
- Push Button
- Piezo Buzzer
- 3x 220Ω Resistor
- Potentiometer
- Breadboard
- Jumper Wires

## Circuit Diagram

![Sprites](./Images/Project4b.png)

## Retrospective

I'm super proud of what I was able to achieve on such a small display with limited input. I managed to get animations, sound effects, a menu, and some pretty readable graphics, all encompasing a game that I found genuinely fun to play for a bit. I had a great time in both the planning stages and the implementation stages, getting a bit of game coding in that builds on what I've learned in other classes.

If I were to continue on this project, which I might, here's some things I would want to do:

- More sound effects, possibly even music
- Adding more buttons as input, enabling...
- More Games! While coming up with the dinosaur game idea, I came up with a full list of ideas using anywhere from 1-4 buttons of input, and I'd like to try allowing the player to choose between a selection of different games to play.
- Designing a case in the SHED Makerspace to encapsulate the device.

## Postmortem Video: 
	<https://youtu.be/kMx1ePb0-ow>

## Sources

<https://cdn.sparkfun.com/assets/9/5/f/7/b/HD44780.pdf>