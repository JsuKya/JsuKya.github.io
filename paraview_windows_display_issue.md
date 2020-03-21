### Paraview在Windows平台下显示问题

平台：Windows 10 LSTC 64位

软件：ParaView-5.8.0-Windows-Python3.7-msvc2015-64bit版本

问题描述：打开paraview后选择任意物理量显示云图时，就会出现显示问题，具体可见下图。
![](/images/paraview_windows_display_issue/display_issue.png)
经过Google，得知是Intel显卡导致的问题，具体可见[issue 1936](https://gitlab.kitware.com/paraview/paraview/issues/19364)。

解决办法有两个：
* 使用最新版（nightly）的Paraview.
* 使用Nvidia显卡打开Paraview.
  
我选择了第二种:laughing:，打开Nvidia的控制面板（Win控制面板-查看方式改为大图标-Nvidia控制面板），然后进入管理3D设置将Paraview设置使用N卡打开，具体可见下图。
![](/images/paraview_windows_display_issue/nvidia_setting.png)
![](/images/paraview_windows_display_issue/ok.png)
问题顺利解决，Happy paraview!