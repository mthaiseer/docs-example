# Introduction
The **view container** component implements inserting a view block that can hold any other element in the applet interface, similar to the `<div>` element in HTML language.

## usage restrictions 

- The view component can be scrolled by using a fixed width or height, using overflow-x or overflow-y to set the scroll property, or making a scroll view through scroll-view
- The view component does not support covering the map component. It can be achieved through the same layer rendering cover-view to cover component.

### .axml sample code
```html
<!-- API-DEMO page/component/view.axml -->
<view class="page">
  <view>
    <button a:if="{{returnIndex}}" onTap="returnIndex">Back to homepage</button>
  </view>
  <view class="page-description">View container, equivalent to web div or react-native View. </view>
  <view class="page-section">
    <view class="page-section-demo">
      <view class="stream">
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Chris</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              Welcome to the Alipay applet! ! !
            </view>
            <view class="postBody__date">
              May 20
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Jack</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              @Chris How do I get started?
            </view>
            <view class="postBody__date">
              May 21
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Chris</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              You can view the Demo to have a simple understanding of the applet; then download our IDE for development.
            </view>
            <view class="postBody__date">
              May 22
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Jessie</view>
          </view>
          <!-- hover red -->
          <view class="postBody" hover-class="red">
            <view class="postBody__content">
              Thumbs up!
            </view>
            <view class="postBody__date" hidden>
              June 1
            </view>
          </view>
        </view>
        <view class="post" hidden>
          <view class="postUser">
            <view class="postUser__name">Jessie</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              Like! +1
            </view>
            <view class="postBody__date">
              June 1
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</view>
````

### .js sample code
````javascript
// API-DEMO page/component/view.js
Page({
  data: {
    pageName: 'component/view',
  },
  onLoad() {
    this.setData({
      returnIndex: getCurrentPages().length === 1,
    })
  },
  returnIndex() {
    my.switchTab({ url: '/page/component/index' });
  },
});
````

### .acss sample code
````css
/* API-DEMO page/component/view.acss */
.post + .post {
  margin-top: 10rpx;
}
.post {
  display: flex;
}
.postUser {
  flex: 0 1 auto;
  padding-bottom: 20rpx;
}
.postUser__name {
  width: 180rpx;
  color: #57727C;
  font-size: 24rpx;
  font-weight: 700;
  line-height: 1;
  text-align: center;
  margin-top: 60rpx;
}
.postBody {
  flex: 1 1 0%;
  position: relative;
  padding: 30rpx;
  border: 2rpx solid #CAD0D2;
  border-radius: 8rpx;
}
.postBody:after,
.postBody:before {
  right: 100%;
  top: 70rpx;
  border: solid transparent;
  content: " ";
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
}
.postBody:after {
  border-color: transparent;
  border-right-color: #ffffff;
  border-width: 16rpx;
  margin-top: -16rpx;
}
.postBody:before {
  border-color: transparent;
  border-right-color: #CAD0D2;
  border-width: 18rpx;
  margin-top: -18rpx;
}
.postBody__content {
  color: #57727C;
  font-size: 24rpx;
}
.postBody__date {
  margin-top: 10rpx;
  color: #86969C;
  font-size: 20rpx;
  text-transform: uppercase;
  letter-spacing: 2rpx;
}
````

## attribute description
| **Properties** | **Type** | **Description** |
| --- | --- | --- |
| disable-scroll | Boolean | Whether to prevent scrolling pages within the area. <br />**Default:** false<br />**Description:** If a view is nested within a view, the inner view will disable scrolling when `disable-scroll` is set to true in the outer view. |
| hover-class | String | The style class to add on touch. |
| hover-start-time | Number | How long to hold the click state, in milliseconds. |
| hover-stay-time | Number | Hold time of the click state after releasing, in milliseconds. |
| hidden | Boolean | Whether to hide. <br />**Default: **false |
| class | String | Custom style name. |
| style | String | Inline style. |
| animation | Object | For animation, see [my.createAnimation](api/ui-animation#mycreateanimation) for details. The animation generated by `my.createAnimation` is implemented by transition (Transition), which only triggers `onTransitionEnd`, not `onAnimationStart`, `onAnimationIteration`, `onAnimationEnd`. <br />**Default: **{} |
| hover-stop-propagation | Boolean | Whether to prevent the current element's ancestors from appearing click state. <br />**Default:** false<br />**Version Requirements:** Base Libraries [1.10.0](/mini/framework/compatibility) and above |
| onTap | EventHandle | Tap. |
| onTouchStart | EventHandle | The touch action starts. |
| onTouchMove | EventHandle | Move after touch. |
| onTouchEnd | EventHandle | Touch action ends. |
| onTouchCancel | EventHandle | Touch action is interrupted, such as incoming call reminder, pop-up window. |
| onLongTap | EventHandle | Triggered after a long press for 500ms, moving after the long press event is triggered will not trigger the scrolling of the screen. |
| onTransitionEnd | EventHandle | Fired when the transition ends. <br />**Version requirements:** Base library [1.8.0](/mini/framework/compatibility) and above |
| onAnimationIteration | EventHandle | Fired each time a new animation process is started. (Not triggered for the first time)<br />**Version requirements:** Base library [1.8.0](/mini/framework/compatibility) and above |
| onAnimationStart | EventHandle | Fired when the animation starts. <br />**Version requirements:** Base library [1.8.0](/mini/framework/compatibility) and above |
| onAnimationEnd | EventHandle | Fired when the animation ends. <br />**Version requirements:** Base library [1.8.0](/mini/framework/compatibility) and above |
| onAppear | EventHandle | Triggered when the visible area of ??????the current element exceeds 50%. <br />**Version requirements:** Base library [1.9.0](/mini/framework/compatibility) and above |
| onDisappear | EventHandle | Triggered when the invisible area of ??????the current element exceeds 50%. <br />**Version requirements:** Base library [1.9.0](/mini/framework/compatibility) and above |
| onFirstAppear | EventHandle | Fired when the first visible area of ??????the current element reaches 50%. <br />**Version requirements:** Base library [1.9.4](/mini/framework/compatibility) and above |
| role | - | Indicates the semantic role of the component. When set to img, the screen reader software will read **image** aloud after the component is focused; when set to button, the screen reader software will read aloud **button** after focusing. See [aria-component] for details