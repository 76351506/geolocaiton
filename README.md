# Navigator - geolocaiton

## 概念
Geolocation 接口是一个用来获取设备地理位置的可编程的对象，它可以让Web内容访问到设备的地理位置，这将允许Web应用基于用户的地理位置提供定制的信息。说实话：其实Geolocation 就是用来获取到当前设备的经纬度（位置）
## 方法
navigator.geolocaiton.getCurrentPosition()
navigator.geolocaiton.watchPostition()
navigator.geolocaiton.clearWatch()

## 获取地址坐标
```js
/*
 * @Author: heinan
 * @Date: 2021-09-18 09:37:31
 * @Last Modified by: heinan
 * @Last Modified time: 2021-09-18 09:57:46
 */
window.geoLocation = (() => {
  class Location {
    constructor() {
      this.geolocation = null;
      this.init();
    }
    init() {
      if (navigator.geolocation) {
        this.geolocation = window.navigator.geolocation;
        this.getCurrentLocation();
      }
    }
    handlerSuccess(position) {
      console.log(position.coords.latitude, position.coords.longitude);
    }
    handlerFaild({ code }) {
      let msg = "";
      switch (code) {
        case 1:
          msg = "用户拒绝了位置服务";
          alert(msg);
          break;

        case 2:
          msg = "获取不到位置信息";
          alert(msg);
          break;

        case 3:
          msg = "获取信息超时";
          alert(msg);
          break;
      }
      return new Error(msg);
    }
    getCurrentLocation() {
      this.geolocation.getCurrentPosition(
        this.handlerSuccess,
        this.handlerSuccess
      );
    }
  }
  return new Location();
})();
console.log(geoLocation);
```
