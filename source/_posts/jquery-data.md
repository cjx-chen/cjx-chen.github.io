---
title: 【Jquery】循环渲染并定义data取值
date: 2022-01-09 10:02:15
img: https://img.php.cn/upload/article/000/000/194/ffb4ed33d825a51cd2aa47468fe5219c.png
categories: 
- 前端
tags:
- Jquery
---

```javascript
var items = ''
for (let i = 0; i < res.data.length; i++) {
    items += `
      <div class="list">
        <div class="prize">${res.data[i].prize_name}</div>
        <div class="receive" data-url="${res.data[i].receiveUrl}" style="display: ${res.data[i].goods_type == 2?'block' : 'none'}">领取</div>
    </div>`
    console.log(res.data[i].goods_type)

}
$('.pop').html(items)
```