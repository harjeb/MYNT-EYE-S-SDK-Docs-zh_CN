.. _get_img_params:

获取图像标定参数
==================

通过 API 的 ``GetIntrinsics()`` ``GetExtrinsics()`` 函数，就可以获取当前打开设备的图像标定参数和相机使用的模型。

.. tip::
  参数的具体含义可以参考 ``tools/writer/config`` 下的参数文件，其中
  S2100/S210A 对应的相机参数在 ``tools/writer/config/S210A``
  S1030 对应的相机参数在  ``tools/writer/config/S1030``
  equidistant表示等距模型，pinhole表示针孔模型

参考代码片段：

.. code-block:: c++

  auto &&api = API::Create(argc, argv);

  LOG(INFO) << "Intrinsics left: {" << *api->GetIntrinsicsBase(Stream::LEFT)
            << "}";
  LOG(INFO) << "Intrinsics right: {" << *api->GetIntrinsicsBase(Stream::RIGHT)
            << "}";
  LOG(INFO) << "Extrinsics right to left: {"
            << api->GetExtrinsics(Stream::RIGHT, Stream::LEFT) << "}";

参考运行结果，于 Linux 上：

.. code-block:: bash

  $ ./samples/_output/bin/tutorials/get_img_params
  I0510 15:00:22.643263  6980 utils.cc:26] Detecting MYNT EYE devices
  I0510 15:00:23.138811  6980 utils.cc:33] MYNT EYE devices:
  I0510 15:00:23.138849  6980 utils.cc:37]   index: 0, name: MYNT-EYE-S1000
  I0510 15:00:23.138855  6980 utils.cc:43] Only one MYNT EYE device, select index: 0
  I0510 15:00:23.210491  6980 get_img_params.cc:23] Intrinsics left: {width: 752, height: 480, fx: 736.38305001095545776, fy: 723.50066150722432212, cx: 356.91961817119693023, cy: 217.27271340923883258, model: 0, coeffs: [-0.54898645145016478, 0.52837141203888638, 0.00000000000000000, 0.00000000000000000, 0.00000000000000000]}
  I0510 15:00:23.210551  6980 get_img_params.cc:24] Intrinsics right: {width: 752, height: 480, fx: 736.38305001095545776, fy: 723.50066150722432212, cx: 456.68367112303980093, cy: 250.70083335536796199, model: 0, coeffs: [-0.51012886039889305, 0.38764476500996770, 0.00000000000000000, 0.00000000000000000, 0.00000000000000000]}
  I0510 15:00:23.210577  6980 get_img_params.cc:26] Extrinsics left to right: {rotation: [0.99701893306553813, -0.00095378124886237, -0.07715139279485062, 0.00144939967628305, 0.99997867219985104, 0.00636823256494144, 0.07714367342455503, -0.00646107164115277, 0.99699905125522237], translation: [-118.88991734400046596, -0.04560580387053091, -3.95313736911933855]}

完整代码样例，请见 `get_img_params.cc <https://github.com/slightech/MYNT-EYE-S-SDK/blob/master/samples/tutorials/data/get_img_params.cc>`_ 。
