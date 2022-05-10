卫星定位导航模块
======================================================
GPS/北斗双模定位导航模块，可用于导航，定位，授时等。

通信接口UART，默认波特率：9600，数据位8，停止位1。数据格式为 NEMA0183 标准，输出频率为1Hz。板载指示灯在定位成功时闪烁。

定位精度10m，首次定位时间大于32秒。

 
   
应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     导入 gps 模块 
    '''
    from openaie import gps
    
    '''
     类：gps
     参数:
        port: 端口号 -- 1或7 
        location_formatting: 经纬度格式
            'ddm' -- Decimal Degree Minute (ddm) - 40° 26.767′ N
            'dms' -- Degrees Minutes Seconds (dms) - 40° 26′ 46″ N
            'dd'  -- Decimal Degrees (dd) - 40.446° N
    '''
    class gps(port, location_formatting='ddm')
    
    '''
     方法：更新数据 
     @return 接收到的语句，未接收到信息返回None
    '''
    stat = gps.update()
    
    '''
     变量：可见卫星数 
    '''
    gps.satellites_in_view
    
    '''
     变量：使用卫星数 
    '''
    gps.satellites_in_use
    
    '''
     变量：经度（字符串）
    '''
    gps.longitude_string
    
    '''
     变量：纬度（字符串）
    '''
    gps.latitude_string
    
    '''
     变量：经度（浮点数）
    '''
    gps.longitude[0]
    
    '''
     变量：纬度（浮点数）
    '''
    gps.latitude[0]
    
    '''
     变量：海拔（m）
    '''
    gps.altitude
    
    '''
     变量：速度（km/h）
    '''
    gps.speed[2]
    
    '''
     变量：日期（UTC时间，北京时间+8）
        日，月，年
    '''
    day, month, year = gps.date[:]
    
    '''
     变量：时间戳（UTC时间，北京时间+8）
        时，分，秒
    '''
    hour, minute, second = gps.timestamp[:]
    
 
案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 信息读取显示** 

::

    from machine import UART, Pin
    import lcd
    from openaie import*


    my_gps = gps(port=1, location_formatting='dd')

    lcd.rotation(0)
    lcd.set_backlight(100)
     
    sentence_count = 0
    while True:
        stat = my_gps.update() # 更新数据 
        if stat: # 接收到语句
            #print(stat)
            stat = None
            sentence_count += 1 # 接收语句计数
            
            lcd.clear(color=(0,0,0))
             
            # 卫星信息
            lcd.draw_string(10, 30, '可见卫星: %s 颗'%my_gps.satellites_in_view, fc=(0,0,255), bc=(0,0,0))
            lcd.draw_string(10, 50, '使用卫星: %s 颗'%my_gps.satellites_in_use, fc=(0,0,255), bc=(0,0,0))
            # 位置 
            lcd.draw_string(10, 70, '经度: '+my_gps.longitude_string(), fc=(0,0,255), bc=(0,0,0))
            lcd.draw_string(10, 90, '纬度: '+my_gps.latitude_string(), fc=(0,0,255), bc=(0,0,0))
            lcd.draw_string(10, 110, '海拔: %d m'%my_gps.altitude, fc=(0,0,255), bc=(0,0,0))
            lcd.draw_string(10, 130, '速度: %.2f km/h'%my_gps.speed[2], fc=(0,0,255), bc=(0,0,0))
            # 日期 UTC
            day, month, year = my_gps.date[:]
            date_string = "20%02d/%02d/%02d"%(year, month, day)
            lcd.draw_string(10, 150, date_string, fc=(0,0,255), bc=(0,0,0))
            # 时间 UTC
            hour, minute, second = my_gps.timestamp[:]
            t = " %02d:%02d:%02d "%(hour, minute, second)
            lcd.draw_string(110, 150, t, fc=(0,0,255), bc=(0,0,0))
            
            lcd.draw_string(10, 200, ('count: %d'%  sentence_count), fc=(0,0,255), bc=(0,0,0))
            
            #lcd.draw_string(10, 270, '东经: %.5f'%my_gps.longitude[0], fc=(0,0,255), bc=(0,0,0))
            #lcd.draw_string(10, 290, '北纬: %.5f'%my_gps.latitude[0], fc=(0,0,255), bc=(0,0,0))
            lcd.display()
 
------------------------------------------------------
















        