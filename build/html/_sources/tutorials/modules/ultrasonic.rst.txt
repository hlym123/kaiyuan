超声波测距传感器
======================================================
量程：2~200cm；误差：±1%

.. figure:: ul_sensor.png 
   :width: 260
   :align: center
   
应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     导入 ultrasonic 模块 
    '''
    from openaie import ultrasonic
    
    '''
     类：超声波测距传感器
     参数:
        port: 端口号 -- 1~8 
    '''
    class ultrasonic(port)
    
    '''
     方法：触发测量 
    '''
    ultrasonic.measure()
    
    '''
     方法：读取测量值 
     说明：在触发测量后等待100ms，再读取测量值
    '''
    ultrasonic.read()
    
    
案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 超声波测距显示** 

::

    import time
    from openaie import *


    us_sensor = ultrasonic(4)
            
    while True:
        us_sensor.measure() # 触发测量  
        time.sleep_ms(120)    # 等待测量完成 
        print("distance: %.1fcm\r\n"%us_sensor.read()) # 读取测量结果 
        time.sleep_ms(380) 

------------------------------------------------------

        