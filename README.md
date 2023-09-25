import pygame
import sys
import random

# Initialize Pygame
pygame.init()

# Constants
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
DOG_SIZE = 50
BACKGROUND_COLOR = (255, 255, 255)
DOG_COLOR = (255, 0, 0)

# Create the screen
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Jumping Dogs")

# Create a list to store dog positions
dogs = []

# Function to add a new dog at a random position
def add_dog():
    x = random.randint(0, SCREEN_WIDTH - DOG_SIZE)
    y = random.randint(0, SCREEN_HEIGHT - DOG_SIZE)
    dogs.append([x, y])

# Main game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.MOUSEBUTTONDOWN:
            # Check if the mouse click is inside any of the dogs
            for dog in dogs:
                dog_rect = pygame.Rect(dog[0], dog[1], DOG_SIZE, DOG_SIZE)
                if dog_rect.collidepoint(event.pos):
                    # Make the dog jump by changing its y-position
                    dog[1] -= 20

    # Clear the screen
    screen.fill(BACKGROUND_COLOR)

    # Draw the dogs on the screen
    for dog in dogs:
        pygame.draw.rect(screen, DOG_COLOR, (dog[0], dog[1], DOG_SIZE, DOG_SIZE))

    # Update the display
    pygame.display.flip()

    # Add a new dog at random intervals
    if random.random() < 0.01:
        add_dog()

# Quit Pygame
pygame.quit()
sys.exit()
