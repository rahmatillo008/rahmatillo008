import pygame
import random

# O'yin oynasi o'lchami
WIDTH = 800
HEIGHT = 600

# Mashina va yo'l rasmlari
CAR_IMAGE = pygame.image.load("car.png")
ROAD_IMAGE = pygame.image.load("road.png")

# Mashina obyekti
class Car:
    def __init__(self):
        self.image = pygame.transform.scale(CAR_IMAGE, (50, 100))
        self.rect = self.image.get_rect()
        self.rect.centerx = WIDTH // 2
        self.rect.bottom = HEIGHT - 20
        self.speed_x = 0

    def update(self):
        self.rect.x += self.speed_x

        # Yo'l chekkasiga yetganda mashinani to'xtatish
        if self.rect.right > WIDTH or self.rect.left < 0:
            self.speed_x = 0

    def accelerate(self):
        self.speed_x += 1

    def brake(self):
        self.speed_x -= 1

# O'yin oynasini yaratish
pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Mashina O'yini")

clock = pygame.time.Clock()

car = Car()

game_over = False

# O'yin tsikli
while not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_RIGHT:
                car.accelerate()
            elif event.key == pygame.K_LEFT:
                car.brake()

    car.update()

    # O'yin oynasini tozalash
    screen.fill((255, 255, 255))
    screen.blit(ROAD_IMAGE, (0, 0))
    screen.blit(car.image, car.rect)

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
