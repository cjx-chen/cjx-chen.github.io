---
title: 【微信小程序】微信支付
date:  2021-09-16 13:31:32
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- API
---

## 简介
微信的支付方式有以下几种，不同的支付方式适用于不同的支付场景，而本文讲的就是 **小程序支付** 方式：
![](https://img-blog.csdnimg.cn/efe3056960574c2db71de174ff156728.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_18,color_FFFFFF,t_70,g_se,x_16)
说到支付功能就要涉及到金钱交易，必定是有比较严格的规范及流程，如要求小程序必须具备**企业**性质，必须拥有[微信支付商户平台](https://pay.weixin.qq.com/index.php/core/home/login?return_url=/)的账号；

> PS：申请微信支付商户平台需要一个微信小程序或公众号等，建议按照以下流程进行操作

## 准备工作
1. **申请微信小程序账号**
· 申请成功可拿到 `AppID`（小程序 id）和 `AppSecret`（小程序密钥）；
· 申请类型为企业性质，否则无法接入微信支付；
2. **微信小程序认证**
通过认证的小程序才能接入微信支付和绑定商户平台；
3. 申请商户平台账号
· 需要第一步申请的 `AppID`；
· 申请成功可拿到 `MchID`（商户 id）和 `MchKey`（商户密钥）；
4. **微信小程序关联商户号**
微信和商户都认证成功后，在微信后台`微信支付`菜单中进行关联；
5. **接入微信支付**
在微信后台`微信支付`菜单中进行接入；

## 小程序支付流程
简要支付流程如下：
1. 用户发起支付请求；
2. 后端调用统一下单接口得到 `prepay_id`；
3. 把支付所需参数返回前端；
4. 前端调用支付接口进行支付操作；
5. 支付结果通知；
6. 前端根据不同的支付结果给用户不同的提示；

> PS：难点在第 2、3、5 步，一定要仔细查看相关接口文档，否则容易出错，接下来我们按照以上 6 个步骤详细讲解在微信小程序中的支付流程

## 支付前的操作
因为严格意义上来说这不属于支付流程中的步骤，但支付过程中需要用到用户唯一标识 `openid`，所以建议在用户进入小程序时就进行这一步的操作：

1. 调用 `wx.login()` 接口获取 `code`，并把 `code` 传到服务器；
2. 后端服务器拿到 `code` 后调用 `code2Session` 接口获取 `openid` 和 `session_key`；
> 建议把openid存入数据库，方便随时获取，下面的步骤也会用到

3. 后端服务器保好 `appid`, `secret`, `mch_id`, `mch_key`（这些数据分别在小程序后台和商户平台中获得，我是把它们做成 commonjs 模块并保存在 `config/wx.js` 文件中以方便调用）；

> PS：开发者需要自行维护用户登录状态（用户登录状态的维护本文不做展开，请自行查阅相关资料）

## 小程序端：用户向商户服务器发起支付请求
这步没什么好说的，当用户点击支付按钮时，给我们自己的后端接口发起一个请求，携带必要的参数（如：`body`, `total_fee` 等），接口地址需要自行编写，如我的接口地址为 `https://api/prepay`

```javascript
  /**
   * 向后端发送打赏请求
   */
  gotoPay: function (event) {
    // console.log(event.currentTarget.dataset.index);
    const totalFee = this.data.nums[event.currentTarget.dataset.index];
    this.setData({
      totalFee: totalFee,
      toSelectNumShow: false,
      paidShow: true
    });
    wx.request({
      url: 'https://api/prepay',
      method: 'post',
      data: {
        body: '打赏', // 商品描述
        total_fee: totalFee // 总金额，单位为元
      },
      header: {
        'content-type': 'application/json'
      },
      success(res) {
        console.log(res);
        if (res.data.code === 1) {
          try {
            console.log(res.data.data);
            // 得到接口返回的数据，向微信发起支付
            const result = wx.requestPayment({
              // 5个必传参数
              timeStamp: res.data.data.timeStamp,
              nonceStr: res.data.data.nonceStr,
              package: res.data.data.packages,
              signType: res.data.data.signType,
              paySign: res.data.data.paySign
            });
            console.log('支付结果：', result);
          } catch (err) {
            console.log(err);
            wx.showToast({
              title: '支付失败'
            });
          }
        } else {
          console.log('支付请求失败！');
          console.log(res);
        }
      },
      fail(msg) {
        console.log(msg);
      }
    });
  },
```

> PS：可能会有小伙伴产生疑惑，为什么不直接通过 `wx.requestPayment()`
> 在小程序端发起请求而要先请求商户自己的服务器呢？原因很简单，安全性问题，`wx.requestPayment()` 需要 2 个重要参数 `paySign` 和 `package`，需要 `appid`, `secret`, `openid`, `mch_key` 等私密数据，这些私密的数据不应该在前端暴露出来，而是放在自己的服务器中更安全，所以需要向自己的服务器发起这个请求拿到这些参数，下一步才能真正发起支付。



---
## 参考文献
[微信支付之小程序支付](https://segmentfault.com/a/1190000022606064)
[微信支付之H5支付](https://www.cnblogs.com/zxk5211/p/14040310.html)

