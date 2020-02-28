# 打开面板

通过家庭 Id 和设备 Id 进入对应设备面板页面，家庭和设备的 Id 需要通过公版 SDK 接口获取

**接口说明**

打开设备面板

``` java
gotoPanelViewControllerWithDevice(Activity activity, long homeId, String devId, ITuyaPanelLoadCallback loadCallback);
```
**参数说明**

| 参数         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| activity     | 在面板内打开新面板时应使用 TuyaPanelSDK.getCurrentActivity() |
| homeId       | 家庭 Id 通过公版 SDK 接口获取                                |
| devId        | 设备Id 通过公版 SDK 接口获取                                |
| loadCallback | 面板加载回调                                                |

**示例代码**
``` java
// 加载状态回调里界面操作的 Context 应使用 TuyaPanelSDK.getCurrentActivity()
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
    
//打开面板
TuyaPanelSDK.getPanelInstance().gotoPanelViewControllerWithDevice(TuyaPanelSDK.getCurrentActivity(), mCurrentHomeId, bean.getDevId(), mLoadCallback);
```
