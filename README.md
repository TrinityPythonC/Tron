Tron game from the 1980s


![Tron picture](https://github.com/TrinityPythonC/Tron/blob/main/wikifiles/wikiTron.png)


# Getting started
This game is programed with Python, and so you will need to install Python to run it.

# tkinter

We use the Python built in library tkinter to display a window with graphics

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

mainwin.mainloop()
```


# The Canvas

Now add a canvas to draw on

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

mainwin.mainloop()
```


# The Grid
Now create a grid to store the location of the dots that make up the lines. We use this to detect collisions between the lines

```    
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

grid = []  # playfield, 500 by 500    
for i in range(500):
    L=[]   
    for j in range(500):      
       L.append(0)    
    grid.append(L)    

mainwin.mainloop()
```

# Dots and Lines

This game is made up of dots and lines.

We use the `create_line()` function to create dots and then lines are made up of dots.

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

grid = []  # playfield, 500 by 500   
for i in range(500):
    L=[]   
    for j in range(500):      
       L.append(0)    
    grid.append(L)    

def drawdot(x,y,colour):
    global grid
    grid[x][y] = 1
    canvas1.create_line(x*4,y*4,x*4+4,y*4,width=4,fill=colour)

def drawline(x,y,dx,dy,n,colour):
    for i in range(n):
        drawdot(x+dx*i,y+dy*i,colour)

mainwin.mainloop()
```

# Walls
Now create the boundary with walls


```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

grid = []  # playfield, 500 by 500   
for i in range(500):
        L=[]   
        for j in range(500):      
           L.append(0)    
        grid.append(L)    


def drawdot(x,y,colour):
        global grid
        grid[x][y] = 1
        canvas1.create_line(x*4,y*4,x*4+4,y*4,width=4,fill=colour)

def drawline(x,y,dx,dy,n,colour):
        for i in range(n):
            drawdot(x+dx*i,y+dy*i,colour)

# draw walls
drawline(0,1,1,0,200,"yellow")
drawline(199,1,0,1,150,"yellow")
drawline(199,150,-1,0,200,"yellow")
drawline(0,150,0,-1,150,"yellow")

mainwin.mainloop()
```


# Player 1

Lets create Player 1

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x680")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

player1alive = True
x1 = 50   # player 1 x-location
y1 = 50   # player 1 y-location
dx1 = 0   # x1 speed
dy1 = 1   # y1 speed

grid = []  # playfield, 500 by 500   
for i in range(500):
        L=[]   
        for j in range(500):      
           L.append(0)    
        grid.append(L)    


def drawdot(x,y,colour):
        global grid
        grid[x][y] = 1
        canvas1.create_line(x*4,y*4,x*4+4,y*4,width=4,fill=colour)

def drawline(x,y,dx,dy,n,colour):
        for i in range(n):
            drawdot(x+dx*i,y+dy*i,colour)

# draw walls
drawline(0,1,1,0,200,"yellow")
drawline(199,1,0,1,150,"yellow")
drawline(199,150,-1,0,200,"yellow")
drawline(0,150,0,-1,150,"yellow")

mainwin.mainloop()
```


# Keyboard Input

We can easily test for keyboard input with tkinter

First bind the keyboard input to a function that we call `mykey()`

`mainwin.bind("<Key>", mykey)`

and define the function `mkey()`

```
def mykey(event):
       global dx1, dy1
       if event.char == "w":
         dy1 = -1
         dx1 = 0
       if event.char == "d":
         dy1 = 0
         dx1 = 1
       if event.char == "a":
         dy1 = 0
         dx1 = -1
       if event.char == "s":
         dy1 = 1
         dx1 = 0
```

# Movement!

To make our player move, we use a timer that gets called every 100 milliseconds:

`mainwin.after(100,timerupdate)`


and the function `timerupdate()` looks like this


```
def timerupdate():
       global x1,y1, player1alive
       if player1alive:
         x1 = x1 + dx1
         y1 = y1 + dy1
       if grid[x1][y1] == 1:  # collision with line
          player1alive = False
       drawdot(x1,y1,"blue")
       mainwin.after(100,timerupdate)
```

and we call `timerupdate()` just before `mainloop()` at the end of our program

```
mainwin.after(100,timerupdate)
mainwin.mainloop()
```


# Player 2

Finally, we add code for Player 2, which is just a copy of the code for Player 1

```
player2alive = True
x2 = 80 # player 2 x-location
y2 = 50 # player 2 y-location
dx2 = 0 # x2 speed
dy2 = 1 # y2 speed

def mykey(event):
    global dx1, dy1, dx2, dy2
    if event.char == "w":
        dy1 = -1
        dx1 = 0
    if event.char == "d":
        dy1 = 0
        dx1 = 1
    if event.char == "a":
        dy1 = 0
        dx1 = -1
    if event.char == "s":
        dy1 = 1
        dx1 = 0
    if event.char == "i":
        dy2 = -1
        dx2 = 0
    if event.char == "l":
        dy2 = 0
        dx2 = 1
    if event.char == "j":
        dy2 = 0
        dx2 = -1
    if event.char == "k":
        dy2 = 1
        dx2 = 0

def timerupdate():
    global x1,x2,y1,y2, player1alive, player2alive
    if player1alive:
      x1 = x1 + dx1
      y1 = y1 + dy1
    if player2alive:
      x2 = x2 + dx2
      y2 = y2 + dy2
    if grid[x1][y1] == 1:  # collision
       player1alive = False
    if grid[x2][y2] == 1:
       player2alive = False
    drawdot(x1,y1,"blue")
    drawdot(x2,y2,"red")
    mainwin.after(100,timerupdate)
```

# Collision Explosions

After a player collides with a wall, we can create an explosion as follows:

```
import random 
  
def explosion(x,y):
    drawdot(x,y, "black")
    for i in range(100):
        ex = random.randint(-4,4)
        ey = random.randint(-4,4)
        drawdot(x+ex,y+ey, "black")
    for i in range(3):
        ex = random.randint(-3,3)
        ey = random.randint(-3,3)
        drawdot(x+ex,y+ey, "white")
    canvas1.update()

def drawdot(x,y,colour):
    global grid
    grid[x][y] = 1
    if colour == "black":
        grid[x][y] = 0
    canvas1.create_line(x*4,y*4,x*4+4,y*4, width =4, fill=colour)
    
def timerupdate():
...
    if grid[x1][y1] == 1:
       if player1alive:
            explosion(x1,y1) 
       player1alive = False  
    if grid[x2][y2] == 1:
       if player2alive:
            explosion(x2,y2) 
       player2alive = False
```


# Printing the Score

We erase the contents of the window each time we start a level, and so we need to call `printscores()` each time we start a level
```
canvastext= Canvas(mainwin,width=784,height=64, bg = "black")
canvastext.place(x=6,y=607)
font1 = ("Arial",16,"bold")
def printscr(mytext,x,y,mycolour):
    canvastext.create_text(x,y,text=mytext, fill=mycolour,font=font1, anchor="sw") 

def printscores():  # all text gets deleted at the end of each game
    printscr("Player 1 keyboard controls: w, a, s, d",10,24,"red")
    printscr("Score: "+str(score1),160,49,"red")
    printscr("Player 2 keyboard controls: i, j, k, l",420,24,"blue")
    printscr("Score: "+str(score2),560,49,"blue")

printscores()

```


# Robot Player (AI)

First create variables for the AI player

```
AIalive = True
xai = 100  # AI x-location
yai = 50   # AI y-location
dxai = 0   # AI x speed
dyai = 1   # AI y speed
```


Now create a function to choose the direction for the AI player when it encounters a wall

```
def goclearAI():
    global dxai, dyai, AIalive
    dxai = 0
    dyai = 0
    godirections = []
    if grid[xai+1][yai] == 0:
        godirections.append("right")
    if grid[xai-1][yai] == 0:
        godirections.append("left")
    if grid[xai][yai+1] == 0:
        godirections.append("down")
    if grid[xai][yai-1] == 0:
        godirections.append("up")
    if godirections == []:
       if AIalive:
            explosion(xai,yai)
       AIalive = False
    else:
      go = random.choice(godirections)
      if go == "right": dxai = 1
      elif go == "left": dxai = -1
      elif go == "up": dyai = -1
      elif go == "down": dyai = 1
```

Here is the function to control the AI. Most of the time it does not change `dxai` and `dyai`, since the robot normally moves in a straight line. 
If it encounters a wall then the robot changes direction about 99% of the time.
If it does not encounter a wall then it makes a random turn about 1% of the time.

```
def controlAI():
    if grid[xai+dxai][yai+dyai] == 1:
        if random.randint(1,100) > 1 : # turn to avoid wall
           goclearAI()
    elif random.randint(1,100) > 98: # make a random turn
        goclearAI()
```

Finally, we update the position of the robot in `timerupdate()`:

```
def timerupdate():
    global x1,x2,y1,y2,xai,yai, player1alive, player2alive, AIalive
    controlAI()
...
    if AIalive:
      xai = xai + dxai
      yai = yai + dyai
    if grid[xai][yai] == 1:
       if AIalive:
            explosion(xai,yai)
       AIalive = False
    if AIalive:  
       drawdot(xai,yai,"light green")
```


# Starting Again

After two players have crashed, we start again by resetting all the variables:

```
def startagain():
    global x1,y1,dx1,dy1,x2,y2,dx2,dy2,xai,yai,dxai,dyai
    global player1alive, player2alive, AIalive
    global score1, score2
    if AIalive:
            print("AI wins!!!",200,200,"yellow")
    if player1alive:
        score1 = score1 + 1
        print("Player 1 wins!!!",100,200,"yellow")
    if player2alive:
        score2 = score2 + 1
        print("Player 2 wins!!!",100,200,"yellow")
    canvastext.delete("all")
    printscores()
    canvastext.update()
    canvas1.update()
    time.sleep(2)
    player1alive = True
    x1 = 50 
    y1 = 50 
    dx1 = 0 
    dy1 = 1
    player2alive = True
    x2 = 150 # player 2 x-location
    y2 = 50  # player 2 y-location
    dx2 = 0  # player 2 x-speed
    dy2 = 1  # player 2 y-speed
    AIalive = True
    xai = 100  # AI x-location
    yai = 50   # AI y-location
    dxai = 0   # AI x speed
    dyai = 1   # AI y speed
    canvas1.delete("all")
    cleargrid()
    drawwalls()
```
```
def cleargrid():
    global grid
    for i in range(500):
      for j in range(500):
          grid[i][j] = 0
```


Finally, add the following code to the end of `timerupdate`:

```
def timerupdate():
...
    alivecount = sum([player1alive, player2alive, AIalive])
    if alivecount <= 1:
        startagain()
    mainwin.after(100,timerupdate)

```



> [!TIP]
Look at our Wiki page  https://github.com/TrinityPythonC/Tron/wiki

> [!NOTE]
> This section is not complete

***

# section 1
## sub section 1
### sub sub section 1

***

here is a table

| one | two |
|----|---|
|three| four|

Here is a list

* one
  * (a)
  * (b)
* two

***
inline maths: $e=mc^2$

display maths:

$$ e^{i \pi} = -1 $$
  
***
link to code: (see https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-a-permanent-link-to-a-code-snippet) for instructions

https://github.com/TrinityPythonC/Tron/blob/2b7cfa6e061f79c59fdefadc75cd1b72d8149760/tron.py#L29-L54
