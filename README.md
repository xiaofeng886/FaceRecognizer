# FaceRecognizer
iOS平台实时离线人脸检测、身份识别
## 环境
考虑移动平台的需要，使用技术 iOS 8.0+ & OpenCV（2.4.13 ios-framework）实现的人脸识别、解锁Demo。非FaceID ，只要有前置摄像头都可以使用。
* 录入
![(录入)](http://images0.cnblogs.com/blog2015/497279/201506/141204508639539.gif)
录入之前，可以更改你的数字标签。
点击开始后，轻轻转动头部，直到所有的红点变绿，录入完成。
* 识别
![(录入)](http://images0.cnblogs.com/blog2015/497279/201506/141204508639539.gif)
开始识别后，会有红框选中识别的面部，需要先通过活体检测，才会比对该面部的身份信息。
识别成功后，会弹出对应人身份的数字标签。
## 技术实现
主要步骤：视频提取 -> 人脸检测 -> 预处理 -> 人脸识别
### 视频提取
* 是用iphone手机前置摄像头来提取数据，截取视频流中每帧图像进行人脸检测。使用的是iOS原生的方法。
### 人脸检测
* 使用OpenCV自带的人脸Haar特征分类器和已经预训练好的 "haarcascade_frontalface_alt2.xml" 模型，进行人脸检测。
### 预处理
* 截取检测到的人脸， 将图像灰度化，统一大小（80，80）的尺寸，归一化处理。
### 人脸识别
* 使用OpenCV的LBPH人脸识别器，对图像进行识别。
* 需要先训练LBPH人脸识别器，为了识别效果更好，提前将反面的人脸素材倒入工程进行预训练，人脸库使用的是ORL的人脸库，包含40个人，每个人10张不同姿态的灰度照片。
* 在工程启动时进行预训练，之后在录入目标人脸的时候，更新训练后的模型。
* 在识别时，可以得到预测的目标人脸标签和置信度。
## 其他
* 为了识别的鲁棒性更好，录入时特意选取目标的8张不同姿态的人脸进行训练。
* 由于是使用单2d摄像头，工程针对目标有活体检测的处理，可以有效避免图片骗过识别器从而解锁的情况。
