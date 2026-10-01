#python_code
```
import pygame
import random
pygame.init()



Width = 800
Height = 600
screen = pygame.display.set_mode((Width, Height))

pygame.display.set_caption("Racing game")

clock = pygame.time.Clock()
lanes = [135,235,335,435,535,635]

line_offset = 0
grass_offset = 0
tree_offset = -100

start_menu = True
# ---------------------Player Car-------------------
car_x = 375
car_y = 500

car_width = 50
car_height = 50

car_speed = 8
#-----------------Images------------------------------------
car_image = pygame.image.load("car_red_3.png").convert_alpha()
car_image = pygame.transform.scale(car_image,(40,60))

enemy_image = pygame.image.load("car_blue_3.png").convert_alpha()
enemy_image = pygame.transform.scale(enemy_image,(40,60))
enemy_image = pygame.transform.rotate(enemy_image, 180)

grass_image = pygame.image.load("land_grass.png").convert_alpha()
grass_image = pygame.transform.scale(grass_image,(100,100))

car_image = pygame.image.load("car_red_3.png").convert_alpha()
car_image = pygame.transform.scale(car_image,(40,60))

tree_image = pygame.image.load("tree_small.png").convert_alpha()
tree_image = pygame.transform.scale(tree_image,(90,90))


# ---------------------Enemy Car-------------------
enemies = []
for i in range(4):
	enemy_x = random.choice(lanes)
	enemy_y = -150 * i

	enemies.append([enemy_x, enemy_y])

enemy_width = 40
enemy_height = 60

enemy_speed = 6
#------------------------Coin----------------------
coin_x = random.choice(lanes)
coin_y = -200

coin_radius = 15
coin_speed = enemy_speed

diamond_x = random.choice(lanes)
diamond_y = -800
diamond_speed = enemy_speed
diamond_radius = 12

game_over = False
over_font = pygame.font.SysFont(None, 80)


score = 0
font = pygame.font.SysFont(None, 40)
running = True
while running:
	clock.tick(60)
	#-------------------------Events---------------------------
	for event in pygame.event.get():
		if event.type == pygame.QUIT:
			running = False
		if game_over and event.type == pygame.KEYDOWN:
			if event.key == pygame.K_r:
				score = 0

				car_x = 375
				car_y = 500

				enemy_speed = 6

				coin_x = random.choice(lanes)
				coin_y = -200

				enemies = []

				for i in range(4):
					enemy_x = random.choice(lanes)
					enemy_y = -150 * i
					enemies.append([enemy_x, enemy_y])

				game_over = False
		if start_menu and event.type == pygame.KEYDOWN:
			if event.key == pygame.K_SPACE:
				start_menu = False
	if game_over:


		text = over_font.render("GAME OVER",True, (255,0,0))

		screen.blit(text ,(200,200))

		score_text = font.render(f"Score:{score}",True, (0,0,0))
		screen.blit(score_text ,(300,300))

		R_text = font.render("Press R To Restart",True, (255,255,0))
		screen.blit(R_text ,(250,350))

		pygame.display.update()

		continue
	if start_menu:
		screen.fill ((20,20,20))

		title = over_font.render("RACING GAME", True, (255,255,255))
		start_text = font.render("Press Space To Start", True, (255,255,0))
		move_text = font.render("Left / Right : Move", True, (200,200,200))

		screen.blit(move_text, (250,370))
		screen.blit(title, (180,200))
		screen.blit(start_text, (250,320))

		pygame.display.update()

		continue
	#--------------------------Moves---------------------------
	keys = pygame.key.get_pressed()

	if keys[pygame.K_LEFT]:
		car_x -= car_speed

	if keys[pygame.K_RIGHT]:
		car_x += car_speed

	if car_x < 100:
		car_x = 100

	if car_x > 650:
		car_x = 650

	for enemy in enemies:
		enemy[1] += enemy_speed

	for enemy in enemies:
		if enemy[1] > Height:
			enemy[1] = -100
			enemy[0] = random.choice(lanes)
			score += 1

			if score % 5 == 0:
				enemy_speed += 0.5
	coin_y += enemy_speed
	if coin_y > Height:
		coin_y = -200
		coin_x = random.choice(lanes)

	diamond_y += enemy_speed
	if diamond_y > Height:
		diamond_y= -1000
		diamond_x = random.choice(lanes)

	line_offset += enemy_speed
	if line_offset >= 60:
		line_offset = 0

	grass_offset += enemy_speed
	if grass_offset >= 100:
		grass_offset = 0

	tree_offset += enemy_speed
	if tree_offset >= 150:
		tree_offset = 0


	#--------------------------Touches----------------------------
	for enemy in enemies:
		if (
			car_x < enemy[0] + enemy_width
			and car_x + car_width > enemy[0]
			and car_y < enemy[1] + enemy_height
			and car_y + car_height > enemy[1]
		):
			game_over = True
	if (
			car_x < coin_x + coin_radius
			and car_x + car_width > coin_x
			and car_y < coin_y + coin_radius
			and car_y + car_height > coin_y
		):
		score += 5
		coin_x = random.choice(lanes)
		coin_y = -200

	if (
			car_x < diamond_x + diamond_radius
			and car_x + car_width > diamond_x
			and car_y < diamond_y + diamond_radius
			and car_y + car_height > diamond_y
		):
		score += 20
		diamond_x = random.choice(lanes)
		diamond_y = -100
	#----------------------------Objects--------------------------
	screen.fill((50, 150, 50))



	pygame.draw.rect(screen,
	                 (70,70,70),
	                 (100,0,600,Height))

	for y in range(-60, Height, 60) :
		pygame.draw.rect(screen,
		                 (255,255,255),
		                 (200,y + line_offset, 3, 20))
		pygame.draw.rect(screen,
		                 (255,255,255),
		                 (300,y + line_offset, 3, 20))
		pygame.draw.rect(screen,
		                 (255,255,255),
		                 (400,y + line_offset, 3, 20))
		pygame.draw.rect(screen,
		                 (255,255,255),
		                 (500,y + line_offset, 3, 20))
		pygame.draw.rect(screen,
		                 (255,255,255),
		                 (600,y + line_offset, 3, 20))
	for y in range(-100,Height,100):
		screen.blit(grass_image, (0,y+ grass_offset))
		screen.blit(grass_image, (700,y+ grass_offset))

	for y in range(-150,Height + 150, 150):
		screen.blit(tree_image, (5,y + tree_offset))
		screen.blit(tree_image, (705,y + tree_offset))


	screen.blit(car_image, (car_x, car_y))

	for enemy in  enemies:

		screen.blit(enemy_image, (enemy[0],enemy[1]))

	pygame.draw.circle(screen,
	                   (255,215,0),
	                   (coin_x,coin_y),
	                   coin_radius)
	pygame.draw.circle(screen,
	                   (255,255,100),
	                   (coin_x,coin_y),
	                   8)

	pygame.draw.polygon(
	    screen,
	    (0,225, 255),
	    [
	        (diamond_x, diamond_y - 12),
	        (diamond_x + 12, diamond_y),
	        (diamond_x, diamond_y + 12),
		    (diamond_x - 12, diamond_y)
	    ]
	)
	pygame.draw.polygon(
	    screen,
	    (225,225, 255),
	    [
	        (diamond_x, diamond_y - 6),
	        (diamond_x + 6, diamond_y),
	        (diamond_x, diamond_y + 6),
		    (diamond_x - 6, diamond_y)
	    ]
	)

	score_text = font.render(f"Score:{score}",True, (255,255,255))

	screen.blit(score_text ,(10,10))

	pygame.display.update()

pygame.quit()

```

### Images
**![[tree_small.png]]

![[car_blue_3.png]]

![[car_red_3.png]]

![[land_grass.png]]