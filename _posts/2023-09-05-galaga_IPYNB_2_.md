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
import random

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 800, 600
WHITE = (255, 255, 255)
PLAYER_SIZE = 50
FPS = 60

# Create the screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("2D Game with Pygame")

# Player class
class Player:
    def __init__(self, x, y, name):
        self.name = name
        self.x = x
        self.y = y
        self.max_lives = 3
        self.lives = self.max_lives
        self.max_health = 100
        self.health = self.max_health
        self.speed = 5
        self.abilities = {
            "Basic Attack": {"damage": 20, "healing": 0},
            "Fireball": {"damage": 30, "healing": 0},
            "Heal": {"damage": 0, "healing": 25},
            "Lightning Strike": {"damage": 40, "healing": 0},
            "Steal Life": {"damage": 20, "healing": 10},
        }

    def move(self, dx, dy):
        self.x += dx
        self.y += dy

    def choose_ability(self):
        # Simulate ability selection here
        ability_name = random.choice(list(self.abilities.keys()))
        ability = self.abilities[ability_name]
        return ability_name, ability

    def take_damage(self, damage):
        self.health -= damage
        if self.health < 0:
            self.health = 0

    def heal(self, healing):
        self.health += healing
        if self.health > self.max_health:
            self.health = self.max_health

# Create players
player1 = Player(100, HEIGHT // 2, "Player 1")
player2 = Player(WIDTH - 100, HEIGHT // 2, "Player 2")

players = [player1, player2]

# Game loop
clock = pygame.time.Clock()
running = True
current_player = random.choice(players)

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    dx, dy = 0, 0

    if keys[pygame.K_LEFT]:
        dx = -current_player.speed
    if keys[pygame.K_RIGHT]:
        dx = current_player.speed
    if keys[pygame.K_UP]:
        dy = -current_player.speed
    if keys[pygame.K_DOWN]:
        dy = current_player.speed

    current_player.move(dx, dy)

    # Check for collisions or interactions between players here
    # You can add the ability mechanics here as well

    # Switch players
    current_player = player1 if current_player == player2 else player2

    # Clear the screen
    screen.fill(WHITE)

    # Draw players
    for player in players:
        pygame.draw.rect(screen, (0, 0, 255), (player.x, player.y, PLAYER_SIZE, PLAYER_SIZE))

    # Draw health bars
    for player in players:
        pygame.draw.rect(screen, (255, 0, 0), (player.x, player.y - 10, PLAYER_SIZE, 5))
        pygame.draw.rect(screen, (0, 255, 0), (player.x, player.y - 10, (player.health / player.max_health) * PLAYER_SIZE, 5))

    pygame.display.flip()
    clock.tick(FPS)

# Quit Pygame
pygame.quit()

```
