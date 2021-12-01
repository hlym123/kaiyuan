按键  
======================================================
按键按下接低电平，弹起接高电平。

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
            time.sleep_ms(10)
            if button1.is_press():
                print("button 1 press")
            while (button1.is_press()) : # 等待按键释放
                pass
        if button2.is_press(): # 检测到按键按下
            time.sleep_ms(10)
            if button2.is_press():
                print("button 2 press")
            while (button2.is_press()) : # 等待按键释放
                pass
    
------------------------------------------------------
      