# 一、本周工作
1、板载计算机内存问题

2、采集数据, 准备开展点云拼接研究工作

3、给王博文采集大区域范围的单目RGB数据

4、读稻田的论文




# 二、具体细节
## 2.1 板载计算机内存问题
- 板载计算机总内存为128G(可扩展), 可用空间在62G左右

 ![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/29.jpg)

- 测试：
  - 同时订阅左右目RGB图片，内存从```62G --> 17G```, 用时：```9min```
  - 订阅左目RGB图片，内存从```62G --> 16G```, 用时：```15min```
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/22.png)

## 2.2 采集数据
- mapping 
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/25.png)

视频链接：https://www.bilibili.com/video/BV1BW4y1M7Lk/?spm_id_from=333.999.0.0&vd_source=88bceb64b89804ec0cf90b2e004bf688

- 3D build
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/26.png)

视频链接：https://www.bilibili.com/video/BV19K4116768/?spm_id_from=333.788.recommend_more_video.0&vd_source=88bceb64b89804ec0cf90b2e004bf688

- 雷达点云
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/27.png)

## 2.3 图片提取点云（.obj --> .pcd）
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/28.png)

采用的方法：https://www.zhihu.com/question/37577447


## 2.4 用cloudcompare软件手动拼接(思路)
https://www.bilibili.com/video/BV1mu411z7Vx/?spm_id_from=333.999.0.0&vd_source=88bceb64b89804ec0cf90b2e004bf688



# 三、遇到的问题及解决
## 3.1 录制的过程中报warn：rosbag record buffer exceed. dropping oldest queued message
![](https://github.com/ZYJ-Group/darren_pty/blob/main/darren_pty/pic(Ninth%20week)/24.jpg)

原因：
录制bag包的流程分为2个部分，一个流程订阅消息，并且放入队列，另一个流程从队列中读取消息，并且保存到bag文件中。可能当录制内存过大bag包时，写入磁盘速度过慢导致队列中的消息无法及时取出，使得队列buff溢出


解决：提高rosbag的缓存空间

rosbag record -o /home/inin/data/ -b 4096 订阅对应的话题 // 将缓存空间设置成4096

参考：
https://zhuanlan.zhihu.com/p/438698296

https://blog.csdn.net/lemonxiaoxiao/article/details/113357811


