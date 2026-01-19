#### 打包
- 首先要能够打出一个 minSdk=19 的包
- 自己项目：所有的模块中gradle配置：android -> defaultConfig -> `minSdk 19`
- 第三方库：有些第三方库minSdk是21，所以要改成19，能自己编的自己编，不能自己编的这样做：
```xml
AndroidManifest.xml中
<manifest
    <uses-sdk
        android:minSdkVersion="19"
        tools:overrideLibrary="org.webrtc:google-webrtc" />
</manifest>
```
- 经过这番折腾后，基本都能打出一个 minSdk=19 的包了

#### 运行
##### 问题1
- 报错：java.lang.ClassNotFoundException: Didn't find class "xxxxxx" on path: DexPathList[[zip file "/data/app/xxxxxx.apk"]，这是传说中的64K方法数问题，需要这样做：
- app模块的build.gradle增加配置：
```groovy
android {
    defaultConfig {
        // 这项配置用于告诉gradle构建时产生多个dex文件
        multiDexEnabled true
    }
}

dependencies {
    // androidX的包，用于向下兼容安卓5.0以下的设备，因为从安卓5.0开始，系统自动支持加载多个dex，无需程序员手动install
    implementation 'androidx.multidex:multidex:2.0.1'
    // 老的support包
    // implementation 'com.android.support:multidex:1.0.3'
}
```
- 自定义Application中，这样配置：
```Kotlin
override fun attachBaseContext(base: Context?) {
    super.attachBaseContext(base)
    MultiDex.install(this)
}
```
##### 问题2
- 












