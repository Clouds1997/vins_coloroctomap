## 具有彩色动态八叉树地图的vins
slam部分请看 SLAM framework [VINS-Mono](https://github.com/HKUST-Aerial-Robotics/VINS-Mono).
是基于VINS-RGBD这个工程进行修改的 [VINS-RGBD](https://github.com/STAR-Center/VINS-RGBD)
八叉树地图是根据 dre-slam进行修改的 [dre-slam] (https://github.com/ydsf16/dre_slam)

总体来说功能：
（1）定位是用vins-mono的地位
（2）vins-rgbd 在vins的基础上，对于深度的使用
（3）dre-slam 的具有回环功能的八叉树地图


## 1. Prerequisites（应该还不太全）
1.1. **Ubuntu** 16.04 or 18.04.

1.2. **ROS** version Kinetic or Melodic fully installation

1.3. **Ceres Solver**
Follow [Ceres Installation](http://ceres-solver.org/installation.html)

1.4. **Sophus**
```
  git clone http://github.com/strasdat/Sophus.git
  git checkout a621ff
```


## 2. Datasets 
Recording by RealSense D435i. Contain 9 bags in three different applicaions:
+ [Handheld](https://star-center.shanghaitech.edu.cn/seafile/d/0ea45d1878914077ade5/)
+ [Wheeled robot](https://star-center.shanghaitech.edu.cn/seafile/d/78c0375114854774b521/) ([Jackal](https://www.clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/))
+ [Tracked robot](https://star-center.shanghaitech.edu.cn/seafile/d/f611fc44df0c4b3d936d/)

Note the rosbags are in compressed format. Use "rosbag decompress" to decompress.

Topics:
+ depth topic: /camera/aligned_depth_to_color/image_raw
+ color topic: /camera/color/image_raw
+ imu topic: /camera/imu




## 3. Licence
The source code is released under [GPLv3](http://www.gnu.org/licenses/) license.
