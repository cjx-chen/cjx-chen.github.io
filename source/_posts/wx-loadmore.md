---
title: 【微信小程序】下拉刷新与上拉加载
date: 2021-09-23 16:51:38
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 效果
![方法一](https://img-blog.csdnimg.cn/06e35853ae6e4b4682b74724cd7b5ed9.gif)
![方法二](https://img-blog.csdnimg.cn/7c572f7efb684ed8a8483fd4f3741e15.gif)
## 方法
1. 在 `<scroll-view>` 里设定 `bindscrolltoupper` 和 `bindscrolltolower` 实现监听微信小程序下拉和下滑；

2. `onPullDownRefresh` 和 `onReachBottom` 方法实现小程序下拉加载和上拉刷新；
---

## 代码
### 方法一
#### index.wxml
```html
<!-- 顶部 关注 | 广场 标签栏 & 搜索框 -->
<view>
  <van-row class="roof">
    <van-col span="8">
      <view class="swiper-tab">
        <view class="bre swiper-tab-list {{currentTab==0 ? 'on' : ''}}" data-current="0" bindtap="swichNav">
          关注
        </view>
        <view class="swiper-tab-list {{currentTab==1 ? 'on' : ''}}" data-current="1" bindtap="swichNav">
          广场
        </view>
      </view>
    </van-col>
    <van-col span="16">
      <van-search placeholder="搜索您感兴趣的物品吧～" focus="false" disabled="true" shape="round" bindtap="gotoSearch"></van-search>
    </van-col>
  </van-row>
  <!-- 关注 | 广场 -->
  <swiper style="height: {{ clientHeight?clientHeight+'px':'auto' }}" current="{{ currentTab }}" class="swiper-box" duration="300" bindchange="bindChange">
    <swiper-item>
      <scroll-view scroll-y="true" class="scroll" style="height: {{ clientHeight?clientHeight+'px':'auto' }}" bindscrolltolower="getMoreArticle">
        <waterfall-focus list="{{ FocusArticle }}" scene="deshion"></waterfall-focus>
      </scroll-view>
    </swiper-item>
    <swiper-item>
      <scroll-view scroll-y="true" class="scroll" style="height: {{ clientHeight?clientHeight+'px':'auto' }};" bindscrolltolower="getMoreArticle">
        <waterfall-square results="{{ SquareArticle }}" scene="deshion"></waterfall-square>
      </scroll-view>
    </swiper-item>
  </swiper>
</view>
```

#### index.js
```javascript
// 获取本地缓存中的USERID
const USERID = wx.getStorageSync('USERID');

Page({

  /**
   * 页面的初始数据
   */
  data: {
    // 滑动导航栏当前页面索引
    currentTab: 0,
    SquareArticle: [],
    FocusArticle: [],
    onRefresh: false,
    focusPageNum: 1,
    focusPageSize: 2,
    squarePageNum: 1,
    squarePageSize: 4,
    userId: USERID
  },

  /**
   * tab切换功能(关注、广场)
   */
  // 滑动切换tab
  bindChange: function (e) {
    const that = this;
    that.setData({
      currentTab: e.detail.current
    });
    if (that.data.currentTab === 0) {
      // 获取关注文章列表
      that.getFocusArticle();
    } else if (that.data.currentTab === 1) {
      // 获取广场文章列表
      that.getSquareArticle();
    }
  },

  // 点击tab切换
  swichNav: function (e) {
    const that = this;
    if (that.data.currentTab === e.target.dataset.current) {
      return false;
    } else {
      that.setData({
        currentTab: e.target.dataset.current
      });
    }
    // console.log('currentTab', that.data.currentTab);
    if (that.data.currentTab === 0) {
      // 获取关注文章列表
      that.getFocusArticle();
    } else if (that.data.currentTab === 1) {
      // 获取广场文章列表
      that.getSquareArticle();
    }
  },

  /**
   * 进入搜索界面
   */
  gotoSearch: function () {
    // 当前要跳转到另一个界面，但是会保留现有界面
    wx.navigateTo({
      url: '../search-article/search-article'
    });
  },

  /**
   * 获取广场文章列表
   */
  getSquareArticle: function () {
    const that = this;
    const onRefresh = that.data.onRefresh; // false为重新刷新数据，true为分页累加数据
    if (onRefresh && that.data.currentTab === 1) {
      that.setData({
        squarePageNum: that.data.squarePageNum + 1
      });
    }
    // console.log('onRefresh', onRefresh);
    // console.log('currentTab', that.data.currentTab);
    // 发起网络请求
    wx.request({
      url: 'url',
      method: 'get',
      data: {
        page_num: that.data.squarePageNum,
        page_size: that.data.squarePageSize,
        user_id: that.data.userId
      },
      header: {
        'content-type': 'application/x-www-form-urlencoded'
      },
      success: (res) => {
        // console.log(res);
        if (res.data.code === 1) {
          // console.log('广场文章列表获取成功！', res.data.message);
          const squareDatas = res.data.data;
          // console.log('datas', squareDatas);
          if (onRefresh) {
            if (squareDatas.length === 0) {
              wx.showToast({
                title: '没有更多数据啦',
                icon: 'none'
              });
            } else {
              that.setData({
                SquareArticle: that.data.SquareArticle.concat(squareDatas)
              });
            }
          } else {
            that.setData({
              SquareArticle: squareDatas
            });
          }
        } else {
          console.log('广场文章列表获取失败！', res.data.message);
        }
      },
      complete: (msg) => {
        wx.hideLoading();
      },
      fail: (msg) => {
        wx.hideLoading();
        console.log(msg);
      }
    });
  },

  /**
   * 获取关注文章列表
   */
  getFocusArticle: function () {
    const that = this;
    const onRefresh = that.data.onRefresh; // false为重新刷新数据，true为分页累加数据
    if (onRefresh && that.data.currentTab === 0) {
      that.setData({
        focusPageNum: that.data.focusPageNum + 1
      });
    }
    // 发起网络请求
    wx.request({
      url: 'url',
      method: 'get',
      data: {
        page_num: that.data.focusPageNum,
        page_size: that.data.focusPageSize,
        user_id: that.data.userId
      },
      header: {
        'content-type': 'application/x-www-form-urlencoded'
      },
      success: (res) => {
        // console.log(res);
        if (res.data.code === 1) {
          // console.log('关注文章列表获取成功！', res.data.message);
          const focusDatas = res.data.data;
          if (onRefresh) {
            // console.log('length', focusDatas.length);
            if (focusDatas.length === 0) {
              wx.showToast({
                title: '没有更多数据啦',
                icon: 'none'
              });
            } else {
              that.setData({
                FocusArticle: that.data.FocusArticle.concat(focusDatas)
              });
            }
          } else {
            that.setData({
              FocusArticle: focusDatas
            });
          }
        } else {
          console.log('关注文章列表获取失败！', res.data.message);
        }
      },
      complete: (msg) => {
        wx.hideLoading();
      },
      fail: (msg) => {
        wx.hideLoading();
        console.log(msg);
      }
    });
  },

  /**
   * 获取更多文章列表
   */
  getMoreArticle: function () {
    // console.log('Bottom');
    wx.showLoading({
      title: '正在拼命加载 w(ﾟДﾟ)w'// 加载转圈显示
    });
    const that = this;
    that.setData({
      onRefresh: true // 累加数据
    });
    if (that.data.currentTab === 0) {
      // console.log('currentTab=0, getFocusArticle');
      // 获取关注文章列表
      that.getFocusArticle();
    } else if (that.data.currentTab === 1) {
      // console.log('currentTab=1, getSquareArticle');
      // 获取广场文章列表
      that.getSquareArticle();
    }
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    // 获取页面高度
    const that = this;
    wx.getSystemInfo({
      success: function (res) {
        that.setData({
          clientHeight: res.windowHeight
        });
      }
    });
    if (that.data.currentTab === 0) {
      // 获取关注文章列表
      that.getFocusArticle();
    } else if (that.data.currentTab === 1) {
      // 获取广场文章列表
      that.getSquareArticle();
    }
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {

  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {

  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {

  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {

  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {

  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {

  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {

  }
});
```


### 方法二
#### index.js
```javascript
// 获取本地缓存
const USERID = wx.getStorageSync('USERID');
const PROFILEURL = wx.getStorageSync('profileUrl');
const NICKNAME = wx.getStorageSync('nickname');
const POSTNUM = wx.getStorageSync('postNum');
const ISFOLLOWING = wx.getStorageSync('isFollowing');
const INTRODUCE = wx.getStorageSync('introduce');
const TAGLIST = wx.getStorageSync('tagList');

Page({

  /**
   * 页面的初始数据
   */
  data: {
    UserInfo: [{
      profileUrl: PROFILEURL,
      nickname: NICKNAME,
      postNum: POSTNUM,
      isFollowing: ISFOLLOWING,
      introduce: INTRODUCE,
      tagList: TAGLIST
    }],
    ArticleList: [],
    pageNum: 1,
    pageSize: 4,
    personalId: USERID,
    userId: USERID,
    onRefresh: false
  },

  /**
   * 分页获取文章列表
   */
  getArticleList: function () {
    const that = this;
    const onRefresh = that.data.onRefresh; // false为重新刷新数据，true为分页累加数据
    if (onRefresh) {
      that.setData({
        pageNum: that.data.pageNum + 1
      });
    }
    // 发起网络请求
    wx.request({
      url: `url/${USERID}`,
      method: 'get',
      data: {
        page_num: that.data.pageNum,
        page_size: that.data.pageSize,
        personal_id: that.data.personalId,
        user_id: that.data.userId
      },
      header: {
        'content-type': 'application/x-www-form-urlencoded'
      },
      success: (res) => {
        // console.log(res);
        if (res.data.code === 1) {
          // console.log('个人信息获取成功！', res.data.message);
          const ArticleDatas = res.data.data.articleList;
          // console.log(datas);
          if (onRefresh) {
            if (ArticleDatas.length === 0) {
              wx.showToast({
                title: '没有更多数据啦',
                icon: 'none'
              });
            } else {
              that.setData({
                ArticleList: this.data.ArticleList.concat(ArticleDatas)
              });
            }
          } else {
            that.setData({
              ArticleList: ArticleDatas
            });
          }
        } else {
          console.log('个人信息获取失败！', res.data.message);
        }
      },
      complete: (msg) => {
        wx.hideLoading();
      },
      fail: (msg) => {
        wx.hideLoading();
        console.log(msg);
      }
    });
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    this.getArticleList();
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {

  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {

  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {

  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {

  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {

  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {
    wx.showLoading({
      title: '正在拼命加载 w(ﾟДﾟ)w'// 加载转圈显示
    });
    const that = this;
    that.setData({
      onRefresh: true // 累加数据
    });
    that.getArticleList();
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {

  }
});
```
---

## 另一个项目代码
### 效果
![](https://img-blog.csdnimg.cn/8fb00676a4064837be9b9c049383e193.gif)
### index.wxml
```html
<scroll-view scroll-top="{{ scrollTop }}" scroll-y="true" style="height:{{ scrollHeight }}px; " class="list" bindscrolltolower="bindDownLoad" bindscrolltoupper="topLoad" bindscroll="scroll">
    <view class="article-block" wx:for="{{ ArticleList }}" wx:key="index" bindtap="gotoArticleDetail" data-articleid="{{ item.article_id }}">
      <view class="article-text">
        <view class="article-title">{{ item.title }}</view>
        <view class="article-time">{{ item.release_time }}</view>
      </view>
      <image class="article-image" src="{{ item.image }}"></image>
    </view>
    <view class="body-view">
     <loading hidden="{{hidden}}" bindchange="loadingChange">
       加载中...
     </loading>
   </view>
  </scroll-view>
```
### index.js
```javascript
const url = 'http://api/articlelist'
let page = 0
const pageSize = 5
const sort = 'last'
const isEasy = 0
const langeId = 0
const posId = 0
const unlearn = 0
// 请求数据
const loadMore = function(that) {
  that.setData({
    hidden: false
  })
  wx.request({
    url: url,
    data: {
      page: page,
      page_size: pageSize,
      sort: sort,
      is_easy: isEasy,
      lange_id: langeId,
      pos_id: posId,
      unlearn: unlearn
    },
    success: function(res) {
      // console.info(that.data.list);
      const list = that.data.ArticleList
      for (let i = 0; i < res.data.list.length; i++) {
        list.push(res.data.list[i])
      }
      that.setData({
        list: list
      })
      page++
      that.setData({
        hidden: true
      })
    }
  })
}

Page({
  /**
   * 页面的初始数据
   */
  data: {
    hidden: true,
    scrollTop: 0,
    scrollHeight: 0,
    ArticleList: [
      {
        article_id: 1,
        title: 'This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 1
      },
      {
        article_id: 2,
        title: 'This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 2
      },
      {
        article_id: 3,
        title: 'This is Title This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 3
      },
      {
        article_id: 4,
        title: 'This is Title This is Title This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 4
      }
    ],
    value: '',
    offset: 0
  },
  
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    const that = this
    wx.getSystemInfo({
      success: function (res) {
        that.setData({
          scrollHeight: res.windowHeight * 3 / 5
        })
      }
    })
    that.getSayings()
    that.getArticleList()
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {

  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {

  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {

  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {

  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {

  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {

  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {

  },
  
  /**
   * 页面滑动到底部
   */
  bindDownLoad: function () {
    const that = this
    loadMore(that)
    console.log('lower')
  },

  /**
   * 页面滚动
   * @param {*} event
   */
  scroll: function (event) {
    // 该方法绑定了页面滚动时的事件，这里记录了当前的position.y的值,为了请求数据之后把页面定位到这里来。
    this.setData({
      scrollTop: event.detail.scrollTop
    })
  },

  /**
   * 上拉刷新
   * @param {*} event
   */
  topLoad: function(event) {
    //  该方法绑定了页面滑动到顶部的事件，然后做上拉刷新
    page = 0
    this.setData({
      ArticleList: [
        {
          article_id: 1,
          title: 'This is Title',
          release_time: '2020-03-12 09:42:19',
          image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
          text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
          teacher_id: 1
        }
      ],
      scrollTop: 0
    })
    loadMore(this)
    console.log('lower')
  }
 })
```
### index.css

```css
/* 每日文章 */
.article-block{
  display: flex;
  height: 220rpx;
  width: 350rpx;
  margin: 0 50rpx 0 50rpx;
  padding: 20rpx 0 20rpx 0;
  border-top: 1px solid rgba(222, 222, 222, 0.5);
}

.article-text{
  position: absolute;
  flex: 1;
  height: 220rpx;
  width: 350rpx;
}

.article-title{
  position: absolute;
  top: 10rpx;
  font-size: 28rpx;
  padding-bottom: 10rpx;
}

.article-time{
  position: absolute;
  bottom: 0rpx;
  font-size: 22rpx;
  color: darkgrey;
  padding-bottom: 10rpx;
}

.article-image{
  position: absolute;
  right: 30rpx;
  width: 300rpx;
  height: 220rpx;
}
```

### 拓展
这里简单讲述一下另一种方法：
1. 首先要在 json 文件里设置 `window` 属性；
2. 设置 js 里 `onPullDownRefresh` 和 `onReachBottom` 方法；

下拉加载说明：
当处理完数据刷新后，`wx.stopPullDownRefresh` 可以停止当前页面的下拉刷新。

#### 代码
```javascript
onPullDownRefresh(){
　　console.log('--------下拉刷新-------')
　　wx.showNavigationBarLoading() //在标题栏中显示加载
　　wx.request({
     url: 'https://URL',
     data: {},
     method: 'GET',
     // OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT
     // header: {}, // 设置请求的 header
     success: function(res){
      // success
     },
     fail: function() {
      // fail
     },
     complete: function() {
      // complete
      wx.hideNavigationBarLoading() //完成停止加载
      wx.stopPullDownRefresh() //停止下拉刷新
   }
})
```
