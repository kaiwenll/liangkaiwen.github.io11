amlogic 常用命令：

======================================
插播一条vim命令             :TlistToggle 显示函数列表

======================================
网络 

busybox ifconfig eth0 up
=======================================
按键
dmesg :    获取内核报告的信息
dmesg -c  清理内核中的信息
2、按顺序按遍遥控器的每个按钮（如果你觉得没按到，你可以多按几次，但一定要按顺序）
3、运行 dmesg | grep "code is 0x" | rev |cut -c 5-6,9-10| rev |uniq >> /sdcard/IRdump.log
然后会在/sdcard/下创建包含scancodes的IRdump.log文件，这些会被用在remote.conf文件中，所以请务必按顺序按下，否则之后你会搞乱。
下一步就是remote.conf文件了，默认路径是/system/etc/remote.conf


======================================
package:/system/app/SWSettings_tv.apk=net.sunniwell.app.swsettings
net.sunniwell.app.swsettings/.SWSettingsActivity

am start net.sunniwell.app.swsettings/.SWSettingsActivity

package:/system/priv-app/Settings.apk=com.android.settings
package:/system/app/SWSettings_base_KitKat.apk=net.sunniwell.settings
package:/system/priv-app/SettingsProvider.apk=com.android.providers.settings

======================================
54:C5:7A:A9:8A:D1

    echo 1 > /sys/class/remount/need_remount;mount -o rw,remount /system

    //查看本地包名

    pm list packages -f | grep -i local

    package:/system/app/SWLocalPlayer_tv.apk=net.sunniwell.app.localplayer
    dumpsys package net.sunniwell.app.localplayer

    net.sunniwell.app.localplayer/.SWLocalPlayerAllActivity
    am broadcast -a net.sunniwell.action.LOCALPLAY_ABLUM 显示一个页面

    net.sunniwell.app.localplayer/.SWLocalPlayerActivity

    原生设置包名
    com.android.settings/.Settings$UserSettingsActivity 

    4.1  logo编译
        制作bmp格式的开机logo图片，分辨率建议为1080p,重命名为bootup,覆盖到device/amlogic/p201_iptv/res_pack$
        如果是单独调试，可以按如下步骤，单独制作：
        ./out/host/linux-x86/bin/imgpack
        -r  device/amlogic/p201_iptv/res_pack/ 
        out/target/product/p201_iptv/res-package.img
            参数说明：
               res_pack是源图片路径，
               res-package.img是生成文件，即logo.img 
            4.2  logo升级
            Amlogic除特殊分区外都可以采用cat命令的形式替换分区文件，例如recovery、log等分区。
            Logo的升级操作：cat /storage/external_storage/sda1/res-package.img  > /dev/block/logo
            另外，amlogic支持动态更新开机logo，系统提供API，更新开机logo图片，支持jpg, png, bmp等常见格式，重启生效。 

            小系统logo.img 目录 platform/on-project/pub/images
            ~/project/s905l2/platform/release/images/logo.img 不对的，一般不修改release目录下的内容

            开机动画
            ./platform/release/system/media
