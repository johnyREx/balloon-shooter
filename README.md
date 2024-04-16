We all know the importance of the pygame library in terms of game development. We know that Pygame is a collection of Python modules for making video games. It is a collection of computer graphics and sound libraries for the Python programming language. Pygame is well suited to the development of client-side applications that may be packaged as a standalone executable.

In our last article, we have covered the basics of the pygame library and did two projects. Therefore, in this article Balloon Shooter Game using Python PyGame, we are going to develop a fully working and full-fledged Ballon Shooter game. So, therefore, let’s get started and develop another project that will surely help you to brush up on your concepts.


What the game is all about?
The simple plot in this game is that there will be balloons moving all over the screen. The player will have a target like an arrow and with the help of a mouse, the player has to bust those moving ballons. There will be a counter for busted balloons and on busting each moving balloon successfully, the busting score will increase.

What we will use?
For the development of the Balloon Shooter Game using Python PyGame, we will use various pygame modules to add different functionalities to the game. We have to code for continuous movement of balloons, a shooting functionality, and updating the score every time the balloon is busted. All these functions can be done using various modules like draw, mouse, render, etc.

For the balloon’s color and shape, we will make use of the draw module that provides various functions for shapes like ellipses, circles, etc. Therefore, in order to interact with the system and above all, to add functionality like quit game and resume the game, we will use the sys module and add functionality that is based on random events we will use the random library. Apart from these libraries, we will also use the math module.

Now that we know the basic libraries and modules that we will use for the development of this game, let’s get started with some rules of the games and the flow of the code.

Game Rules to keep in mind:
It should be a single-player game.
The game should be able to keep track of the total number of ballons busted.
Code flow:
Importing pygame, random, sys, and math
Pygame library initialization
Declaring the required variables
Declaring variables that store color codes
Defining balloon class
Show balloon location using pointer() function
Display the score
To close the game
Function to keep track of the events
Call to game() function
Complete code for Balloon Shooter Game using Python
Getting started:
Importing pygame, random, sys, and math :
The very first task we will do in developing the Balloon Shooter Game using Python PyGame is importing all the required libraries and modules for this project.

import pygame
import sys
import random
from math import *
Pygame library initialization:
Now after importing, we will initialize the pygame library.

pygame.init()
Explanation:
All imported pygame modules are initialized via pygame.init(). If a module fails, no exceptions will be thrown, but the overall number of successful and unsuccessful inits will be returned as a tuple. Individual modules can be individually initialized, however, pygame.init() initializes all imported pygame modules, which provides a convenient method to get things started. Individual module init() routines will throw exceptions if they fail.

Declaring the required variables
Now after importing, we will declare all the variables that we will use in the development of this project.

width = 700
height = 600

display = pygame.display.set_mode((width, height))
pygame.display.set_caption("CopyAssignment - Balloon Shooter Game")
clock = pygame.time.Clock()

margin = 100
lowerBound = 100

score = 0
Explanation:
Line 1 & 2: The width and height variable will be used to set the size of the display screen
On-Line 3: display basically stores the pygame screen that is shown using the set_mode() function.
Line 4: This line sets the name of the screen to “CopyAssignment – Balloon Shooter Game”. This is done using the set_display function that is used to give the screen a name.
Line 5: Keeps track of time.
On-Line 6 & 7: Stores the margin value
Line 8: Keeps track of the score. This value is updated as the player bust the balloons.

Declaring variables that store color codes:
These variables store the color code in RBG form

white = (230, 230, 230)
lightBlue = (4, 27, 96)
red = (231, 76, 60)
lightGreen = (25, 111, 61)
darkGray = (40, 55, 71)
darkBlue = (64, 178, 239)
green = (35, 155, 86)
yellow = (244, 208, 63)
blue = (46, 134, 193)
purple = (155, 89, 182)
orange = (243, 156, 18)

font = pygame.font.SysFont("Arial", 25)
Explanation:
Line 1 & 11: Variable declaration with values.
Line 12: This font variable holds the font that is used to display the number of balloons busted. This is done using the SysFont() function from the font module that takes in the name of the font and the size of the font.

Defining balloon class:
Now comes the actual coding for the game. First of all, we will define a class and in that class, we will write the logic for functions that can do the following functions:

A function that moves the balloon
A function to show the balloon on screen
To check if the balloon is busted or not:
Function to reset balloons
Class definition:
class Balloon:
    def __init__(self, speed):
        self.a = random.randint(30, 40)
        self.b = self.a + random.randint(0, 10)
        self.x = random.randrange(margin, width - self.a - margin)
        self.y = height - lowerBound
        self.angle = 90
        self.speed = -speed
        self.proPool= [-1, -1, -1, 0, 0, 0, 0, 1, 1, 1]
        self.length = random.randint(50, 100)
        self.color = random.choice([red, green, purple, orange, yellow, blue])
Explanation:
In this class named Balloon, we have used the __init()__ function to assign the value for speed. We have used the self parameter as a reference to the current class to access variables. We have used to access variables that help to set the angle of the balloon, speed, etc.

The last line, self.color holds the list of different colors that will be selected on a random basis and will set the color of the ballon to that selected color.

A function that moves the balloon:
def move(self):
        direct = random.choice(self.proPool)

        if direct == -1:
            self.angle += -10
        elif direct == 0:
            self.angle += 0
        else:
            self.angle += 10

        self.y += self.speed*sin(radians(self.angle))
        self.x += self.speed*cos(radians(self.angle))

        if (self.x + self.a > width) or (self.x < 0):
            if self.y > height/5:
                self.x -= self.speed*cos(radians(self.angle)) 
            else:
                self.reset()
        if self.y + self.b < 0 or self.y > height + 30:
            self.reset()
Explanation:
This function holds the logic for the movement of the balloons. We have used the proPool which is a list of 0,1 and -1. On a random basis, any element is selected, and then using the conditionals the angle is set.

The angle of the movement of the balloon is set using the sin function from the math module. angle is passed as a parameter that is set to 90.

Logic to show the balloon on screen:
def show(self):
        pygame.draw.line(display, darkBlue, (self.x + self.a/2, self.y + self.b), (self.x + self.a/2, self.y + self.b + self.length))
        pygame.draw.ellipse(display, self.color, (self.x, self.y, self.a, self.b))
        pygame.draw.ellipse(display, self.color, (self.x + self.a/2 - 5, self.y + self.b - 3, 10, 10))
Explanation:
This function is responsible for displaying the balloons on the screen. The balloon tails are drawn using the line function. And the balloon is drawn using the ellipse function with display, color, and the position passed as parameters.

To check if the balloon is busted or not:
    def burst(self):
        global score
        pos = pygame.mouse.get_pos()

        if isonBalloon(self.x, self.y, self.a, self.b, pos):
            score += 1
            self.reset()
Explanation:
The above code check if the balloon is busted or not. global is a keyword used to set the variable as global.

the pos variable takes the cursor position and then using conditionals this position is compared with the position of the balloon using the isonBalloon() function. The basic logic is that if the position of the cursor and balloon is matched and a MOUSEBUTTONDOWN event occurs then there should be an increase in score. And so If the position matches then the value in the score variable is increased by 1.

Function to reset balloons:
    def reset(self):
        self.a = random.randint(30, 40)
        self.b = self.a + random.randint(0, 10)
        self.x = random.randrange(margin, width - self.a - margin)
        self.y = height - lowerBound 
        self.angle = 90
        self.speed -= 0.002
        self.proPool = [-1, -1, -1, 0, 0, 0, 0, 1, 1, 1]
        self.length = random.randint(50, 100)
        self.color = random.choice([red, green, purple, orange, yellow, blue])
Explanation:
This actually resets the balloon’s position. When the balloons are busted and when the score is increased, the reset() function is called

balloons = []
noBalloon = 10
for i in range(noBalloon):
    obj = Balloon(random.choice([1, 1, 2, 2, 2, 2, 3, 3, 3, 4]))
    balloons.append(obj)

def isonBalloon(x, y, a, b, pos):
    if (x < pos[0] < x + a) and (y < pos[1] < y + b):
        return True
    else:
        return False


Show balloon location using pointer() function
def pointer():
    pos = pygame.mouse.get_pos()
    r = 25
    l = 20
    color = lightGreen
    for i in range(noBalloon):
        if isonBalloon(balloons[i].x, balloons[i].y, balloons[i].a, balloons[i].b, pos):
            color = red
    pygame.draw.ellipse(display, color, (pos[0] - r/2, pos[1] - r/2, r, r), 4)
    pygame.draw.line(display, color, (pos[0], pos[1] - l/2), (pos[0], pos[1] - l), 4)
    pygame.draw.line(display, color, (pos[0] + l/2, pos[1]), (pos[0] + l, pos[1]), 4)
    pygame.draw.line(display, color, (pos[0], pos[1] + l/2), (pos[0], pos[1] + l), 4)
    pygame.draw.line(display, color, (pos[0] - l/2, pos[1]), (pos[0] - l, pos[1]), 4)

def lowerPlatform():
    pygame.draw.rect(display, darkGray, (0, height - lowerBound, width, lowerBound))
Explanation:
This function is responsible for showing the location of balloons on the display screen. At first, we initialized variable pos() that gets the position of the mouse cursor and declared variables l, r, and color.

We then used a for loop that runs in the range of 10. And as the loop runs the balloons that are made of a line and two ellipses are displayed continuously. Their position is decided using the pos, l, and r variables.

In the last line, we defined a function named lowerPlatform() that will display a dark grey colored rectangle at the bottom of the screen on white the score will be displayed.

Display the score:
def showScore():
    scoreText = font.render("Balloons Bursted : " + str(score), True, white)
    display.blit(scoreText, (150, height - lowerBound + 50))
Explanation:
This function’s main logic is to keep the track of the score. The text “Balloons Bursted” is displayed using the render() function and is displayed in white color.

To close the game:
def close():
    pygame.quit()
    sys.exit()
Explanation:
Whenever the user wants to quit the game, the function close() is called and this function contains:

pygame.quit: This actually runs that code whose main purpose is to deactivate the pygame library
sys.exit(): This is used in order to simply close the program without creating any dialogue box.

To keep track of the events:
def game():
    global score
    loop = True

    while loop:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                close()
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_q:
                    close()
                if event.key == pygame.K_r:
                    score = 0
                    game()

            if event.type == pygame.MOUSEBUTTONDOWN:
                for i in range(noBalloon):
                    balloons[i].burst()

        display.fill(lightBlue)
        
        for i in range(noBalloon):
            balloons[i].show()

        pointer()
        
        for i in range(noBalloon):
            balloons[i].move()

        
        lowerPlatform()
        showScore()
        pygame.display.update()
        clock.tick(60)
Explanation:
This is the main function of this code and here we have used a while loop in order to compare the events that are happening during the game and take steps accordingly.

We used event.type() to compare the events. If the player wants to quit then the QUIT event takes place. If the player tries to bust the balloons then the MOUSEBUTTONDOWN event takes place.

We used a fill function of the display module to fill the colour of the screen. In the end, we called two functions lowerPlatform() which will display a rectangle and showScore() which will show the scores on that rectangle.

Call to game() function:
game()

Explanation:

This is simply a call to the game() function because in order to start the game the call to this function is important

