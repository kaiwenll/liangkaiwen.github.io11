# 常用命令

### vim命令

```
TlistToggle //显示函数列表
/ \c //查找不区分大小写
跳转到上/下一个修改的位置 
当你编辑一个很大的文件时，经常要做的事是在某处进行修改，然后跳到另外一处。如果你想跳回之前修改的地方，使用命令：
Ctrl+o
来回到之前修改的地方
类似的：
Ctrl+i
会回退上面的跳动。
[{
]}
```
### 网络 

```
busybox ifconfig eth0 up
```
### amloggic获取遥控器按键信息

首先清理内核中的信息

```
dmesg //获取内核报告的信息
dmesg -c  //清理内核中的信息
```
按顺序按遍遥控器的每个按钮（如果你觉得没按到，你可以多按几次，但一定要按顺序） 

```
dmesg | grep "code is 0x" | rev |cut -c 5-6,9-10| rev |uniq >> /sdcard/IRdump.log
```
然后会在/sdcard/下创建包含scancodes的IRdump.log文件，这些会被用在remote.conf文件中，所以请务必按顺序按下，否则之后你会搞乱。

下一步就是remote.conf文件了，默认路径是

```
/system/etc/remote.conf
```

这里演示通过apk名字查找包名，并最终用am命令启动Activity

```
package:/system/app/SWSettings_tv.apk=net.sunniwell.app.swsettings
net.sunniwell.app.swsettings/.SWSettingsActivity

am start net.sunniwell.app.swsettings/.SWSettingsActivity

package:/system/priv-app/Settings.apk=com.android.settings
package:/system/app/SWSettings_base_KitKat.apk=net.sunniwell.settings
package:/system/priv-app/SettingsProvider.apk=com.android.providers.settings
```
```
//查看本地包名

pm list packages -f | grep -i local

package:/system/app/SWLocalPlayer_tv.apk=net.sunniwell.app.localplayer
dumpsys package net.sunniwell.app.localplayer

net.sunniwell.app.localplayer/.SWLocalPlayerAllActivity
am broadcast -a net.sunniwell.action.LOCALPLAY_ABLUM 显示一个页面

net.sunniwell.app.localplayer/.SWLocalPlayerActivity

//原生设置包名
com.android.settings/.Settings$UserSettingsActivity 
```
amlogic system 分区设置为WR

```
echo 1 > /sys/class/remount/need_remount;mount -o rw,remount /system
```

### logo制作

​    制作bmp格式的开机logo图片，分辨率建议为1080p,重命名为bootup,覆盖到device/amlogic/p201_iptv/res_pack$
如果是单独调试，可以按如下步骤，单独制作：

```
./out/host/linux-x86/bin/imgpack
-r  device/amlogic/p201_iptv/res_pack/ 
out/target/product/p201_iptv/res-package.img
```
__参数说明__

res_pack是源图片路径，
res-package.img是生成文件，即logo.img 

#### logo升级
Amlogic除特殊分区外都可以采用cat命令的形式替换分区文件，例如recovery、log等分区。
Logo的升级操作

```
cat /storage/external_storage/sda1/res-package.img  > /dev/block/logo
```


另外，amlogic支持动态更新开机logo，系统提供API，更新开机logo图片，支持jpg, png, bmp等常见格式，重启生效。 

小系统logo.img 目录 platform/on-project/pub/images
~/project/s905l2/platform/release/images/logo.img 不对的，一般不修改release目录下的内容

#### 开机动画
./platform/release/system/media

### android平台的三个编译命令----make,mm,mmm
在android源码根目录下，执行以下三步即可编译android:
1. build/envsetup.sh #这个脚本用来设置android的编译环境;
2. lunch #选择编译目标
3. make #编译android整个系统

### android平台提供了三个命令用于编译，这3个命令分别为：
```
1. make: 不带任何参数则是编译整个系统；
make MediaProvider： 单个模块编译，会把该模块及其依赖的其他模块一起编译(会搜索整个源代码来定位MediaProvider模块所使用的Android.mk文件，还要判断该模块依赖的其他模块是否有修改)；
2. mmm packages/providers/MediaProvider: 编译指定目录下的模块，但不编译它所依赖的其它模块；
3. mm: 编译当前目录下的模块，它和mmm一样，不编译依赖模块;
4. mma: 编译当前目录下的模块及其依赖项
以上三个命令都可以用-B选项来重新编译所有目标文件。
```

