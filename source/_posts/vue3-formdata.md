---
title: 【Vue3】使用 multipart/form-data 提交数据
date: 2022-01-17 19:27:28
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Javascript
---

## 代码
```javascript
// Txt上传前
const beforeUploadTxt = (file) => {
	console.log('file', file);
	
	// 获取图片地址
	const reader = new FileReader();
	reader.readAsDataURL(file);
	reader.onload = e => {
	  // console.log('e.target', e.target)
	  file.path = e.target.result;
	  console.log('url', file.path)
	  txtFile.value = [file];
	};
	return false;
}

// Txt上传
const handleUploadTxt = () => {
	console.log('txt', txtFile.value[0]);
	
	if (!txtFile.value.length) {
	  message.warning('请先上传文件！');
	  console.log('Please upload first');
	  return;
	}
	
	// 使用formData格式传递参数
	let params = new FormData();
	params.append('txt', txtFile.value[0]);
	
	loading.value = true;
	
	try {
	  axios.post('/upload_txt', params).then((res) => {
	    message.success('请求成功！');
	    console.log(res)
	  })
	} catch (err) {
	  console.log(err);
	} finally {
	  loading.value = false;
	}
}
```
