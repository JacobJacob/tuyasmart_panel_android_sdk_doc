# Click Panel Toolbar Right Menu

Open other pages through the callback on the toolbar right menu of the panel

**Interface Descprition**

Click the toolbar right menu get the current panel device Id

``` java
void setPressedRightMenuListener(ITuyaPressedRightMenuListener listener);
```
**Parameter Description**

| Parameter                          | Description                            |
| ----------------------------- | ------------------------------- |
| ITuyaPressedRightMenuListener | the deviceId  |
**Sample Code**
``` java
TuyaPanelSDK.getPanelInstance().setPressedRightMenuListener(new ITuyaPressedRightMenuListener() {
    @Override
    public void onPressedRightMenu(String deviceId) {
        Toast.makeText(TuyaPanelSDK.getCurrentActivity(), "PanelMore", Toast.LENGTH_SHORT).show();
    }
});
```
