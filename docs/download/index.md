# 资源下载

## 说明

NextPilot导航飞控项目目前只支持NP-H05系列飞控，该飞控采用两块一模一样的主控芯片，分别运行飞行控制程序和惯性导航程序，故我们提供了两个固件（飞控固件、导航固件），需要分别通过FCS-USB下载飞控固件、通过INS-USB下载导航固件。

> 注意：
>
> 由于两个主控芯片相同，很容易搞混，下载前一定要注意，根据固件类型选择对应的USB烧写！！！两个USB连接方式请参考产品说明。

## 飞控固件

### v1.0-beta

- 默认固件：[fcs_v4_default.bin](./1-飞控固件/v1.0-beta/fcs_v4_default.bin)

- SITL：[sitl-qemu.bin](./1-飞控固件/v1.0-beta/sitl-qemu.bin)

- HITL：[fcs_v4_default-HITL.bin](./1-飞控固件/v1.0-beta/fcs_v4_default-HITL.bin)

## SITL相关脚本

软件在环仿真相关脚本的使用请参考[软件在环仿真](../manual/03-飞行仿真/01-软件在环仿真.md)。

- 软件在环仿真启动脚本（必须）：[qemu.bat](./4-仿真脚本/sitl-qemu/qemu.bat)；
- 日志提取脚本（非必须）：[extract_sd.bat](./4-仿真脚本/sitl-qemu/extract_sd.bat)；

## 导航固件

### v1.0-beta

[ins_v1.0.bin](./2-导航固件/v1.0/ins_hal_V4_20251120.bin)



## 地面站软件

### 百度网盘

通过网盘分享的文件：nextpilot-user-assets
链接: https://pan.baidu.com/s/1-OiGOEX7B2mDmwkJNmagVg 提取码: next



### gitee仓库

点击链接[代码 - nextpilot-user-assets - NextPilot](https://e.gitee.com/nextpilot/repos/nextpilot/nextpilot-user-assets/sources)进入NextPilot资源仓库，然后可以点击右侧`克隆/下载`按钮，选择直接下载ZIP压缩包即可。如果只希望下载某个特定文件，可以找到后，鼠标右键点击选择`下载`。

