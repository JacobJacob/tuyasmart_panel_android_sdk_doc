# Get the Panel Router Url

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