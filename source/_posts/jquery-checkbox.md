---
title: 【jQuery】获取 input checkbox 被选中的值
date: 2022-01-09 11:02:35
img: https://img.php.cn/upload/article/000/000/194/ffb4ed33d825a51cd2aa47468fe5219c.png
categories: 
- 前端
tags:
- Jquery
---

## 代码

```html
<html>
    <head>
        <meta charset="gbk">
        <!-- 引入JQuery -->
        <script src="jquery-1.3.1.js" type="text/javascript"></script>
    </head>
 
    <body>
        <input type="checkbox" value="橘子" name="check">橘子1</input>
        <input type="checkbox" value="香蕉" name="check">香蕉1</input>
        <input type="checkbox" value="西瓜" name="check">西瓜1</input>
        <input type="checkbox" value="芒果" name="check">芒果1</input>
        <input type="checkbox" value="葡萄" name="check">葡萄1</input>
        
        <input type="button" value="方法1" id="b1">
        <input type="button" value="方法2" id="b2">
    </body>
  
    <script>
        //方法1
        $("#b1").click(function(){
            //$('input:checkbox:checked') 等同于 $('input[type=checkbox]:checked')
            //意思是选择被选中的checkbox
            $.each($('input:checkbox:checked'),function(){
                window.alert("你选了："+
                    $('input[type=checkbox]:checked').length+"个，其中有："+$(this).val());
            });
        });
        
        //方法2
        $("#b2").click(function(){
            $.each($('input:checkbox'),function(){
                if(this.checked){
                    window.alert("你选了："+
                        $('input[type=checkbox]:checked').length+"个，其中有："+$(this).val());
                }
            });
        });
    </script>
</html>
```
