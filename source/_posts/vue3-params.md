---
title: 【Vue3】Vue-Router4.x 实现路由跳转传参
date: 2022-01-14 16:17:55
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- router
---

## 传递参数

```javascript
<script>
  import {
    useRouter
  } from "vue-router";
  export default {
    setup() {
      const router = useRouter()
      const methods = {
        goMain() {
          router.push({
            path: "/main",
            query: {
              id: 123
            }
          })
        }
      }
      return {
        ...methods
      };
    },
  };
</script>
```

## 接收参数

```javascript
<script>
  import {
    onMounted
  } from "vue";
  import {
    useRoute
  } from "vue-router";
  export default {
    setup() {
      const route = useRoute()
      onMounted(() => {
        console.log(route.query.id)
      })
    }
  }
</script>
```
