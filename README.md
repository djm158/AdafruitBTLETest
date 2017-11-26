BTLETest
========

Simple test for sending and receiving data to a Bluetooth Low Energy UART service from an Android 4.3 or 4.4 device.


Build a simple Bluefruit LE + Arduino circuit and load the Bluefruit LE library echoDemo on the Arduino.

Make sure bluetooth is enabled, then load the BLETest application (has a generic Android icon).  Once started the app will immediately search for BTLE devices and connect to the first one it finds with the UART service.  Status messages will be displayed in a text view on the screen.  

Once you see the connected and services discovered message, try typing text in the edit view at the top and click Send to send it to the Arduino.  From the Arduino side try sending text from its serial monitor to the BLETest app.

The source for this app is written in the latest version (3.0.0) of [Android Studio](http://developer.android.com/sdk/installing/studio.html).

Tested on Android 8.0 devices (Nexus 6P, Google Pixel XL). Needed to enable USB debugging and set USB configuration to "MTP (Media Transfer Protocl) in Developer Settings -> Select USB Configuration

This app assumes the UART service is sending a float as a byte array. It is therefore necessary to wrap the received value in a `ByteBuffer` and reorder that data to little endian byte order. see `onCharacteristicChanged` in `MainActivity.java`

```
float f1 = ByteBuffer.wrap(characteristic.getValue()).order(ByteOrder.LITTLE_ENDIAN).getFloat();
```

Thanks to [Tony Dicola](https://github.com/tdicola/) for the example code.
