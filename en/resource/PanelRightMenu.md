# Click Panel Toolbar Right Menu

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
