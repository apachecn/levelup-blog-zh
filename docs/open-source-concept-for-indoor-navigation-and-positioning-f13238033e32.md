# 室内导航和定位的开源概念

> 原文：<https://levelup.gitconnected.com/open-source-concept-for-indoor-navigation-and-positioning-f13238033e32>

这是 Navigine 团队，今天我们将向您介绍[室内导航和定位技术](https://navigine.com/)，以及针对特定领域的开源地理定位软件。

![](img/cb81da6a89cd1848d8c48ab534056ad7.png)

由[卡西亚·博雅诺斯卡](https://dribbble.com/kabojanowska)

# 室内导航定位系统是关于什么的？

我们都熟悉 GPS 系统，它可以根据卫星信号确定物体的位置。但是这项技术有一个明显的缺点——它不能在建筑物内部发挥作用。室内导航定位系统(IPS)是为解决封闭空间中的导航任务而设计的。第一个系统帮助创建到感兴趣的点的路线和建立方便的导航；第二个定义了物体在空间中的位置。

室内导航系统在以下方面得到了实际应用:

*   ***医疗保健*** —协助创建通往医疗机构办公室和房间的路线，跟踪资产和患者的移动。
*   ***行业*** —通过监控危险区域和跟踪公司的动产和不动产来提高运营安全性。
*   ***物流和仓库*** —使用室内定位算法，帮助员工建立通往必要货摊和集装箱的便捷路线，并在建筑中找到物品。
*   ***零售业务*** —提供向用户智能手机发送折扣和促销通知的可能性，方便在商店中导航。
*   ***交通***——确保机场和车站的客流量监控，让乘客在互动地图上找到所需物品。
*   ***博物馆和展览*** —借助便捷的展厅导航和交互式指南，改善参观者的用户体验。
*   ***智能办公室*** —允许为员工实时构建逐步导航，并通过远程气候控制管理确保舒适的工作环境。

# 它是如何工作的？

室内导航和定位系统需要两个组件才能有效运行:

*   **装备**。比如基于蓝牙、Wi-Fi、UWB 等的信标和网关。
*   **软件**。用于处理和可视化从设备获得的数据的程序。

为了确定建筑物内的物体位置，该技术利用了来自不同设备的传感器的各种数据，包括 BLE 信号、加速度计、陀螺仪磁力计等。接收到的原始数据使用我们将要谈到的特殊而复杂的算法进行处理。

# 室内导航的开源软件

在现代世界中，在高科技领域工作的大多数公司都支持开源倡议，即[开源软件](https://github.com/Navigine)供全面使用。这非常方便，因为开放代码允许任何用户应用它来开发新的寻路软件开源程序或修复其中的错误。

专门从事室内导航的公司也支持开放源代码倡议，并在其存储库或数据库中放置部分程序，这些程序可用作开发具有室内导航和跟踪功能的解决方案的基础。

# 计步器算法

计步器根据从安装在用户智能手机中的加速度传感器获得的数据来评估步数(时间点及其长度)。计步器算法分析输入加速度分量(ax，ay，az)和时间标记。

计算步数的示例:

# 互补滤波器

空间中的物体方向由安装在用户智能手机中的陀螺仪、加速度计和磁力计传感器来定义。

用于估计空间中物体方位的互补滤波器示例:

# 位置估计器

基于 RSSI(接收信号强度指示器)数据，位置估计器将当前位置定义为最近发射机的位置。

RSSI 算法室内定位代码计算物体位置的例子:

根据所选择的导航技术，算法可以确保 0.5 到 10 米的精度。