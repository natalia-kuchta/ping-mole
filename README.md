  ### Start game
```npm run dev```

Ping Mole is a classic whack-a-mole game built using Vue 3 and Vite. The player’s goal is to click the mole as it appears in different holes, aiming to score as many points as possible within a 30-second time limit. The game provides immediate feedback on hits and misses with color-coded indicators and allows players to start or end the game at any time.

## Features
```
Dynamic Mole Movement: The mole randomly appears in one of nine holes every second.
Score Tracking: Points increase when the player correctly hits the mole, and decrease for incorrect clicks.
Timed Gameplay: The game automatically ends after 30 seconds.
Visual Feedback: Holes show a green or red color to indicate hits or misses.
Interactive UI: Animated start and end game buttons for smooth gameplay.
```


## Game Mechanics
```
Start Game: The Start Game button resets the score and starts the 30-second timer.
Hit Detection: The player clicks a hole to attempt a hit. A correct hit on the mole adds points, while a miss deducts points.
End Game: The Game Over button ends the game early, showing the final score.
```


## Code Overview
```
startGame(): Initializes the score, resets the game status, and spawns the mole.
spawnMole(): Moves the mole to a new random hole every second.
pingMole(index): Checks if the clicked hole contains the mole and adjusts the score based on hit or miss.
endGame(): Ends the game by clearing the timer and showing the final score.
```
### Demo


https://github.com/user-attachments/assets/6ff16ed4-ed30-4143-8c33-a3daeef10d09

