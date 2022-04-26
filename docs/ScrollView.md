# Introduction
Scrollable view area. The scroll-view scroll bar can disable scrolling globally, but cannot disable scrolling distance display in scroll-view.

## usage restrictions

- When using vertical scrolling, you need to specify a fixed height, you can set `height` through acss.
- When scrolling the scroll-view, it will prevent the page from rebounding, so scrolling in the scroll-view cannot trigger the `onPullDownRefresh` pull-down refresh function.
- scroll-view does not support `scroll-x=true` and `scroll-y=true` to take effect at the same time, only one can be used. You can disable scrolling by setting `disable-scroll` to true using view.
- When the scroll-view is full, the page cannot be swiped, which will cause the navigation bar to slide transparently. You can set the navigation bar style through my.setNavigationBar navigation bar title, navigation bar background color, bottom border color of navigation bar, logo image in the upper left corner of navigation bar .
- The scroll-view component does not support custom pull-to-refresh.
- The scroll bar of the scroll-view component is hidden by default in Android and only displayed when sliding. It cannot be hidden in iOS.
- The scroll-view component does not support custom modification under iOS, but allows custom scrollbar style through `::-webkit-scrollbar` under Android.


## sample code

### .json sample code
````json
// API-DEMO page/component/scroll-view.json
{
  "defaultTitle": "Scroll View"
}
````

### .axml sample code <br />
```html
<!-- API-DEMO page/component/scroll-view.axml -->
<view class="page">
  <view class="page-description">scrollable view area</view>
  <view class="page-section">
    <view class="page-section-title">vertical scroll</view>
    <view class="page-section-demo">
      <scroll-view scroll-y="{{true}}" style="height: 200px;" onScrollToUpper="upper" onScrollToLower="lower" onScroll="scroll" scroll-into-view="{{toView}} " scroll-top="{{scrollTop}}">
        <view id="blue" class="scroll-view-item bc_blue"></view>
        <view id="red" class="scroll-view-item bc_red"></view>
        <view id="yellow" class="scroll-view-item bc_yellow"></view>
        <view id="green" class="scroll-view-item bc_green"></view>
      </scroll-view>
    </view>
    <view class="page-section-btns">
      <view onTap="tap">next</view>
      <view onTap="tapMove">move</view>
      <view onTap="scrollToTop">scrollToTop</view>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">horizontal scroll</view>
    <view class="page-section-demo">
      <scroll-view class="scroll-view_H" scroll-x="{{true}}" style="width: 100%" >
        <view id="blue2" class="scroll-view-item_H bc_blue"></view>
        <view id="red2" class="scroll-view-item_H bc_red"></view>
        <view id="yellow2" class="scroll-view-item_H bc_yellow"></view>
        <view id="green2" class="scroll-view-item_H bc_green"></view>
      </scroll-view>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">custom scrollbar (Andriod only)</view>
    <view class="page-section-demo">
      <scroll-view class="scroll-view-custom-scrollbar" scroll-y="{{true}}" style="height: 200px;">
        <view id="blue" class="scroll-view-item bc_blue"></view>
        <view id="red" class="scroll-view-item bc_red"></view>
        <view id="yellow" class="scroll-view-item bc_yellow"></view>
        <view id="green" class="scroll-view-item bc_green"></view>
      </scroll-view>
    </view>
  </view>
</view>
````

### .js sample code
````javascript
// API-DEMO page/component/scroll-view.js
const order = ['blue', 'red', 'green', 'yellow'];
Page({
  data: {
    toView: 'red',
    scrollTop: 100,
  },
  upper(e) {
    console.log(e);
  },
  lower(e) {
    console.log(e);
  },
  scroll(e) {
    this.setData({
      scrollTop: e.detail.scrollTop,
    });
  },
  scrollEnd() {
  },
  scrollToTop(e) {
    console.log(e);
    this.setData({
      scrollTop: 0,
    });
  },
  tap(e) {
    for (let i = 0; i < order.length; ++i) {
      if (order[i] === this.data.toView) {
        const next = (i + 1) % order.length;
        this.setData({
          toView: order[next],
          scrollTop: next * 200,
        });
        break;
      }
    }
  },
  tapMove() {
    this.setData({
      scrollTop: this.data.scrollTop + 10,
    });
  },
});
````

### .acss sample code
````css
/* API-DEMO page/component/swiper-view.acss */
.scroll-view_H {
  white-space: nowrap;
  display:flex;
}
.scroll-view-item {
  height: 200px;
}
.scroll-view-item_H {
  flex-shrink:0;
  flex-grow: 0;
  width: 300px;
  height: 200px;
}
/* The following code is only valid under Android */
.scroll-view-custom-scrollbar::-webkit-scrollbar {
  display: block;
  background-color: black;
  width: 10px;
}
.scroll-view-custom-scrollbar::-webkit-scrollbar-thumb {
  background-color: white;
}
````

## attribute description
| **Properties** | **Type** | **Description** |
| --- | --- | --- |
| class | String | External style name. |
| style | String | Inline style name. |
| scroll-x | Boolean | Allows horizontal scrolling. <br />**Default: **false |
| scroll-y | Boolean | Allow vertical scrolling. <br />**Default: **false |
| upper-threshold | Number | The distance from the top/left (in px) to trigger the `scrolltoupper` event. <br />**Default:** 50 |
| lower-threshold | Number | The distance from the bottom/right (in px) to trigger the `scrolltolower` event. <br />**Default:** 50 |
| scroll-top | Number | Set the vertical scroll bar position. |
| scroll-left | Number | Set the horizontal scroll bar position. |
| scroll-into-view| String | Scroll to the child element, the value should be the id of a child element. When scrolling to this element, the top of the element is aligned to the top of the scroll area. <br />**Note:** `scroll-into-view` takes precedence over `scroll-top`. |
| scroll-with-animation | Boolean | Use an animation transition when setting the scrollbar position. <br />**Default: **false |
| scroll-animation-duration | Number | When `scroll-with-animation` is set to true, `scroll-animation-duration` can be set to control the execution time of the animation, in ms. <br /> |
| enable-back-to-top | Boolean | When clicking on the iOS top status bar or double-clicking on the Android title bar, the scroll bar returns to the top, only vertical. <br />**Default:** false<br />|
| trap-scroll | Boolean | When scrolling vertically, when scrolling to the top or bottom, it is forbidden to trigger the page scroll, and still only trigger the scroll-view itself. <br />**Default:** false<br /> |
| onScrollToUpper | EventHandle | Scrolling to the top/left triggers the `scrolltoupper` event. |
| onScrollToLower | EventHandle | Scrolling to the bottom/right triggers the `scrolltolower` event. |
| onScroll | EventHandle | Fired when scrolling, ` event.detail = {scrollLeft, scrollTop, scrollHeight, scrollWidth}`. |
| onTouchStart | EventHandle | The touch action starts. |
| onTouchMove | EventHandle | Move after touch. <br /> |
| onTouchEnd | EventHandle | Touch action ends.  |
| onTouchCancel | EventHandle | The touch action is interrupted, such as incoming call reminder, pop-up window. <br /> |
| disable-lower-scroll | String | Before scrolling, determine the scroll direction. When the direction is top/left, if the value is `always`, scrolling will always be disabled. If the value is `out-of-bounds` and the current Already scrolled to the top/left, scrolling disabled. <br /> |
| disable-upper-scroll | String | Before scrolling, judge the scroll direction. When the direction is bottom/right, if the value is `always`, scrolling will always be disabled. If the value is `out-of-bounds` and the current Already scrolled to the bottom/right, scrolling disabled. <br /> |