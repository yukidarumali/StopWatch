# StopWatch
My first repository on GitHub
# template for "Stopwatch: The Game"
import simplegui
# define global variables

t= 0
x= 0
y= 0
running = None
# define helper function format that converts time
# in tenths of seconds into formatted string A:BC.D
def format(t):
    
    D = t %10
    C =( t %100-D)/10
    B =( t- C*10-D)/100
    A = 0
    while B > 5:
        B -= 6
        A +=1
    return str(A)+":"+str(B)+str(C)+"."+str(D)    
# define event handlers for buttons; "Start", "Stop", "Reset"

def start_handler():
    global running
    running =True
    timer.start()
    
def stop_handler():
    global t
    global x
    global y
    global running
    timer.stop()
    if running == True and t%10 == 0 :
        x +=1
        y +=1
    elif running ==True:
        y +=1
    running =False    
    
    
def reset_handler():
    global t
    global x
    global y
    timer.stop()
    t = 0
    x = 0
    y = 0
# define event handler for timer with 0.1 sec interval
def timer_handler():
    global t
    t +=1
timer = simplegui.create_timer(100,timer_handler)    
# define draw handler
def draw_handler(canvas):
    global t
   
    canvas.draw_text(format(t), (100, 200), 80, 'White')
    canvas.draw_text( str(x)+"/"+str(y) ,(320,50),40,'#7ad9df')
    canvas.draw_polygon([[70, 100], [70, 260],[330, 260] , [330, 100]], 20, 'White')
# create frame
frame = simplegui.create_frame("StopWatch",400,400)
frame.set_canvas_background('#feeed0')
start = frame.add_button("Start",start_handler,200)
stop = frame.add_button("Stop",stop_handler,200)
reset = frame.add_button("Reset",reset_handler,200)
# register event handlers
frame.set_draw_handler(draw_handler)
# start frame
frame.start()
# Please remember to review the grading rubric

