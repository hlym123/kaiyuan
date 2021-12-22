海龟画图 
======================================================

显示屏分辨率为320*240，海龟画图画布原点为显示屏中心点 

应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

:: 

    '''
     导入 turtle 模块 
    '''
    from openaie import turtle
    
    '''
     方法：放下画笔（移动画笔绘图） 
    '''
    turtle.pendown()

    '''
     方法：抬起画笔（移动画笔不绘图） 
    '''
    turtle.pendup()    
    
    '''
     方法：设置画笔颜色 
     参数：r,g,b 取值范围：0~255
    '''    
    turtle.pencolor(r,g,b)

    '''
     方法：设置画笔大小 
     参数：width
    '''    
    turtle.pensize(width)

    '''
     方法：清除绘图 
    '''    
    turtle.clear()

    '''
     方法：复位，回到初始状态  
    '''    
    turtle.reset()

    '''
     方法：移动画笔到指定位置 
     参数：x
     参数：y
    '''    
    turtle.goto(x,y)

    '''
     方法：顺时针方向旋转指定角度 
     参数：angle
    '''    
    turtle.right(angle)
    
    '''
     方法：逆时针方向旋转指定角度 
     参数：angle
    '''    
    turtle.left(angle)

    '''
     方法：向前移动 
     参数：step — 步进值
    '''    
    turtle.forward(step)

    '''
     方法：向后移动
     参数：step — 步进值
    '''    
    turtle.backward(step)

    '''
     方法：设置画笔坐标x  
     参数：x
    '''    
    turtle.setx(x)

    '''
     方法：设置画笔坐标y  
     参数：y
    '''    
    turtle.sety(y)

    '''
     方法：写文本  
     参数：text — 文本内容
    '''
    turtle.write(text)    
    
    '''
     方法：读取画笔当前位置(x, y)
     返回：x, y 
    '''
    turtle.position()
    
    '''
     方法：返回画笔坐标x 
     返回：x
    '''
    turtle.xcor()
    
    '''
     方法：返回画笔坐标y 
     返回：y 
    '''
    turtle.ycor()
    
     '''
     方法：回到原点 
    '''
    turtle.home()
    
    '''
     方法：返回画笔位置到坐标(x, y)的距离  
     参数：x 水平位置
     参数：y 垂直位置
     返回：两点距离  
    '''
    turtle.distance(x, y)
    
    '''
     方法：返回画笔位置与位置(x, y)的夹角
     参数：x 水平位置
     参数：y 垂直位置
     返回：夹角  
    '''
    turtle.towards(x, y)
 
    '''
     方法：返回画笔当前方向 
     返回：
    '''
    turtle.heading()
    
    '''
     方法：  
    '''
    
     '''
     方法：
    '''
    
    '''
     方法：
    '''
 
 

画太阳花
++++++++++++++++++++++++++++++++++++++++++++++++++++++
::

    import time
    from openaie import turtle  # 导入 turtle 模块


    turtle.clear(color=(0,0,0)) # 设置背景为黑色
    turtle.penup()              # 抬起画笔
    turtle.goto(-100, -8)       # 移动画笔到位置(-100, -8)
    turtle.pendown()            # 放下画笔，开始绘图
    turtle.pencolor(255,255,0)  # 设置画笔颜色为黄色 
    for i in range(50): 
        turtle.forward(200)     # 向前移动 200
        time.sleep_ms(100)
        turtle.left(170)        # 逆时针方向旋转 170°



画五角星
++++++++++++++++++++++++++++++++++++++++++++++++++++++
正五边形的内角为(n-2)*180/n = (5-2)*180/5 = 108°，五角星内角为36°
 
::

    import math, time 
    from openaie import turtle


    length = 160   
    turtle.clear(color=(0,0,0)) # 设置背景为黑色
    turtle.pensize(3)           # 设置画笔大小为3
    turtle.pencolor(255,255,0)  # 设置画笔颜色为黄色
    turtle.penup()
    # 根据五角星边长 length 计算画笔起始位置 
    turtle.goto(-(length*math.cos(math.radians(36))-length/2), -length*math.sin(math.radians(72))/2)
    turtle.pendown()
    turtle.left(36) # 逆时针旋转36°
    for i in range(5): 
        turtle.forward(length)
        turtle.left(144)
        time.sleep_ms(500)  
 

画正多边形
++++++++++++++++++++++++++++++++++++++++++++++++++++++        

::

    import time
    from openaie import turtle 


    NUM = 6  # 边数
    L = 50   # 边长
    interior_angle = (NUM-2)*180/NUM # 计算多边形内角
    turtle.clear(color=(0,0,0))
    turtle.penup()
    turtle.goto(-25,-50)
    turtle.pendown()
    turtle.pensize(3)
    turtle.pencolor(0,0,255)
    for i in range(NUM): 
        turtle.forward(L)
        turtle.left(180-interior_angle) 
        time.sleep_ms(300)

        
画树 
++++++++++++++++++++++++++++++++++++++++++++++++++++++ 
树的颜色随机变化 

::

    from openaie import turtle
    import random


    def draw_colorful_tree(branch_len):  
        r = random.randint(0, 255) # 生成 0~255 的随机数
        g = random.randint(0, 255)
        b = random.randint(0, 255)
        turtle.pencolor(r, g, b)   # 根据随机数设置画笔颜色
        if branch_len>5:
            turtle.forward(branch_len)
            turtle.right(20)
            draw_colorful_tree(branch_len-15)
            turtle.left(40)
            draw_colorful_tree(branch_len-10)
            turtle.right(20)
            turtle.backward(branch_len)
            
    turtle.clear(color=(0,0,0))
    while True:
        turtle.reset()
        turtle.left(90)
        turtle.penup()
        turtle.pensize(3)
        turtle.backward(120)
        turtle.pendown()
        draw_colorful_tree(70) 

    
绘制科赫雪花 
++++++++++++++++++++++++++++++++++++++++++++++++++++++
按键切换科赫雪花阶数

::

    from openaie import turtle, button1, button2
    import time, random
    

    def draw_koch(size, n):
        if n==0:
            turtle.forward(size)
        else:
            for angle in [0, 60, -120, 60]:
                turtle.left(angle)
                draw_koch(size/3, n-1)

    def koch_curve(n):
        turtle.clear(color=(0,0,0))
        turtle.pensize(1)
        turtle.penup()
        turtle.goto(-100, 60)
        r = random.randint(0, 255)
        g = random.randint(0, 255)
        b = random.randint(0, 255)
        turtle.pencolor(r, g, b)
        turtle.pendown()
        level = n # 科赫雪花阶数
        draw_koch(200, level)
        turtle.right(120)
        draw_koch(200, level)
        turtle.right(120)
        draw_koch(200, level)

    num = 1
    koch_curve(num)

    while (True):
        if button1.is_press(): # 检测到按键按下
            time.sleep_ms(10)  # 延时消抖
            if button1.is_press():
                num += 1
                if num > 4:
                    num = 1
                koch_curve(num)
            while (button1.is_press()) : # 等待按键释放
                pass
        if button2.is_press(): # 检测到按键按下
            time.sleep_ms(10)
            if button2.is_press():
                num -= 1
                if num < 1:
                    num = 4
                koch_curve(num)
            while (button2.is_press()) : # 等待按键释放
                pass

