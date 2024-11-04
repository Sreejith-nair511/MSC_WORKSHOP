# MSC_WORKSHOP
 WORKSHOP_CODING

DETAIL EXAPLANATION 

Initialization

import pygame
import time
import random

# Initialize Pygame
pygame.init()
Import necessary modules: pygame for game functionalities, time for handling time-related tasks, and random for generating random positions for the food.

Initialize Pygame to use its functionalities.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Set Up Display

# Define colors
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)

# Set display dimensions
dis_width = 800
dis_height = 600
dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('FIRST GAME THE SNAKE ONE ')

# Set clock
clock = pygame.time.Clock()

snake_block = 10
snake_speed = 15

font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)
Define color constants using RGB values.

Set up the game window with specified width and height.

Initialize the game clock to control the frame rate.

Define the size of each block of the snake and the snake's speed.

Load fonts for displaying text and score.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Display Score and Snake

def your_score(score):
    value = score_font.render("Your Score: " + str(score), True, yellow)
    dis.blit(value, [0, 0])

def our_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(dis, black, [x[0], x[1], snake_block, snake_block])
your_score(score): Renders and displays the score on the screen.

our_snake(snake_block, snake_list): Draws the snake on the screen using the positions stored in snake_list.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------=====================
Display Message

def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 6, dis_height / 3])
Renders and displays a message on the screen (e.g., "You Lost! Press Q-Quit or C-Play Again").
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Main Game Loop

def gameLoop():
    game_over = False
    game_close = False

    x1 = dis_width / 2
    y1 = dis_height / 2

    x1_change = 0
    y1_change = 0

    snake_List = []
    Length_of_snake = 1

    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
Initializes game state variables.

Sets the initial position of the snake.

Initializes variables for the snake's movement.

Creates an empty list to store the snake's body parts.

Sets the initial length of the snake.

Randomly generates the initial position of the food.
=-----------------------------=============================================--------------------------------------------------------------------------------------==============================--------------
Handle Game Over and Restart

    while not game_over:

        while game_close == True:
            dis.fill(blue)
            message("You Lost! Press Q-Quit or C-Play Again", red)
            your_score(Length_of_snake - 1)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()
while not game_over: Main game loop.

while game_close == True: Handles the game over state, displaying a message and waiting for user input to quit or restart.
==========================================================================================================================================================================================================
Handle Events and Movement

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0
Handles Pygame events, such as quitting the game or pressing arrow keys to move the snake.
============================================================================================================================================================================================================
Check Boundaries and Update Positions

        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += x1_change
        y1 += y1_change
        dis.fill(blue)
        pygame.draw.rect(dis, green, [foodx, foody, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]

        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True
Checks if the snake hits the boundaries, setting game_close to True.

Updates the snake's position based on the changes from key presses.

Draws the game elements (background, food, snake).

Updates the snake's body list and checks for collisions with itself.


============================================================================================================================================================================================================
END OF PROGRAM :)
