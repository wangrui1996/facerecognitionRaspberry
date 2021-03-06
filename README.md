
![wangrui](https://img.shields.io/wercker/ci/wercker/docs.svg)

# 树莓派上移植FaceNet(PC机上也可运行)

--------------------
<br>
<br>

FaceNet网路可以参考具体的论文["FaceNet: A Unified Embedding for Face Recognition and Clustering"](http://arxiv.org/abs/1503.03832)了解熟悉，源码主要参考了[Facenet](https://github.com/davidsandberg/facenet),以及[MTCNN
](https://github.com/davidsandberg/facenet/tree/master/src/align).自己对源码整体做了一些改动以及增加特征提取后的欧氏距离与数据库中对比的结果,或者使用SVM进行分类。


##环境配置

--------------------------

<br>
<br>

- 将[20180408-102900](https://drive.google.com/open?id=1R77HmFADxe87GmoLwzfgMu_HY0IhcyBz)下载解压到data/model/文件夹下。
- 进入[tensorflow-on-arm](https://github.com/lhelontra/tensorflow-on-arm/releases)下载最新版本的tensorflow或者选择自己需要的版本下载。通过pip3直接在树莓派上安装，
- '''sudo apt-get install python3-opencv''' 直接安装Opencv，
> 警告: 在树莓派上导入tensorflow 或者 cv2时,会因为缺乏相应的库而报错，只需将相应的库安装后，即可成功导入。接下来的库可以通过运行python3 main.py来查找，缺少什么库则直接通过Pip3安装即可。

<br>
<br>
<br>
<br>

##人脸检测

---------------

<br>
<br>


*检测结果示例可以在[data/result/record](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/result/record)文件夹下找到*

![Result](data/result/record/f.gif)

![Result](data/result/record/相机.gif)

<br>

首先我们需要在[data/config/camera.txt](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/config/camera.txt)文件中配置摄像头以及对应的名称。

| Label | Path |
|-------|-------------------|
| 相机   |   ./cera/2.mp4 |
|   f   |    0   |

可以知道名称可以随便取，而路劲可以是视频文件也可以是摄像头的索引号
<br>
<br>

欧氏距离进行分类



<br>

命令行输入:  (默认通过欧氏距离分类)

'''
python3 main.py 
'''

<br>
<br>

通过SVM进行分类:



<br>

'''
命令行输入 python3 main.py --mode 1 
'''

<br>
<br>

像人脸数据库中添加人脸

---------------

<br>

命令行运行:

'''
python3 main.py --mode 3
'''

然后选择在命令行中输入1.从摄像头中获取人脸图片，2.从视频中获取人脸图片，3.将[data/facedir](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/facedir)文件夹下的图片转换到人脸数据库[data/middle](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/middle)中。
<br>
- 如果选择 1:
则讲会从摄像头获取的人脸图片存储到[data/videoout](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/videoout)中,你需要在[data/middle](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/middle)创建相应的人脸文件夹，并且将videoout人脸图片放入middle文件夹中，因为数据库人脸读取是读取middle中的人脸图片进行对比。
- 如果选择 2:
你将在下一阶段选择对应的视频路径，之后将会将检测到的人脸输出至data/videoout中，之后步骤同1.
- 如果选择 3:
则会将data/facedir中的人脸图片转换至data/middlle中，但而且原人脸数据库中的人脸文件夹名称不会改变。

<br>
<br>

通过svm进行训练



<br>

我们需要通过前一步骤也就是通过添加数据库中的人脸放进data/middle中，然后命令行输入:

'''
python3 main.py --mode 2
'''

训练后的文件放入了[data/model/svm/model](https://github.com/wangrui1996/facerecognitionRaspberry/blob/master/data/model/svm/model)中



![Crates.io](https://img.shields.io/crates/l/rustc-serialize.svg)
