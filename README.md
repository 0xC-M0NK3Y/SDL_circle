# SDL_circle
Two function missing in SDL2, SDL_RenderDrawCircle and SDL_RenderFillCircle.  
  
### Prototypes
```c
int SDL_RenderDrawCircle(SDL_Renderer *renderer, int x, int y, int radius);  
int SDL_RenderFillCircle(SDL_Renderer *renderer, int x, int y, int radius);  
```
### Overview
Basically reimplementing this algorithm.  
https://fr.wikipedia.org/wiki/Algorithme_de_trac%C3%A9_d%27arc_de_cercle_de_Bresenham  
See below in Algorithm.  

Its optimised by calling SDL_RenderDrawPoints or SDL_RenderDrawLines instead of SDL_RenderDrawPoint and SDL_RenderDrawLine multiple times.  
Feel free to use it as you want.  
 
### Algorithm
```
procédure tracerCercle (entier rayon, entier x_centre, entier y_centre)
	déclarer entier x, y, m ;
	x ← 0 ;
	y ← rayon ;             // on se place en haut du cercle 
	m ← 5 - 4*rayon ;       // initialisation
	Tant que x <= y         // tant qu'on est dans le second octant
		tracerPixel( x+x_centre, y+y_centre ) ;
		tracerPixel( y+x_centre, x+y_centre ) ;
		tracerPixel( -x+x_centre, y+y_centre ) ;
		tracerPixel( -y+x_centre, x+y_centre ) ;
		tracerPixel( x+x_centre, -y+y_centre ) ;
		tracerPixel( y+x_centre, -x+y_centre ) ;
		tracerPixel( -x+x_centre, -y+y_centre ) ;
		tracerPixel( -y+x_centre, -x+y_centre ) ;
		si m > 0 alors	//choix du point F
			y ← y - 1 ;
			m ← m - 8*y ;
		fin si ;
		x ← x + 1 ;
		m ← m + 8*x + 4 ;
	fin tant que ;
fin de procédure ;
```
