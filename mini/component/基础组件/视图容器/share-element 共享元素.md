# 简介
共享元素是一种动画形式，表现为元素像是在页面间穿越一样。使用时需在当前页放置 share-element 组件，同时在 [page-container](https://opendocs.alipay.com/mini/04ne6j) 容器中放置对应的 share-element 组件，对应关系通过属性值 name 映射。当设置 [page-container](https://opendocs.alipay.com/mini/04ne6j) 显示时，transform 属性为 true 的共享元素会产生动画。当前页面容器退出时，会产生返回动画。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 该组件需与[ page-container](https://opendocs.alipay.com/mini/04ne6j) 组件结合使用。

# 使用

## 示例代码

### index.axml
```html
<view>
	<view class="screen screen1">
		<block a:for="{{contacts}}" a:key="id" a:for-item="contact">
			<view class="contact" onTap="showNext" data-idx="{{index}}">
				<share-element duration="{{duration}}" class="name" name="name" transform="{{transformIdx === index}}">
					{{contact.name}}
				</share-element>
				<view class="list">
					<view>Phone: {{contact.phone}}</view>
					<view>Mobile: {{contact.mobile}}</view>
					<view>Email: {{contact.email}}</view>
				</view>
			</view>
		</block>
	</view>
</view>

<page-container
	show="{{show}}"
	overlay="{{overlay}}"
	close-on-slide-down
	duration="{{duration}}"
	position="{{position}}"
	onBeforeEnter="onBeforeEnter"
	onEnter="onEnter"
	onAfterEnter="onAfterEnter"
	onBeforeLeave="onBeforeLeave"
	onLeave="onLeave"
	onAfterLeave="onAfterLeave"
	onClickOverlay="onClickOverlay"
>
	<view class="screen screen2">
		<view class="contact">
			<share-element class="name" name="name" duration="{{duration}}" transform>
				{{contact.name}}
			</share-element>
			<view class="paragraph {{show ? 'enter' : ''}}">
				Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus nisl enim, sodales non augue efficitur, sagittis
				varius neque. Fusce dolor turpis, maximus eu volutpat quis, pellentesque et ligula. Ut vehicula metus in nibh
				mollis ornare. Etiam aliquam lacinia malesuada. Vestibulum dignissim mollis quam a tristique. Maecenas neque
				mauris, malesuada vitae magna eu, congue consectetur risus. Etiam vitae pulvinar ex. Maecenas suscipit mi ac
				imperdiet pretium. Aliquam velit mauris, euismod quis elementum sed, malesuada non dui. Nunc rutrum sagittis
				ligula in dapibus. Cras suscipit ut augue eget mollis. Donec auctor feugiat ipsum id viverra. Vestibulum eu nisi
				risus. Vestibulum eleifend dignissim.
				
			</view>
			<button class="screen2-button" onTap="showPrev" hidden="{{!show}}" hover-class="none">Click Me</button>
		</view>
	</view>
</page-container>
```

### index.js
```javascript
const contacts = [
  {
    id: 1,
    name: "Frank",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 2,
    name: "Susan",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 3,
    name: "Emma",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 4,
    name: "Scott",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 5,
    name: "Bob",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 6,
    name: "Olivia",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 7,
    name: "Anne",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
  {
    id: 8,
    name: "sunny",
    phone: "0101 123456",
    mobile: "0770 123456",
    email: "frank@emailionicsorter.com",
  },
];

Page({
  /**
   * 页面的初始数据
   */
  data: {
    contacts,
    contact: contacts[0],
    transformIdx: 0,
    position: "center",
    duration: 300,
    show: false,
    overlay: false,
  },

  showNext(e) {
    const idx = e.currentTarget.dataset.idx;
    this.setData({
      show: { _v: true },
      contact: contacts[idx],
      transformIdx: idx,
    });
  },

  showPrev() {
    this.setData({
      show: { _v: false },
    });
  },
  onBeforeEnter(res) {
    console.log(res);
  },
  onEnter(res) {
    console.log(res);
  },
  onAfterEnter(res) {
    console.log(res);
  },
  onBeforeLeave(res) {
    console.log(res);
  },
  onLeave(res) {
    console.log(res);
  },
  onAfterLeave(res) {
    console.log(res);
  },
});
```

### index.acss
```css
page {
  color: #333;
  background-color: #ddd;
  overflow: hidden;
}

button {
  border: 0 solid #0010ae;
  background-color: #1f2afe;
  color: #fff;
  font-size: 120%;
  padding: 8px 16px;
  outline-width: 0;
  -webkit-appearance: none;
  box-shadow: 0 8px 17px rgba(0, 0, 0, 0.2);
}

.screen {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 16px;
  -webkit-overflow-scrolling: touch;
}

.contact {
  position: relative;
  padding: 16px;
  background-color: #fff;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}

.name {
  height: 65px;
  font-size: 2em;
  font-weight: bold;
  text-align: center;
  margin: 10px 0;
}

.list {
  padding-top: 8px;
  padding-left: 32px;
}

.screen1 {
  overflow-y: scroll;
  padding: 0;
}

.screen1 .contact {
  margin: 16px;
  height: auto;
  width: auto;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.2);
}

.screen2-button {
  display: block;
  margin: 24px auto;
}

.paragraph {
  -webkit-transition: transform ease-in-out 300ms;
  transition: transform ease-in-out 300ms;
  -webkit-transform: scale(0.6);
  transform: scale(0.6);
}

.enter.paragraph {
  transform: none;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 映射标记。 |
| transform | Boolean | 是否进行动画。<br />**默认值：** false |
| duration | Number | 动画时长，单位毫秒。<br />**默认值：** 300 |
| easing-function | String | CSS 缓动函数。<br />**默认值：** ease-out |


