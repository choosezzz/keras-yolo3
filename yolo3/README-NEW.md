#####自定义训练步骤

1. 将待训练图片放到 VOCdevkit/VOC2007/JPEGImages/ 路径下

2. 将标注文件xml格式，放到 VOCdevkit/VOC2007/Annotations 路径下

3. 执行 VOCdevkit/VOC2007/ 路径下的test.py文件，将会在VOCdevkit/VOC2007/Main路径下随机
   生成对应的训练集、测试集等txt文件
   
4. 生成的数据集不能供yolov3直接使用。需要运行voc_annotation.py ，在voc_annotation.py
   需改你要检测的种类 classes = ["示例：RBC","等等，你要训练识别的种类"]，运行该文件，在
   项目根目录生成对应的文件 2007_test.txt 2007_train.txt  2007_val.txt
   
5. 修改参数 yolo3.cfg ,搜索yolo，修改对应的配置：filters = ## filter：3*(5+len(classes))
   classes = ##检测种类数目，random = 原来是1，显存小改为0
 
6. 修改model_data下的voc_classes.txt为自己训练的类别，例如：RBC (一个种类一行)

7. 运行mytrain.py 训练结束将会生成对应的trained_weight.h5 (因为程序中有logs/000/目录，你需
   要创建这样一个目录，这个目录的作用就是存放自己的数据集训练得到的模型。不然程序运行到最后会
   因为找不到该路径而发生错误)
   
8.修改yolo.py文件，将如下路径改为自定义的文件，就可以用来识别自己的模型图片了
        "model_path": 'model_data/yolo.h5',
        "anchors_path": 'model_data/yolo_anchors.txt',
        "classes_path": 'model_data/coco_classes.txt',