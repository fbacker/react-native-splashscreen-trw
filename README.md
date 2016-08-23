# react-native-splashscreen-trw
Set a splash screen for Android 'the right way'.

This component is compatible with React Native 0.25 and newer.




## Installation (Android)

* In `android/settings.gradle`

```
...
include ':react-native-splashscreen-trw'
project(':react-native-splashscreen-trw').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splashscreen-trw/android')
```

* In `android/app/build.gradle`

```
...
dependencies {
    ...
    // From node_modules
    compile project(':react-native-splashscreen-trw'')
}
```

* if you want change the layout, create an own res/drawable/splash_layout.xml
Default layout
```
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:drawable="@color/splashBackground"/>

    <item>
        <bitmap
            android:gravity="center"
            android:src="@mipmap/ic_launcher"/>
    </item>

</layer-list>
```

* In MainActivity.java

```
...
/**
 * Note here that we are rewrite the whole MainApplication, no ReactPackages
 */
 private ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
 //private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
     @Override
    protected boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage()
      );
    }
  };
 }

 public void setReactNativeHost(ReactNativeHost reactNativeHost) {
   this.mReactNativeHost = reactNativeHost;
}

public void setReactNativeHost(ReactNativeHost reactNativeHost) {
  this.mReactNativeHost = reactNativeHost;
}
...

```

* In MainActivity.java
```
...
import com.fbacker.splashscreen.RCTSplashScreenPackage;    //import package
...
/**
 * We are adding createRootView and adding all the react packages here instead.
 */
 @Override
  protected ReactRootView createRootView() {

      MainApplication mainApplication = (MainApplication)this.getApplication();
      mainApplication.setReactNativeHost( new ReactNativeHost(mainApplication) {
          @Override
          protected boolean getUseDeveloperSupport() {
              return BuildConfig.DEBUG;
          }

          @Override
          protected List<ReactPackage> getPackages() {
            return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                new RCTSplashScreenPackage(MainActivity.this), <!-- add the package

                ...
            );
          }

      });

      return super.createRootView();
  }
...

```


* In `android/app/**/colors.xml`

```
...
<!-- change background color -->
<color name="splashBackground">#e8e8e8</color>
...
```


## Usage

When app is loaded remove the splash screen
```js
...
import SplashScreen from 'react-native-splashscreen-trw'
...
componentDidMount () {
  if(Platform.OS === 'android'){
    SplashScreen.close('scale', 850, 500);
  }
}
...

```

## Method

* close(animationType, duration, delay)
  close splash screen with custom animation

  * animationType: determine the type of animation. enum('opacity', 'scale')
  * duration: determine the duration of animation
  * delay: determine the delay of animation
