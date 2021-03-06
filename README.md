# Adding Hazards to Your Platform Game

So....you made a character that can jump around. That's great and all, but every story needs some conflict and every Hero needs a villain. In this lesson, we will learn how to create multiple **hazards** that cause harm to the Hero. We will create a pit that the Hero can fall into and a moving attacker. To display the player's status, we will create a variable to track the number of lives remaining and a meter to display the Hero's health.

## A Note on Abstraction

There are many different kinds of hazards: Koopa Troopas, lava pits, falling rocks, spikes, knives, bullets, fire breathing dragons, and any other enemy you can imagine. Even though all of these hazards are different, they share certain characteristics. It is important to combine common characteristics into blocks to make our code simpler and reduce duplication. 

We learned about the concept of **abstraction** when discussing custom command blocks and reporters. Custom blocks allow you to combine multiple commands into a single named block of code. If you write your entire game in a straight line, it will get very long and complicated. If you find that making a simple change to your game logic involves changing the same value in many places, chances are you can **refactor** your code to reduce duplication. If it is hard to find a particular piece of logic when asked, chances are your program can be simplified to make it easier to read. Think about reading a book that has no chapters, paragraphs, or indentation: It would just be a big wall of text. A good program should be divided into named sections that make it easy to read and debug.

Let's consider a game with 10 different hazards and 10 different powerups. Many of them probably share some common characteristics. For instance, a health powerup and an enemy attack both change the Hero's health. So we may want to create a custom block for managing the Hero's health. We may also want a custom block for changing the number of lives a player has remaining. Falling into a lava pit and touching a "1-up" both change the number of lives a player has remaining, even if they change it in opposite ways. 

### Falling into a Pit

A common stationary hazard is a pit that the Hero must jump over. Failing to clear the pit results in the loss of life. Easy enough. Let's start with our visual representation of the pit - it is just a hole in the ground like the one below:

<img src="pit.png" />

We have already coded logic to make the Hero fall until reaching the ground. So if we erase the ground, our Hero should keep falling. Try this out now.

#### Boundaries

You should notice that your character keeps falling. Since the Hero never reaches the ground, you are stuck in a repeat loop. The number of lives will be a variable that stores a number. At the beginning of the game, we can initialize this variable with the number of starting lives in our game. For now, let's choose 3. Then each time the player dies, we will decrease this number by 1. 

<img src="check_boundaries.png" />

#### Keeping Track of Death

Will want to keep track of the player's lives. At the beginning of the game, lets create a variable to store the number of lives. Each time the player dies, we can broadcast a message to subtract a life. One variable that keeps track of a player's health, let's say the player has a health bar with 3 hearts. Lose all hearts, you lose a life. 

When the player dies, we will want to subtract one from the number of lives. Why do we want this in a custom block? Well, there maybe more than one hazard that takes away the player's life, or there may be a powerup that gives the player another life. We also might want to add a sprite that changes costumes when the player loses a life or execute other code when the number of lives change. Therefore, it is good to combine all of this code into a single block. 

<img src="change_lives.png" />

<img src="repeat_until.png" />

#### Starting a New Life

<img src="start_game_start_life.png" />

<img src="initialize_life.png" />

<img src="lives_check.png" />

### Adding a Moving Enemy

Let's add an Enemy sprite to our game that will cause damage to our hero. This enemy won't be able to kill the Hero with one touch, but will cause the Hero to lose health.

#### Creating an Enemy Sprite

Create a new Sprite in Snap and name it "Enemy". The Enemy sprite should have one or more costumes. For this example, the enemy will be a large cat. Right click and save the following set of images to a folder, then drag them to the costumes tab in Snap. 
 
![Cat 1](./cat1.png)
![Cat 2](./cat2.png)
![Cat 3](./cat3.png)
![Cat 4](./cat4.png)
![Cat 5](./cat5.png)

To animate the enemy, add a short script with a forever loop that changes costumes every 0.1 seconds to make the Enemy sprite appear in motion. Add a "go to X-Y" block to set the Enemy sprite's starting X-Y position to the right side of the stage. Then add a motion block to make the Enemy move towards the Hero as it changes costumes. See the example script below.

<img src="enemy_script.png" />

When the Enemy sprite touches the Hero Sprite, we will want to subtract health points from the Hero. Let's create a custom block called "Change Health" that changes the Hero's health, and call the custom block when the Enemy sprite touches the Hero.

<img src="change_health.png" />

When the Enemy touches the Hero, the hero should also change costumes or bounce backwards to show the attack's effects visually. This will be left as an exercise for you.

#### Creating a Health Meter

When the Enemy touches the Hero, the hero loses health. In most games, there is a visual indicator of the amount of health that the Hero has remaining. You can create a health meter by creating a new sprite with different costumes that change based on the amount of health the player has remaining. When the player is injured, you should broadcast a message to the health meter so that it knows when to change costumes. Here are some costumes that can be used for a health meter and a script that updates the health meter when a message is received:

![Health 100](./health100.png)

![Health 75](./health75.png)

![Health 50](./health50.png)

![Health 25](./health25.png)

<img src="health_script.png" />
