---
layout: post
title: Python galaga
description: These examples show the basic language structures and constructs of Python using input and output (print) commands.
courses: {'csp': {'week': 3}}
categories: ['C4.0']
type: hacks
---

```python
import pygame
import sys
import random
import requests
from PIL import Image
from io import BytesIO

# Initialize Pygame
pygame.init()

# Constants
SCREEN_WIDTH, SCREEN_HEIGHT = 800, 600
PLAYER_SPEED = 10
ENEMY_SPEED = 2
ENEMY_SIZE = (50, 50)
ENEMY_GENERATION_RATE = 60
ENEMY_HIT_RADIUS = 0
BULLET_SPEED = 2
BULLET_SIZE = (10, 10)
DIFFICULTY_INCREASE_INTERVAL = 3600

# Create the screen
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Galaga Clone")

# Function to load an image from a URL and resize it
def load_and_resize_image_from_url(url, size):
    response = requests.get(url)
    img_data = Image.open(BytesIO(response.content))
    img_data = img_data.resize(size)
    return pygame.image.fromstring(img_data.tobytes(), img_data.size, img_data.mode)

# Load images from URLs and resize them
player_url = "https://freepngimg.com/thumb/categories/1873.png"  # Replace with your image URL
enemy_url = "https://cdn-icons-png.flaticon.com/512/1477/1477230.png"  # Replace with your image URL

player_img = load_and_resize_image_from_url(player_url, (ENEMY_SIZE[0], ENEMY_SIZE[1]))
enemy_img = load_and_resize_image_from_url(enemy_url, ENEMY_SIZE)

# Set up player rect
player_rect = player_img.get_rect()
player_rect.centerx = SCREEN_WIDTH // 2
player_rect.bottom = SCREEN_HEIGHT - 20

# Initialize player position and velocity
player_x_velocity = 0

# Create a clock object to control the frame rate
clock = pygame.time.Clock()

# Enemy generation
enemies = []

def generate_enemy():
    enemy = pygame.Rect(random.randint(0, SCREEN_WIDTH - ENEMY_SIZE[0]), 0, ENEMY_SIZE[0], ENEMY_SIZE[1])
    enemies.append(enemy)

# Bullet generation
bullets = []
enemy_bullets = []

def shoot_bullet():
    bullet = pygame.Rect(player_rect.centerx - BULLET_SIZE[0] // 2, player_rect.top, BULLET_SIZE[0], BULLET_SIZE[1])
    bullets.append(bullet)

def enemy_shoot_bullet(enemy):
    bullet = pygame.Rect(enemy.centerx - BULLET_SIZE[0] // 2, enemy.bottom, BULLET_SIZE[0], BULLET_SIZE[1])
    enemy_bullets.append(bullet)

# Initialize game variables
score = 0
difficulty_increase_timer = 0
game_over = False

# Main game loop
running = True
enemy_timer = 0
start_time = pygame.time.get_ticks()

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        # Handle key presses
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player_x_velocity = -PLAYER_SPEED
            elif event.key == pygame.K_RIGHT:
                player_x_velocity = PLAYER_SPEED
            elif event.key == pygame.K_SPACE:
                shoot_bullet()

        # Handle key releases
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                player_x_velocity = 0

    # Update player position based on keyboard input
    player_rect.x += player_x_velocity

    # Generate enemies periodically
    enemy_timer += 1
    if enemy_timer >= ENEMY_GENERATION_RATE:
        generate_enemy()
        enemy_timer = 0

    # Update enemy positions
    for enemy in enemies:
        enemy.y += ENEMY_SPEED

        # Periodically make enemies shoot
        if random.randint(1, 300) == 1:
            enemy_shoot_bullet(enemy)

    # Update bullet positions
    for bullet in bullets:
        bullet.y -= BULLET_SPEED

    for bullet in enemy_bullets:
        bullet.y += BULLET_SPEED

    # Check for collisions between player and enemies
    for enemy in enemies:
        if player_rect.colliderect(enemy):
            game_over = True
            break

    # Check for collisions between bullets and enemies
    for bullet in bullets:
        for enemy in enemies:
            if bullet.colliderect(enemy):
                bullets.remove(bullet)
                enemies.remove(enemy)
                score += 1

    # Check for collisions between enemy bullets and player
    for bullet in enemy_bullets:
        if bullet.colliderect(player_rect):
            game_over = True
            break

    # Clear the screen
    screen.fill((0, 0, 0))

    # Draw player
    screen.blit(player_img, player_rect)

    # Draw enemies
    for enemy in enemies:
        screen.blit(enemy_img, enemy.topleft)

    # Draw bullets
    for bullet in bullets:
        pygame.draw.rect(screen, (255, 0, 0), bullet)

    for bullet in enemy_bullets:
        pygame.draw.rect(screen, (0, 0, 255), bullet)

    # Update the display
    pygame.display.flip()

    # Limit the frame rate
    clock.tick(60)

    # Increase difficulty every 6 minutes
    current_time = pygame.time.get_ticks()
    if current_time - start_time >= DIFFICULTY_INCREASE_INTERVAL:
        ENEMY_GENERATION_RATE -= 5
        BULLET_SPEED += 1
        start_time = current_time
        difficulty_increase_timer += 1

    if game_over:
        running = False

# Display score when game over
font = pygame.font.Font(None, 36)
text = font.render(f'Score: {score}', True, (255, 255, 255))
text_rect = text.get_rect()
text_rect.center = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)

screen.blit(text, text_rect)
pygame.display.flip()

# Wait for a few seconds before quitting
pygame.time.delay(3000)  # 3000 milliseconds (3 seconds)

# Quit Pygame
pygame.quit()
sys.exit()

```


    An exception has occurred, use %tb to see the full traceback.


    SystemExit


