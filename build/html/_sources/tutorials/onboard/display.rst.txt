
液晶显示屏
====================================================== 
分辨率：240*320(QVGA)


应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     方法：初始化
    ''' 
    lcd.init()
    
    ''' 
     方法：清空显示
     参数：
        color: 24位，0~0xFFFFFF
    ''' 
    lcd.clear(color)
    
    '''
     方法：设置显示方向
     参数：
        r: 0, 1, 2, 3
    '''
    lcd.rotation(r)
    
    '''
     方法：设置背光亮度
     参数：
        val: 0~100
    '''
    lcd.set_backlight(val)
    
    '''
     方法：画字符 
     参数：
        x, y: 起始位置
        string: 字符串
        fc: 字体颜色
        bc: 背景色
    '''
    lcd.draw_string(x, y, string, fc, bc)
    
    '''
     方法：画线 
     参数：
        x0, y0: 起点位置
        x1, y1: 终点位置
        color: 线颜色
        thickness: 线宽
    '''
    lcd.draw_line(x0, y0, x1, y1, color, thickness=1)

    '''
     方法：画矩形 
     参数：
        x, y: 起始位置
        w, h：宽和高
        color: 线颜色
        thickness: 线宽
        fill: 是否填充
    '''
    lcd.draw_rectangle(x, y, w, h, color, thickness=1, fill=0)

    '''
     方法：画圆 
     参数：
        x, y: 圆心位置
        radius： 半径
        color: 线颜色
        thickness: 线宽
        fill: 是否填充
    '''
    lcd.draw_circle(x, y, radius, color, thickness=1, fill=0)
   

案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 绘图测试**
::

    import lcd

    lcd.set_backlight(80)
    lcd.clear(0)
    lcd.rotation(0)
    lcd.draw_line(10, 10, 80, 80, 0x00FF00, 5)
    lcd.draw_rectangle(100, 20, 80, 60, 0xFF0000, 8, 0)
    lcd.draw_circle(120, 160, 30, 0x0000FF, 1, 1)
    lcd.draw_string(20, 230, "lcd draw test", 0xFFFFFF, 0)


    
    
    
    
    
    
    



