==================
https://github.com/weicht/one_sig/tree/v1.0

flutter create -I swift one_sig
cd one_sig/
<< added to github and tagged as v1.0>>



==================
https://github.com/weicht/one_sig/tree/v1.1

I add these to pubspec.yaml url_launcher: "^3.0.3"
contacts_service: "^0.0.9"
shared_preferences: "^0.4.3"
flutter_secure_storage: "^3.1.2"
permission_handler: "^2.1.0"

And when I run in simulator, I get an Xcode error:
Xcode's output:
↳
    === BUILD TARGET shared_preferences OF PROJECT Pods WITH CONFIGURATION Debug ===
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/permission_handler-2.1.2/ios/Classes/PermissionManager.swift:50:59: error: 'openSettingsURLString' has been renamed to 'UIApplicationOpenSettingsURLString'
                    guard let url = URL(string: UIApplication.openSettingsURLString),
                                                              ^~~~~~~~~~~~~~~~~~~~~
                                                              UIApplicationOpenSettingsURLString
    UIKit.UIApplication:64:22: note: 'openSettingsURLString' was introduced in Swift 4.2
        public class let openSettingsURLString: String
                         ^
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/permission_handler-2.1.2/ios/Classes/PermissionManager.swift:55:45: error: argument labels '(rawValue:)' do not match any available overloads
                    let optionsKeyDictionary = [UIApplication.OpenExternalURLOptionsKey(rawValue: "universalLinksOnly"): NSNumber(value: true)]
                                                ^                                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/permission_handler-2.1.2/ios/Classes/PermissionManager.swift:55:45: note: overloads for 'UIApplication.OpenExternalURLOptionsKey' exist with these partially matching parameter lists: (coder: NSCoder), (stringLiteral: StaticString), (format: NSString, CVarArg...), (string: NSString), (utf8String: UnsafePointer<Int8>), (UTF8String: UnsafePointer<Int8>), (string: String), (contentsOfFile: String), (contentsOf: URL), (contentsOfURL: URL), (cString: UnsafePointer<Int8>), (CString: UnsafePointer<Int8>)
                    let optionsKeyDictionary = [UIApplication.OpenExternalURLOptionsKey(rawValue: "universalLinksOnly"): NSNumber(value: true)]
                                                ^
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/permission_handler-2.1.2/ios/Classes/PermissionManager.swift:59:91: error: 'openSettingsURLString' has been renamed to 'UIApplicationOpenSettingsURLString'
                    let success = UIApplication.shared.openURL(URL.init(string: UIApplication.openSettingsURLString)!)
                                                                                              ^~~~~~~~~~~~~~~~~~~~~
                                                                                              UIApplicationOpenSettingsURLString
    UIKit.UIApplication:64:22: note: 'openSettingsURLString' was introduced in Swift 4.2
        public class let openSettingsURLString: String
                         ^
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/permission_handler-2.1.2/ios/Classes/PermissionManager.swift:99:54: error: closure tuple parameter '(key: String, value: Any)' does not support destructuring
            return Dictionary(uniqueKeysWithValues: input.map { key, value in (UIApplication.OpenExternalURLOptionsKey(rawValue: key), value)})
                                                                ^~~~~~~~~~
                                                                (arg) -> <#Result#> let (key, value) = arg; return 


This page indicated an issue adding swift plugin support to Obj-c projects, but my flutter app was build with -I swift, so not sure if it truly applies to just Obj-C.  One comment seemed to indicated that you still need to add at least one .swift file for the build to truly use swift, so it may still be building in Obj-C mode since my project is empty except the default flutter demo app.
https://pub.dartlang.org/packages/permission_handler

Went to this page for support
https://github.com/flutter/flutter/issues/16049

Adding this one line to the post_install section allowed build to work:
    config.build_settings['SWIFT_VERSION'] = '3.2' # <--- add this

Build worked and ran in simulator
Tagged as v1.1 and committed


==================
https://github.com/weicht/one_sig/tree/v1.2

I added onesignal to pubspec.yaml.  When I try to run in simulator it fails with:

Launching lib/main.dart on iPhone XR in debug mode...
Starting Xcode build...
Xcode build done.                                            1.2s
Failed to build iOS app
Error output from Xcode build:
↳
    ** BUILD FAILED **


Xcode's output:
↳
    === BUILD TARGET onesignal OF PROJECT Pods WITH CONFIGURATION Debug ===
    In file included from /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/onesignal-1.0.5/ios/Classes/OneSignalCategories.m:28:
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/onesignal-1.0.5/ios/Classes/OneSignalCategories.h:28:9: fatal error: 'OneSignal/OneSignal.h' file not found
    #import <OneSignal/OneSignal.h>
            ^~~~~~~~~~~~~~~~~~~~~~~
    1 error generated.
    /Users/weicht/devel/flutter/.pub-cache/hosted/pub.dartlang.org/onesignal-1.0.5/ios/Classes/OneSignalTagsController.m:29:9: fatal error: 'OneSignal/OneSignal.h' file not found
    #import <OneSignal/OneSignal.h>
            ^~~~~~~~~~~~~~~~~~~~~~~
    1 error generated.

Could not build the application for the simulator.
Error launching application on iPhone XR.

Tagged as v1.2 and committed
