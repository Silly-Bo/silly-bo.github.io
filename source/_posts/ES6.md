---
title: ES6
date: 2019-06-14 14:44:31
categories:
- web前端
tags:
- ES6
---
#### let和const
let 和 var 都是声明变量，但是区别还是有很多的，先看一个小示例
```javascript
    //重复声明
    let a = 10;
    let a = 20;
    console.log(a)// Uncaught SyntaxError: Identifier 'a' has already been declared

    //作用域下
    if(true){
        let a = 10;
    }
    console.log(a)  // a is not defined

    if(true){
        var a = 10;
    }
    console.log(a)  // 10

    //预解析
    console.log(a) // undefined
    var a = 10; 

    console.log(a) // Cannot access 'a' before initialization(初始化之前无法访问a)
    let a = 10; 
```
var：
1. 可以重复声明变量
2. 全局作用域 和 函数作用域
3. 会进行预解析

let:
1. 在同一作用域下不能重复声明变量
2. 全局作用域 和 块级作用域 {}
3. 没有预解析
    
const:
1. 声明的时候必须赋值，一但赋值后面就不能修改了
2. 没有预解析

#### 块级作用域

```html
    <ul id="ul">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
<script>
    let ul = document.querySelectorAll("#ul li")
    for(let i=0; i<ul.length; i++){
        ul[i].onclick = function(){
            console.log(i) // 0 1 2
        }
    }
    console.log(i) // i is not defined

    for(var i=0; i<ul.length; i++){
        ul[i].onclick = function(){
            console.log(i) // 3 3 3
        }
    }
    console.log(i) // 4

// 这里for循环可以看成下面的分解，for循环几次就相当于开辟了几个代码块，所以不会出现3 3 3情况
        {
            i = 0;
            ul[i].onclick = function(){
                console.log(i)
            }
        }

        {
            i = 1;
            ul[i].onclick = function(){
                console.log(i)
            }
        }

        {
            i = 2;
            ul[i].onclick = function(){
                console.log(i)
            }
        }
</script>
```

#### 解构赋值

```javascript  
// 1.对象的结构赋值
    let obj = {
        a: 1,
        b: 2
    }
    // es5写法
    // let a = obj.a;
    // let b = obj.b;

    // es6写法
    let {a,b} = obj  //需要注意的是，这里的前面的a,b要对应的obj里面的key一样
    console.log(a,b) // 1 2

// 2.数组的结构赋值
    let Arr = ["a","b","c"]
    let [x,y,c] = Arr
    console.log(x,y,c)  //a b c
    // 注意： 这里的x对应的是Arr数组下标的0项，y对应的是1，从对应的下标是2
    /*
    一个例子：
    let a = 10 
    let b = 20

    要求：交换 a b的值

    原来的方法: 
    let c = a
        a = b
        b = c

    通过结构赋值方法：
    let [b,a] = [a,b]
    */
// 3.字符串的结构赋值
    let str = "yubo"
    let [a,b] = str  //注意的是字符串的结构，跟数组一样前面用的是[X,X]
    console.log(a,b) //y u

```

#### 展开运算符

展开运算符语法···（三个点）

```javascript
// 数组的展开运算符
    // 基本用法
    let arr =['a','b'];
    let arr2 = [1,2,3,...arr,4,5];
    console.log(arr2)
    // 剩余参数
    let arr = [1,2,3,4,5,6]
    let [a,b,...c]= arr; 
    //这里...c会将arr中剩余的值都放在一个数组中
    console.log(a,b,c)// 1 2 [3, 4, 5, 6]

// 对象的展开运算符
    let obj = {
        a: 'a',
        b: 'b'
    }
    let obj2 = {
        ...obj,
        c: 1,
        d: 2
    }
    let {a,b,...c} = obj2
    //这里...c会将obj2中剩余的值都放在一个对象中
    console.log(a,b,c) // a b {c: 1, d: 2}

```

#### Set

```javascript   

// Set是构造函数，用来构建某一类型的对象，这里通过一个数组去重，来看下Set的用法：
    let arr  = [2,1,2,3,4,1,7,5]
    let set = new Set(arr)  // 数组去重但是数组去重后变成对象 {2, 1, 3, 4, 7,5}
    arr = [...set]    // 通过展开运算符，在赋值给数组
    console.log(arr) //[2, 1, 3, 4, 7, 5]

    /* 
    1.size属性:
        console.log(set.size)   6  数值的个数，相当于length
    
    2.set方法：
        set.clear();   清空所有值

        set.delete(val)  删除某一项
        参数：
            val  要删除的值
        返回值：
            true || false  是否删除成功（没有正值才会删除不成功)
        
        set.has(val) 是否包含某项
        参数：
            val 要查找的值
        返回值：
            true || false 是否包含这个值

        set.add(val) 添加某一项
        参数：
            val 要添加的值
        返回值：
            set对象本身（可以进行链式操作set.add(X).add(X).add(X)）
    */


```

#### Map

```javascript
    let arr = [
        ["a",1],
        ["b",2],
        ["c",3],
    ]
    let map = new Map(arr) 
    console.log(map) // {"a" => 1, "b" => 2, "c" => 3}

    /*
    1.属性
        map.size  //数值的个数
        console.log(map.size) // 3
    2.方法
        map.clear() 清空所有值

        map.delete(key) 删除某一项
        参数：
            key 要删除的值
        返回值：
            true || false 是否删除成功(如果没有这个值，才会出现删除不成功)
        
        map.get(key) 获取某一项的值
        参数：
            key 数据的key值 
        返回值：
            获取的key对应的value值
        
        map.has(key) 是否包含某项
        参数：
            key 要查找的值
        返回值：
            true || false 是否包含这个值

        map.set(key,value) 设置某个值
        参数：
            key   数据的key值
            value 数据的value值
        返回值：
            返回map对象本身（可以是链式操作）
    */
```

#### 函数新增内容

```javascript
// 箭头函数
/*
    形参=>返回值

    (形参，形参) => 返回值

    () => 返回值

    () => {
        执行语句
    }

    (形参,形参)=>{
        执行语句
    }
*/
// rest参数
    // 之前函数不定参取值的时候我们可以用arguments来获取
    let fun = function(){
        console.log(arguments) //[1, 2, 3, 4]
    }
    //  现在用了箭头函数，就会发现，箭头函数没有anguments,那么怎么获取不定参数呢，可以用rest参数
    let fun = (...arg)=>{
        console.log(arg)
    }
    fun(1,2,3,4)
// 箭头函数 this指向
let fn;
let fn2 = function(){
    console.log(this)
    fn= ()=>{
        console.log(this)
    }
}
这个时候下面调用的函数打印的this指向的都是window
fn2()
fn()

下面进行改写后，在看看this指向，改写将fn2下的this指向到了document.body,
而fn箭头函数在fn2的作用域下，所以fn的this也是指向body
fn2 = fn2.bind(document.body)
fn2()
fn()
/*
  总结：箭头函数本身没有this,调用箭头函数的this时，指向是其声明时所在的作用域的this
*/

//箭头函数的默认值
let fn = (a=2,b=3)=>{
    console.log(a,b)
}
fn(1,2)  // 1 2
fn()     // 2 3

```

#### 函数新增方法

```javascript
Array.from(类数组)  把一个类数组转换成真正的数组
返回值：
    转换之后新的数组

也可以对类数组进行操作，然后返回出符合条件的
Array.from(类数组,(item,index){
    return 设置的条件
})

把一个类数组转换成数组两种方法也可以用展开运算符
[...类数组]

Array.of()  //将传入的值，成数组返回
console.log(Array.of('a',1,2,34,12)) // ["a", 1, 2, 34, 12]

Array.isArray() //判断是不是数组
返回值：
    true || false  

```

#### 数组的find 和 findIndex

```javascript  
arr.find()  //返回具体的值
    // 例子：
    let arr = [1,2,3,4,5,6,7,8];
    let newArr = arr.find((item,index)=>{
        return item > 3
    })
    console.log(newArr) // 4 
    // 总结： 返回的是数组中第一个满足条件的值，没有找到满足条件的返回undefined    

arr.findIndex() //返回的是索引
    // 例子：
    let arr = [1,3,4,5,7,8];
    let newArr = arr.findIndex((item,index)=>{
        return item > 3
    })
    console.log(newArr) // 2
    // 总结： 返回的是数组中第一个满足条件的索引，没有找到满足条件的返回 -1   

```

#### 数组扁平化flat和includes

```javascript  

arr.flat(number) //将扁平化数组展开
参数：
    number 提取几层
    let arr = [
        ["张三",10],
        ["李四",20],
        ["王二麻",30]
    ]
    console.log( arr.flat(1))  //["张三", 10, "李四", 20, "王二麻", 30]
    /*这里是直接能看出来里面就一层，所以直接arr.flat(1)就可以转变成一维数组，如果
    遇到不知道有多少层的情况，我们可以用Infinity来转变*/
    
    let arr = [
        ["张三",10],
        ["李四",20],
        ["王二麻",30,
            ["a",
                ["张三",10],
                ["李四",20],
                ["王二麻",30],
            ]
        ]
    ]
     console.log( arr.flat(Infinity)) 
    // ["张三", 10, "李四", 20, "王二麻", 30, "a", "张三", 10, "李四", 20, "王二麻", 30]

arr.flatMap()  //数组扁平化处理
    let arr = [
        ["张三",10],
        ["李四",20],
        ["王二麻",30]
    ] 

   let newArr = arr.flatMap((item)=>{
        console.log(item) //可以拿到每一个小数组
        item = item.filter((item,index)=>{
            return index == 0  //此处 是将没个小数组的第一项（也就是姓名）过滤取出
        })
        return item
    })
    console.log(newArr)  //["张三", "李四", "王二麻"]
    注意：arr.flatMap() 只能处理一层，如果里面还有，需要进行递归来处理

arr.fill() //数组填充
    let arr = [0,1,2,3,4,5]

    如果一个参数，则是全部填充
    // console.log(arr.fill("a"))  //["a", "a", "a", "a", "a", "a"]

    如果传入连个参数，第一个参数是要填充的值，第二个参数是从第几位开始
    console.log(arr.fill('a',4)) //[0, 1, 2, 3, "a", "a"]

    如果传入三个参数，第一个参数要填充的值，第二个参数要从第几位开始，第三个参数是到第几位结束（不包括结束的位置）
    console.log(arr.fill('a',3,4)) //[0, 1, 2, 'a', 4, 5]

arr.includes(val,fromIndex)
参数：
    val  要查找的值
    fromIndex 从第几位开始，可传可不传
返回值：
    true  表示包含这个值，
    false 表示没有检索到
```

#### 字符串新增方法

```javascript
    let str = '我爱你我的祖国，一刻也不能分割';
str.includes(val,fromIndex) //检索是都包含
参数：
    val 查找包含的值 
    fromIndex 从什么位置开始
返回值：
    true  表示包含这个值，
    false 表示没有检索到

str.startsWith(val,startIndex) //是否以某个字符串开始
参数：
    val  要检索的值
    startIndex 从第几位开始

str.endsWith(val,startIndex) //是否以某个字符串结束
参数：
    val  要检索的值
    startIndex 从第几位开始（值得注意的是，这里的开始位置是从前面）

str.repeat(num) //重复
参数：
    num 重复的次数

```

#### 对象新增方法

```javascript
原来我们对象的写法如下
    let a = "10"
    let b = "20"
    let obj = {
        a: a,
        b: b,
        c: function(){
        console.log('1111') 
        }
    }
现在通过es6可以这样写
    let obj = {
        a,
        b,
        c(){
            console.log('1111') 
        }
    }
属性名表达式：
    原来在对象中操作属性值是这样的
        let name = "张三"
        let obj = {
            name: 111
        }
        obj[name] = 111
        console.log(obj) //{name: 111, 张三: 111}

    在es6中就省去了，下面的操作，直接在对象中操作
        let name = "张三"
        let obj = {
            [name]: 111 
        }
         console.log(obj) //{张三: 111}

Object.assign(val,val2) 合并对象
参数：
    val  要被合并到的对象位置
    val2 被合并的对象值
例子：
    let obj ={
        a:1,
        b:2
    }
    let obj2 ={
        c:3,
        d:4
    }
    // Object.assign(obj,obj2)
    console.log(Object.assign(obj,obj2)) //{a: 1, b: 2, c: 3, d: 4}
    Object.assign({},obj,obj2) //这样可以，将obj和obj2两个值合并到空对象中

Object.is() //判断两个值是否相同的值
规则：
    两个值都是undefined
    两个值都是null
    两个值都是true 或者都是false
    两个值都是由相同个数的字符按照相同的顺序组成的字符串
    两个值指向同一个对象
    两个值都是数字并且
        都是 +0 
        都是 -0
        都是 NaN

```