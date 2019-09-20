# 日志分析案例

### 设置点击关于进程挂掉

```java
root@p201_iptv:/ # logcat -c ; logcat | grep 6940
D/SWSystemService( 6940): [20190918223328776][net.sunniwell.setting.jx.service.SWSystemService][handleScreenSave][204]:-----screen save time-----1 
D/ContextImpl( 6940): cls name is:net.sunniwell.setting.jx.ui.AboutActivity
W/ContextImpl( 6940): Calling a method in the system process without a qualified user: android.app.ContextImpl.startActivity:1129 android.content.ContextWrapper.startActivity:311 net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity:76 net.sunniwell.setting.jx.MainActivity.onClick:71 android.view.View.performClick:4438 
W/ContextImpl( 6940): Calling a method in the system process without a qualified user: android.app.ContextImpl.startActivity:1141 android.app.ContextImpl.startActivity:1130 android.content.ContextWrapper.startActivity:311 net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity:76 net.sunniwell.setting.jx.MainActivity.onClick:71 
I/ActivityManager( 5131): START u0 {flg=0x10000000 cmp=net.sunniwell.setting.jx/.ui.AboutActivity} from pid 6940
I/dalvikvm( 6940): Could not find method android.net.pppoe.PppoeManager.getPppoeType, referenced from method net.sunniwell.setting.jx.ui.AboutActivity.getEthernetInfo
W/dalvikvm( 6940): VFY: unable to resolve virtual method 975: Landroid/net/pppoe/PppoeManager;.getPppoeType ()I
D/dalvikvm( 6940): VFY: replacing opcode 0x6e at 0x00ce
I/dalvikvm( 6940): Could not find method android.net.pppoe.PppoeManager.getPppoeType, referenced from method net.sunniwell.setting.jx.ui.AboutActivity.getIpAddr
W/dalvikvm( 6940): VFY: unable to resolve virtual method 975: Landroid/net/pppoe/PppoeManager;.getPppoeType ()I
D/dalvikvm( 6940): VFY: replacing opcode 0x6e at 0x0038
I/dalvikvm( 6940): Could not find method android.net.DhcpInfoInternal.setDhcpInfo, referenced from method net.sunniwell.setting.jx.ui.AboutActivity.getNetworkInfo
W/dalvikvm( 6940): VFY: unable to resolve virtual method 895: Landroid/net/DhcpInfoInternal;.setDhcpInfo (Landroid/net/DhcpInfo;)V
D/dalvikvm( 6940): VFY: replacing opcode 0x6e at 0x0008
D/KERNEL  ( 6940): remote: 
D/KERNEL  ( 6940): release key report
D/KERNEL  ( 6940): nec_release
D/KERNEL  ( 6940): remote: 
D/KERNEL  ( 6940): release ircode = 0xce,
D/KERNEL  ( 6940): remote: 
D/KERNEL  ( 6940): scancode = 0x0061, maptable = 2,code:0x00000000
D/KERNEL  ( 6940): 
I/EthernetManager( 6940): Init Ethernet Manager
I/PppoeManager( 6940): Init Pppoe Manager
D/AboutActivity( 6940): [20190918223328956][net.sunniwell.setting.jx.ui.AboutActivity][getIpAddr][395]:------updateUI-----false 
D/AboutActivity( 6940): [20190918223328959][net.sunniwell.setting.jx.ui.AboutActivity][getEthernetInfo][434]:=======modeSecure===0 
D/AboutActivity( 6940): [20190918223328961][net.sunniwell.setting.jx.ui.AboutActivity][getEthernetInfo][435]:===setEthernetInfo==mode======dhcp 
D/AndroidRuntime( 6940): Shutting down VM
W/dalvikvm( 6940): threadid=1: thread exiting with uncaught exception (group=0x41627ba8)
I/EthernetManager( 6940): getDhcpInfo
D/EthernetManager( 6940): ===,getDhcpInfo,tenderType:jicai
E/AndroidRuntime( 6940): FATAL EXCEPTION: main
E/AndroidRuntime( 6940): Process: net.sunniwell.setting.jx, PID: 6940
E/AndroidRuntime( 6940): java.lang.NoSuchMethodError: android.net.DhcpInfoInternal.setDhcpInfo
E/AndroidRuntime( 6940): 	at net.sunniwell.setting.jx.ui.AboutActivity.getNetworkInfo(AboutActivity.java:468)
E/AndroidRuntime( 6940): 	at net.sunniwell.setting.jx.ui.AboutActivity.getEthernetInfo(AboutActivity.java:439)
E/AndroidRuntime( 6940): 	at net.sunniwell.setting.jx.ui.AboutActivity.getIpAddr(AboutActivity.java:423)
E/AndroidRuntime( 6940): 	at net.sunniwell.setting.jx.ui.AboutActivity.setData(AboutActivity.java:130)
E/AndroidRuntime( 6940): 	at net.sunniwell.setting.jx.ui.AboutActivity.onResume(AboutActivity.java:84)
E/AndroidRuntime( 6940): 	at android.app.Instrumentation.callActivityOnResume(Instrumentation.java:1215)
E/AndroidRuntime( 6940): 	at android.app.Activity.performResume(Activity.java:5373)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread.performResumeActivity(ActivityThread.java:2778)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread.handleResumeActivity(ActivityThread.java:2817)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2250)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread.access$800(ActivityThread.java:135)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1196)
E/AndroidRuntime( 6940): 	at android.os.Handler.dispatchMessage(Handler.java:102)
E/AndroidRuntime( 6940): 	at android.os.Looper.loop(Looper.java:136)
E/AndroidRuntime( 6940): 	at android.app.ActivityThread.main(ActivityThread.java:5047)
E/AndroidRuntime( 6940): 	at java.lang.reflect.Method.invokeNative(Native Method)
E/AndroidRuntime( 6940): 	at java.lang.reflect.Method.invoke(Method.java:515)
E/AndroidRuntime( 6940): 	at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:842)
E/AndroidRuntime( 6940): 	at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:658)
E/AndroidRuntime( 6940): 	at dalvik.system.NativeStart.main(Native Method)
I/Process ( 6940): Sending signal. PID: 6940 SIG: 9
I/ActivityManager( 5131): Process net.sunniwell.setting.jx (pid 6940) has died.
W/InputMethodManagerService( 5131): Got RemoteException sending setActive(false) notification to pid 6940 uid 1000
```

```java
package net.sunniwell.setting.jx.ui;

import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.InetAddress;

import android.content.Context;
import android.content.Intent;
import android.net.ConnectivityManager;
import android.net.DhcpInfo;
import android.net.DhcpInfoInternal;
import android.net.NetworkInfo.State;
import android.net.NetworkUtils;
import android.net.ethernet.EthernetManager;
import android.net.pppoe.PppoeManager;
import android.net.wifi.WifiInfo;
import android.net.wifi.WifiManager;
import android.os.Build;
import android.os.SystemProperties;
import android.provider.Settings;
import android.text.format.Formatter;
import android.view.Gravity;
import android.widget.FrameLayout;
import android.widget.FrameLayout.LayoutParams;
import net.sunniwell.common.log.SWLogger;
import net.sunniwell.setting.jx.R;
import net.sunniwell.setting.jx.bean.EthernetsBean;
import net.sunniwell.setting.jx.constant.Constants;
import net.sunniwell.setting.jx.manager.EthernetsManager;
import net.sunniwell.setting.jx.util.SWIPUtils;
import net.sunniwell.setting.jx.view.RightTextImageLayout;
import net.sunniwell.setting.jx.view.RightTextLayout;
import net.sunniwell.setting.jx.view.SWRelativeLayout;
import net.sunniwell.setting.jx.view.SWRelativeLayout.onRelativeClickListener;
import net.sunniwell.setting.jx.view.SWRelativeLayout.onRelativeFocusChangeListener;

public class AboutActivity extends BaseActivity implements onRelativeFocusChangeListener, onRelativeClickListener {

	private SWLogger LOG = SWLogger.getLogger(AboutActivity.class);
	private Context mContext;
	private SWRelativeLayout mSWCustomServiceLayout;
	private SWRelativeLayout mSWOfficialWebsiteLayout;
	private SWRelativeLayout mSWLegalInformationLayout;
	private SWRelativeLayout mSWDevicesNameLayout;
	private SWRelativeLayout mSWIpaddrLayout;
	private SWRelativeLayout mSWDevicesVersionLayout;
	private SWRelativeLayout mSWAndroidVersionLayout;
	private SWRelativeLayout mSWKernelVersionLayout;
	private SWRelativeLayout mSWSystemVersionLayout;
	private SWRelativeLayout mSWProductManuLayout;
	private SWRelativeLayout mSWMacAddrLayout;
	private FrameLayout mFrameLayout;

	private RightTextLayout mRightTextLayout;
	private RightTextImageLayout mRightTextImageLayout;
	// private RightButtonLayout mRightButtonLayout;

	private EthernetManager mEthernetManager;
	private EthernetsManager mEthernetsManager;
	private PppoeManager mPppoeManager;
	private WifiManager mWifiManager;
	private ConnectivityManager mConnectivityManager;

	@Override
	protected int setViewId() {
		return R.layout.activity_about;
	}

	@Override
	protected void initData() {
		mContext = this;

		mEthernetManager = (EthernetManager) mContext.getSystemService(Context.ETHERNET_SERVICE);
		mEthernetsManager = EthernetsManager.getInstance(mContext);
		mPppoeManager = (PppoeManager) mContext.getSystemService(Context.PPPOE_SERVICE);
		mWifiManager = (WifiManager) mContext.getSystemService(Context.WIFI_SERVICE);
		mConnectivityManager = (ConnectivityManager) mContext.getSystemService(Context.CONNECTIVITY_SERVICE);
	}

	@Override
	protected void onResume() {
		super.onResume();

		setData();
	}

	@Override
	protected void initView() {
		mSWCustomServiceLayout = (SWRelativeLayout) findViewById(R.id.swlayout_custom_service);
		mSWOfficialWebsiteLayout = (SWRelativeLayout) findViewById(R.id.swlayout_official_website);
		mSWLegalInformationLayout = (SWRelativeLayout) findViewById(R.id.swlayout_legal_information);
		mSWDevicesNameLayout = (SWRelativeLayout) findViewById(R.id.swlayout_devices_name);
		mSWIpaddrLayout = (SWRelativeLayout) findViewById(R.id.swlayout_ipaddr);
		mSWDevicesVersionLayout = (SWRelativeLayout) findViewById(R.id.swlayout_devices_version);
		mSWAndroidVersionLayout = (SWRelativeLayout) findViewById(R.id.swlayout_android_version);
		mSWKernelVersionLayout = (SWRelativeLayout) findViewById(R.id.swlayout_kernel_version);
		mSWSystemVersionLayout = (SWRelativeLayout) findViewById(R.id.swlayout_system_version);
		mSWProductManuLayout = (SWRelativeLayout) findViewById(R.id.swlayout_produce_manu);
		mSWMacAddrLayout = (SWRelativeLayout) findViewById(R.id.swlayout_mac_addr);
		mFrameLayout = (FrameLayout) findViewById(R.id.frame_right_about_content);

		mSWCustomServiceLayout.setOnRelativeFocusChangeListener(this);
		mSWOfficialWebsiteLayout.setOnRelativeFocusChangeListener(this);
		mSWLegalInformationLayout.setOnRelativeFocusChangeListener(this);
		mSWDevicesNameLayout.setOnRelativeFocusChangeListener(this);
		mSWIpaddrLayout.setOnRelativeFocusChangeListener(this);
		mSWDevicesVersionLayout.setOnRelativeFocusChangeListener(this);
		mSWAndroidVersionLayout.setOnRelativeFocusChangeListener(this);
		mSWKernelVersionLayout.setOnRelativeFocusChangeListener(this);
		mSWSystemVersionLayout.setOnRelativeFocusChangeListener(this);
		mSWProductManuLayout.setOnRelativeFocusChangeListener(this);
		mSWMacAddrLayout.setOnRelativeFocusChangeListener(this);

		mSWLegalInformationLayout.setOnRelativeClickListener(this);
		mSWDevicesNameLayout.setOnRelativeClickListener(this);

	}

	private void setData() {
		mSWOfficialWebsiteLayout.setContentText("");
		try {
			String devicesName = Settings.Secure.getString(mContext.getContentResolver(), "stb_name");
			if (devicesName == null) {
				devicesName = mContext.getResources().getString(R.string.text_about_devices_name);
			}
			mSWDevicesNameLayout.setContentText(devicesName);
		} catch (Exception e) {
			e.printStackTrace();
		}
		mSWIpaddrLayout.setContentText(getIpAddr());
		if (SystemProperties.get("ro.custom.build.devicemodel", "UNKNOWN").equals("UNKNOWN")) {
			mSWDevicesVersionLayout.setContentText(SystemProperties.get("ro.build.devicemodel", "UNKNOWN"));
		} else {
			mSWDevicesVersionLayout.setContentText(SystemProperties.get("ro.custom.build.devicemodel", "UNKNOWN"));
		}
		String androidVersion = SystemProperties.get("ro.build.version.release", "UNKNOWN");
		mSWAndroidVersionLayout.setContentText(androidVersion);
		mSWKernelVersionLayout.setContentText(getKernelVersion());
		String versionStr = Build.VERSION.INCREMENTAL;
		String displayVersionStr = null;
		if (SystemProperties.get("ro.custom.version.incremental", "UNKNOWN").equals("UNKNOWN")) {
			displayVersionStr = SystemProperties.get("ro.brand.version.incremental", "");
		} else {
			displayVersionStr = SystemProperties.get("ro.custom.version.incremental", "");
		}
		if (!displayVersionStr.equals("")) {
			versionStr = displayVersionStr;
		}
		mSWSystemVersionLayout.setContentText(versionStr);
		String productName = SystemProperties.get("ro.factory.name", "UNKNOWN");
		mSWProductManuLayout.setContentText(productName);
		String mac = SystemProperties.get("ro.mac", "UNKNOWN");
		if ("".equals(mac) || "UNKNOWN".equals(mac)) {
			mac = SystemProperties.get("ro.bootmac", "UNKNOWN");
		}
		mSWMacAddrLayout.setContentText(mac.toUpperCase());
	}

	@Override
	public void onClick(SWRelativeLayout layout) {
		switch (layout.getId()) {
			case R.id.swlayout_legal_information:
				startDetailsActivity(Constants.ABOUT_LEGAL_DETAILS);
				break;
			case R.id.swlayout_devices_name:
				startDetailsActivity(Constants.ABOUT_DEVICES_NAME);
				break;
			default:
				break;
		}
	}

	@Override
	public void onFocusChange(SWRelativeLayout view, boolean hasFocus) {
		LOG.d("----FocusChange----hasFocus" + hasFocus);
		if (hasFocus) {
			int[] location = new int[2];
			switch (view.getId()) {
				case R.id.swlayout_custom_service:
					int csH = mSWCustomServiceLayout.getHeight();
					mSWCustomServiceLayout.getLocationOnScreen(location);// 在整个屏幕内的绝对坐标
					int csY = location[1] - csH * 3 / 2;
					LOG.d("-----mSWCustomServiceLayout y = " + csY);
					addRightTextImage(csY);
					break;
				case R.id.swlayout_official_website:
					int owH = mSWOfficialWebsiteLayout.getHeight();
					mSWOfficialWebsiteLayout.getLocationOnScreen(location);// 在整个屏幕内的绝对坐标
					int owY = location[1] - owH * 3 / 2;
					LOG.d("-----mSWOfficialWebsiteLayout y = " + owY);
					addRightTextView(owY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_official_website));
					break;
				case R.id.swlayout_legal_information:
					int liH = mSWLegalInformationLayout.getHeight();
					mSWLegalInformationLayout.getLocationOnScreen(location);
					int liY = location[1] - liH * 3 / 2;
					LOG.d("-----mSWLegalInformationLayout y = " + liY);
					addRightTextView(liY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_legal_information));
					break;
				case R.id.swlayout_devices_name:
					int dnH = mSWDevicesNameLayout.getHeight();
					mSWDevicesNameLayout.getLocationOnScreen(location);
					int dnY = location[1] - dnH * 3 / 2;
					LOG.d("-----mSWDevicesNameLayout y = " + dnY);
					addRightTextView(dnY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_devices_name));
					break;
				case R.id.swlayout_ipaddr:
					int ipH = mSWIpaddrLayout.getHeight();
					mSWIpaddrLayout.getLocationOnScreen(location);
					int ipY = location[1] - ipH * 3 / 2;
					LOG.d("-----mSWIpaddrLayout y = " + ipY);
					addRightTextView(ipY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_ip_addr));
					break;
				case R.id.swlayout_devices_version:
					int dvH = mSWDevicesVersionLayout.getHeight();
					mSWDevicesVersionLayout.getLocationOnScreen(location);
					int dvY = location[1] - dvH * 3 / 2;
					LOG.d("-----mSWDevicesVersionLayout y = " + dvY);
					addRightTextView(dvY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_devices_version));
					break;
				case R.id.swlayout_android_version:
					int avH = mSWAndroidVersionLayout.getHeight();
					mSWAndroidVersionLayout.getLocationOnScreen(location);
					int avY = location[1] - avH * 3 / 2;
					LOG.d("-----mSWAndroidVersionLayout y = " + avY);
					addRightTextView(avY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_android_version));
					break;
				case R.id.swlayout_kernel_version:
					int kvH = mSWKernelVersionLayout.getHeight();
					mSWKernelVersionLayout.getLocationOnScreen(location);
					int kvY = location[1] - kvH * 3 / 2;
					LOG.d("-----mSWKernelVersionLayout y = " + kvY);
					addRightTextView(kvY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_kernel_version));
					break;
				case R.id.swlayout_system_version:
					int svH = mSWSystemVersionLayout.getHeight();
					mSWSystemVersionLayout.getLocationOnScreen(location);
					int svY = location[1] - svH * 3 / 2;
					LOG.d("-----mSWSystemVersionLayout y = " + svY);
					addRightTextView(svY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_system_version));
					break;
				case R.id.swlayout_produce_manu:
					/*int pmH = mSWProductManuLayout.getHeight();
					mSWProductManuLayout.getLocationOnScreen(location);
					int pmY = location[1] - pmH * 3 / 2;
					LOG.d("-----mSWProductManuLayout y = " + pmY);
					addRightTextView(pmY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_produce_manu));*/
					if (mRightTextLayout != null) {
						mFrameLayout.removeView(mRightTextLayout);
					}
					break;
				case R.id.swlayout_mac_addr:
					int maH = mSWMacAddrLayout.getHeight();
					mSWMacAddrLayout.getLocationOnScreen(location);
					int maY = location[1] - maH * 3 / 2;
					LOG.d("-----mSWMacAddrLayout y = " + maY);
					addRightTextView(maY);
					mRightTextLayout.setRightText(mContext.getResources().getString(R.string.right_function_mac_addr));
					break;
				default:
					break;
			}
		}
	}

	private void addRightTextView(int y) {
		LOG.d("----addRightTextView----");
		if (mRightTextImageLayout != null) {
			mFrameLayout.removeView(mRightTextImageLayout);
		}
		if (mRightTextLayout == null) {
			mRightTextLayout = new RightTextLayout(mContext);// 上下文，导致崩溃
		} else {
			mFrameLayout.removeView(mRightTextLayout);
		}
		LOG.d("------setH-----" + y);
		FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.WRAP_CONTENT);
		params.gravity = Gravity.CENTER_HORIZONTAL;
		params.topMargin = y;
		mRightTextLayout.setLayoutParams(params);
		// 动态添加按钮到右布局
		mFrameLayout.addView(mRightTextLayout);
	}

	private void addRightTextImage(int y) {
		LOG.d("----addRightTextImage----");
		if (mRightTextLayout != null) {
			mFrameLayout.removeView(mRightTextLayout);
		}
		if (mRightTextImageLayout == null) {
			mRightTextImageLayout = new RightTextImageLayout(mContext);
		} else {
			mFrameLayout.removeView(mRightTextImageLayout);
		}
		LOG.d("------setH-----" + y);
		if (y < 54) {
			y = 54;
		}
		FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.WRAP_CONTENT);
		params.gravity = Gravity.CENTER_HORIZONTAL;
		params.topMargin = y;
		mRightTextImageLayout.setLayoutParams(params);
		// 动态添加按钮到右布局
		mFrameLayout.addView(mRightTextImageLayout);
	}

	// private void addRightButton(int y) {
	// if (mRightTextImageLayout != null) {
	// mFrameLayout.removeView(mRightTextImageLayout);
	// }
	// if (mRightButtonLayout == null) {
	// mRightButtonLayout = new RightButtonLayout(mContext);
	// } else {
	// mFrameLayout.removeView(mRightButtonLayout);
	// }
	// LOG.d("------setH-----" + y);
	// FrameLayout.LayoutParams params = new
	// FrameLayout.LayoutParams(LayoutParams.MATCH_PARENT,
	// LayoutParams.WRAP_CONTENT);
	// params.gravity = Gravity.CENTER_HORIZONTAL;
	// params.topMargin = y;
	// mRightButtonLayout.setLayoutParams(params);
	// // 动态添加按钮到右布局
	// mFrameLayout.addView(mRightButtonLayout);
	// }

	private void startDetailsActivity(String name) {
		Intent intent = new Intent(AboutActivity.this, AboutDetailsActivity.class);
		intent.putExtra(Constants.EXTRA_METHOD_NAME, name);
		startActivity(intent);
	}

	/**
	 * 获取内核版本号
	 *
	 * @return 内核版本号
	 */
	public String getKernelVersion() {
        String kernelVersion = "";
        InputStream inputStream = null;
        try {
            inputStream = new FileInputStream("/proc/version");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
            return kernelVersion;
        }
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream), 8 * 1024);
        String info = "";
        String line = "";
        try {
            while ((line = bufferedReader.readLine()) != null) {
                info += line;
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                bufferedReader.close();
                inputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
 
        try {
            if (info != "") {
                final String keyword = "version ";
                int index = info.indexOf(keyword);
                line = info.substring(index + keyword.length());
                index = line.indexOf(" ");
                kernelVersion = line.substring(0, index);
            }
        } catch (IndexOutOfBoundsException e) {
            e.printStackTrace();
        }
 
        return kernelVersion;
    }


	private String getIpAddr() {
		String ipAddr = "";
		WifiInfo wifiInfo = mWifiManager.getConnectionInfo();
		DhcpInfo info = mWifiManager.getDhcpInfo();
		String ssid = null;
		LOG.d("------updateUI-----" + mWifiManager.isWifiEnabled());
		if (mWifiManager.isWifiEnabled()) {
			int mode = mPppoeManager.getPppoeType();
			ssid = wifiInfo.getSSID();
			LOG.d("======updateUi======ssid" + wifiInfo.getSSID() + "=ip=" + info.ipAddress + "=mask=" + info.netmask + "=gateway=" + info.gateway + "=dns=" + info.dns1);
			LOG.d("========state======" + mConnectivityManager.getNetworkInfo(ConnectivityManager.TYPE_WIFI).getState());
			if (wifiInfo != null && ssid != null && !ssid.equals("") && mConnectivityManager.getNetworkInfo(ConnectivityManager.TYPE_WIFI).getState() == State.CONNECTED) {
				LOG.d("========mode======" + mode);
				if (mode == PppoeManager.DEVICE_TYPE_WIFI) {
					try {
						LOG.d("=====mode======" + mode);
						EthernetsBean bean = new EthernetsBean();
						getNetworkInfo(bean, mPppoeManager.getDhcpInfo());
						ipAddr = bean.getIp();
					} catch (Exception e) {
						e.printStackTrace();
					}
				} else {
					ipAddr = Formatter.formatIpAddress(wifiInfo.getIpAddress());
				}
			} else {
				ipAddr = "";
			}
		} else {
			ipAddr = "";
		}
		if (ipAddr == null || ipAddr.equals("")) {
			// 有线信息
			ipAddr = getEthernetInfo(mEthernetManager.getEthernetMode());
		}
		return ipAddr;
	}

	private String getEthernetInfo(String mode) {
		String ethIpaddr = "";
		String modeSecure = Settings.Secure.getString(mContext.getContentResolver(), "mode_ipoe");
		if (modeSecure == null) {
			modeSecure = "0";
		}
		LOG.d("=======modeSecure===" + modeSecure);
		LOG.d("===setEthernetInfo==mode======" + mode);
		if (mode != null) {
			EthernetsBean bean = new EthernetsBean();
			getNetworkInfo(bean, mEthernetsManager.getEthernetDhcpInfo());
			String ip = bean.getIp();
			LOG.d("=======netLinkStatus=======ip====" + ip);
			boolean netLinkStatus = mEthernetManager.getNetLinkStatus();
			LOG.d("=======netLinkStatus===========" + netLinkStatus);
			if (netLinkStatus) {
				ethIpaddr = ip;
			} else {
				ethIpaddr = "";
			}
		} else {
			ethIpaddr = "";
		}
		return ethIpaddr;
	}

	private void getNetworkInfo(EthernetsBean bean, DhcpInfo dhcpInfo) {
		if (dhcpInfo != null) {
			if (dhcpInfo != null) {
				bean.setIp(SWIPUtils.intToIp(dhcpInfo.ipAddress));
				bean.setMask(SWIPUtils.intToIp(dhcpInfo.netmask));
				bean.setGateway(SWIPUtils.intToIp(dhcpInfo.gateway));
				bean.setDns(SWIPUtils.intToIp(dhcpInfo.dns1));
				bean.setDns2(SWIPUtils.intToIp(dhcpInfo.dns2));
			}
		}
	}

}

```

### 点文件管理闪退

主要分析 __Unable to find explicit activity class {net.sunniwell.app.localplayer/net.sunniwell.app.localplayer.SWLocalPlayerAllActivity}; have you declared this activity in your AndroidManifest.xml__

得出调用不到相应apk

```
root@p201_iptv:/ # logcat -c ; logcat | grep 12611                             
D/ContextImpl(12611): cls name is:net.sunniwell.app.localplayer.SWLocalPlayerAllActivity
E/InputEventSender(12611): Exception dispatching finished signal.
E/MessageQueue-JNI(12611): Exception in MessageQueue callback: handleReceiveCallback
W/ContextImpl(12611): Calling a method in the system process without a qualified user: android.app.ContextImpl.startActivity:1129 android.content.ContextWrapper.startActivity:311 net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity:76 net.sunniwell.setting.jx.MainActivity.onClick:71 android.view.View.performClick:4438 
W/ContextImpl(12611): Calling a method in the system process without a qualified user: android.app.ContextImpl.startActivity:1141 android.app.ContextImpl.startActivity:1130 android.content.ContextWrapper.startActivity:311 net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity:76 net.sunniwell.setting.jx.MainActivity.onClick:71 
I/ActivityManager( 5187): START u0 {flg=0x10000000 cmp=net.sunniwell.app.localplayer/.SWLocalPlayerAllActivity} from pid 12611
E/MessageQueue-JNI(12611): android.content.ActivityNotFoundException: Unable to find explicit activity class {net.sunniwell.app.localplayer/net.sunniwell.app.localplayer.SWLocalPlayerAllActivity}; have you declared this activity in your AndroidManifest.xml?
E/MessageQueue-JNI(12611): 	at android.app.Instrumentation.checkStartActivityResult(Instrumentation.java:1651)
E/MessageQueue-JNI(12611): 	at android.app.Instrumentation.execStartActivity(Instrumentation.java:1447)
E/MessageQueue-JNI(12611): 	at android.app.ContextImpl.startActivity(ContextImpl.java:1158)
E/MessageQueue-JNI(12611): 	at android.app.ContextImpl.startActivity(ContextImpl.java:1130)
E/MessageQueue-JNI(12611): 	at android.content.ContextWrapper.startActivity(ContextWrapper.java:311)
E/MessageQueue-JNI(12611): 	at net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity(MainMenuModel.java:76)
E/MessageQueue-JNI(12611): 	at net.sunniwell.setting.jx.MainActivity.onClick(MainActivity.java:71)
E/MessageQueue-JNI(12611): 	at android.view.View.performClick(View.java:4438)
E/MessageQueue-JNI(12611): 	at android.view.View.onKeyUp(View.java:8241)
E/MessageQueue-JNI(12611): 	at android.view.KeyEvent.dispatch(KeyEvent.java:2936)
E/MessageQueue-JNI(12611): 	at android.view.View.dispatchKeyEvent(View.java:7665)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1403)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/MessageQueue-JNI(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/MessageQueue-JNI(12611): 	at com.android.internal.policy.impl.PhoneWindow$DecorView.superDispatchKeyEvent(PhoneWindow.java:2044)
E/MessageQueue-JNI(12611): 	at com.android.internal.policy.impl.PhoneWindow.superDispatchKeyEvent(PhoneWindow.java:1506)
E/MessageQueue-JNI(12611): 	at android.app.Activity.dispatchKeyEvent(Activity.java:2445)
E/MessageQueue-JNI(12611): 	at com.android.internal.policy.impl.PhoneWindow$DecorView.dispatchKeyEvent(PhoneWindow.java:1965)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$ViewPostImeInputStage.processKeyEvent(ViewRootImpl.java:3854)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$ViewPostImeInputStage.onProcess(ViewRootImpl.java:3828)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$AsyncInputStage.forward(ViewRootImpl.java:3527)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:3428)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$AsyncInputStage.apply(ViewRootImpl.java:3584)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:3428)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$AsyncInputStage.forward(ViewRootImpl.java:3560)
E/MessageQueue-JNI(12611): 	at android.view.ViewRootImpl$ImeInputStage.onFinishedInputEvent(ViewRootImpl.java:3720)
E/MessageQueue-JNI(12611): 	at android.view.inputmethod.InputMethodManager$PendingEvent.run(InputMethodManager.java:2013)
E/MessageQueue-JNI(12611): 	at android.view.inputmethod.InputMethodManager.invokeFinishedInputEventCallback(InputMethodManager.java:1707)
E/MessageQueue-JNI(12611): 	at android.view.inputmethod.InputMethodManager.finishedInputEvent(InputMethodManager.java:1698)
E/MessageQueue-JNI(12611): 	at android.view.inputmethod.InputMethodManager$ImeInputEventSender.onInputEventFinished(InputMethodManager.java:1990)
E/MessageQueue-JNI(12611): 	at android.view.InputEventSender.dispatchInputEventFinished(InputEventSender.java:141)
E/MessageQueue-JNI(12611): 	at android.os.MessageQueue.nativePollOnce(Native Method)
E/MessageQueue-JNI(12611): 	at android.os.MessageQueue.next(MessageQueue.java:138)
E/MessageQueue-JNI(12611): 	at android.os.Looper.loop(Looper.java:123)
E/MessageQueue-JNI(12611): 	at android.app.ActivityThread.main(ActivityThread.java:5047)
E/MessageQueue-JNI(12611): 	at java.lang.reflect.Method.invokeNative(Native Method)
E/MessageQueue-JNI(12611): 	at java.lang.reflect.Method.invoke(Method.java:515)
E/MessageQueue-JNI(12611): 	at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:842)
E/MessageQueue-JNI(12611): 	at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:658)
E/MessageQueue-JNI(12611): 	at dalvik.system.Native
D/AndroidRuntime(12611): Shutting down VM
W/dalvikvm(12611): threadid=1: thread exiting with uncaught exception (group=0x41627ba8)
E/AndroidRuntime(12611): FATAL EXCEPTION: main
E/AndroidRuntime(12611): Process: net.sunniwell.setting.jx, PID: 12611
E/AndroidRuntime(12611): android.content.ActivityNotFoundException: Unable to find explicit activity class {net.sunniwell.app.localplayer/net.sunniwell.app.localplayer.SWLocalPlayerAllActivity}; have you declared this activity in your AndroidManifest.xml?
E/AndroidRuntime(12611): 	at android.app.Instrumentation.checkStartActivityResult(Instrumentation.java:1651)
E/AndroidRuntime(12611): 	at android.app.Instrumentation.execStartActivity(Instrumentation.java:1447)
E/AndroidRuntime(12611): 	at android.app.ContextImpl.startActivity(ContextImpl.java:1158)
E/AndroidRuntime(12611): 	at android.app.ContextImpl.startActivity(ContextImpl.java:1130)
E/AndroidRuntime(12611): 	at android.content.ContextWrapper.startActivity(ContextWrapper.java:311)
E/AndroidRuntime(12611): 	at net.sunniwell.setting.jx.model.impl.MainMenuModel.showPositionActivity(MainMenuModel.java:76)
E/AndroidRuntime(12611): 	at net.sunniwell.setting.jx.MainActivity.onClick(MainActivity.java:71)
E/AndroidRuntime(12611): 	at android.view.View.performClick(View.java:4438)
E/AndroidRuntime(12611): 	at android.view.View.onKeyUp(View.java:8241)
E/AndroidRuntime(12611): 	at android.view.KeyEvent.dispatch(KeyEvent.java:2936)
E/AndroidRuntime(12611): 	at android.view.View.dispatchKeyEvent(View.java:7665)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1403)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/AndroidRuntime(12611): 	at android.view.ViewGroup.dispatchKeyEvent(ViewGroup.java:1408)
E/AndroidRuntime(12611): 	at com.android.internal.policy.impl.PhoneWindow$DecorView.superDispatchKeyEvent(PhoneWindow.java:2044)
E/AndroidRuntime(12611): 	at com.android.internal.policy.impl.PhoneWindow.superDispatchKeyEvent(PhoneWindow.java:1506)
E/AndroidRuntime(12611): 	at android.app.Activity.dispatchKeyEvent(Activity.java:2445)
E/AndroidRuntime(12611): 	at com.android.internal.policy.impl.PhoneWindow$DecorView.dispatchKeyEvent(PhoneWindow.java:1965)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$ViewPostImeInputStage.processKeyEvent(ViewRootImpl.java:3854)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$ViewPostImeInputStage.onProcess(ViewRootImpl.java:3828)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$AsyncInputStage.forward(ViewRootImpl.java:3527)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:3428)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$AsyncInputStage.apply(ViewRootImpl.java:3584)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:3428)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:3401)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:3451)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:3420)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$AsyncInputStage.forward(ViewRootImpl.java:3560)
E/AndroidRuntime(12611): 	at android.view.ViewRootImpl$ImeInputStage.onFinishedInputEvent(ViewRootImpl.java:3720)
E/AndroidRuntime(12611): 	at android.view.inputmethod.InputMethodManager$PendingEvent.run(InputMethodManager.java:2013)
E/AndroidRuntime(12611): 	at android.view.inputmethod.InputMethodManager.invokeFinishedInputEventCallback(InputMethodManager.java:1707)
E/AndroidRuntime(12611): 	at android.view.inputmethod.InputMethodManager.finishedInputEvent(InputMethodManager.java:1698)
E/AndroidRuntime(12611): 	at android.view.inputmethod.InputMethodManager$ImeInputEventSender.onInputEventFinished(InputMethodManager.java:1990)
E/AndroidRuntime(12611): 	at android.view.InputEventSender.dispatchInputEventFinished(InputEventSender.java:141)
E/AndroidRuntime(12611): 	at android.os.MessageQueue.nativePollOnce(Native Method)
E/AndroidRuntime(12611): 	at android.os.MessageQueue.next(MessageQueue.java:138)
E/AndroidRuntime(12611): 	at android.os.Looper.loop(Looper.java:123)
E/AndroidRuntime(12611): 	at android.app.ActivityThread.main(ActivityThread.java:5047)
E/AndroidRuntime(12611): 	at java.lang.reflect.Method.invokeNative(Native Method)
E/AndroidRuntime(12611): 	at java.lang.reflect.Method.invoke(Method.java:515)
E/AndroidRuntime(12611): 	at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:842)
E/AndroidRuntime(12611): 	at com.android.interna
I/Process (12611): Sending signal. PID: 12611 SIG: 9
I/ActivityManager( 5187): Process net.sunniwell.setting.jx (pid 12611) has died.
W/InputMethodManagerService( 5187): Got RemoteException sending setActive(false) notification to pid 12611 uid 1000

```

这里点击文件管理退出，因为缺少apk导致，安装相应apk既可解决问题

