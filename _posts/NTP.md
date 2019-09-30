### ntp server

+ 不能同步NTP服务器

```
01-01 08:00:30.340 E/SntpClient( 5209): request time failed: java.net.SocketTimeoutException
01-01 08:00:30.340 D/NtpTrustedTime( 5209): forceRefresh() from cache miss
01-01 08:00:30.340 W/NtpTrustedTime( 5209): update ntp fail change ntp server to 120.210.203.62
01-01 08:00:30.340 W/NtpTrustedTime( 5209): update ntp fail change ntp server to 120.210.203.62
01-01 08:00:30.340 W/NtpTrustedTime( 5209): update ntp fail change ntp server to 120.210.203.62
01-01 08:00:30.340 D/NtpTrustedTime( 5209): ntp time server is 120.210.203.62
01-01 08:00:30.340 D/NtpTrustedTime( 5209): ntp time server is 120.210.203.62
01-01 08:00:30.480 E/SntpClient( 5209): request time failed: java.net.SocketTimeoutException
01-01 08:00:32.080 D/DevInfoService( 5209): get addrss... name=AccountPassword
```

+ 同步现网使用的NTP地址  ```setting put global ntp_server 183.224.42.4```
+ 183.207.253.53 js100

系统调用 ***NtpTrustedTime.java*** 

***SystemService.java***



### Android中通过NTP服务器获取时间功能源码分析

1 相关文件：

```java
frameworks\base\services\java\com\android\server\ SystemServer.java
frameworks\base\services\java\com\android\server\ NetworkTimeUpdateService.java
frameworks\base\core\java\android\util\NtpTrustedTime.java
frameworks\base\core\java\android\net\SntpClient.java
frameworks\base\core\res\res\values\config.xml
```

2 实现原理：
2.1 ***SystemServer*** 的 ***run*** 中：

```Java
ActivityManagerService.self().systemReady(new Runnable() {
            public void run() {
                try {
                    	if (networkTimeUpdaterF != null) 
                    		networkTimeUpdaterF.systemReady();    
                } catch (Throwable e) { } catch (Throwable e) {
  					reportWtf("making Network Time Service ready", e);
            }
...
}
```

2.2 再来看看***NetworkTimeUpdateService***中的相关代码：
`systemReady`

***`MyHandler`***

重点来看看 ***onPollNetworkTime*** 这个函数：

在看这个函数之前先来理解几个相关变量，理解了这几个变量之后，该函数就比较好理解了。
在 ***NetworkTimeUpdateService*** 的构造函数中：

几个关键的变量：

> 当NTP时间获取成功后，再次请求NTP时间的间隔
> ***`mPollingIntervalShorterMs`***
> 当NTP时间获取失败后，再次请求NTP时间的间隔
> ***`mTimeErrorThresholdMs`***
> 当NTP时间和系统时间不相同时，要更新系统时间的阀值
> 这几个变量的值是通过资源文件里读取的，配置的地址为 ***config.xml*** ,来看看相关的内容：

现场日志

![1569249615424](C:\Users\liangkaiwen\AppData\Roaming\Typora\typora-user-images\1569249615424.png)

明天让测试抓个修改过IP的日志 报文