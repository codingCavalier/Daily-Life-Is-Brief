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
- 某些第三方库，代码中的限制，低于21直接抛出异常导致程序无法继续运行，如`com.squareup.okhttp3:okhttp:4.4.0`中的代码：
```Kotlin
val isSupported: Boolean = when {
  !isAndroid -> false
  else -> {
    // Fail Fast
    check(
        Build.VERSION.SDK_INT >= 21) { "Expected Android API level 21+ but was ${Build.VERSION.SDK_INT}" }

    true
  }
}
```
- 降低第三方库的版本。首先要查明，哪些地方引入了这个第三方库的这个版本：
- Terminal命令行中执行`.\gradlew :app:androidDependencies`查看有哪些构建变体
- 然后执行`./gradlew :app:dependencyInsight --dependency okhttp:4.4.0 --configuration 某个你喜欢的构建变体`
    - 例如：./gradlew :app:dependencyInsight --dependency okhttp:4.4.0 --configuration debugRuntimeClasspath
- 这是我的依赖情况，可以自己分析一下最根上是哪个库引入了这个第三方库的这个版本：
- <img width="544" height="355" alt="image" src="https://github.com/user-attachments/assets/0cf4059b-b8ec-440e-adf0-cde2bf06e496" />

##### 问题3
- 编译时报错：Unrecognized VM option 'MaxPermSize=512m'，因为Java 8移除了此项配置，可以改为：-XX:MaxMetaspaceSize=512m









