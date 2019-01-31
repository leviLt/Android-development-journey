# 关于这个项目
> 创建这个项目的原因是自己菜,经常记不住很多不常有的API,以及不常使用的方法,但是有时确非常的有用  
> 因此欢迎大家也在里面添加内容,一个人的力量是有限的,但是众人的力量确实不可估量的
# 开始进入正题
## 一、TV适配 
### 1、判断是否是TV
- 1.通过UIModeManager
```
UIModeManager.getCurrentModeType() == Configuration.UI_MODE_TYPE_TELEVISION
```
- 2.通过PackageManager的SystemFeature判断
```
getPackageManager().hasSystemFeature(PackageManager.FEATURE_TELEVISION)
//如果大于5.0 
getPackageManager().hasSystemFeature(PackageManager.FEATURE_LEANBACK)
```
- 3.创建values-television,创建bool值判断
```
//values-television 文件夹下的xml文件
<bool name="isTelevision">true</bool>
//values 文件夹下的xml文件
<bool name="isTelevision">false</bool>
//判断
getResources().getBoolean(R.bool.isTelevision)
```
- 4.原本以为这样就可以了,事实上还差的远,标准的TV,上面的几种方式就可以了,但是还有我们出乎意料的模改的TV(乐视TV、小米盒子就判断不出来)
```
//1.通过产品/硬件制造商判断是否包含TV的字段
Build.MANUFACTURER.toLowerCase().equals("tv")
//2.硬件最终的名称是否包含tv
Build.MODEL.toLowerCase().contains("tv")
```
目前通过上诉的方式基本上都可以判断是否是TV,包含亚马逊的Fire TV、以及国产的TV、盒子等等
### 二、Android 开发如果都不知道点常用的ADB调试,一看就不专业
> 下面我就列举一些我们最常用的,ADB调试有很多强大的功能,如果想要好好的研究,我贴下链接!(ADB)[https://developer.android.com/studio/command-line/adb?hl=zh-cn]
- 1.查看当前连接设备
```
adb devices
```
