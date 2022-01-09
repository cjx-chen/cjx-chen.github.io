---
title: 【JavaScript】select 事件监听及选中
date: 2022-01-09 11:33:55
img: https://pic1.zhimg.com/v2-bde07fdceb700b45ea02f16e3bb099e7_1440w.jpg?source=172ae18b
categories: 
- 前端
tags:
- Html
- JavaScript
- Jquery
---

## 效果
![](https://img-blog.csdnimg.cn/d1b20756f414499d80645d25421e11eb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_16,color_FFFFFF,t_70,g_se,x_16)

## 代码
### Html

```html
<!-- 创建作品集 -->
<div class="create-block">
  <div class="create-mainbackground" style="min-width: 600px;">
    <div style="border-bottom: 1px solid #212529; border-radius: 5px;">
      <h3 style="margin-left: 5px;">创建作品集</h3>
    </div>
    <div class="row">
      <div class="col" style="text-align: center;">
        <label for="inputs">作品集标题：</label>
        <input type="text" id="workTitle" style="width: 500px;"></input>
        <br />
        <label for="textarea">作品集描述：</label>
        <textarea type="text" id="workDescription" class="description"></textarea>
        <br />
        <label for="inputState1">一级分类：</label>
        <select id="category1" style="width: 500px;" name="category" onchange="changeCate1(this)">
          <option selected value="-1">请选择作品集所属一级分类...</option>
        </select>
        <br />
        <label for="inputState2">二级分类：</label>
        <select id="category2" style="width: 500px;" name="category" onchange="changeCate2(this)">
          <option selected value="-1">请选择作品集所属二级分类...</option>
        </select>
        <div class="commit">
          <input type="button" class="btn btn-outline-light" id="commit" value="创建" onclick="createWork()">
        </div>
      </div>
    </div>
  </div>
</div>
```

### JavaScript
```javascript
/**
 * 创建作品集
 */
function createWork() {
  const userId = getUrlParam('usersId');
  const userName = getUrlParam('usersName');

  const workTitle = $("#workTitle").val();
  const workDescription = $("#workDescription").val();
  const category1 = $("#category1").val();
  const category2 = $("#category2").val();

  if (workTitle === "") {
    alert("作品集标题不能为空！");
  } else if (workDescription === "") {
    alert("作品集描述不能为空！");
  } else if (category1 === "-1") {
    alert("请选择一级分类！");
  } else if (category2 === "-1") {
    alert("请选择二级分类！");
  } else if (workTitle !== "" && workDescription !== "" && category1 !== "-1" && category2 !== "-1") {
    const params = {
      userId: userId,
      userName: userName,
      worksTitle: workTitle,
      worksDescription: workDescription,
      categoriesId: category2
    }
    $.ajax({
      type: 'post',
      url: 'http://localhost:8080/api/v1/createworks',
      dataType: "json",
      contentType: "application/json",
      data: JSON.stringify(params),
      async: true,
      success: function (res) {
        // console.log(res);
        if (res.resultCode === 200) {
          console.log('创建作品集成功！');
          Toast('创建作品集成功！');
          $("#workTitle").val("");
          $("#workDescription").val("");
          $("#category1").val("-1");
          $("#category2").val("-1");
          gotoHome();
        } else {
          console.log('创建作品集失败！');
          Toast(`创建作品集失败！${res.message}！`);
        }
      },
      error: function (XMLHttpRequest, textStatus, errorThrown) {
        alert(textStatus);
      }
    });
  }
}

/**
 * 下拉框获取一级分类
 */
function getPrimaryCateDraw() {
  $.ajax({
    type: 'get',
    url: "http://localhost:8080/api/v1/getPrimaryCategories",
    async: true,
    success: function (res) {
      console.log(res);
      const Datas = res.data;
      // console.log(Datas);

      let items = '';
      items += '<option selected value="-1">请选择作品集所属一级分类...</option>';
      for (let i = 0; i < Datas.length; i++) {
        items += `
          <option value="${Datas[i].categoriesId}">${Datas[i].categoriesName}</option>
        `;
      }
      $('#category1').html(items);
    }
  });
}

/**
 * 获取一级分类选中值
 * @param {*} that 
 */
function changeCate1(that) {
  console.log(that.value);
  const pid = that.value;

  if (pid !== -1) {
    getSecondaryCateDraw(pid);
  }
}

/**
 * 下拉框获取二级分类
 * @param {一级分类id} pid
 */
function getSecondaryCateDraw(pid) {
  const categoriesPid = pid;
  // const pos = i;
  // const cateNum = length;

  $.ajax({
    type: 'get',
    url: `http://localhost:8080/api/v1/getSecondaryCategories/${categoriesPid}`,
    async: true,
    success: function (res) {
      console.log(res);
      const Datas = res.data;
      // console.log(Datas);

      let items = '';
      items += '<option selected value="-1">请选择作品集所属二级分类...</option>';
      for (let i = 0; i < Datas.length; i++) {
        items += `
          <option value="${Datas[i].categoriesId}">${Datas[i].categoriesName}</option>
        `;
      }
      $('#category2').html(items);
    }
  });
}

/**
 * 获取二级分类选中值
 * @param {*} that 
 */
function changeCate2(that) {
  console.log(that.value);
  const id = that.value;
  return id;
}
```
