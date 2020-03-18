# 获取面板内路由地址
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