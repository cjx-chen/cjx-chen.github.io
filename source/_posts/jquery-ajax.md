---
title: 【Jquery】jQuery+ajax请求
date: 2022-01-09 10:45:44
img: https://img.php.cn/upload/article/000/000/194/ffb4ed33d825a51cd2aa47468fe5219c.png
categories: 
- 前端
tags:
- Jquery
---

## 普通 GET 请求

```javascript
/**
 * 获取首页作品集
 * @param {页码} n 
 */
function getWorks(n) {
  const usersId = getUrlParam('usersId');
  const usersName = getUrlParam('usersName');

  const pageNum = n !== null ? n : 1;
  const pageSize = 6;

  $.ajax({
    type: 'get',
    url: "http://localhost:8080/api/v1/getworks",
    data: {
      pageNum: pageNum,
      pageSize: pageSize
    },
    async: true,
    success: function (res) {
      console.log(res);
    });
}
```
## JSON 格式 POST 请求

```javascript
/**
 * 登录
 */
function login() {
  const username = $("#floatingUsername").val();
  const password = $("#floatingPassword").val();

  if (username === "") {
    alert("用户名不能为空！");
  } else if (password === "") {
    alert("密码不能为空！");
  } else if (username !== "" && password !== "") {
    const params = {
      usersName: username,
      usersPassword: password
    }
    $.ajax({
      type: 'post',
      url: 'http://localhost:8080/api/v1/uesr/login',
      dataType: "json",
      contentType: "application/json",
      data: JSON.stringify(params),
      async: true,
      success: function (res) {
        // console.log(res);
        if (res.resultCode === 200) {
          console.log('登录成功！');
          Toast('登录成功！');
        } else {
          console.log(`登录失败！${res.message}！`);
          Toast('登录失败！用户名或密码错误！')
        }
      },
      error: function (XMLHttpRequest, textStatus, errorThrown) {
        alert(textStatus);
      }
    });
  }
}
```
## FormData 格式 POST 请求

```javascript
/**
 * 多图上传
 */
 function uploadMultiImg() {
  // console.log('files', $('#fileId2')[0].files);

  const params = new FormData();
  const filesNum = $('#fileId2')[0].files.length;

  // console.log('files', files);
  
  const picturesDescription = $('#multiDescription').val();
  const worksId = $('.multiSelect').val();

  console.log('multiDescription', picturesDescription);
  console.log('worksId', worksId);

  if (filesNum <= 1) {
    alert('请选择不少于1张图片！');
  } else if (worksId == -1) {
    alert('请选择所属作品集！')
  } else {
    for(let i = 0; i < filesNum; i ++) {
      params.append('files', $('#fileId2')[0].files[i]);
    }
    params.append('picturesDescription', picturesDescription);
    params.append('worksId', worksId);

    $.ajax({
      type: 'post',
      url: 'http://localhost:8080/api/v1/upload/multiFiles',
      data: params,
      singleFileUploads: false,  // false表示支持批量上传
      processData: false,// 不处理数据
      contentType: false, // 不设置内容类型
      async: true,
      success: function (res) {
        console.log(res);
        if (res.resultCode === 200) {
          const Path = res.data;
          // console.log('多图上传成功！');
          Toast('多图上传成功！');
        } else {
          // console.log('多图上传失败！');
          Toast(`多图上传失败！${res.message}！`);
        }
      },
      error: function (XMLHttpRequest, textStatus, errorThrown) {
        alert(textStatus);
      }
    });
  }
}
```
