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
  替换所有行的内容：      :%s/from/to/g
        :%s/from/to/g   ：  对所有行的内容进行替换。
  在VIM中进行文本替换：
```
### vim替换文本：
>    1.  替换当前行中的内容：    :s/from/to/    （s即substitude）
        :s/from/to/     ：  将当前行中的第一个from，替换成to。如果当前行含有多个
                            from，则只会替换其中的第一个。
        :s/from/to/g    ：  将当前行中的所有from都替换成to。
        :s/from/to/gc   ：  将当前行中的所有from都替换成to，但是每一次替换之前都
                            会询问请求用户确认此操作。
        注意：这里的from和to都可以是任何字符串，其中from还可以是正则表达式。
>
    2.  替换某一行的内容：      :33s/from/to/g
        :.s/from/to/g   ：  在当前行进行替换操作。
        :33s/from/to/g  ：  在第33行进行替换操作。
        :$s/from/to/g   ：  在最后一行进行替换操作。

> 
    3.  替换某些行的内容：      :10,20s/from/to/g
        :10,20s/from/to/g   ：  对第10行到第20行的内容进行替换。
        :1,$s/from/to/g     ：  对第一行到最后一行的内容进行替换（即全部文本）。
        :1,.s/from/to/g     ：  对第一行到当前行的内容进行替换。
        :.,$s/from/to/g     ：  对当前行到最后一行的内容进行替换。
        :'a,'bs/from/to/g   ：  对标记a和b之间的行（含a和b所在的行）进行替换。
                                其中a和b是之前用m命令所做的标记。
>    
    4.  替换所有行的内容：      :%s/from/to/g
        :%s/from/to/g   ：  对所有行的内容进行替换。
>    
    5.  替换命令的完整形式：    :[range]s/from/to/[flags]
        5.1 s/from/to/
            把from指定的字符串替换成to指定的字符串，from可以是正则表达式。
        5.2 [range]
            有以下一些表示方法：
            不写range   ：  默认为光标所在的行。
            .           ：  光标所在的行。
            1           ：  第一行。
            $           ：  最后一行。
            33          ：  第33行。
            'a          ：  标记a所在的行（之前要使用ma做过标记）。
            .+1         ：  当前光标所在行的下面一行。
            $-1         ：  倒数第二行。（这里说明我们可以对某一行加减某个数值来
                            取得相对的行）。
            22,33       ：  第22～33行。
            1,$         ：  第1行 到 最后一行。
            1,.         ：  第1行 到 当前行。
            .,$         ：  当前行 到 最后一行。
            'a,'b       ：  标记a所在的行 到标记b所在的行。
            %           ：  所有行（与 1,$ 等价）。
            ?chapter?   ：  从当前位置向上搜索，找到的第一个chapter所在的行。（
                            其中chapter可以是任何字符串或者正则表达式。
            /chapter/   ：  从当前位置向下搜索，找到的第一个chapter所在的行。（
                            其中chapter可以是任何字符串或者正则表达式。
            注意，上面的所有用于range的表示方法都可以通过 +、- 操作来设置相对偏
            移量。
        5.3 [flags]
            这里可用的flags有：
            无      ：  只对指定范围内的第一个匹配项进行替换。
            g       ：  对指定范围内的所有匹配项进行替换。
            c       ：  在替换前请求用户确认。
            e       ：  忽略执行过程中的错误。
            注意：上面的所有flags都可以组合起来使用，比如 gc 表示对指定范围内的
            所有匹配项进行替换，并且在每一次替换之前都会请用户确认。
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

