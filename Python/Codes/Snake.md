#python_code
```
import pygame
import random

pygame.init()

WIDTH = 800
HEIGHT = 600
running = True
snake_x = 200
snake_y = 300
snake_size = 30

speed_x = 0
speed_y = 0
food_size = 20
food_x = random.randint(0, WIDTH - food_size)
food_y = random.randint(0, HEIGHT - food_size)

screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Game_1")
clock = pygame.time.Clock()
snake_body = []
snake_length = 1
score = 0
font = pygame.font.SysFont(None, 40)
game_speed = 30

banana_x = random.randint(0, WIDTH - food_size)
banana_y = random.randint(0, HEIGHT - food_size)

magic_x = random.randint(0, WIDTH - food_size)
magic_y = random.randint(0, HEIGHT - food_size)

try:
    with open("highscore.txt", "r") as file:
        high_score = int(file.read())

except:
    high_score = 0

game_over = False


magic_visible = False
magic_timer = 0

obstacles = []

for i in range(10):
    obstacles.append([random.randint(0,WIDTH - 20),random.randint(0,HEIGHT - 20)])
game_started = False
while running:
    clock.tick(game_speed)
    magic_timer += 1

    if not magic_visible and magic_timer >= 600:
        magic_visible = True
        magic_timer = 0
        magic_x = random.randint(0, WIDTH - food_size)
        magic_y = random.randint(0, HEIGHT - food_size)

    if magic_visible and magic_timer >= 300:
        magic_visible = False
        magic_timer = 0


    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_RIGHT and speed_x != -5:
                speed_x = 5
                speed_y = 0
            elif event.key == pygame.K_LEFT and speed_x != 5:
                speed_x = -5
                speed_y = 0

            elif event.key == pygame.K_UP and speed_y != 5:
                speed_x = 0
                speed_y = -5
            elif event.key == pygame.K_DOWN and speed_y != -5:
                speed_x = 0
                speed_y = 5

            if game_over and event.key == pygame.K_r :
                snake_x = 200
                snake_y = 300
                speed_x = 0
                speed_y = 0
                snake_body = []
                snake_length = 1
                score = 0
                game_speed = 30
                game_over = False
            if not game_started and event.key == pygame.K_SPACE:
                game_started = True

    if game_over:
        over_font = pygame.font.SysFont(None, 80)

        text = over_font.render("GAME OVER", True, (255,0,0))

        screen.blit(text, (220,220))

        scrore_text = font.render(f"Score:{score}", True, (255,255,255))
        screen.blit(score_text, (300,320))
        restart_font = pygame.font.SysFont(None, 35)
        restart_text = restart_font.render("Press R To Restart", True, (255,255,0))
        screen.blit(restart_text, (250,380))
        pygame.display.update()

        continue


    screen.fill((25, 35, 45))
    if not game_started:

        title_font = pygame.font.SysFont(None,100)

        title_text= title_font.render("SNAKE GAME", True, (0,255,0))

        started_text = font.render("Press Space To Start", True, (255,255,255))

        screen.blit(title_text, (180,200))
        screen.blit(started_text, (240,320))
        pygame.display.update()
        continue

    for x in range(0, WIDTH, 20):
        pygame.draw.line(screen, (40, 50, 60), (x, 0), (x, HEIGHT))
    for y in range(0, WIDTH, 20):
        pygame.draw.line(screen, (40, 50, 60), (0, y), (WIDTH, y))
#-------------------------------FOOD-----------------------------------------------

    pygame.draw.circle(screen, (255, 0, 0), (food_x, food_y), 10)
    pygame.draw.circle(screen, (255, 255, 0), (banana_x, banana_y), 10)

    if magic_visible:
        pygame.draw.circle(screen, random.choice([(255,255,65),(150,150,150),(0,0,255),(255,0,0),(0,255,0)]), (magic_x, magic_y), 13)

    for obstacle in obstacles:
        pygame.draw.rect(screen, (100,100,100), (obstacle[0],obstacle[1],20,20))
    score_text = font.render(f"Score: {score}", True, (255, 255, 255))
    screen.blit(score_text, (10, 10))
    high_text = font.render(f"High Score: {high_score}", True, (255, 255, 0))
    screen.blit(high_text, (10, 50))
    snake_x += speed_x
    snake_y += speed_y

    head = [snake_x, snake_y]
    snake_body.append(head)

    if snake_length > 4:
        for part in snake_body[:-1]:
            if part == head:
                game_over = True

    if snake_x < 0:
        snake_x = WIDTH - snake_size

    if snake_x > WIDTH - snake_size:
        snake_x = 0

    if snake_y < 0:
        snake_y = HEIGHT - snake_size

    if snake_y > HEIGHT - snake_size:
        snake_y = 0

    if len(snake_body) > snake_length:
        del snake_body[0]

    for i, part in enumerate(snake_body[:-1]):
        size = max(6, int(snake_size * (i + 1) / len(snake_body)))
        offset = (snake_size - size) // 2

        pygame.draw.circle(screen, (0, 150, 0), (part[0] + snake_size // 2 , part[1] + snake_size //2),size // 2)

    head = snake_body[-1]

    pygame.draw.circle(screen, (0, 200, 0),
                       (head[0] + snake_size // 2,
                        head[1] + snake_size // 2),
                       snake_size // 2 + 1.5)

    if speed_x > 0:
        eye1 = (head[0] + 20, head[1] + 10)
        eye2 = (head[0] + 20, head[1] + 20)

    elif speed_x < 0:
        eye1 = (head[0] + 10, head[1] + 10)
        eye2 = (head[0] + 10, head[1] + 20)

    elif speed_y < 0:
        eye1 = (head[0] + 10, head[1] + 10)
        eye2 = (head[0] + 20, head[1] + 10)

    else:
        eye1 = (head[0] + 10, head[1] + 20)
        eye2 = (head[0] + 20, head[1] + 20)

    pygame.draw.circle(screen, (255, 255, 255), eye1, 3)
    pygame.draw.circle(screen, (255, 255, 255), eye2, 3)
    pygame.draw.circle(screen, (255, 255, 255), eye1, 3)
    pygame.draw.circle(screen, (0,0,0), eye1, 1)
    pygame.draw.circle(screen, (0,0,0), eye2, 1)





    if (snake_x < food_x + food_size
        and snake_x + snake_size > food_x
        and snake_y < food_y + food_size
        and snake_y + snake_size > food_y):
        food_x = random.randint(0, WIDTH - food_size)
        food_y = random.randint(0, HEIGHT - food_size)
        snake_length += 1
        score += 1

        if score > high_score:
            high_score = score
            with open("highscore.txt", "w") as file:
                file.write(str(high_score))

        if score % 5 == 0:
            game_speed += 5

    if (snake_x < banana_x + food_size
        and snake_x + snake_size > banana_x
        and snake_y < banana_y + food_size
        and snake_y + snake_size > banana_y):
        banana_x = random.randint(0, WIDTH - food_size)
        banana_y = random.randint(0, HEIGHT - food_size)
        snake_length += 3
        score += 3

        if score > high_score:
            high_score = score
            with open("highscore.txt", "w") as file:
                file.write(str(high_score))

        if score % 5 == 0:
            game_speed += 5

    if magic_visible and (snake_x < magic_x + food_size
        and snake_x + snake_size > magic_x
        and snake_y < magic_y + food_size
        and snake_y + snake_size > magic_y):
        magic_x = random.randint(0, WIDTH - food_size)
        magic_y = random.randint(0, HEIGHT - food_size)
        snake_length += 8
        score += 8
        game_speed += 5
        magic_visible = False
        magic_timer = 0

        if score > high_score:
            high_score = score
            with open("highscore.txt", "w") as file:
                file.write(str(high_score))

        if score % 5 == 0:
            game_speed += 5

    for obstacle in obstacles:

        if (
            snake_x < obstacle[0] + 20
            and snake_x + snake_size > obstacle[0]
            and snake_y < obstacle[1] + 20
            and snake_y + snake_size > obstacle[1]
        ):
            game_over = True



    pygame.display.update()

pygame.quit()

```