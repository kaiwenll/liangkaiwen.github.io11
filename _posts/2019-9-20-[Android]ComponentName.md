## **壁纸不显示问题总结**

 + 通过日志分析 ``` W/WallpaperManager(pid):WallpaperService not running```初步定位是服务没有开启的原因

 + 在 ***/system/build.prop*** 中增加 ***sys.wallpaper.enable=true*** 之后继续追查 log 

    + 首先开机之后查看服务状态是正确的
     
      ```
      root@p201_iptv:/ # getprop | grep wallpaper
      [sys.wallpaper.enable]: [true]
      ```
     
    + 发现log中还是会打印``` W/WallpaperManager(pid):WallpaperService not running```

   ***

 + 然后代码追定位到 ***frameworks/base/services/java/com/android/server/SystemServer.java***

   *honestly speaking , I don't know why direct here , but chaoyang bro let me do that.*

   + ### 搜索 Wallpaper 找到系统服务添加wallpaper的代码

     ```
     if (!disableNonCoreServices && context.getResources().getBoolean(
                             R.bool.config_enableWallpaperService) &&
                             SystemProperties.getBoolean("sys.wallpaper.enable", false)) {
                     try {
                         Slog.i(TAG, "Wallpaper Service");
                         if (!headless) {               
                             wallpaper = new WallpaperManagerService(context);
                             ServiceManager.addService(Context.WALLPAPER_SERVICE, wallpaper);
                         }         
                     } catch (Throwable e) {        
                         reportWtf("starting Wallpaper Service", e);
                     }
                 }
     
     ```

     ### 继续查找，***initAndLoop()*** 方法里，创建了一个对象 *wallpaperF*

     ```
     final WallpaperManagerService wallpaperF = wallpaper;
     ```

     ### 这里会检测这个标志位，如果不为1，就创建一个 systemUi 线程

     ```
                     Thread th = new Thread("test") {
                         public void run() {
                             try {
                                 Thread.sleep(3000);
                             } catch (Exception e) {}
                             if (!headless) {
                                 startSystemUi(contextF);
                             }
                         }
                     };
                     if (SystemProperties.getBoolean("sys.wallpaper.enable", false))
                         th.start();
     
     ```

     

     ###  ***wallpaperF.systemRunning（）*** 

     ```
     
                     try {
                         if (wallpaperF != null) wallpaperF.systemRunning();
                     } catch (Throwable e) {        
                         reportWtf("Notifying WallpaperService running", e);
                     }
                     Slog.i(TAG, "BootStage Notifying WallpaperService running");
     
     ```

     

     ### 继续追到 ***WallpaperManagerService.java*** 

      可以看到 ***ComponentName***  这里 调用了包名 ***com.android.systemui*** ，百度一下这个包名对应的 apk 是 ***SystemUI.apk*** ，使用 ***pm install*** 安装这个apk , 背景图片显示正常

     ```
         /**  
          * Name of the component used to display bitmap wallpapers from either the gallery or
          * built-in wallpapers.
          */
         static final ComponentName IMAGE_WALLPAPER = new ComponentName("com.android.systemui",
                 "com.android.systemui.ImageWallpaper");
     ```

     

     ### 这里简单介绍一下 ***ComponentName*** 的使用

     ComponentName：可以启动其他应用的Activity、Service.

     ```
     ComponentName    chatActivity =new ComponentName(param1,param2);
     
     param1:Activity、Service所在应用的包名
     
     param2:Activity、Service的包名+类名
     ```

     Activity:

     ```
      ComponentName chatActivity =new ComponentName("com.npf.chat", "com.npf.chat.ui.ChatActivity");
     
         Intent intent =new Intent();
     
         intent.setComponent(chatActivity);
     
         startActivity(intent);
     ```

     Service:

     ```
       ComponentName chatService =new ComponentName("com.npf.chat", "com.npf.chat.ui.ChatService");
     
         Intent intent =new Intent();
     
         intent.setComponent(chatService );
     
         startService(intent);
     ```

     注:

     ```
     如果该Activity非应用入口(入口Activity默认android:exported="true")，则需要再清单文件中添加   android:exported="true"。Service也需要添加android:exported="true"。允许外部应用调用。
     
        <activity android:name="com.npf.chat.ui.ChatActivity"
     
         android:exported="true"/>
     
        <service android:name="com.npf.chat.ui.ChatService"
     
         android:exported="true"/>
     ```

     
