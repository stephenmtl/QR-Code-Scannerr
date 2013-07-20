QR-Code-Scannerr
================

QR Code/Barcode Scanner for Phonecap 

Cross-platform BarcodeScanner for Cordova / PhoneGap.

Follows the Cordova Plugin spec, so that it works with Plugman.

This plugin leverages Cordova/PhoneGap's require/define functionality used for plugins.

Note: the Android source for this project includes an Android Library Project. pluginstall currently doesn't support Library Project refs, so its been prebuilt as a jar library. Any updates to the Library Project should be committed with an updated jar.

Using the plugin

The plugin creates the object cordova/plugin/BarcodeScanner with the method scan(success, fail).

The following barcode types are currently supported:

Android

QR_CODE
DATA_MATRIX
UPC_E
UPC_A
EAN_8
EAN_13
CODE_128
CODE_39
CODE_93
CODABAR
ITF
RSS14
PDF417
RSS_EXPANDED


iOS

QR_CODE
DATA_MATRIX
UPC_E
UPC_A
EAN_8
EAN_13
CODE_128
CODE_3
success and fail are callback functions. Success is passed an object with data, type and cancelled properties. Data is the text representation of the barcode data, type is the type of barcode detected and cancelled is whether or not the user cancelled the scan.

A full example could be:

   var scanner = cordova.require("cordova/plugin/BarcodeScanner");

   scanner.scan(
      function (result) {
          alert("We got a barcode\n" +
                "Result: " + result.text + "\n" +
                "Format: " + result.format + "\n" +
                "Cancelled: " + result.cancelled);
      }, 
      function (error) {
          alert("Scanning failed: " + error);
      }
   );
Encoding a Barcode

The plugin creates the object window.plugins.barcodeScanner with the method encode(type, data, success, fail). Supported encoding types:

TEXT_TYPE
EMAIL_TYPE
PHONE_TYPE
SMS_TYPE
A full example could be:

   var scanner = cordova.require("cordova/plugin/BarcodeScanner");

   scanner.encode(BarcodeScanner.Encode.TEXT_TYPE, "http://www.nytimes.com", function(success) {
            alert("encode success: " + success);
          }, function(fail) {
            alert("encoding failed: " + fail);
          }
        );
