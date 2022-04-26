# Introduction
Slider view container. Among them, only swiper-item can be placed, otherwise it will lead to undefined behavior. The swiper height can be controlled by setting the height of the swiper item element. The height of the swiper-item depends on the height of the first swiper-item, and the width and height are automatically set to 100%.

## usage restrictions

- The swiper component cannot be used on the map. The map component is a native component created by the client. The level of the native component is the highest, so no matter what the z-index is set to, other components in the page cannot be placed among the native components. superior.
- The spacing between the first image and the left side of the swiper component can be consistent with the image spacing of the item in the component, and the front margin can be set according to `previous-margin`.
- Call the swiper component, the nested cover-view of swiper-item will cause a large blank after the last swiper-item, and swiper-item cannot add events, it is recommended to use [view](/mini/component/view) for embedding set.
- A swiper can have multiple swiper-items, but only one is displayed in the foreground.

## sample code

### .json sample code
````javascript
// API-DEMO page/component/swiper.json
{
  "defaultTitle": "Swiper",
  "pullRefresh": false,
  "allowsBounceVertical": false
}
````

### .axml sample code
```html
<!-- API-DEMO page/component/swiper.axml-->
<view class="page">
  <view class="page-description">slider view container</view>
  <view class="page-section">
    <view class="page-section-demo">
      <swiper
        class="demo-swiper"
        previousMargin="10px"
        nextMargin="10px"
        indicator-dots="{{indicatorDots}}"
        autoplay="{{autoplay}}"
        vertical="{{vertical}}"
        interval="{{interval}}"
        circular="{{circular}}"
      >
        <block a:for="{{background}}">
          <swiper-item key="swiper-item-{{index}}">
            <view class="swiper-item bc_{{item}}"></view>
          </swiper-item>
        </block>
      </swiper>
      <view class="margin-t">
        <slider onChange="intervalChange" value="{{interval}}" show-value min="500" max="2000"/>
        <view>interval</view>
      </view>
    </view>
    <view class="page-section-btns">
      <view onTap="changeIndicatorDots">indicator-dots</view>
      <view onTap="changeAutoplay">autoplay</view>
      <view onTap="changeVertical">vertical</view>
    </view>
    <view class="page-section-btns">
      <view onTap="changeCircular">circular</view>
    </view>
  </view>
</view>
````

### .js sample code
````javascript
// API-DEMO page/component/swiper.js
Page({
  data: {
    background: ['blue', 'red', 'yellow'],
    indicatorDots: true,
    autoplay: false,
    vertical: false,
    interval: 1000,
    circular: false,
  },
  onLoad() {
  },
  changeIndicatorDots(e) {
    this.setData({
      indicatorDots: !this.data.indicatorDots,
    });
  },
  changeVertical() {
    this.setData({
      vertical: !this.data.vertical,
    });
  },
  changeCircular(e) {
    this.setData({
      circular: !this.data.circular,
    });
  },
  changeAutoplay(e) {
    this.setData({
      autoplay: !this.data.autoplay,
    });
  },
  intervalChange(e) {
    this.setData({
      interval: e.detail.value,
    });
  },
});
````

### .acss sample code
````css
/* API-DEMO page/component/swiper.acss */
.swiper-item{
  display: block;
  height: 150px;
  margin:10px;
  background-color:#e0ffff;
}
.margin-t {
  margin-top: 24px;
}
````

## attribute description
| **Properties** | **Type** | **Description** |
| --- | --- | --- |
| indicator-dots | Boolean | Whether to display indicator-dots. <br />**Default: **false |
| indicator-color | Color | Indicator point color. <br />**Default:** rgba(0, 0, 0, .3) |
| indicator-active-color | Color | The color of the currently selected indicator point. <br />**Default:**#000 |
| active-class | String | The `class` when the `swiper-item` is visible. <br /> |
| changing-class | String | `class` when `acceleration` is set to `{{true}}` and in the process of sliding, and several screens in the middle are visible. <br /> |
| autoplay | Boolean | Whether to switch automatically. <br />**Default: **false |
| current | Number | The index of the current page, the left and right arrows can be added to control the scrolling of the carousel. <br />**Default:** 0 |
| duration | Number | Sliding animation duration. <br />**Default:** 500(ms) |
| interval | Number | Auto switch interval. <br />**Default:** 5000(ms) |
| circular | Boolean | Whether to enable infinite swipe. <br />**Default: **false |
| vertical | Boolean | Whether the sliding direction is vertical. <br />**Default: **false |
| previous-margin | String | The front margin, in px, 1.9.0 currently only supports horizontal direction. <br />**Default value:** 0px<br /> |
| next-margin | String | The back margin, in px, 1.9.0 currently only supports horizontal direction. <br />**Default value:** 0px<br /><br />**Description:** Removing the set distance of `next-margin` removes the left and right margins of the swiper component. |
| acceleration | Boolean | When enabled, it will continuously slide multiple screens according to the sliding speed. <br />**Default:** false<br /> |
| disable-programmatic-animation | Boolean | Whether to disable the use of animation when code changes trigger swiper switching. <br />**Default:** false<br /> |
| onChange | EventHandle | Triggered when current changes, `event.detail = {current, isChanging}`, where `isChanging` only has value when `acceleration` is set to `{{true}}`, when continuous sliding multi-screen , `isChanging` is `true` when several screens in the middle trigger the `onChange` event, and the last screen returns `false`. <br /> |
| onTransition | EventHandle | The transition event is fired when the position of the swiper-item in the swiper changes. <br />Where {dx,dy} = event.detail  |
| onAnimationEnd | EventHandle | The animationEnd event is fired when the animation ends, `event.detail = {current, source}`, where the values ​​of `source` are `autoplay` and `touch`. <br />|
| disable-touch | Boolean | Whether to disable user touch operation. <br />**Default value:** false<br />|
| swipe-ratio | Number | Swipe distance threshold, switch swiper-item when the swipe distance exceeds the threshold. <br />**Default value**: 0.2<br /> |
| swipe-speed | Number | The comprehensive sliding speed threshold. When the threshold is exceeded, the swiper-item is switched. The smaller the value, the more sensitive it is. <br />**Default value**: 0.05<br /> |
| touch-angle | Number | The sliding angle to rely on when calculating user gestures. The angle is calculated from the coordinates of the touchstart event and the first touchmove event. The smaller the value, the higher the requirement on the accuracy of the user's sliding direction. <br />**Default value**: 45<br /> |
| display-multiple-items | Number | The number of sliders to display at the same time. <br />**Default value**: 1<br /> |
| easing-function | String | Toggle easing animation type. <br />**Default value**: default<br /> |
| snap-to-edge | Boolean | When the number of swiper-item is greater than or equal to 2, when the circular is closed and the previous-margin or next-margin is enabled, you can specify whether this margin is applied to the first and last elements. <br />**Default value**: false<br />|
| adjust-height | String | Automatically use the height of the specified slider as the height of the entire container. When vertical is true, no adjustment is made by default. Optional values ​​are: <br /><ul><li>first: the first slider. </li><li>current: The current slider in real time. </li><li>highest: The slider with the highest height. </li><li>none: The height is not adjusted according to the slider, the height of the container depends on its own style. </li></ul> **default**: first<br />|
| adjust-vertical-height | Boolean | When vertical is true, force adjust-height to take effect. <br />**Default value**: false<br />| |