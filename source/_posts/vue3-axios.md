---
title: 【Vue3】axios 封装
date: 2022-01-17 20:40:12
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- axios
- Javascript
---

首先，在项目 src 目录下新建一个 config 文件夹，并在该文件夹下新建一个 index.js：

```javascript
// index.js
export default {
  development: {
    baseUrl: 'http://xxx.xxx.xxx.xxx:xxxx' // 测试接口域名
  },
  beta: {
    baseUrl: 'http://xxx.xxx.xxx.xxx:xxxx' // 测试接口域名
  },
  release: {
    baseUrl: 'http://xxx.xxx.xxx.xxx:xxxx' // 正式接口域名
  },
  production: {
    baseUrl: 'http://xxx.xxx.xxx.xxx:xxxx'
  }
}
```
然后，在项目 src 目录下新建一个 utils 文件夹，并在该文件夹下新建一个 axios.js 与 request.js：

```javascript
// axios.js
import axios from 'axios'
import router from '../router/index'
import config from '../config'

// 这边由于后端没有区分测试和正式，姑且都写成一个接口。
axios.defaults.baseURL = config[import.meta.env.MODE].baseUrl
// 携带 cookie，对目前的项目没有什么作用，因为我们是 token 鉴权
axios.defaults.withCredentials = true
// 请求头，headers 信息
// axios.defaults.headers['X-Requested-With'] = 'XMLHttpRequest'
// axios.defaults.headers['token'] = localGet('token') || ''

// 默认 post 请求，使用 multipart/form-data 形式
axios.defaults.headers.post["Content-Type"] = "multipart/form-data;charset=UTF-8";

// 请求拦截器，内部根据返回值，重新组装，统一管理。
axios.interceptors.response.use(res => {
  if (typeof res !== 'object') {
    message.error('服务端异常！');
    console.log('服务端异常！');
    return Promise.reject(res)
  }
  if (res.status != 200) {
    if (res) {
      console.error(res.data)
    }
    return Promise.reject(res)
  }

  return res
})

export default axios
```

```javascript
import axios from 'axios'

// 创建axios
const service = axios.create({
  baseURL: 'http://xxx.xxx.xxx.xxx:xxxx'
});

//post请求头
service.defaults.headers.post["Content-Type"] = "multipart/form-data;charset=UTF-8";

// 添加请求拦截器
service.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  return config;
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error);
});

// 添加响应拦截器
service.interceptors.response.use(function (response) {
  // 对响应数据做点什么
  console.log('res',response);
  return response;
}, function (error) {
  // 对响应错误做点什么
  return Promise.reject(error);
});

export default service;
```
最后，在 vue 文件中引入 axios：

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
