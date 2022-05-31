# memory_game
from turtle import *
from random import*
from time import*
bg_list= ['purple','brown','red','green','blue','royalblue']
bg = randint(0,5)
bgcolor(bg_list[bg])
level = 1

user_points = [0] * 25
comp_points = [0] * 25
print(user_points)
ht()
def write_text(x, y, size, c , text):
    penup()
    goto(x, y)
    pendown()
    color(c)
    style = ('b tabassom', size, 'bold italic')
    write(text, font=style, align='center')
write_text(-20,130,25,'pink','  welcome to :👇  ')
sleep(1)
write_text(-20,50,35,'gold','  Memory Game !! [let s go..]  ')
write_text(-20,30,16,'purple',' * Made by : Taha *  ')
sleep(5)
clear()
bg_game=['gray','brown','green','purple']
cg = randint(0,3)
bgcolor(bg_game[cg])
write_text(-20,130,25,'yellow',' * Memory Game *  ')

def draw_circle(n , c):
    goto(number_to_point(n))
    pendown()
    color(c)
    begin_fill()
    circle(25)
    end_fill()
    penup()    

def number_to_point(n):
    x = (n % 5 * 50 + 25 ) - 125
    y = (n // 5 * 50 ) - 125
    return x, y

def point_to_number(x, y):
    row = (y + 125) // 50
    col = (x + 125) // 50
    n = int(row * 5 + col)
    if user_points[n] == 0:
        draw_circle(n,'royalblue')
        user_points[n] = 1
    else:
        draw_circle(n,'bisque')
        user_points[n] = 0
 
def drawer():
    for i in range(25):
        draw_circle(i,'bisque')
        user_points[i] = 0
        comp_points[i] = 0
        
    random_list = sample (range(25), level)
    print(random_list)
    
    for i in random_list:
        draw_circle(i, 'gold')
        comp_points[i] = 1
    sleep(2)
    for i in random_list:
        draw_circle(i, 'bisque')
def complete():
    global level
    win = 1
    for i in range(25):
        if user_points[i] == comp_points[i] == 1 :
            draw_circle(i,'lightblue')
        elif comp_points[i] == 1 and user_points[i] == 0 :
            draw_circle(i, 'orange')
            win = 0
        elif comp_points[i] == 0 and user_points[i] == 1 :
            draw_circle(i, 'tomato')
            win = 0
    if win == 1:
        print('*** good job ! continue ...!^0^ ***')
        level = level + 1 
    else:
        print('*** Oh no ! Be careful! ~_~ ***')
        level = 1
    drawer()
      
   
ht()
penup()
speed(0)
drawer()

listen()

onkeypress(complete , 'Return')
onscreenclick( point_to_number )
