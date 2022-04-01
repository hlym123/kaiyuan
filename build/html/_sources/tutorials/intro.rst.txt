简介
======================================================  

“开元编程开发套件”是可用于Python教学、创客项目制作的可编程电子套件，
其由主控和功能模块组成。


.. figure:: 主控2.png 
   :width: 400
   :align: center

主控:
    + 开元

功能模块：
    + 1. 按键组
    + 2. 电位器
    + 3. 温湿度传感器 
    + 4. 超声波测距传感器
    + 5. 光照强度传感器
    + 6. 可编程全彩LED
    + 7. 电机风扇 
    + 8. 舵机 
    + 9. 语音识别模块

    
资料
++++++++++++++++++++++++++++++++++++++++++++++++++++++

`链接 <https://pan.baidu.com/s/1YOXh82LP8uwqedEcwYOmRg>`_ (提取码：rcx6) 

    
库说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

 openaie.py 是开元主控模块的二次封装

    没有找到端口问题 
 https://www.cnblogs.com/ccfwz/p/14862076.html

 
综合测试案例 
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::
  
    '''
     开元套件测试案例 
     硬件连接：
        可编程全彩LED       -- 端口1
        按键组              -- 端口2 
        电位器              -- 端口3 
        舵机                -- 端口4 
        温湿度传感器        -- 端口5
        光照强度传感器      -- 端口6
        电机风扇            -- 端口7 
        超声波测距传感器    -- 端口8
        
     实验现象：
         可编程全彩LED模块 3个LED 红蓝绿色跳变
         显示屏显示温湿度，光照强度，电位器值，超声波测量结果，按键状态
         电位器控制舵机和风扇转动（顺时针）
    '''
    import time, lcd 
    from openaie import *
    from machine import Timer

    rgb = rgb_led(1)             # 可编程全彩LED     -- 端口1
    bt2 = button_group(2)        # 按键组            -- 端口2 
    p = potentiometer(3)         # 电位器            -- 端口3 
    s = servo(4)                 # 舵机              -- 端口4 
    th = th_sensor(5)            # 温湿度传感器      -- 端口5
    light = light_sensor(6)      # 光照强度传感器    -- 端口6
    m = motor_fan(7)             # 电机风扇          -- 端口7
    us_sensor = ultrasonic(8)    # 超声波测距传感器  -- 端口8

    lcd.rotation(0)
    lcd.clear(color=0)

    c = 0
    def rgb_display(a):
        global c 
        if c == 0:
            for i in range(3):
                rgb.set(i, (20, 0, 0))  
        elif c == 1:
            for i in range(3):
                rgb.set(i, (0, 20, 0))  
        elif c == 2:
            for i in range(3):
                rgb.set(i, (0, 0, 20))  
        rgb.display()
        c += 1
        if c == 3:
            c = 0

    # 创建并开启500ms周期定时器        
    tim = Timer()
    tim.init(period=500, mode=Timer.PERIODIC, callback=rgb_display)

    time_sensor_update = time.ticks_add(time.ticks_ms(), 500)
    read_flag = False
    while True:
        if time.ticks_diff(time.ticks_ms(), time_sensor_update): # 500ms间隔
            if read_flag:
                read_flag = False
                time_sensor_update = time.ticks_add(time.ticks_ms(), 500)
                try :
                    th_info = "温度: %.1fC  湿度: %d%%"%(th.read_temperature(), th.read_humidity())
                    light_info = "光照强度: %dlux"%light.read()
                    dis_info = "距离: %dcm"%us_sensor.read()
                    lcd.clear(color=0)
                    lcd.draw_string(10, 16, th_info, fc=(0,0,255), bc=(0,0,0))
                    lcd.draw_string(10, 38, light_info, fc=(0,0,255), bc=(0,0,0))
                    lcd.draw_string(10, 60, dis_info, fc=(0,0,255), bc=(0,0,0))
                except:
                    pass
            else:
                read_flag = True
                try :
                    us_sensor.measure()
                except:
                    pass
               
        val = p.read() 
        m.set(val)
        s.write(math_map(val, 0, 100, 0, 180))
       
        if bt2.is_press(1):  
            lcd.draw_string(10, 110, "按键1 按下", fc=(255,0,0), bc=(0,0,0))
        else :
            lcd.draw_string(10, 110, "按键1 释放", fc=(0,255,0), bc=(0,0,0))
        if bt2.is_press(2):  
            lcd.draw_string(110, 110, "按键2 按下", fc=(255,0,0), bc=(0,0,0))
        else :
            lcd.draw_string(110, 110, "按键2 释放", fc=(0,255,0), bc=(0,0,0))
        

        lcd.draw_string(10, 82, "电位器值: %d "%val, fc=(0,0,255), bc=(0,0,0))
        lcd.display()
        time.sleep_ms(50)





------------------------------------------------------

 
        
 



    

 