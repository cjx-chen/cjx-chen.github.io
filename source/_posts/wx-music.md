---
title: 【微信小程序】音乐播放器
date:   2021-08-31 12:14:26
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 场景

使用微信小程序实现一个简易的音乐播放器：[Github地址](https://github.com/beatzcs/audio_demo)

## 效果

![](https://img-blog.csdnimg.cn/721820db27dc4facbfc595dc8349ddb8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_9,color_FFFFFF,t_70,g_se,x_16)
虽然界面很简单,但是一个音频播放器该有的功能大部分都有了（没有歌词显示功能）。

主要实现的功能有：

1. 实现音频播放，暂停；
2. 实现拖拽进度条，快进音频进度；
3. 实现上一首，下一首，列表循环播放；
4. 实现关闭小程序，也可在后台播放，正式版需要通过审核，开发版本可正常测试；

## 代码

### index.js

#### 数据初始化

```javascript
  /**
   * 页面的初始数据
   */
  data: {
    playStatus: true,
    audioIndex: 0,
    progress: 0,
    duration: 0,
    audioList: [],
    showList: true
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function(options) {
    this.setData({
      audioList: data
    })
    this.playMusic();
  },
```

#### playMusic 切换播放歌曲的方法

```javascript
  playMusic: function() {
    let audio = this.data.audioList[this.data.audioIndex];
    let manager = wx.getBackgroundAudioManager();
    manager.title = audio.name || "音频标题";
    manager.epname = audio.epname || "专辑名称";
    manager.singer = audio.author || "歌手名";
    manager.coverImgUrl = audio.poster;
    // 设置了 src 之后会自动播放
    manager.src = audio.src;
    manager.currentTime = 0;
    let that = this;
    manager.onPlay(function() {
      console.log("======onPlay======");
      that.setData({
        playStatus: true
      })
      that.countTimeDown(that, manager);
    });
    manager.onPause(function() {
      that.setData({
        playStatus: false
      })
      console.log("======onPause======");
    });
    manager.onEnded(function() {
      console.log("======onEnded======");
      that.setData({
        playStatus: false
      })
      setTimeout(function() {
        that.nextMusic();
      }, 1500);
    });
  },
```

#### countTimeDown 循环计时，进度展示

```javascript
  //循环计时
  countTimeDown: function(that, manager, cancel) {
    if (that.data.playStatus) {
      setTimeout(function() {
        if (that.data.playStatus) {
          // console.log("duration: " + manager.duration);
          // console.log(manager.currentTime);
          that.setData({
            progress: Math.ceil(manager.currentTime),
            progressText: that.formatTime(Math.ceil(manager.currentTime)),
            duration: Math.ceil(manager.duration),
            durationText: that.formatTime(Math.ceil(manager.duration))
          })
          that.countTimeDown(that, manager);
        }
      }, 1000)
    }
  },
```

#### sliderChange slider的拖拽事件

```javascript
//拖动事件
  sliderChange: function(e) {
    let manager = wx.getBackgroundAudioManager();
    manager.pause();
    manager.seek(e.detail.value);
    this.setData({
      progressText: this.formatTime(e.detail.value)
    })
    setTimeout(function() {
      manager.play();
    }, 1000);
  },
```

#### lastMusic 上一首

```javascript
  //上一首
  lastMusic: function() {
    let audioIndex = this.data.audioIndex > 0 ? this.data.audioIndex - 1 : this.data.audioList.length - 1;
    this.setData({
      audioIndex: audioIndex,
      playStatus: false,
      progress: 0,
      progressText: "00:00",
      durationText: "00:00"
    })
    setTimeout(function() {
      this.playMusic();
    }.bind(this), 1000);
  },
```

#### playOrpause 中间的按钮,播放/暂停切换

```javascript
  //播放按钮
  playOrpause: function() {
    let manager = wx.getBackgroundAudioManager();
    if (this.data.playStatus) {
      manager.pause();
    } else {
      manager.play();
    }
  },
```

#### nextMusic 下一首

```javascript
  //下一首
  nextMusic: function() {
    let audioIndex = this.data.audioIndex < this.data.audioList.length - 1 ? this.data.audioIndex + 1 : 0;
    this.setData({
      audioIndex: audioIndex,
      playStatus: false,
      progress: 0,
      progressText: "00:00",
      durationText: "00:00"
    })
    setTimeout(function() {
      this.playMusic();
    }.bind(this), 1000);
  },
```

#### listClick 列表点击事件

```javascript
  //列表点击事件
  listClick: function(e) {
    let pos = e.currentTarget.dataset.pos;
    if (pos != this.data.audioIndex) {
      this.setData({
        audioIndex: pos,
        showList: false
      })
      this.playMusic();
    } else {
      this.setData({
        showList: false
      })
    }
  },
```

#### 界面切换，时长格式化

```javascript
  //界面切换  pageChange: function() {    this.setData({      showList: true    })  },  //格式化时长  formatTime: function(s) {    let t = '';    s = Math.floor(s);    if (s > -1) {      let min = Math.floor(s / 60) % 60;      let sec = s % 60;      if (min < 10) {        t += "0";      }      t += min + ":";      if (sec < 10) {        t += "0";      }      t += sec;    }    return t;  },
```

### index.wxml

```html
<!--index.wxml--><view class="container">  <view wx:if="{{showList}}" class="list">    <view wx:for="{{audioList}}" class='item {{audioIndex==index?"active":""}}' bindtap='listClick' data-pos='{{index}}'>      <view>{{item.name}}</view>      <text>{{item.author}}</text>    </view>  </view>  <view wx:else class='background'>    <view class='info'>      <view>{{audioList[audioIndex].name||""}}</view>      <view>{{audioList[audioIndex].author||""}}</view>    </view>    <image class='list' bindtap='pageChange' src='/images/list.png'></image>    <image class='poster {{playStatus?"rotate":"rotate-paused"}}' mode="scaleToFill" src='{{audioList[audioIndex].poster}}'></image>    <view class='progress'>      <text>{{progressText}}</text>      <slider class='bar' bindchange="sliderChange" bindchanging="sliderChanging" value="{{progress}}" step="1" min='0' max='{{duration}}' activeColor="#1aad19" block-size="12" block-color="#1aad19" />      <text>{{durationText}}</text>    </view>    <view class='buttons'>      <image class='button' bindtap='lastMusic' src='/images/last.png'></image>      <image class='button' bindtap='playOrpause' src='{{playStatus?"/images/pause.png":"/images/play.png"}}'></image>      <image class='button' bindtap='nextMusic' src='/images/next.png'></image>    </view>  </view></view>
```

### index.wxss

```css
/**index.wxss**/.item {  border: 1rpx solid #eee;  padding: 10rpx;  font-size: 11pt;}.active {  background: #a51515;  color: #fff;}.background {  position: fixed;  left: 0;  top: 0;  right: 0;  bottom: 0;  text-align: center;  background: #f5f5f5;}.background .info{  position: fixed;  top: 140rpx;  left: 0;  right: 0;  font-size: 12pt;  color: #353535;}.background .list {  position: fixed;  right: 40rpx;  top: 40rpx;  width: 60rpx;  height: 60rpx;}.background .poster {  width: 150rpx;  height: 150rpx;  border-radius: 50%;  margin-top: 400rpx;}.rotate {  animation: rotate 10s linear infinite;}.rotate-paused {  animation: rotate 10s linear infinite;  animation-play-state: paused;}@keyframes rotate {  0% {    transform: rotate(0deg);  }  50% {    transform: rotate(180deg);  }  100% {    transform: rotate(360deg);  }}.progress {  position: fixed;  bottom: 90rpx;  left: 50rpx;  right: 50rpx;  display: flex;  align-items: center;  font-size: 10pt;  color: rgb(87, 49, 49);  text-align: center;}.progress .bar {  flex: 1;}.progress text {  flex-basis: 90rpx;}.buttons {  position: fixed;  bottom: 20rpx;  left: 50rpx;  right: 50rpx;  display: flex;  justify-content: space-around;  align-items: center;}.buttons .button {  width: 70rpx;  height: 70rpx;}
```

## 其他

要实现关闭小程序后,依然后台播放,微信顶部悬浮展示,需要再 app.json 配置 `requiredBackgroundModes` 属性：
![](https://img-blog.csdnimg.cn/e614b3d5b8584735afde528d5a3a5696.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_10,color_FFFFFF,t_70,g_se,x_16)
附上官方相关 API 链接：
[BackgroundAudioManager.html](https://developers.weixin.qq.com/miniprogram/dev/api/media/background-audio/BackgroundAudioManager.html)
[wx.getBackgroundAudioManager()](https://developers.weixin.qq.com/miniprogram/dev/api/media/background-audio/wx.getBackgroundAudioManager.html)
[slider 组件](https://developers.weixin.qq.com/miniprogram/dev/component/slider.html)

---

转载自：[https://www.jianshu.com/p/e1d210a978a7](https://www.jianshu.com/p/e1d210a978a7)

