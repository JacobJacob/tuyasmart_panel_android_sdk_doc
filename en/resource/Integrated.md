# Integrated PanleSDK
1. Create Project

   Build your project in the Android Studio and integrate Tuyasmart HomeSDK

2. Configure the root build.gradle

  ``` groovy
  allprojects {
      repositories {
          maven { url 'https://maven-other.tuya.com/repository/maven-releases/' }
          maven { url 'https://jitpack.io' }
      }
  }
  ```

3. Configure the module build.gradle

  ``` groovy
  android {
        defaultConfig {
          ndk {
              abiFilters "armeabi-v7a", "arm64-v8a"
          }
      }

      repositories {
          flatDir {
              dirs 'libs'
          }
      }
      compileOptions {
          sourceCompatibility 1.8
          targetCompatibility 1.8
      }

      packagingOptions {
          pickFirst 'lib/*/libc++_shared.so'
      }
  
    lintOptions {
          abortOnError false
      }
  }
	dependencies {
      implementation fileTree(dir: 'libs', include: ['*.jar'])
      implementation 'com.tuya.smart:panel-sdk:0.4.0'
      implementation "com.tuya.smart:tuyasmart-TuyaRNApi:5.22.54-open"
      implementation 'com.tuya.smart:tuyasmart:3.13.0'

      implementation 'com.weigan:loopView:0.1.1'
      implementation 'com.facebook.infer.annotation:infer-annotation:0.11.2'
      implementation 'com.facebook.soloader:soloader:0.8.0'
      implementation 'com.facebook.fresco:fresco:1.3.0'
      implementation "com.facebook.fresco:imagepipeline-okhttp3:1.3.0"
      implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.2.0'
      implementation 'javax.inject:javax.inject:1'
      implementation 'com.alibaba:fastjson:1.1.67.android'
      implementation 'com.facebook.react:react-native:0.51.1.11'
      implementation 'org.apache.commons:commons-compress:1.9'
      implementation 'com.kyleduo.switchbutton:library:1.4.2'
      implementation 'com.github.PhilJay:MPAndroidChart:v3.0.3'
      implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
      implementation 'io.reactivex.rxjava2:rxandroid:2.0.1'
      implementation 'io.reactivex.rxjava2:rxjava:2.1.7'
      implementation 'com.android.support.constraint:constraint-layout:1.1.3'
  	}
  ```

    **Optional Configuration**

    * Amap (only China configure)

    ``` groovy
    implementation 'com.amap.api:search:6.9.2'
    implementation 'com.amap.api:map2d:5.2.0'
    implementation 'com.tuya.smart:tuyasmart-react-native-amap:1.0.0'
    ```

    * GoogleMap (only GooglePlay confingure)

    ``` groovy
    implementation 'com.tuya.smart:tuyasmart-react-native-googlemap:1.0.0'
    implementation 'com.google.android.gms:play-services-maps:16.1.0'
    ```

    * QQ Music

    ``` groovy
    implementation(name: 'qqmusic-innovation-aidl-api-sdk-1.0.0-SNAPSHOT-release', ext: 'aar')
  	implementation 'com.tuya.smart.rnplugin:tyrctspeakermanager:1.0.15-open'
    def tvsVer = '2.3.0'
    implementation "com.tencent.yunxiaowei.dmsdk:core:$tvsVer"
    implementation "com.tencent.yunxiaowei.webviewsdk:webviewsdk:$tvsVer"
    ```

    * Sweeper

    ``` groovy
    implementation 'com.tuya.smart:tuyasmart-react-native-fetch-blob:3.12.0r123h1'
    implementation 'com.tuya.smart.rnplugin:tyrctlasermanager:1.0.12-h1'
    implementation 'com.tuya.smart.rnplugin:tyrctlasermap:1.1.30'
    implementation 'com.tuya.smart.rnplugin:tyrctpointmap:1.0.19'
    implementation 'com.tuya.smart.rnplugin:tyrctvisionmanager:1.0.7'
    implementation 'com.tuya.smart.rnplugin:tyrctvisionmap:1.0.11'
    implementation 'com.tuya.smart.rnplugin:tyrcttransfermanager:1.0.5'
    implementation 'com.tuya.smart:tuyasmart-react-sweeper-common:1.0.0-rc.5'
    ```

4. Configure the progurad

  ``` 
  # react-native
  -keep,allowobfuscation @interface com.facebook.common.internal.DoNotStrip
  -keep,allowobfuscation @interface com.facebook.proguard.annotations.DoNotStrip
  -keep,allowobfuscation @interface com.facebook.proguard.annotations.KeepGettersAndSetters
  # Do not strip any method/class that is annotated with @DoNotStrip
  -keep @com.facebook.proguard.annotations.DoNotStrip class *
  -keep @com.facebook.common.internal.DoNotStrip class *
  -keepclassmembers class * {
      @com.facebook.proguard.annotations.DoNotStrip *;
      @com.facebook.common.internal.DoNotStrip *;
  }
  -keepclassmembers @com.facebook.proguard.annotations.KeepGettersAndSetters class * {
    void set*(***);
    *** get*();
  }
  -keep class * extends com.facebook.react.bridge.JavaScriptModule { *; }
  -keep class * extends com.facebook.react.bridge.NativeModule { *; }
  -keepclassmembers,includedescriptorclasses class * { native <methods>; }
  -keepclassmembers class *  { @com.facebook.react.uimanager.UIProp <fields>; }
  -keepclassmembers class *  { @com.facebook.react.uimanager.annotations.ReactProp <methods>; }
  -keepclassmembers class *  { @com.facebook.react.uimanager.annotations.ReactPropGroup <methods>; }
  -dontwarn com.facebook.react.**
  -keep,includedescriptorclasses class com.facebook.react.bridge.** { *; }

  #Amap
  -dontwarn com.amap.**
  -keep class com.amap.api.maps.** { *; }
  -keep class com.autonavi.** { *; }
  -keep class com.amap.api.trace.** { *; }
  -keep class com.amap.api.navi.** { *; }
  -keep class com.autonavi.** { *; }
  -keep class com.amap.api.location.** { *; }
  -keep class com.amap.api.fence.** { *; }
  -keep class com.autonavi.aps.amapapi.model.** { *; }
  -keep class com.amap.api.maps.model.** { *; }
  -keep class com.amap.api.services.** { *; }

  #Google Play Services
  -keep class com.google.android.gms.common.** {*;}
  -keep class com.google.android.gms.ads.identifier.** {*;}
  -keepattributes Signature,*Annotation*,EnclosingMethod
  -dontwarn com.google.android.gms.**

  #MPAndroidChart
  -keep class com.github.mikephil.charting.** { *; }
  -dontwarn com.github.mikephil.charting.**

  -keep class com.tuya.**.**{*;}
  -dontwarn com.tuya.**.**
  ```

5. Init Tuya Smart Android PanelSDK in the Application

    ``` java
    public class TuyaSmartApp extends Application {

        @Override
        public void onCreate() {
            super.onCreate();
            TuyaWrapper.init(this);
            TuyaPanelSDK.init(this," TUYA_SMART_APPKEY","TUYA_SMART_SECRET");
        }
    }
    ```