#python_code
```
import pygame

pygame.init()

Width = 800
Height = 600

screen = pygame.display.set_mode((Width, Height))

pygame.display.set_caption("Ping Pong")

clock = pygame.time.Clock()

# ---------------paddle information--------------------
paddle_x = 50
paddle_y = 250

paddle_width = 20
paddle_height = 100

paddle_speed = 0

paddle2_x = Width - 70
paddle2_y = 250

paddle2_width = 20
paddle2_height = 100

paddle2_speed = 0


# ---------------Ball information----------------------
ball_x = 400
ball_y = 300

ball_radius = 10

ball_speed_y = 5
ball_speed_x = 5

player_score = 0
computer_score = 0

font = pygame.font.SysFont(None, 50)

game_over = False

winner = ""

game_mode = None
menu = True
running = True
while running:
	clock.tick(60)
	# ------------------------------Event-----------------------
	for event in pygame.event.get():
		if event.type == pygame.QUIT:
			running = False

		if event.type == pygame.KEYDOWN:
			if event.key == pygame.K_UP:
				paddle2_speed = -7
			elif event.key == pygame.K_DOWN:
				paddle2_speed = 7

			if event.key == pygame.K_w:
				paddle_speed = -7
			elif event.key == pygame.K_s:
				paddle_speed = 7

		if event.type == pygame.KEYUP:
			if event.key == pygame.K_UP:
				paddle2_speed = 0
			elif event.key == pygame.K_DOWN:
				paddle2_speed = 0

			if event.key == pygame.K_w:
				paddle_speed = 0
			elif event.key == pygame.K_s:
				paddle_speed = 0

		if game_over and event.key == pygame.K_r:
			player_score = 0
			computer_score = 0

			ball_x = Width // 2
			ball_y = Height // 2

			ball_speed_x = 5
			ball_speed_y = 5

			paddle_y = 250
			paddle2_y = 250

			winner = ""
			game_over = False

		if menu and event.type == pygame.KEYDOWN:

			if event.key == pygame.K_1:
				game_mode = "AI"
				menu = False
			elif event.key == pygame.K_2:
				game_mode = "2P"
				menu = False
	# ---------------------Start Menu-----------------------
	if menu:
		screen.fill((25, 35, 45))
		title = font.render("Pong", True, (255, 255, 255))
		mode1 = font.render("1 - Single Player", True, (255, 255, 255))
		mode2 = font.render("2 - Two players", True, (255, 255, 255))

		screen.blit(title, (330, 150))
		screen.blit(mode1, (250, 250))
		screen.blit(mode2, (250, 320))
		pygame.display.update()

		continue


	if game_over:
		big_font = pygame.font.SysFont(None, 80)
		text = big_font.render(winner, True, (255, 255, 0))
		screen.blit(text, (180, 250))

		restart_text = font.render("Press R To Restart", True, (255, 255, 255))
		screen.blit(restart_text, (250, 350))
		pygame.display.update()
		continue
	screen.fill((25, 35, 45))
	pygame.draw.line(screen, (100, 100, 100), (Width // 2, 0), (Width // 2, Height), 3)

	pygame.draw.circle(screen, (100, 100, 100), (Width // 2, Height // 2), 60, 30)
	paddle_y += paddle_speed
	ball_x += ball_speed_x
	ball_y += ball_speed_y

	if paddle_y < 0:
		paddle_y = 0

	if paddle_y > Height - paddle_height:
		paddle_y = Height - paddle_height

	if ball_y <= ball_radius:
		ball_speed_y *= -1

	if ball_y >= Height - ball_radius:
		ball_speed_y *= -1
	# -----------------------------touch-----------------------
	if (
								ball_x - ball_radius < paddle_x + paddle_width
					and ball_x + ball_radius > paddle_x
				and ball_y > paddle_y
			and ball_y < paddle_y + paddle_height
	):
		ball_x = paddle_x + paddle_width + ball_radius
		ball_speed_x *= -1.05
		offset = ball_y - (paddle_y + paddle_height / 2)
		ball_speed_y = offset / 10

	if (
								ball_x - ball_radius < paddle2_x + paddle2_width
					and ball_x + ball_radius > paddle2_x
				and ball_y > paddle2_y
			and ball_y < paddle2_y + paddle2_height
	):
		ball_x = paddle2_x - ball_radius
		ball_speed_x *= -1.05

		offset = ball_y - (paddle2_y + paddle2_height / 2)
		ball_speed_y = offset / 10
	#--------------------------AI moving-----------------------------
	if game_mode == "AI":
		if ball_y < paddle2_y + paddle2_height // 2:
			paddle2_y -= 4

		if ball_y > paddle2_y + paddle2_height // 2:
			paddle2_y += 4

	if paddle2_y < 0:
		paddle2_y = 0

	if paddle2_y > Height - paddle2_height:
		paddle2_y = Height - paddle2_height
	#-----------------------------------second player---------------
	if game_mode == "2P":
		paddle2_y += paddle2_speed

	# -----------------------Shapes-----------------------
	pygame.draw.rect(screen, (255, 255, 255),
	                 (paddle_x, paddle_y,
	                  paddle_width,
	                  paddle_height))

	pygame.draw.rect(screen, (255, 255, 255),
	                 (paddle2_x, paddle2_y,
	                  paddle2_width,
	                  paddle2_height))

	pygame.draw.circle(screen, (25, 255, 255),
	                   (ball_x, ball_y),
	                   ball_radius)
	# -----------------------Scores----------------------
	if ball_x < 0:
		computer_score += 1
		ball_x = Width // 2
		ball_y = Height // 2

		ball_speed_x = 5
		ball_speed_y = 5

	if ball_x > Width:
		player_score += 1
		ball_x = Width // 2
		ball_y = Height // 2

		ball_speed_x = 5
		ball_speed_y = 5

	if player_score >= 5:
		game_over = True
		winner = "YOU WIN!"
	if computer_score >= 5:
		game_over = True
		winner = "COMPUTER WINS!"
	# ---------------------------------------------------

	player_text = font.render(str(player_score),
	                          True,
	                          (255, 255, 255))
	computer_text = font.render(str(computer_score),
	                            True,
	                            (255, 255, 255))

	screen.blit(player_text, (Width // 2 - 25, 20))
	screen.blit(computer_text, (Width // 2 + 10, 20))

	pygame.display.update()

pygame.quit()

```