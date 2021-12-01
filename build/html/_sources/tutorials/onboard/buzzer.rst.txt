蜂鸣器 
======================================================
无源蜂鸣器，可通过不同频率的信号驱动，发出不同音调的声音。

应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

    
::

    ''' 
     方法：蜂鸣器鸣响
     参数：
        freq -- 频率
    ''' 
    buzzer.tone(freq) 

    ''' 
     方法：关停蜂鸣器
    ''' 
    buzzer.no_tone()    

         
案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 鸣响测试**

::

    import time
    from openaie import buzzer
    
    tone_list = (289, 661, 700, 786, 882, 990, 1112) # Do、Re、Mi、Fa、Sol、La、Si
    for i in range(7):    
        buzzer.tone(tone_list[i])
        time.sleep_ms(500)
    buzzer.no_tone()