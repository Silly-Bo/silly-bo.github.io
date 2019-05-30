---
title: DOM
date: 2019-05-28 20:56:26
categories: # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- web前端 # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- javascript # 可配置多个标签，注意格式
---
#### 一、DOM节点
##### 1.节点分类 
+ 元素节点： 每个Html元素
+ 属性节点： Html元素的属性
+ 文本节点： Html内的文本
+ 注释节点： 注释 `<!----->`
+ 文档节点： 整个文档document

##### 2.节点类型(nodeType)
+ 元素节点 1
+ 文本节点 3
+ 注释节点 8
+ 文档节点（document） 9
+ 文档声明 10

##### 3.节点名称(nodeName)
+ 元素节点：与标签名相同（大写）
+ 文本节点：为#text
+ 注释节点：为#comment
+ 文档节点：为#document
+ 文档声明：为html

#### 二、DOM关系
##### 1.父子之间
+ 查找子级
  + childNodes  获取子节点（包括所有节点：文本节点，元素节点，注释节点...）
  + children    获取子元素
  + firstChild  第一个子节点
  + firstElementChild 第一个子元素
  + lastChild   最后一个子节点
  + lastElementChild 最后一个子元素

```html
    <div id="div">
        <p>p1</p>
        <p>p2</p>
        <p>p3</p>
        <p>p4</p>
        <p>p5</p>
        <p>p6</p>
    </div>
```
```javascript  
    let div = document.querySelect('#div');
    console.log(div.childNodes) 
    /*这里获取的所有节点包括了换行的文本节点*/
    //NodeList(13) [text, p, text, p, text, p, text, p, text, p, text, p, text]

    console.log(div.children)
    //HTMLCollection(6) [p, p, p, p, p, p]

    //通过nodeType节点类型，也可以将childNodes所有的节点给过滤成类似children获取的所有的元素
    // 因为元素节点是 1 过滤时候做个判断就好
    let _div = div.childNodes
    _div = [..._div].filter(item=>{
        return item.nodeType == 1
    })
    console.log(_div)
    // (6) [p, p, p, p, p, p]

    //第一个子节点
    console.log(div.firstChild) //#text
    //第一个子元素
    console.log(div.firstElementChild); //<p>p1</p1>
    //最后一个子节点
    console.log(div.lastChild) //#text
    //最后一个子元素
    console.log(div.lastElementChild); //<p>p6</p1>
```
##### 2.兄弟之间
+ 查找兄弟
  + nextSibling 下一个兄弟节点
  + nextElementSibling 下一个兄弟元素
  + previousSibling 上一个兄弟节点
  + previousElementSibling 上一个兄弟元素
```javascript
    同上面的实例就不写了
```
##### 3.父子之间
+ 查找父级
  + parentNode  父节点
  + parentElement 父元素
  + offsetParent 定位父级（元素根据定位的父级，如果父级没有定位，那么找到的就是他的父级）

#### 三、NodeList 和 HTMLCollection 区别
##### NodeList
+ childNodes
+ querySelectorAll

##### HTMLCollection
+ children
+ getElementsByTagName
+ getElementsByClassName

区别：
1. NodeList有forEach方法，HTMLCollection没有forEach
2. HTMLCollection每次调用都会去动态获取内容，NodeList中，childNodes有动态更新，但是querySelectorAll不会动态更新

#### 四、DOM属性操作
setAttribute()      设置属性
getAttribute()      获取属性
removeAttribute()   移除属性

#### 五、自定义属性
```html
    <div id="box" class="mm" data-bobo="test"></div>
    <script>
        let div = document.querySelector('#box')
        console.log(div.dataset.bobo); //test  这里是获取自定义属性
         
        div.dataset.mytest="test2" //设置自定义属性
        console.log(div.dataset.mytest) //test2
    </script>
```
#### 六、offset 、client 和 scroll
##### 1. offset
```html
<style>
    #box{
        margin: 50px auto;
        position: relative;
        width: 500px;
        height: 500px;
        border: 1px solid #000;
    }
    #div{
        position: absolute;
        left: 150px;
        top: 150px;
        width: 100px;
        height: 100px;
        padding: 10px;
        /* margin: 10px; */
        border: 5px solid #ccc;
        background: red;
    }
</style>
<body>
    <div id="box">
        <div id="div"></div>
    </div>
    <script>
    // offset 可视的 可见的
        // offsetWith   可视宽度 + border + padding
        // offsetHeight 可视高度 + border + padding
        // offsetTop    当前元素相对于其 offsetParent 元素的顶部的距离  top + margin
        // offsetLeft   当前元素相对于其 offsetParent 元素的左侧的距离  left + margin
        let div = document.querySelector('#div');
        // console.log(div.offsetWidth);
        // console.log(div.offsetTop);
    </script>
</body>
</html>
```
##### 2. client
```html
<style>
    #box{
        margin: 50px auto;
        position: relative;
        width: 500px;
        height: 500px;
        border: 1px solid #000;
    }
    #div{
        position: absolute;
        left: 150px;
        top: 150px;
        width: 100px;
        height: 100px;
        padding: 10px;
        /* margin: 10px; */
        border: 5px solid #ccc;
        background: red;
    }
</style>
<body>
    <div id="box">
        <div id="div"></div>
    </div>
    <script>
    // client
        // clientWidth  元素本身 with + padding
        // clientHeight 元素本身 height + padding
        // clientTop    元素上边框的宽度 => border
        // clientLeft   元素左边框的宽度 => border
        // console.log(div.clientWidth,div.clientHeight); 
        console.log(div.clientTop,div.clientLeft); 
    </script>
</body>
</html>
```
##### 3. scroll
```html
<style>
    #box{
        margin: 50px auto;
        position: relative;
        width: 300px;
        height: 300px;
        border: 1px solid #000;
        overflow: auto;
       
    }
    #div{
        position: absolute;
        width: 100px;
        background: red;
    }
</style>
<body>
    <div id="box">
        <div id="div">
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
            你好你好你好你好你好你好你好你好你好你好你好你好你好你好你好
        </div>
    </div>
    <script>
        // scrollHeight 如果内容高度比元素自己高度高，则是内容高度，否则就是元素自身的高度
        // scrollWidth  如果内容宽度比元素自己宽度宽，则是内容宽度，否则就是元素自身的宽度，注意：需要减掉滚动条的宽度
        // scrollTop 元素上下滚动的高度 
        // scrollLeft 元素左右滚动的距离
        let box = document.querySelector('#box');
        // console.log(box.scrollHeight); //内容的高度 
        // console.log(box.scrollWidth); //内容的宽度 
        setTimeout(()=>{
            console.log(box.scrollTop)  //上下滚动的高度
        },2000)
    </script>
</body>
</html>
```
#### 七、 获取元素在可视区的绝对位置
```html
<style>
    *{
        margin: 0;
        padding: 0;
    }
    div{
        height: 100px;
        border: 1px solid #000;
    }
    #box{
        padding: 10px;
        background-color: red;
    }
</style>
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div id="box">5</div>
    <div>6</div>
    <div>7</div>
    
    <script>
        let div = document.querySelector('#box')
        div.onclick =()=>{
            console.log(div.getBoundingClientRect()) //获取到一个对象 DOMRect {x: 8, y: 64, width: 1333, height: 102, top: 64, …}
            // bottom: 166   元素底部，相对于可视区顶部的距离
            // height: 122   元素的可视高度，就是元素自身高度 + padding + border
            // left: 0       元素左侧距离可视区左边的距离       
            // right: 1349   元素右侧距离可视区右边的距离
            // top: 64       元素相对于可视区顶部的距离
            // width: 1349   元素可视区宽度
        }
    </script>
</body>
```
```html
<style>
    #box{
        position: relative;
        height: 300px;
        width: 300px;
        border: 1px solid #000;
        margin: 0 auto;
    }
    #div{
        position: absolute;
        top: 100px;
        left: 100px;
        height: 100px;
        width: 100px;
        background: red;
        border: 5px solid #000;
    }
</style>
<body>
    <div id="box">
        <div id="div"></div>
    </div>
    <script>
        /* 因为 getBoundingClientRect有兼容，
         下面自己简单封装一个到可视区的距离 */
        let div = document.querySelector('#div');
         console.log(getOffsetClient(div)) 
         function getOffsetClient(el){
            let left = el.offsetLeft;
            let top  = el.offsetTop;
            while(el.offsetParent){
                el = el.offsetParent;
                left += el.offsetLeft + el.clientLeft;
                top  += el.offsetTop + el.clientTop;
            }
            return {left,top}
        }
    </script>
</body>
```
#### 八、 表格的一些操作
```html
<body>
    <table border="1" id="table" width="300">
        <thead>
            <tr>
                <th>1</th>
                <th>2</th>
                <th>3</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </tbody>
    </table>
</body>
<script>
    let table = document.querySelector("#table")
    // table.tHead     获取的是 thead表头
    // table.tBodies   获取的是 tbody
    // rows 获取行（tr）
    // cells  获取单元格（ td 或者 th ）

    console.log(table.tHead) 
    console.log(table.tHead.rows[0].cells[0]) 
    console.log(table.tBodies) 
    console.log(table.tBodies[0].rows) 
    console.log(table.tBodies[0].rows[0].cells)
    console.log(table.tBodies[0].rows[0].cells[0])
</script>

```