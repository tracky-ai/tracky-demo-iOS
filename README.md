# Tracky - iOS Integration Guide

## Integrating Tracky into Your iOS Application

### Step 1: Adding the AppsFlyer SDK
To incorporate the AppsFlyer SDK into your iOS app, you can add it as an SPM (Swift Package Manager) package dependency. Navigate to your project settings, access the 'Package Dependencies' tab, and add the AppsFlyer package to your target under `Package Dependencies`. For alternatives to SPM or for additional details, refer to the AppsFlyer [Install SDK guide](https://dev.appsflyer.com/hc/docs/install-ios-sdk).

### Step 2: Incorporating Tracky Code
Firstly, add the `Tracky.swift` file to your project, which is available in this example project.

For those utilizing the appDelegate, integrate the `start` method of the `Tracky` class instance within the `application:didFinishLaunchingWithOptions:` method as follows:
```swift
import UIKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
    
    // Existing AppDelegate variables
    
    let tracky = Tracky()
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Existing app initialization code
        
        tracky.start { message in
            #if DEBUG
            print(message)
            #endif
        }
    }    
}
```
Feel free to modify this code to suit your project's needs.

### Step 3: Updating AppsFlyer SDK Configuration 
Before usage, update the `appsFlyerDevKey`, `appleAppID`, and `appInviteOneLinkID` parameters of the `AppsFlyerLib.shared()` instance:
```swift
AppsFlyerLib.shared().appsFlyerDevKey = "<YOUR_DEV_KEY>"
AppsFlyerLib.shared().appleAppID = "<APPLE_APP_ID>"
AppsFlyerLib.shared().appInviteOneLinkID = "<ONE_LINK_ID>"
```
- Acquire `<YOUR_DEV_KEY>` from the AppsFlyer dashboard. Refer to [Adding an app to AppsFlyer](https://support.appsflyer.com/hc/en-us/articles/207377436-Adding-an-app-to-AppsFlyer) if needed.
- `<APPLE_APP_ID>` is your app's identifier in the AppStore.
- Obtain `<ONE_LINK_ID>` for your app. See [OneLink ID information](https://support.appsflyer.com/hc/en-us/articles/208874366-OneLink-links-and-experiences#create-a-onelink-link) for guidance.

Find more details in the [iOS SDK Integration guide](https://dev.appsflyer.com/hc/docs/integrate-ios-sdk).

### Step 4: Event Handling
- `StartTrial`: Trigger this event when a deepLink is received. `Tracky.swift` handles this automatically.
- `Purchase`: To track purchases, use the `trackPurchase(currency:value:)` method in `Tracky.swift`. Currency and value parameters are mandatory. Refer to `Tracky.swift` for additional event details.

## Testing Your Integration

### Facebook Configuration
You can check a guide of how to test Facebook test Ads in [this document](https://github.com/tracky-ai/tracky-demo-iOS/blob/main/Doc/Tracky.AI%20-%20Creating%20a%20test%20Facebook%20Ads%20link.pdf).

### Preparing Your Device
Follow the comprehensive guide on [Registering test devices](https://support.appsflyer.com/hc/en-us/articles/207031996) for device preparation.

We tested the AppsFlyer integration using the IDFV (Identifier for Vendor) method:
1. [Install the IDFV test tool app](https://dev.appsflyer.com/hc/docs/install-the-idfv-test-tool-app#how-to-install-the-idfv-testing-tool-app).
2. [Register your test device](https://support.appsflyer.com/hc/en-us/articles/207031996#add-a-device-manually-via-the-user-interface).

Keep the IDFV test tool app installed until all testing is complete. Note that Apple assigns a unique IDFV upon the installation of the first app from a vendor and removes it when the last app from that vendor is uninstalled. If you uninstall the test tool app, you might have to re-register your test device.

### Running Tests on Your Device
1. Uninstall your app from the device.
2. Navigate to `https://tracky.ai/preland?..` using a browser, using the link generated in previous steps.
3. On the preland page, click on the "Download on the AppStore" banner to be redirected to the OneLink landing page. If your app isn't available on the AppStore yet, a message stating "The app you are looking for is unavailable" will appear. This is expected.
4. Compile and launch the app on your device using Xcode.
5. Successful integration results in receiving deepLink data, including a `deepLinkValue` parameter. If using `Tracky.swift`, this value is handled automatically and can be accessed via the `Tracky.deepLinkValue` property.

### Event Reception Verification
[TODO]
