# Flappy-bird-python
1/14/25
#kenny
#10/14/25
#1/14 Daily Code: FLAPPY BIRB

import pygame
import random
pygame.init()

screen = pygame.display.set_mode((800, 600)) #game window
pygame.display.set_caption("Flappy Bird") #game window title
clock = pygame.time.Clock() #handle Fps
font = pygame.font.Font(None, 36) #Font for displaying the score
font2 = pygame.font.Font(None, 72)#larger font

score = 0 #Score variable

#Bird class
class Bird:
    def __init__(self):
        self.y = 400
        self.velocity = 0
        
    def flap(self):
        self.velocity = -3 # flap
        
    def physics(self):
        self.velocity += 0.1 # gravity
        self.y += self.velocity
        
    def draw(self):
        pygame.draw.rect(screen, (255, 0, 0), (50, self.y, 30, 30))
 

# Pipe class
class Pipe:
    def __init__(self, x):
        self.x = x
        self.height = random.randint(50, 400)
        self.gap = 150 # Gap size between topp and bottom pipes
        
    def move(self):
        self.x -= 2 # Move pipes to the left
    
    def draw(self):
        # Draw the top pipe
        pygame.draw.rect(screen, (0, 255, 0), (self.x, 0, 50, self.height))
        # Draw the bottom pipe
        pygame.draw.rect(screen, (0, 255, 0), (self.x, self.height + self.gap, 50, 600 - (self.height + self.gap)))

bird = Bird()
pipes = []
spawn_pipe = 0 #timer for pipe spawn


        
running = True
while running: #game loop============================================
    clock.tick(60)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.MOUSEBUTTONDOWN:
            bird.flap()
    bird.physics()

#spawn pipes
spawn_pipe += 1 #increment timer
if spawn_pipe >= 150: #pipe is spawned every 150 frames
    pipes.append(Pipe(800)) #this INSTANTIATES a new pipe and puts it in the list!
    spawn_pipe = 0 #reset timer

#move pipes!
for pipe in pipes: #walk through list of pipes
    pipe.move() #move each pipe
    if check_collision(50, bird.y pipe.x, pipe.height): # check collision with bird
        running = False #kill game if u hit a pipe
#destroy pipes that have gone off screen !!!!!!!!!!!!!!!!!!!!!WORK!!!!!!!!!!!!!
i = len(pipes) - 1 #start at end of list
while i >= 0:
    if pipes[i]
  
  # Render section-----------------------------------------------------
    screen.fill((0, 0, 0))
  
    bird.draw()
    
    score_text = font.render("Score:", True, (255, 255, 255))
    screen.blit(score_text, (650, 20))
    score_text2 = font.render(str(score), True, (255, 255, 255))
    screen.blit(score_text2, (750, 20))
    
    pygame.display.flip()
  
  
#---end of game loop------------------
    
pygame.quit()
