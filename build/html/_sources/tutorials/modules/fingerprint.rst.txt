指纹识别模块
======================================================
 

.. figure:: ul_sensor.png 
   :width: 260
   :align: center
   
应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     导入 fingerprint_sensor 模块 
    '''
    from openaie import fingerprint_sensor
    
    '''
     类：指纹识别模块 
     参数:
        port: 端口号 -- 1或7 
    '''
    class fingerprint(port)
    
    '''
     方法：录入指纹
     @id: 
    '''
    fingerprint.enroll(id)
    
    '''
     方法：验证指纹  
    '''
    fingerprint.verify()
    
    '''
     方法：删除指纹
     @id: 
    '''
    fingerprint.delete(id)
    
    
案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 指纹录入与识别** 

::

    import time 
    from openaie import button1, button2, fingerprint_sensor


    fingerprint = fingerprint_sensor(1)
     
    id_num = 1

    while (True):
        if button1.is_press(): # 检测到按键按下
            time.sleep_ms(10) # 延时消抖
            if button1.is_press():
                print("\n===============")
                print("  准备录入指纹  ")
                print("===============")
                fingerprint.enroll(id_num)
                id_num+=1
            while (button1.is_press()) : # 等待按键释放
                pass
            
        if button2.is_press(): # 检测到按键按下
            time.sleep_ms(10) # 延时消抖
            if button2.is_press():
                print("\n===============")
                print("  开始指纹识别  ")
                print("===============")
                fingerprint.verify()
            while (button2.is_press()) : # 等待按键释放
                pass
        


------------------------------------------------------

        