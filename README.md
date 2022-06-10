# issue3799
### GitHub link
- https://github.com/firebase/firebase-android-sdk/issues/3799
### Prerequisite
- Add google-services.json
### Steps to reproduce
- Open app and put to background
- Create a test campaign from Firebase Messaging Console and send to the app
- Click the notification and tap the notification to open app
- Check DebugView and see that `notification_receive` is received, but `notification_open` is not.
### Summary
- `notification_open` event is not reported in DebugView when opening notifications if `android:launchMode="singleTask"` is set in MainActivity. 

### Analysis
Setting `android:launchMode="singleTask"` will not allow new instances to be created when a new intent (e.g. notification) is received, rather it is redirected to the `onNewIntent()` method.
As a result, the `logNotificationOpen` method will not be invoked within the `onActivityCreated` method of the `FcmLifecycleCallbacks` class.
