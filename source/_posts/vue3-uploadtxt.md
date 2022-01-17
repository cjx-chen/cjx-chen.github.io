---
title: 【Vue3】AntDesign 文件上传
date: 2022-01-17 19:27:28
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- AntDesign
- Javascript
---

## 效果
![](https://img-blog.csdnimg.cn/0f699cedb8f44783aef9b961ed32aa32.gif)

## 代码

```html
<template>
	<div class="upload-block">
      <!-- <div class="msgTitle">请上传以下格式的文档：</div>
      <div class="msgContent">.txt.</div> -->
      <div class="uploadBtn">
        <a-upload v-model:file-list="txtFile" name="txt" accept=".txt" :multiple="true"
          :before-upload="beforeUploadTxt" :headers="headers" :showUploadList="true" :withCredentials="true"
          :disabled="loading">
          <a-button v-if="txtFile.length < 1 && excelFile.length < 1" type="primary" class="selectFileBtn">
            <upload-outlined></upload-outlined>
            txt
          </a-button>
        </a-upload>
      </div>
    </div>
</template>
```

```javascript
<script>
  import { defineComponent, ref, onMounted, reactive, toRefs } from 'vue'
  import { message } from 'ant-design-vue';
  import { UploadOutlined } from '@ant-design/icons-vue';
  import axios from '../utils/axios'

  export default defineComponent({
    name: 'Index',
    components: {
      UploadOutlined
    },
    setup() {
      const tags = reactive({
        tag: '',
        pos: ''
      });

      const txtFile = ref([]);

      const loading = ref(false);

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

	  // 上传后
	  const txtChange = info => {
        if (info.file.status !== 'uploading') {
          // txtFile = info.file;
          console.log(info.file, info.txtFile);
        }

        if (info.file.status === 'done') {
          message.success(`${info.file.name} 文件上传成功！`);
        } else if (info.file.status === 'error') {
          message.error(`${info.file.name} 文件上传失败！`);
        }
      }
      
      return {
        loading,
        txtFile,
        headers: {
          'Content-Type': 'multipart/form-data'
        },
        txtChange,
        beforeUploadTxt,
        handleUploadTxt
      }
    }
  })
</script>
```

参考资料：[vue中的文件上传和下载](https://www.cnblogs.com/yuyujuan/p/10867557.html)