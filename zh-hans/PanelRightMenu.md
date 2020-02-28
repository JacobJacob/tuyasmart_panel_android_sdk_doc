# 点击面板右上角按钮

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
