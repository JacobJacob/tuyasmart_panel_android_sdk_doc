## 打开面板

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

## 面板事件回调

### 点击面板右上角按钮

通过面板右上角按钮回调打开其他页面

**接口说明**

进入面板页面后点击右上角按钮可以获取当前面板设备 Id

``` java
void setPressedRightMenuListener(ITuyaPressedRightMenuListener listener);
```
**参数说明**

| 参数                          | 说明                            |
| ----------------------------- | ------------------------------- |
| ITuyaPressedRightMenuListener | 点击按钮回调获取当前面板设备 Id |
**示例代码**
``` java
TuyaPanelSDK.getPanelInstance().setPressedRightMenuListener(new ITuyaPressedRightMenuListener() {
    @Override
    public void onPressedRightMenu(String deviceId) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), "PanelMore", Toast.LENGTH_SHORT).show();
    }
});
```

### 获取面板内路由地址
获取面板内部路由地址跳转对应页面

**接口说明**

进入面板页面后点击跳转按钮获取路由地址

``` java
void setOpenUrlListener(ITuyaOpenUrlListener listener);
```
**参数说明**

| 参数                 | 说明                     |
| -------------------- | ------------------------ |
| ITuyaOpenUrlListener | 点击按钮回调获取路由地址 |

**示例代码**
``` java
TuyaPanelSDK.getPanelInstance().setOpenUrlListener(new ITuyaOpenUrlListener() {
    @Override
    public void handleOpenURLString(String urlString) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), urlString, Toast.LENGTH_SHORT).show();
    }
});
```
## 释放面板资源

在退出应用的时候调用释放资源

**示例代码**

``` java
TuyaPanel.getInstance().onDestroy();
```

## 清除所有面板缓存

面板文件会存放在当前 app 存储目录下，若需要清理可调用此方法

**示例代码**

``` java
TuyaPanelSDK.getPanelInstance().clearPanelCache();
```