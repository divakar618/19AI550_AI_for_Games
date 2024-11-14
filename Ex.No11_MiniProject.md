# Ex.No: 11  Mini Project 
### DATE: 
### REGISTER NUMBER: 212222240026
### AIM:
To write a Python program to simulate the space shotter using Pygame.

## Algorithm:

1.Initialize Pygame: Set up the display and initialize necessary modules.

2.Load Images: Load player and enemy images, handle errors if images cannot be loaded.

3.Define Classes:

Player: Control player movement and shooting bullets.

Bullet: Define bullet behavior and movement.

Enemy: Spawn enemies, move them, and handle their interactions with bullets and the player.

4.Game Loop:

Handle user input for player movement and shooting.

Update the state of all game objects (player, bullets, enemies).

Check for collisions between bullets and enemies.

5.End Game Conditions: Define conditions for game over (e.g., player colliding with an enemy).

6.Exit: Clean up and quit Pygame when the game is over.

## Program:
```python
import pygame
import random
# Initialize Pygame
pygame.init()
# Set up the display
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Space Shooter")
# Define colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
# Set up the clock for frame rate
clock = pygame.time.Clock()
# Load player image
try:
    player_img = pygame.image.load(r"C:\Users\Hp\OneDrive\Desktop\games\player.png")
    print("Player image loaded successfully.")
except pygame.error as e:
    print(f"Unable to load player image: {e}")
# Scale the player image if needed
player_img = pygame.transform.scale(player_img, (100, 50))  # Scale to fit your game
# Define classes for the player, bullet, and enemy
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = player_img
        self.rect = self.image.get_rect()
        self.rect.centerx = screen_width // 2
        self.rect.bottom = screen_height - 10
        self.speed = 5
    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT] and self.rect.left > 0:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT] and self.rect.right < screen_width:
            self.rect.x += self.speed
class Bullet(pygame.sprite.Sprite):
    def __init__(self, x, y):
        super().__init__()
        self.image = pygame.Surface((5, 10))
        self.image.fill(WHITE)
        self.rect = self.image.get_rect()
        self.rect.centerx = x
        self.rect.bottom = y
        self.speed = -10
    def update(self):
        self.rect.y += self.speed
        if self.rect.bottom < 0:
            self.kill()  # Remove the bullet if it goes off-screen
class Enemy(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill((255, 0, 0))  # Red square
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, screen_width - self.rect.width)
        self.rect.y = random.randint(-100, -40)
    def update(self):
        self.rect.y += 1  # Move down for testing
        if self.rect.top > screen_height:
            self.kill()  # Remove the enemy if it goes off-screen
# Create sprite groups
all_sprites = pygame.sprite.Group()
bullets = pygame.sprite.Group()
enemies = pygame.sprite.Group()
# Create player instance
player = Player()
all_sprites.add(player)
# Function to spawn enemies
def spawn_enemy():
    enemy = Enemy()
    all_sprites.add(enemy)
    enemies.add(enemy)
# Main game loop
running = True
score = 0
while running:
    clock.tick(60)
    # Check for events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                # Create and shoot a bullet
                bullet = Bullet(player.rect.centerx, player.rect.top)
                all_sprites.add(bullet)
                bullets.add(bullet)
    # Update all sprites
    all_sprites.update()
    # Check for bullet-enemy collisions
    hits = pygame.sprite.groupcollide(bullets, enemies, True, True)  # Destroy both on collision
    for hit in hits:
        score += 10  # Increase score for each enemy hit
        spawn_enemy()  # Spawn new enemy when one is destroyed
    # Spawn enemies at regular intervals
    if len(enemies) < 5:  # Limit for testing
        spawn_enemy()
    # Check for player-enemy collisions
    if pygame.sprite.spritecollideany(player, enemies):
        running = False  # End the game if the player collides with an enemy
    # Draw everything
    screen.fill(BLACK)
    all_sprites.draw(screen)
    # Display score
    font = pygame.font.SysFont(None, 36)
    score_text = font.render(f"Score: {score}", True, WHITE)
    screen.blit(score_text, (10, 10))
    # Update the display
    pygame.display.flip()
# Quit Pygame
pygame.quit()
```
### Output:
![image](https://github.com/user-attachments/assets/3c97bdd6-e4bf-47bc-b26f-1a826b4227a2)

### Result:

Thus, the simple game was implemented using Pygame, showcasing basic game mechanics such as player movement, shooting, enemy spawning, and collision detection.
