# Open Panel

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
