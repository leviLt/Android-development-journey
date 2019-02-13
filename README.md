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
> 下面我就列举一些我们最常用的,ADB调试有很多强大的功能,如果想要好好的研究,我贴下链接[ADB](https://developer.android.com/studio/command-line/adb?hl=zh-cn)
- 1.基本指令集
   ```
   进入指定设备    adb -s serialNumber shell

   查看版本       adb version

   查看日志       adb logcat

   查看设备       adb devices

   连接状态       adb get-state

   启动ADB服务    adb start-server

   停止ADB服务    adb kill-server

   电脑推送到手机  adb push local remote

   手机拉取到电脑  adb pull remote local
   
   安装           adb install -r xxx.apk
   
   卸载           adb uninstall <packages>
   
   查看进程        adb shell ps

   ```
- 2.ADB 下的AM和PM

   AM :ActivityManager 看意思就是和Activity相关的指令

   ```
   启动Activity        adb shell am start -n com.example.lt/.MainActivity (加入参数在后面添加:-e key value)
      
   杀app的进程          adb shell am force-stop com.example.lt
   
   打开网页             adb shell am start -a anroid.intent.action.VIEW -d "https://www.google.com"
   
   发送广播             adb shell am broadcast -a "xxx.action"
   
   
   
   ```
   PM :PackageManager  和包相关(install/uninstall...)
   ```
   清空缓存数据      adb shell pm clear com.example.lt
   
   查看所有的包名     adb shell pm list packages
   ```
 - 3.输入事件
   
   适配TV的经常要输入一些文字、字符串等等,在遥控器上是很不方便的,这个时候就需要到了:
   ```
   输入框输入字符     adb shell input text "dasdsdasdasd"
   
   ```
 - 4.dumpsys 
 
   dumpsys 是一个非常强大的命令，它可以提供非常多的系统信息
   ```
   查看电池信息                   adb shell dumpsys battery
   
   查看Activity信息              adb shell dumpsys activity
   
   查看正在运行的activity         adb shell dumpsys activity | grep -i "run" (忽略大小写,带有run)
   
   查看APP有哪些进程              adb shell dumpsys activity p <包名>
   
   查看APP有哪些进程过滤掉         adb shell dumpsys activity p <包名> | grep -i "PID" | grep -i "proccess"
   
   note : adb shell dumpsys activity 后面添加 a、p、s  分别对应:activty、proccess、service
   
   ```
 - 5.录屏、截屏
 
   ```
   截屏               adb shell screencap <路径/sdcard/xxx.png>
   
   录屏               adb shell screenrecord <路径/sdcard/xxx.mp4>
   ```    
- 三、数据结构(即使是做Android 你也应该知道些数据结构相关的知识)

  1.什么是数据结构?
    计算机存储、组织
      
