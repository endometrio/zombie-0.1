import pygame
import math
import time



import random
from pygame.constants import MOUSEBUTTONUP




        
NEGRO    = (   0,   0,   0)
BLANCO    = ( 255, 255, 255)
AZUL     = (  50,  50, 255)
VERDE    = (   0, 255,   0)
VERDEosc  = (   0, 100,   0)
ROJO      = ( 255,   0,   0)

pygame.mixer.init()

        
    
class explosion(pygame.sprite.Sprite):
    def __init__(self):
        self.image = pygame.image.load("blood3.png").convert_alpha()
        self.rect = self.image.get_rect()
        self.counter = 0
    def update(self):
        self.counter = self.counter + 1   

   
class weapon(pygame.sprite.Sprite):
    def __init__(self):
        self.image = pygame.image.load("truck.png").convert_alpha()
        self.rect = self.image.get_rect()
        self.rect.bottom,self.rect.left=(670,320)
    def mostrar (self,superficie):
        superficie.blit(self.image,self.rect)   


class healBar(pygame.sprite.Sprite):


    def __init__(self):
        self.healthbar = pygame.image.load("healthbar.png")
        self.health = pygame.image.load("health.png")
        self.corazon = pygame.image.load("corazon.png")
        self.healthvalue = 195
        self.imageHUD= pygame.image.load("bullets.png")
        self.rect2 = self.imageHUD.get_rect()
        self.rect2.x=5
        self.rect2.y=600
    def mostrar (self,superficie):
        superficie.blit(self.imageHUD,self.rect2)
        superficie.blit(self.corazon,(10,4))
        superficie.blit(self.healthbar, (45,5))
        for health1 in range(self.healthvalue):
            superficie.blit(self.health, (health1+48,8))    
            
            
class player(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self) 
        self.santa=pygame.image.load("santa.png")
        
        
        
    def mostrar(self,superficie):
        superficie.blit(self.santa,(360,520))
        

class house(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self) 

        self.image = pygame.image.load("coin.png").convert_alpha()
        self.rect = self.image.get_rect()
        self.rect.bottom,self.rect.left = (630,690)
        self.life = 40
    def mostrar(self,superficie):
        superficie.blit(self.image,self.rect)
                   

class fondo(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self) 

        self.image = pygame.image.load("inter.png").convert_alpha()     
        self.rect = self.image.get_rect()
        self.rect.bottom,self.rect.left = (680,0)
    def mostrar(self,superficie):
        superficie.blit(self.image,self.rect)
        

class mira(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self) 

        self.image = pygame.image.load("mira3.png").convert_alpha()
        self.rect = self.image.get_rect()
        self.rect.left,self.rect.top = (0,0)
        
                
        self.rect.left -= self.rect.width/2      
        self.rect.top -= self.rect.height/2 
    def mostrar (self,superficie):
        superficie.blit(self.image,self.rect)
        self.rect.left,self.rect.bottom = pygame.mouse.get_pos()            
        
            
class npc(pygame.sprite.Sprite):
    def __init__(self):
        
        pygame.sprite.Sprite.__init__(self) 

        self.imagen1=pygame.image.load("zomb.png").convert_alpha()
        self.imagen2=pygame.image.load("zomb2.png").convert_alpha()
        self.imagen3=pygame.image.load("zomb3.png").convert_alpha()
        self.imagen4=pygame.image.load("blood1.png").convert_alpha()
        self.imagen5=pygame.image.load("blood2.png").convert_alpha()
        self.imagen6=pygame.image.load("blood3.png").convert_alpha()
        self.imagen7=pygame.image.load("blood4.png").convert_alpha()
        self.imagen8=pygame.image.load("blood5.png").convert_alpha()
        self.imagen9=pygame.image.load("blood6.png").convert_alpha()
        
        
        self.imagenes = [[self.imagen1,self.imagen2,self.imagen3],[self.imagen4,self.imagen4]]
        
        self.imagen_actual = 0
        self.image = self.imagenes[self.imagen_actual][0]
        self.rect = self.image.get_rect()
        self.rect.left,self.rect.bottom = (740,600)
        self.life = 4
        self.estamuerto = 0
        self.estaenmovimiento = True
        self.rect.width,self.rect.height = (50,50)
        self.rect.x = random.randrange(800,1500)
        self.rect.y = random.randrange(200,412)
        self.murio = False
        
    def update(self):
        
        if self.life > 0:
            self.estamuerto = 0
            self.rect.x -= 3
        elif self.life < 0:
            self.murio = True
            self.estamuerto = 1
            self.rect.x -= 0
        self.image = self.imagenes[self.estamuerto][self.imagen_actual]
                
        self.animacion()
           
        
              
                         
    def animacion (self):
        self.imagen_actual = self.imagen_actual + 1
        if self.imagen_actual > (len(self.imagenes[1])-1):
            self.imagen_actual = 0        
          
 
    
   
    def draw(self,surface):
         
        
        surface.blit(self.image,self.rect)   
        if self.rect.left < 0:
            self.kill()
            
          
  
class npc2(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self) 

        self.imagen1=pygame.image.load("gordo1.png").convert_alpha()
        self.imagen2=pygame.image.load("gordo2.png").convert_alpha()
        self.imagen3=pygame.image.load("gordo3.png").convert_alpha()
        self.imagen9=pygame.image.load("blood6.png").convert_alpha()
        self.imagen9=pygame.image.load("blood6.png").convert_alpha()
        
        
        self.imagenes = [[self.imagen1,self.imagen2,self.imagen3],[self.imagen9,self.imagen9]]
        
        self.imagen_actual = 0
        self.image = self.imagenes[self.imagen_actual][0]
        self.rect = self.image.get_rect()
        self.rect.left,self.rect.bottom = (740,600)
        self.life = 12
        self.estamuerto = 0
        self.estaenmovimiento = True
        self.rect.width,self.rect.height = (50,50)
        self.rect.x = random.randrange(800,1160)
        self.rect.y = random.randrange(200,412)
        
        self.murio = False
    def update(self):
        
        if self.life > 0:
            self.estamuerto = 0
            self.rect.x -= 2
        elif self.life < 0:
            self.murio = True
            self.estamuerto = 1
            
            self.rect.x -= 0
        self.image = self.imagenes[self.estamuerto][self.imagen_actual]
        self.animacion()
        
        
              
                         
    def animacion (self):
        self.imagen_actual = self.imagen_actual + 1
        if self.imagen_actual > (len(self.imagenes[1])-1):
            self.imagen_actual = 0        
          
 
    
   
    def mostrar(self,surface):
        surface.blit(self.image,self.rect)   
                

class bullet(pygame.sprite.Sprite):
    def __init__(self,x=0,y=0):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.image.load("mira3.png").convert_alpha()
        self.rect = self.image.get_rect()
        
        self.x = x
        self.y = y
        self.cantidad = 6 
        self.estacargada = True
    def update(self,superficie):
        superficie.blit(self.image,self.rect)
        
        self.rect.center =  pygame.mouse.get_pos() 
    
    
            
    
    
    def recarga(self):
        self.cantidad += 5
            
              
    
         
            
def main():
    pygame.init()
    pygame.mixer.init()
    guncharge = pygame.mixer.Sound("guncharge.wav")
    pygame.mixer.music.load("chapel.mp3")
    disparo = pygame.mixer.Sound("Pistol.wav")
    zombie = pygame.mixer.Sound("zombieattack.wav")
    zombie.set_volume(0.1)
    zombie_hit = pygame.mixer.Sound("zombiehit.wav")
    zombie_dead = pygame.mixer.Sound("zombiedead.wav")
    scream = pygame.mixer.Sound("scream.wav")
    scream.set_volume(0.1)
    
    dry = pygame.mixer.Sound("dry.wav")
    
    
    pygame.init()
    pantalla=pygame.display.set_mode((800,640))
    salir=False
    reloj1= pygame.time.Clock()
    bull = bullet()
    
    truck = weapon()
    heal_bar = healBar()
    house1 = house()
    zombie1 = npc()
    zombie4 = npc2()

    
    
    player1=player()
    
    fondo1=fondo()
    bullet_list = pygame.sprite.Group(())
    
    shoting = False
    
    all_sprite_list = pygame.sprite.Group()
    zombie_list = [npc(),npc(),npc(),npc(),npc(),npc(),npc(),npc(),npc(),npc()]
    zombie_list_gordo=[npc2(),npc2(),npc2()]
    zombie_sprite = pygame.sprite.Group(())
    zombie_sprite.add(zombie_list)
    zombie_sprite.add(zombie_list_gordo)
    all_sprite_list.add(zombie_sprite) 
    
                
    def player_scores( superficie):
        
        font1 = pygame.font.Font("fast99.ttf", 26)
        display_score = font1.render("Score: %d " % (score), True, BLANCO)
        superficie.blit(display_score,(600,0))
    
    score=0
    
    
    def bullet_cant(superficie):
        
        font2 = pygame.font.Font("fast99.ttf", 26)
        display_score = font2.render(str(bullet_canti) + "/" + str(bullet_cantiMax), True, BLANCO)
        superficie.blit(display_score,(70,605))
    
    bullet_canti = 6
    bullet_cantiMax = 24
    pygame.mixer.music.play()
    while salir!=True:
        
        for event in pygame.event.get():
            
            if event.type == pygame.QUIT:
                salir=True
            if event.type == pygame.MOUSEBUTTONDOWN and bull.estacargada == True :
                shoting = True
                
                   
               
                bullet_canti -= 1
                disparo.play()
                
                
                bull.cantidad -= 1
                if bull.cantidad <= 0:
                    bullet_canti = 0
                    dry.play()
                    
                    bull.estacargada = False   
                        
                
            if event.type == pygame.KEYDOWN and bull.cantidad <= 0 and bullet_cantiMax >= 6:        
                if event.key == pygame.K_r :
                    guncharge.play()
                    bullet_canti += 6
                    bullet_cantiMax -= 6
                    bull.recarga()  
                    bull.estacargada = True     
                        
                    
               
                    
            if event.type == MOUSEBUTTONUP:
                shoting = False
             
                    
                    
                    
               
            
            
        
            
        for zomb in zombie_sprite:
            if zomb.rect.colliderect(bull)and zomb.murio == False  and shoting == True :
                zomb.life -= 1
                zomb.rect.x += 2
                zombie_dead.play()
                if zomb.life <=0:
                    score += 6
            if zomb.rect.left < 0:
                heal_bar.healthvalue -= 13                  
                zomb.rect.x = 890   
                if heal_bar.healthvalue < 0:
                    scream.play()
                       
        
        pygame.mouse.set_visible(False)    
           
                           
        reloj1.tick(30)
       
        
        
        
             
        pantalla.fill((NEGRO))
        
        fondo1.mostrar(pantalla)
        bull.update(pantalla)
        bullet_cant(pantalla)
        player_scores(pantalla)
        truck.mostrar(pantalla)
        house1.mostrar(pantalla)
        player1.mostrar(pantalla) 
        heal_bar.mostrar(pantalla)

        
        all_sprite_list.update()
        all_sprite_list.draw(pantalla)
        
        
        
       
        pygame.display.update()

                
    pygame.quit()

main()
