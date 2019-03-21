.. _slam_orb_slam2:

`ORB_SLAM2 <https://github.com/raulmur/ORB_SLAM2>`_ 如何整合
==============================================================


在 MYNT® EYE 上运行 ORB_SLAM2 ，请依照这些步骤：
------------------------------------------------

1. 下载 `MYNT-EYE-S-SDK <https://github.com/slightech/MYNT-EYE-S-SDK.git>`_ 及安装。
2. 按照一般步骤安装 ORB_SLAM2 。
3. 更新 ``distortion_parameters`` 和 ``projection_parameters`` 参数到 ``<ORB_SLAM2>/config/mynteye_*.yaml``。
4. 在 MYNT® EYE 上运行例子。

双目样例
---------

* 按照 `ROS-StereoCalibration <http://wiki.ros.org/camera_calibration/Tutorials/StereoCalibration>`_ 或 OpenCV 校准双目摄像头，并在 ``<ORB_SLAM2>/config/mynteye_s_stereo.yaml`` 中更新参数。

* 运行脚本 ``build.sh`` ：

.. code-block:: bash

  chmod +x build.sh
  ./build.sh

* 依照下面样式运行双目样例：

.. code-block:: bash

  ./Examples/Stereo/stereo_mynt_s ./Vocabulary/ORBvoc.txt ./config/mynteye_s_stereo.yaml true /mynteye/left/image_raw /mynteye/right/image_raw


ROS 下创建单目和双目节点
------------------------

* 添加 ``Examples/ROS/ORB_SLAM2`` 路径到环境变量 ``ROS_PACKAGE_PATH`` 。打开 ``.bashrc`` 文件，在最后添加下面命令行。 ``PATH`` 为当前 ``ORB_SLAM2`` 存放路径:

.. code-block:: bash

  export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/ORB_SLAM2/Examples/ROS

* 运行脚本 `build_ros.sh` ：

.. code-block:: bash

  chmod +x build_ros.sh
  ./build_ros.sh


Stereo_ROS 例子
~~~~~~~~~~~~~~~~

  * 按照 :ref:`slam_okvis` 中的``获取相机校准参数`` 得到 ``distortion_parameters`` 和 ``projection_parameters`` 参数，并在 ``<ORB_SLAM2>/config/mynteye_s_stereo.yaml`` 中更新参数。

  * 运行 ORB_SLAM2 ``Stereo_ROS`` 例子

1.运行mynteye节点

.. code-block:: bash

  cd [path of mynteye-s-sdk]
  make ros
  source ./wrappers/ros/devel/setup.bash
  roslaunch mynt_eye_ros_wrapper mynteye.launch

2.打开另一个命令行运行ORB_SLAM2

.. code-block:: bash

  rosrun ORB_SLAM2 mynteye_s_stereo ./Vocabulary/ORBvoc.txt ./config/mynteye_s_stereo.yaml true /mynteye/left/image_raw /mynteye/right/image_raw
