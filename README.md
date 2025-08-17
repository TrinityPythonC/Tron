Tron game from the 1980s


![Tron picture](https://github.com/TrinityPythonC/Tron/blob/main/wikifiles/wikiTron.png)


# Getting started
This game is programed with Python, and so you will need to install Python to run it.

# tkinter

We use the Python built in library tkinter to display a window with graphics

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x600")

mainwin.mainloop()
```


# The Canvas

Now add a canvas to draw on

```
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x600")

canvas1= Canvas(mainwin,width=800,height=600, bg = "black")
canvas1.place(x=0,y=0)

mainwin.mainloop()
```


# The Grid
Now create a grid to store the location of the dots that make up the lines. We use this to detect collisions between the lines

```    
from tkinter import *

mainwin = Tk()
mainwin.geometry("800x600")

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
mainwin.geometry("800x600")

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
mainwin.geometry("800x600")

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
mainwin.geometry("800x600")

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



todo:
- [x] make todo list
- [ ] fix program code indentation
- [ ] add more pages
- [ ] read https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#images


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
