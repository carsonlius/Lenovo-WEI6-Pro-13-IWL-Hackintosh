# Lenovo-WEI6-Pro-13-IWL-Hackintosh
>[**中文说明**](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/blob/master/README_CN.MD) | **[English](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/blob/master/README.MD)**
>
> **威 6 Pro/Thinkbook 13s/扬天 S540 交流群**：[681175557](https://jq.qq.com/?_wv=1027&k=54ugIhI)

**此笔记本的其它名字（外观、配置基本一致）：**

> - **Lenovo 扬天 WEI 6 PRO**
> - **Lenovo Thinkbook 13S**
> - **Lenovo 扬天 S540**



### **注意：仅适配`10.14.6`！`10.15`未适配！如有需求请自行测试！**

## 配置信息

| 硬件     |                                                              |
| -------- | ------------------------------------------------------------ |
| 主板     | 联想 LNVNB161216                                             |
| 处理器   | Intel(R) Core(TM) i7-8565U（UHD Graphics 620）               |
| 内存     | 8GB 2400MHz Micron（必须注入内存信息）                       |
| 硬盘     | HFM512GDHTNG-831（反馈S540系列有镁光硬盘，无法安装）         |
| 独立显卡 | AMD 540X Series（已屏蔽 ）                                   |
| 显示器   | FHD 1920x1080                                                |
| 声卡     | ACL 257                                                      |
| 网卡     | Intel AC9560（使用USB网卡{我是USB网卡：`CF-WU810N`}或更换网卡） |
| 触摸板   | Intel I2C HID INT34BB                                        |

## 各项功能情况

#### 存在问题：

**1.有几率出现**（问题尚未定位，Windows切换到macOS最容易出现）
- 卡进度条重启

- 启动后登陆界面黑屏（外接HDMI可显示）

***临时解决方法***：1.长按电源键重启（使用-v等） 2.Windows系统和macOS系统来回切换 3.使用`configold.plist`配置启动。

**2.睡眠可以真正睡眠（电源键灯会呼吸闪亮）！但**

- 有几率唤醒不了，黑屏或直接重启！
- 唤醒成功！卡成PPT！

| 情况 | 名称          | 说明                                                         |
| :--: | ------------- | ------------------------------------------------------------ |
|  ✔   | 电池          | 正常，[可设定电池养护模式](#可能你需要开启这些功能)          |
|  ✔   | 摄像头        | USB定制：`HS07`                                              |
|  ✔   | 蓝牙          | 要么无法关闭，要么无法打开，我选择了打开（测试发现，能向手机发送文件，手机发送不了文件到电脑）隔空投送无法使用！ |
|  ✔   | 扬声器/麦克风 | `ALC257`，注入ID `11` ，各项功能正常，耳机孔自动切换。（[有快捷键](#快捷键)） |
|  ✔   | 触摸板        | 能力有限，只做到了**轮询模式**（[VoodooI2C、HID](https://github.com/alexandred/VoodooI2C/releases)），支持手势，支持关闭（[快捷键](#快捷键)），[需要单独设置，设置教程请点击我！](#触摸板设置教程) |
|  ✔   | HDMI          | 外接显示正常（测试中插拔多次）                               |
|  ✔   | Type-C        | USB定制：`HS03`                                              |
|  ✔   | 3.5mm耳机接口 | 支持耳机插拔自动切换                                         |
|  ✔   | USB接口       | USB定制：`HS01`、`HS02`                                      |
|  ✔   | CPU睿频       | 通过CPU-S查询                                                |
|  ✔   | 亮度调节      | 快捷键`F11`和`F12`EC码是`Q82`，`Q83` ，我设置了无效，但有一个[快捷键](#快捷键) |
|  ❓❌  | 睡眠          | 抽风！秒睡，电源键闪白光表示已经完全睡着，会有醒不过来几率或醒来卡成PPT |
|  ❌   | 指纹模块      | 无解，USB定制已屏蔽                                          |
|  ❌   | 独显          | 暂时无解，AMD可能有机会                                      |
|  ❌   | WIFI          | 暂时无解，最近有大神在研究驱动，如需联网请使用USB网卡或更换网卡 |

## 快捷键

注：在 macOS 中F1-F12和win一样，都要按Fn+按键，但不按Fn就有音量功能键和关闭触摸板键，检测键盘中按下F9和F10有反馈，但没定义操作。

| 按键 | 功能                                    |
| ---- | --------------------------------------- |
| FN+P | 调节亮度-增加亮度（是的就一个增加亮度） |
| F1   | 调节声音-静音（对上键盘符号）           |
| F2   | 调节声音-减少音量（对上键盘符号）       |
| F3   | 调节声音-增加音量（对上键盘符号）       |
| F6   | 关闭触摸板（对上键盘符号，这个功能赞👍） |

### 可能你需要开启这些功能

**1.设置电池、电源模式**

进入Windows系统打开`_Drive and Tools`，运行`BatterySetting_联想管家电池管理.exe`设置。

> 程序来自我几个月前我自己提取的。

充电模式说明：

- 常规：正常充电

- 养护：保持电量在55-60%，延长电池使用寿命

- 快充：可快速充电，但影响电池使用寿命，不建议经常使用

电源模式说明：

- 平衡：自动调节计算机性能与耗电量

- 高性能：有利于提高性能，但耗电量较大

- 超省电：尽可能降低性能以延长电池使用时间

**2.开启 macOS HiDPI**

[开启方法点我传送](https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md)

如果命令执行不了（报错），`_Drive and Tools`有个`hidpi_bak_191119.sh`备份，拖到终端执行即可！



## 触摸板设置教程（屏蔽苹果原装I2C驱动）

1.前往驱动文件夹`\System\Library\Extensions\`中文版可能显示为`\系统\库\Extensions`

2.删除捣乱的两个文件（我config做了屏蔽无效）：

- **`AppleIntellpssI2C.kext`**
- **`AppleIntellpssI2CController.kext`**

3.使用`Hackintool`-`工具（右下角右边盒子图标）`-`重建缓存并修复权限`即可

或者 终端执行 `sudo kextcache -i/` 重建缓存

4.**把`_Drive and Tools`文件夹的`VoodooI2C_9ed8_9ed9.kext`放入`CLOVER\kexts`即可**

| 建议右键新窗口打开图片                                       |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![Trackpad1](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/Trackpad%20(1).png)](https://tva2.sinaimg.cn/large/006bfoyggy1gc1wl59dh0j31hc0u0qv6.jpg) | [![Trackpad2](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/Trackpad%20(2).png)](https://tva4.sinaimg.cn/large/006bfoyggy1gc1wl6ey6ej31hc0u07wh.jpg) | [![Trackpad3](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/Trackpad%20(3).png)](https://tva3.sinaimg.cn/large/006bfoyggy1gc1wl6uaivj31hc0u0e82.jpg) |
| [![Trackpad4](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/Trackpad%20(4).png)](https://tva4.sinaimg.cn/large/006bfoyggy1gc1wl7bug0j31hc0u0hdu.jpg) | [![Trackpad5](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/Trackpad%20(5).png)](https://tvax1.sinaimg.cn/large/006bfoyggy1gc1wl7tim7j31hc0u0hdu.jpg) |                                                              |




## 测试截图

[![0](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/screenshot.png)](https://tvax1.sinaimg.cn/large/006bfoyggy1gc1wl4t65aj31hc0u0qv5.jpg)

[![1](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/pic1.png)](https://tvax3.sinaimg.cn/large/006bfoyggy1gc1wl3rccrj31hc0u0kjl.jpg)

[![2](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/pic2.png)](https://tvax4.sinaimg.cn/large/006bfoyggy1gc1wl4drwqj31hc0u0b2a.jpg)



| 建议右键新窗口打开图片                                       |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![1](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/bluetooth%20(1).png)](https://tvax1.sinaimg.cn/large/006bfoyggy1gc1wl8f27gj3280190u0z.jpg) | [![2](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/bluetooth%20(2).png)](https://tva4.sinaimg.cn/large/006bfoyggy1gc1wl1z59hj32801904qs.jpg) | [![3](https://github.com/Tamshen/Lenovo-WEI6-Pro-13-IWL-Hackintosh/raw/master/_images/bluetooth%20(1).png)](https://tva3.sinaimg.cn/large/006bfoyggy1gc1wl30o3qj3280190e84.jpg) |



## 系统镜像下载

[黑果小兵的博客 macOS Mojave 10.14.6 镜像下载](https://blog.daliansky.net/macOS-Mojave-10.14.6-18G87-Release-version-with-Clover-5033-original-image.html#10146-18g87-下载链接)
