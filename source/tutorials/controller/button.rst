按键  
======================================================
板载两个用户按键 button1 和 button2，按键按下为低电平，弹起为高电平。 

应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::
    
    '''
     导入  button1, button2 模块 
    '''
    from openaie import button1, button2
    
    '''
     方法：检查按键是否按下
     返回值：
        按键按下 -- True 
        按键弹起 -- False
    ''' 
    button1.is_press() 
    button2.is_press() 
    

案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 按键检测** 

::

    import time 
    from openaie import button1, button2

    while (True):
        if button1.is_press(): # 检测到按键按下
            time.sleep_ms(10) # 延时消抖
            if button1.is_press():
                print("button 1 press")
            while (button1.is_press()) : # 等待按键释放
                pass
        if button2.is_press(): # 检测到按键按下
            time.sleep_ms(10) # 延时消抖
            if button2.is_press():
                print("button 2 press")
            while (button2.is_press()) : # 等待按键释放
                pass
				
.. Note:: 机械按键在按下瞬间会存在一定的抖动，此时按键连接引脚读取的电平状态不稳定，可通过一定的延时略过此时的状态。
    
------------------------------------------------------
      