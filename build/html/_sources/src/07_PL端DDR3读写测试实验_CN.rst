PL端DDR3读写测试实验
========================================

**实验VIvado工程为“ddr3_pl_test”。**

硬件介绍
--------

开发板的PL端有2颗16bit
ddr3，这很大程度方便我们移植以前的FPGA工程到ZYNQ系统中，同时也提供了更大的带宽。

.. image:: images/07_media/image1.png
   :width: 6.00417in
   :height: 3.56213in

Vivado工程建立
--------------

创建一个PL端ddr3测试工程
~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: images/07_media/image2.png
   :width: 4.74703in
   :height: 4.00319in

.. image:: images/07_media/image3.png
   :width: 4.8175in
   :height: 4.06261in

.. image:: images/07_media/image4.png
   :width: 5.05661in
   :height: 4.26425in

配置ddr3 IP
~~~~~~~~~~~

1) 在“IP Catalog”的搜索框搜索“mig”，快速找到“Memory Interface
   Generator”，双击

.. image:: images/07_media/image5.png
   :width: 5.86231in
   :height: 3.83231in

2) 点击“Next”

.. image:: images/07_media/image6.png
   :width: 5.99583in
   :height: 4.41458in

3) “Component Name”修改为“ddr3”，以后我们例化ddr3就可以，点击“Next”

.. image:: images/07_media/image7.png
   :width: 5.99583in
   :height: 4.44931in

4) 点击“Next”

.. image:: images/07_media/image8.png
   :width: 6in
   :height: 4.44792in

5) 控制器类型选择“DDR3 SDRAM”，点击“Next”

.. image:: images/07_media/image9.png
   :width: 6.00208in
   :height: 4.42986in

6) “Memory Part”选择“MT41J256m16XX-125”,“Data Width”选择32

.. image:: images/07_media/image10.png
   :width: 6.00208in
   :height: 4.44722in

7) “Input Clock Period”选择5000ps（200MHz）

.. image:: images/07_media/image11.png
   :width: 5.99583in
   :height: 5.57431in

8) “System Clock”选择“No Buffer”,“Reference Clock”选择“Use System
   Clock”，“System Reset Polarity”选择“ACTIVE LOW”，点击“Next”

.. image:: images/07_media/image12.png
   :width: 5.99653in
   :height: 5.54167in

9) 使能DCI Cascade，点击“Next”

.. image:: images/07_media/image13.png
   :width: 6.00139in
   :height: 3.96458in

10) 选择“Fixed Pin Out：Pre-existing pin out is konwn and fixed”

.. image:: images/07_media/image14.png
   :width: 5.99653in
   :height: 3.95764in

11) 点击“Read XDC/UCF”

.. image:: images/07_media/image15.png
   :width: 5.99653in
   :height: 4.43542in

12) 选择ddr.ucf,这里可以选择工程里已经存在的XDC文件，只要包含ddr3的管脚分配信息就可以。

.. image:: images/07_media/image16.png
   :width: 6.00417in
   :height: 4.84306in

13) 点击“Validate”

.. image:: images/07_media/image17.png
   :width: 5.99583in
   :height: 3.98194in

14) 选择测试输出的管脚，这里保持默认，不配置

.. image:: images/07_media/image18.png
   :width: 6.00208in
   :height: 3.99167in

15) 点击“Next”

.. image:: images/07_media/image19.png
   :width: 6.00069in
   :height: 3.98889in

16) 点击“Access”接受条款

.. image:: images/07_media/image20.png
   :width: 5.99792in
   :height: 3.96597in

17) 点击“Next”

.. image:: images/07_media/image21.png
   :width: 6.00139in
   :height: 3.98194in

18) 点击“Generate”

.. image:: images/07_media/image22.png
   :width: 5.99583in
   :height: 3.99375in

19) 在弹出的“Generate Output Products”中选择“Generate”

.. image:: images/07_media/image23.png
   :width: 2.95903in
   :height: 4.06667in

添加其他测试代码
~~~~~~~~~~~~~~~~

其他代码主要功能是配置si5338，读写ddr3并比较数据是否一致，这里不做详细介绍，可参考工程代码。

.. image:: images/07_media/image24.png
   :width: 5.39583in
   :height: 3.5in

下载调试
--------

生成bit文件以后，使用JTAG下载到开发板，我们可以通过LED来观察ddr3测试情况，LED1亮表示si5338配置完成，LED2亮表示ddr3
读写有错误，LED3亮表示ddr3控制器初始化完成，LED4闪烁表示ddr3测试程序在运行。

实验总结
--------

本实验通过PL端Verilog代码直接读写ddr3，通过LED来显示测试结果，我们也可以把ddr3配置成AXI接口，这样方便和ARM系统完成数据交互。


*ZYNQ-7000开发平台 FPGA教程*    - `Alinx官方网站 <http://www.alinx.com>`_