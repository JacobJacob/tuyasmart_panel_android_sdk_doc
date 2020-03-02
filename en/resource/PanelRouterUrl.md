# Get the Panel Router Url

Click some view to get the router url in the current panel to jump to other page

**Interface Description**

Click some view to get the router url

``` java
void setOpenUrlListener(ITuyaOpenUrlListener listener);
```
**Parameter Descrpition**

| Parameter                 | Description                     |
| -------------------- | ------------------------ |
| ITuyaOpenUrlListener | The router url |

**Sample Code**
``` java
TuyaPanelSDK.getPanelInstance().setOpenUrlListener(new ITuyaOpenUrlListener() {
    @Override
    public void handleOpenURLString(String urlString) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), urlString, Toast.LENGTH_SHORT).show();
    }
});
```