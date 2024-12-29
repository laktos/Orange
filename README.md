# Orange
Orange
import pygame
import random
import sys

# Pygame-i başladın
pygame.init()

# Ekranın ölçüləri
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Orange Catcher")

# Rənglər
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
ORANGE = (255, 165, 0)

# Səbətin parametrləri
basket_width = 100
basket_height = 20
basket_x = WIDTH // 2 - basket_width // 2
basket_y = HEIGHT - 50
basket_speed = 10

# Portağal parametrləri
orange_radius = 15
orange_x = random.randint(0, WIDTH - orange_radius)
orange_y = -orange_radius
orange_speed = 5

# Xal
score = 0
font = pygame.font.Font(None, 36)

# Oyun döngəsi
clock = pygame.time.Clock()

running = True
while running:
    screen.fill(WHITE)

    # Tədbirləri yoxlayın
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Klaviatura hərəkətləri
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and basket_x > 0:
        basket_x -= basket_speed
    if keys[pygame.K_RIGHT] and basket_x < WIDTH - basket_width:
        basket_x += basket_speed

    # Portağalın hərəkəti
    orange_y += orange_speed
    if orange_y > HEIGHT:
        orange_x = random.randint(0, WIDTH - orange_radius)
        orange_y = -orange_radius

    # Portağalın səbətə dəyməsini yoxlayın
    if (basket_x < orange_x < basket_x + basket_width) and (basket_y < orange_y + orange_radius):
        score += 1
        orange_x = random.randint(0, WIDTH - orange_radius)
        orange_y = -orange_radius

    # Səbəti çək
    pygame.draw.rect(screen, BLACK, (basket_x, basket_y, basket_width, basket_height))

    # Portağalı çək
    pygame.draw.circle(screen, ORANGE, (orange_x, orange_y), orange_radius)

    # Xalı göstər
    score_text = font.render(f"Score: {score}", True, BLACK)
    screen.blit(score_text, (10, 10))

    # Ekranı yeniləyin
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
sys.exit()
