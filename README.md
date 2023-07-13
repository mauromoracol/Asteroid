# Asteroid
My work
Python
import pygame

# Initialize Pygame
pygame.init()

# Create the screen
screen = pygame.display.set_mode((640, 480))

# Load the images
ship_image = pygame.image.load("ship.png")
asteroid_image = pygame.image.load("asteroid.png")
bullet_image = pygame.image.load("bullet.png")

# Create the ship
ship = pygame.Rect(320, 240, 50, 50)

# Create the asteroids
asteroids = []
for i in range(6):
    asteroid = pygame.Rect(random.randint(0, 640), random.randint(0, 480), 50, 50)
    asteroids.append(asteroid)

# Create the bullets
bullets = []

# Main loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()

    # Update the ship
    if pygame.key.get_pressed()[pygame.K_LEFT]:
        ship.x -= 10
    elif pygame.key.get_pressed()[pygame.K_RIGHT]:
        ship.x += 10

    # Update the asteroids
    for asteroid in asteroids:
        asteroid.x += asteroid.speed

    # Update the bullets
    for bullet in bullets:
        bullet.y -= bullet.speed

    # Check for collisions
    for asteroid in asteroids:
        if asteroid.colliderect(ship):
            print("Game over!")
            break

    for bullet in bullets:
        for asteroid in asteroids:
            if bullet.colliderect(asteroid):
                asteroid.kill()
                bullet.kill()

    # Draw the screen
    screen.fill((0, 0, 0))
    screen.blit(ship_image, ship)
    for asteroid in asteroids:
        screen.blit(asteroid_image, asteroid)
    for bullet in bullets:
        screen.blit(bullet_image, bullet)

    pygame.display.update()
