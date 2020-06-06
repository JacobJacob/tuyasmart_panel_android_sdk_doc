## Open panel

Enter the panel page through the homeId and deviceId.The homeId and deviceId need to be obtained through the public Tuya Smart SDK interface.

**Declaration**

Open Panel

``` java
gotoPanelViewControllerWithDevice(Activity activity, long homeId, String deviceId, ITuyaPanelLoadCallback loadCallback);
```
**Parameter**

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| activity     | Open the panel context must to be used TuyaPanelSDK.getCurrentActivity() |
| homeId       | The homeId need to be obtained through the public Tuya Smart Android SDK interface                              |
| deviceId        | The deviceId need to be obtained through the public Tuya Smart Android SDK interface.                                |
| loadCallback | Status Callback when the panel loads                                                |

**Example**
``` java
final ITuyaPanelLoadCallback mLoadCallback = new ITuyaPanelLoadCallback() {
    @Override
    public void onStart(String deviceId) {
        ProgressUtil.showLoading(TuyaPanelSDK.getCurrentActivity(), "Loading...");
    }
    
    @Override
    public void onError(String deviceId, int code, String error) {
        ProgressUtil.hideLoading();
        Toast.makeText(getApplicationContext(), "errorCode:" + code + ",errorString:" + error, Toast.LENGTH_LONG).show();
    }
    
    @Override
    public void onSuccess(String deviceId) {
        ProgressUtil.hideLoading();
    }
    
    @Override
    public void onProgress(String deviceId, int progress) {
    }
};
    
TuyaPanelSDK.getPanelInstance().gotoPanelViewControllerWithDevice(TuyaPanelSDK.getCurrentActivity(), mCurrentHomeId, bean.getDevId(), mLoadCallback);
```
## Click panle toolbar right menu

Open other pages through the callback on the toolbar right menu of the panel

**Declaration**

Click the toolbar right menu get the current panel deviceId

``` java
void setPressedRightMenuListener(ITuyaPressedRightMenuListener listener);
```
**Parameter**

| Parameter                          | Description                            |
| ----------------------------- | ------------------------------- |
| ITuyaPressedRightMenuListener | the deviceId  |
**Example**
``` java
TuyaPanelSDK.getPanelInstance().setPressedRightMenuListener(new ITuyaPressedRightMenuListener() {
    @Override
    public void onPressedRightMenu(String deviceId) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), "PanelMore", Toast.LENGTH_SHORT).show();
    }
});
```

## Get panle router url

Click some view to get the router url in the current panel to jump to other pages

**Declaration**

Click some view to get the router url

``` java
void setOpenUrlListener(ITuyaOpenUrlListener listener);
```
**Parameter**

| Parameter                 | Description                     |
| -------------------- | ------------------------ |
| ITuyaOpenUrlListener | The router url |

**Example**
``` java
TuyaPanelSDK.getPanelInstance().setOpenUrlListener(new ITuyaOpenUrlListener() {
    @Override
    public void handleOpenURLString(String urlString) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), urlString, Toast.LENGTH_SHORT).show();
    }
});
```

## Release panle resource

Call this method to release resources when exiting the application

**Example**

``` java
TuyaPanel.getInstance().onDestroy();
```

## Clear panel cache

The panel resources files will be stored in the current app storage directory. you can call this method to clean up.

**Example**

``` java
TuyaPanelSDK.getPanelInstance().clearPanelCache();
```
