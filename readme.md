# Bluetooth Low Energy Server with BLESSED-ANDROID library (part 4)

This is part 4 of the BLE server (peripheral) example using the code in 
https://github.com/weliem/bluetooth-server-example.

**This app is about exposing the connected devices to the user interface (UI).**

Recent server and client apps:

**Part 3: add a Battery Service to your server and client**

The code for the server from part 3 is available here: https://github.com/AndroidCrypto/BleServerBlessedPart3
and a description is here: https://medium.com/@androidcrypto/add-a-battery-service-to-your-bluetooth-low-energy-server-part-3-ab42cc96e43b.

The companion code for the client from part 3 is here: https://github.com/AndroidCrypto/BleClientBlessedPart3
and a description is here: https://medium.com/@androidcrypto/add-a-battery-service-listener-to-a-android-bluetooth-low-energy-client-part-3-c70e16ed130a

**Part 2: Enhance your server and client**

The code for the server from part 2 is available here: https://github.com/AndroidCrypto/BleServerBlessedPart2 
and a description is here: https://medium.com/@androidcrypto/enhance-your-own-android-bluetooth-low-energy-server-part-2-980cac9f910f.

The companion code for the client from part 2 is here: https://github.com/AndroidCrypto/BleClientBlessedPart2 
and a description is here: https://medium.com/@androidcrypto/enhance-a-android-bluetooth-low-energy-client-part-2-200aab7255de

**Part 1: Setup your own server and client**

The code for the server from part 1 is available here: https://github.com/AndroidCrypto/BleServerBlessedOriginal 
and a description is here: https://medium.com/@androidcrypto/setup-your-own-android-bluetooth-low-energy-server-part-1-dbf8dadd75b5.

The companion code for the client from part 1 is here: https://github.com/AndroidCrypto/BleClientBlessedOriginal 
and a description is here: https://medium.com/@androidcrypto/setup-a-android-bluetooth-low-energy-client-part-1-70f0eea9149b

The code is changed to get a better user experience when running the server and to be compatible with the 
sample client-app of the library (see below).

The library in use (BLESSED-ANDROID) is available here: https://github.com/weliem/blessed-android 
provided by **Martijn van Welie**.

For a general overview on Bluetooth Low Energy (BLE) see this perfect article: "The Ultimate Guide to Android Bluetooth Low Energy", 
available as PDF in the docs folder as well: https://punchthrough.com/android-ble-guide/.

Screenshot of the running app after startup:
![server_view_after_starting](docs/server00.png?raw=true)

To check that the server is up and running I recommend to install another app on a second device that 
allows to connect to the "Server", I'm using **nRF Connect for Mobile** and it is available on the 
Google's PlayStore:  https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=de&gl=US. I   
provide a simple manual on how to work with the nRF Connect-app here: 
[nRFConnect_manual](nrfconnect_manual.md) or my article on Medium: 
https://medium.com/@androidcrypto/connect-the-android-nrf-connect-mobile-app-with-a-bluetooth-low-energy-device-8ba900d70286

To get the Server app to build you need 2 additional dependencies, add them in build.gradle(app):
```plaintext
    implementation 'com.jakewharton.timber:timber:5.0.1'
    implementation 'com.github.weliem:blessed-android:2.3.4'
```

Additionally a new line is necessary in the settings.gradle file (project settings):
```plaintext
add the line maven { url 'https://jitpack.io' }:

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

You may notice that the AndroidManifest.xml does not contain any Bluetooth related permissions - they are all  
set within the library but you are asked to grant some runtime permissions during startup (depending on the Android 
SDK version running on your Smartphone the server is running on).

Notice regarding a bug in the blessed-library's log system: in BluetoothServer.java you will notice an 
"error" on line 183 ("Cannot resolve method 'plant(timber.log.Timber.DebugTree)'"):
```plaintext
Timber.plant(new Timber.DebugTree());
```
This error is filed as a Timber issue and may get corrected in a newer version. The good news is - you 
can build your app regardless of this "error" and you still see the logged messages in your LogCat.

**Important notice when working with an emulated device running on a Smartphone (e.g. the BleServerBlessedOriginal): 
For security reasons the address the server can get connected is changing very often so when using a client app 
like the nRF Connect-app it is often necessary to (re)run a scan AND choose the newest entry (mostly the most 
bottom down one).**

Some technical details on this app:
```plaintext
minimum SDK is 21
compiled/target SDK is 33
Gradle version is 7.4
```

The library blessed-android is MIT-licensed.

## License

BLE Server Blessed Part 4 is available under the MIT license. See the LICENSE.md file for more info.
