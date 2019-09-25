Admob ANE for Flash Air


## Admob ANE Description
Admob Air Native Extention（Admob ANE）提供了一种在Air ios和Air Android游戏和应用程序中集成admob广告的方法。
您可以使用它与Air iOS和Android App使用相同的actionscript代码，不需要任何更改，不需要java
或者你不需要Admob ANE for ios和Admob ANE for android使用此Ane进行单独版本。

Google移动广告SDK是Google移动广告中的最新一代，具有精致的广告格式和简化的API，可用于访问移动广告网络和广告解决方案。 该SDK使Air移动应用程序开发人员能够最大限度地利用本机移动应用程序的货币化。


## Admob ANE For Air 功能点
使用相同的api支持IOS和Android
支持横幅（所有横幅尺寸）
支持Intersitial
支持奖励视频
支持横向和纵向以及autoOrient
支持AdRequest定位方法，例如子目标，测试模式
支持Air SDK 30到最新版本
支持IOS 8到ios 12
非常简单的API


## Quick Start
#### 1.初始化 Admob ANE 
将Admob ane添加到air项目构建路径，在脚本文件中添加以下代码
```
    import so.cuo.platform.admob.*;
    Admob.getInstance().initAdmobSDK("your admob app ID");

```
#### 2.显示Admob横幅广告在air应用中
这是显示admob横幅的代码
```
    Admob.getInstance().showBanner("your banner ID ",AdmobSize.BANNER_320x50,AdmobPosition.BOTTOM_CENTER);

```

Admob Position类指定放置横幅的位置。 Admob Size指定要显示的女巫大小横幅

#### 3.移除横幅
默认情况下，横幅是可见的， 要隐藏横幅
```
    Admob.getInstance().hideBanner();
```


#### 4.Admob ANE 显示全屏广告
如何将Interstitial集成到Air ios应用程序或flex Android应用程序？
以下是创建插页式广告的代码
```
    Admob.getInstance().cacheInterstitial("your Interstitial ID "); 
```
在展示之前需要加载插页式广告。 在适当的地方展示
在您的应用中停止点，检查之前是否已准备好interstitail
显示它
```
    if (Admob.getInstance().isInterstitialReady()) {
      Admob.getInstance().showInterstitial();
    }
```
#### 5.Custom Admob Banner Ad Sizes
除了_AdSize_上的常量之外，您还可以创建自定义大小：
```
    //Create a 320x250 banner.
    AdSize adSize = new AdSize(320, 250);
    Admob.getInstance().showBannerAbsolute(adSize,0,30);
```
#### 6.设置 Admob附加参数
设置Admob目标参数，例如测试广告和小孩子应用
如果您想测试广告或带有孩子应用，您可以使用admob ANE轻松设置
```
       extraParam=new ExtraParameter();
	extraParam.testDeviceID="true";
	extraParam.isChildApp=true;//if is tagForChildDirectedTreatment,set true
        extraParam.isDesignedForFamilies=true;
        extraParam.nonPersonalizedAds=true;//if want to load non Personalized ads set true
	Admob.getInstance().showBanner("Your banner ID",AdmobSize.BANNER_320x50,AdmobPosition.BOTTOM_CENTER,80,extraParam);
```
#### 7.广告事件
横幅和全屏广告都包含很多的广告事件
你可以对你感兴趣的事件进行监听处理
```
    Admob.getInstance().addEventListener(AdmobEvent.onInterstitialReceive, onAdEvent);
	private function onAdEvent(event:AdmobEvent):void
	{
		if (event.type == AdmobEvent.onBannerReceive)
		{
			trace(event.instanceName,event.data.width, event.data.height);
		}
		if (event.type == AdmobEvent.onInterstitialReceive)
		{
			Admob.getInstance().showInterstitial();
		}
	}
```

#### 9.Admob 奖励视频广告
 视频广告的api和全屏广告的api类似
    
在这里，我们将演示如何在视频上设置广告事件，并在加载成功时显示视频：
```
if(admob.isVideoReady()){
	admob.showVideo();
}else{
	admob.cacheVideo(videoID);
}
    Admob.getInstance().addEventListener(AdmobEvent.onVideoReceive, onVideoEvent);
	private function onVideoEvent(event:AdmobEvent):void
	{
		if (event.type == AdmobEvent.onVideoReceive)
		{
			trace("load video success,you can show video now");
		}
		
	}
```



###  10.IOS  设置
对于ios需要MinimumOSVersion，需要ios 8及更高版本才能使用
```
	<key>MinimumOSVersion</key>
        <string>8.0</string>
```
simple example
```
 <iPhone>
        <InfoAdditions><![CDATA[
			<key>UIDeviceFamily</key>
			<array>
				<string>1</string>
				<string>2</string>
			</array>
				<key>MinimumOSVersion</key>
        <string>8.0</string>
			<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
    <key>NSAllowsArbitraryLoadsForMedia</key>
    <true/>
    <key>NSAllowsArbitraryLoadsInWebContent</key>
    <true/>
</dict>
		]]></InfoAdditions>
        <requestedDisplayResolution>high</requestedDisplayResolution>
    </iPhone>
```


### 11.android 权限设置
admob 17需要Meta Config com.google.android.gms.ads.APPLICATION_ID
请使用您的admob ID替换ca-app-pub-3940256099942544~3347511713
```
<android>
        <manifestAdditions><![CDATA[
			<manifest android:installLocation="auto">
			    <uses-permission android:name="android.permission.INTERNET"/>
			    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
			    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
			     <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
			     <application>
 <meta-data android:name="com.google.android.gms.version"
        android:value="@integer/google_play_services_version" />
			  	   <activity android:name="com.google.android.gms.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" android:theme="@android:style/Theme.Translucent"/>

 <meta-data
            android:name="com.google.android.gms.ads.APPLICATION_ID"
            android:value="ca-app-pub-3940256099942544~3347511713"/>

			     </application>
			</manifest>
		]]></manifestAdditions>
    </android>
```

### 12.获取屏幕尺寸

```
Admob.getInstance().getScreenSize()

```

### 13.ANE ID
```
<extensionID>so.cuo.platform.admob</extensionID>
```

## Screenshots
![ScreenShot](https://github.com/lilili87222/admob-for-flash/blob/master/images/screen.jpg?raw=true)