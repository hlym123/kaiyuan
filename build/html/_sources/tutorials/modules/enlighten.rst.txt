AI模块启蒙 
======================================================
 

.. figure:: enlighten_top.png 
   :width: 260
   :align: center
   
应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     导入 enlighten 模块 
    '''
    from openaie import enlighten
    
    '''
     类：AI模块启蒙
     参数:
        port: 端口号(1或7) 
    '''
    class enlighten(port)
    
    '''
     等待模块连接
    '''
    enlighten.wait_connect()
    
    '''
     设置模块工作模式
     @m: 
        "qrcode scan" -- 二维码扫描 
        "mask detect" -- 口罩检测 
        "image class" -- 图像检测分类 
    '''
    enlighten.set_mode(m)
    
    '''
     请求数据
     @m:
        "qrcode"      -- 二维码信息 
        "mask detect" -- 口罩检测结果 
        "image class" -- 图像检测分类结果  
    '''
    enlighten.request_data(m)
    
    '''
     读取二维码扫描结果
     @return 二维码信息 
    '''
    enlighten.read_qrcode_info()
    
    '''
     读取色块信息
     @return 
        [x, y, w, h, pixels] 
        x, y 为色块中心坐标
        w, h 为色块的宽和高
        pixels 为色块内像素数 
    
     Example:
        x, y, w, h, pixels = enlighten.read_blob_info()
        # 或者 
        res = enlighten.read_blob_info()
        x = res[0]
        y = res[1]
        w = res[2]
        h = res[3]
        pixels = res[4]
    '''
    enlighten.read_blob_info()
    
    
    '''
     读取检测结果
     @return 
        [x, y, w, h, classid, confidence] 
        x, y 为边界框的中心坐标
        w, h 为边界框的宽和高
        classid 为分类结果
        confidence 为置信度 
    
     Example:
        x, y, w, h, classid, confidence = enlighten.read_detect_info()
        # 或者 
        res = enlighten.read_detect_info()
        bbox = res[0:4]      # 边界框参数
        classid = res[4]     # 分类结果
        confidence = res[5]  # 置信度 
    '''
    enlighten.read_detect_info()
  
    
    
案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 二维码扫描** 

::

    import time, lcd
    from openaie import *

    dev = enlighten_com(1)      # 启蒙模块连接到端口1
    dev.wait_connect()          # 等待模块链连接
    dev.set_mode("qrcode scan") # 设为二维码扫描模式 

    lcd.clear(color=(0,0,0))
    lcd.rotation(0)
    lcd.draw_string(10, 10, "二维码扫描", fc=(0,0,255), bc=(0,0,0))
    lcd.display()

    while True:
        if dev.request_data("qrcode") : # 请求二维码扫描结果 
            info = dev.get_qrcode_info()
            lcd.clear(color=(0,0,0))
            lcd.draw_string(10, 10, info, fc=(0,0,255), bc=(0,0,0))
            lcd.display()
        time.sleep_ms(200)
    
**2. 口罩检测**
口罩检查模型的分类结果中，classid为0表示没有戴口罩，1表示戴了口罩。

分类标签映射 label_map = {0: 'unmask', 1: 'mask'}

::

    import time, lcd
    from openaie import * 

    dev = enlighten_com(1)      # 启蒙模块连接到端口1
    dev.wait_connect()          # 等待模块链连接
    dev.set_mode("mask detect") # 设为口罩检测 

    tts = tts(7)

    lcd.clear(color=(0,0,0))
    lcd.rotation(0)
    lcd.draw_string(10, 10, "口罩检测提醒", fc=(0,0,255), bc=(0,0,0))
    lcd.display()

    last_play_time = 0
    while True:
        if dev.request_data("mask detect") : # 请求二维码扫描结果 
            res = dev.get_mask_detect_info()
            classid = res[4] # 分类结果
            conf = res[5]    # 可信度
            if (classid == 0) :
                info = "请你带好口罩"
                print("没戴口罩，可信度%d%%"%(conf*100))
            else :
                info = "你好"
                print("戴了口罩，可信度%d%%"%(conf*100))
                
            delta = time.ticks_diff(time.ticks_ms(), last_play_time) 
            if (delta > 2000): # 播放间隔大于2S
                tts.play(info) # 语音播报
                last_play_time = time.ticks_ms()
                
            lcd.clear(color=(0,0,0))
            lcd.draw_string(10, 10, info, fc=(0,0,255), bc=(0,0,0))
            lcd.display()
        time.sleep_ms(200)

    
**3. 图像检测分类**

模块内置的图像检测分类模型能对以下20中物品检测识别

:: 

    # 分类标签映射 
    label_map = {0:'airplane', 
                 1:'bicycle',
                 2:'bird',
                 3:'steamship',
                 4:'bootle',
                 5:'bus',
                 6:'car',
                 7:'cat',
                 8:'cheer',
                 9:'ox',
                 10:'dining-table',
                 11:'dog',
                 12:'horse',
                 13:'motobike',
                 14:'person',
                 15:'flowerpot',
                 16:'sheep',
                 17:'sofa',
                 18:'train',
                 19:'tetevision'}
                
使用案例

::

    import time, lcd
    from openaie import *

    dev = enlighten_com(1)      # 启蒙模块连接到端口1
    dev.wait_connect()          # 等待模块链连接
    dev.set_mode("image class") # 设为图像分类

    tts = tts(7)

    lcd.clear(color=(0,0,0))
    lcd.rotation(0)
    lcd.draw_string(10, 10, "图像识别分类", fc=(0,0,255), bc=(0,0,0))
    lcd.display()

    # 20class 分类的分类标签 
    label = ("飞机", "自行车", "小鸟", "轮船", "瓶子", "公共汽车", "汽车", "猫", "椅子", "牛",  \
             "餐桌", "狗", "马", "摩托车", "人", "花盆", "羊", "沙发", "火车", "电视")

    last_play_time = 0
    while True:
        if dev.request_data("image class") : # 请求二维码扫描结果 
            res = dev.get_image_class_info()
            info = "识别为: %s, 可信度: %d%%"%(label[res[4]], res[5]*100)
            delta = time.ticks_diff(time.ticks_ms(), last_play_time) 
            if (delta > 2000): # 播放间隔大于2S
                tts.play(label[res[4]]) # 语音播报
                last_play_time = time.ticks_ms()
            lcd.clear(color=(0,0,0))
            lcd.draw_string(10, 10, info, fc=(0,0,255), bc=(0,0,0))
            lcd.display()
        time.sleep_ms(200)


------------------------------------------------------

        