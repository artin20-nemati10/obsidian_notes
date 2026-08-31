#python_code
```
import pygame
import random
pygame.init()
Width = 800
Height = 700
screen = pygame.display.set_mode((Width,Height))

pygame.display.set_caption("Space Shooter")

clock = pygame.time.Clock()
#--------------------player information----------------
player_x = 400
player_y = 600

player_width = 50
player_height = 50

player_speed = 7

lives = 3
#------------------------Bullets------------------------
bullets =[]

bullet_speed = 10
shoot_delay = 150
last_shot = 0
#------------------------Enemies------------------------
enemies = []

enemy_speed = 2

explosions = []
#-----------------------Score---------------------------
score = 0
font = pygame.font.SysFont(None, 40)

for i in range(6):
	enemy_x = random.randint(0,Width - 40)
	enemy_y = random.randint(-300, -40)

	enemies.append([enemy_x,enemy_y])
#---------------------Stars---------------------
stars = []
for star in range(100):
	stars.append([random.randint(0,Width),random.randint(0,Height)])
game_over = False
running = True
while running :
	clock.tick(60)

	for event in pygame.event.get():
		if event.type == pygame.QUIT:
			running = False

		if event.type == pygame.MOUSEBUTTONDOWN:
				if event.button == 1:
					bullet_x = player_x + player_width //2 - 2
					bullet_y = player_y
					bullets.append([bullet_x,bullet_y])


	keys = pygame.key.get_pressed()
	#--------------------------------Moving Options--------------------
	if keys[pygame.K_LEFT]:
		player_x -= player_speed

	if keys[pygame.K_RIGHT]:
		player_x += player_speed

	if player_x < 0:
		player_x = 0

	if player_x > Width - player_width:
		player_x = Width - player_width

	for bullet in bullets:
		bullet[1] -= bullet_speed

	bullets = [bullet for bullet in bullets if bullet[1] > 0]

	for enemy in enemies:
		enemy[1] += enemy_speed

	for enemy in enemies:
		if enemy[1] > Height:
			lives -= 1
			enemy[0] = random.randint(0, Width - 40)
			enemy[1] = random.randint(-300, -40)
	for enemy in enemies:
		if (
			player_x < enemy[0] + 40
		    and player_x + player_width > enemy[0]
			and player_y < enemy[1] + 40
			and player_y + player_height > enemy[1]
		    ):
			lives -= 1

			enemy[0] = random.randint(0, Width - 40)
			enemy[1] = random.randint(-300, -40)
	for bullet in bullets[:]:
		for enemy in enemies:
			if (
				bullet[0]< enemy[0] + 40
				and bullet[0] + 5 > enemy[0]
				and bullet[1] < enemy[1] +40
				and bullet[1] + 15 > enemy[1]
			):
				if bullet in bullets:
					bullets.remove(bullet)
				explosions.append([enemy[0] + 20 , enemy[1] + 20,20])
				enemy[0] = random.randint(0,Width - 40)
				enemy[1] = random.randint(-300, -40)

				score += 1

				break
	mouse_buttons = pygame.mouse.get_pressed()
	if mouse_buttons[0]:

		current_time = pygame.time.get_ticks()
		if current_time - last_shot > shoot_delay:
			bullet_x = player_x + player_width //2 - 2
			bullet_y = player_y
			bullets.append([bullet_x,bullet_y])
			last_shot = current_time
	if lives <= 0:
		game_over= True
	if game_over:
		screen.fill((10,10,10))

		big_font = pygame.font.SysFont(None, 80)

		text = big_font.render("GAME OVER",True ,(255,0,0))

		screen.blit(text, (220,250))
		pygame.display.update()
		continue
	#---------------------Drawing the Objects--------------------
	screen.fill((5,5,20))
	for star in stars:
		pygame.draw.circle(screen,(255,255,255),star, 1)
#######################################

	pygame.draw.polygon(
	    screen,
	    (0, 220, 255),
	    [
	        (player_x + 25, player_y),
	        (player_x + 5, player_y + 40),
	        (player_x + 45, player_y + 40)
	    ]
	)


	pygame.draw.circle(
	    screen,
	    (100, 255, 255),
		    (player_x + 25, player_y + 20),
	    8
	)


	pygame.draw.polygon(
	    screen,
	    (0, 150, 255),
	    [
	        (player_x + 5, player_y + 40),
	        (player_x - 10, player_y + 50),
	        (player_x + 10, player_y + 50)
	    ]
	)


	pygame.draw.polygon(
	    screen,
	    (0, 150, 255),
	    [
	        (player_x + 45, player_y + 40),
	        (player_x + 60, player_y + 50),
	        (player_x + 40, player_y + 50)
	    ]
	)


	pygame.draw.rect(
	    screen,
	    (150, 150, 150),
		    (player_x + 10, player_y + 40, 6, 10)
	)


	pygame.draw.rect(
	    screen,
	    (150, 150, 150),
	    (player_x + 34, player_y + 40, 6, 10)
	)


	pygame.draw.polygon(
	    screen,
	    (255, 120, 0),
	    [
		        (player_x + 13, player_y + 50),
	        (player_x + 8, player_y + 65),
	        (player_x + 18, player_y + 65)
	    ]
	)

	pygame.draw.polygon(
	    screen,
	    (255, 120, 0),
	    [
	        (player_x + 37, player_y + 50),
	        (player_x + 32, player_y + 65),
	        (player_x + 42, player_y + 65)
	    ]
	)

	##########################
	for bullet in bullets:
		pygame.draw.rect(screen,
		                 (0,255,0),
		                 (bullet[0], bullet[1], 4, 18))

	for enemy in enemies:
		pygame.draw.circle(screen,
		                   (225,0,0),
		                   (enemy[0] + 20, enemy[1] + 20),
		                   20)
		pygame.draw.circle(screen,
		                   (225,225,0),
		                   (enemy[0] + 15, enemy[1] + 15),
		                   3)
		pygame.draw.circle(screen,
		                   (225,225,0),
		                   (enemy[0] + 25, enemy[1] + 15),
		                   3)

	score_text = font.render(f"Score: {score}", True, (255,255,255))
	screen.blit(score_text,(10,10))

	lives_text = font.render(f"Lives: {lives}", True, (255,255,255))
	screen.blit(lives_text,(650,10))


	for explosion in explosions[:]:
		pygame.draw.circle(screen,
		                   (255,150,0),
		                   (explosion[0], explosion[1]),explosion[2])

		pygame.draw.circle(screen,
		                   (225,225,0),
		                   (explosion[0], explosion[1]),explosion[2] // 2)
		pygame.draw.circle(screen,
		                   (225,225,255),
		                   (explosion[0], explosion[1]),explosion[2] // 4)
		explosion[2] -= 1

		if explosion[2] <= 0:
			explosions.remove(explosion)
	pygame.display.update()

pygame.quit()
```