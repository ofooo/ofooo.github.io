---
title: javascript基础
toc: true
tags:
  - javascript语法
date: 2019-07-12 08:55:19
categories:
---





## 参考资料
> - []()
> - []()






### 网页中的JavaScript位置

1. ```<button onclick="脚本的文本内容"></button>```   按钮onclick属性
2. ```<a href="javascript:脚本的文本内容"></a>   ```  超链接href属性
3. ```<head><script>脚本内容</script></head> ```  内部脚本
4. ```<head><script src="脚本位置"></script></head> ```  引用脚本文件（若有src，内部脚本无效）

### 网页中的JavaScript命令

```JavaScript
# 基本语法规则
# 每个语句以分号结尾
# 空格和换行都会被无视

# 显示命令
alert("提醒框文本")
console.log("控制台输出文本")
document.write("网页body中要写入的内容")
```

#### 代码/代码块/函数

```javascript
# 语句用分号分隔(分号可选)。JavaScript语句是发给浏览器的命令。语句的作用是告诉浏览器该做什么。
# JavaScript代码是 JavaScript语句的序列。　浏览器按照编写顺序依次执行每条语句
# 代码块把代码分批地组合起来。 代码块以左花括号开始，以右花括号结束。
# 函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。

// 注释用2个撇
// JavaScript的关键字必须以 字母 下划线_ 美元符$ 开始。

// 函数字面量 或 定义一个函数
function myFunction(a, b) { return a * b;} 

// 定义一个函数
const Test = function () {   }

// ES6 新增箭头函数! 使用箭头函数定义函数时可以省略 function 关键字
const Test = (...params) => {    }

// ES6 新增箭头函数! 该函数只有一个参数时可以简写成：
const Test = param => {  return param;  }


x = 123 + 'wxy'  # x = '123wxy'  JavaScript会自动把数字转化成字符串

// 文本字符串中使用反斜杠对代码行进行换行
document.write("你好 \
世界!");


// 字典在JavaScript里就是一个对象
// 访问一个对象的属性  obj.param   obj['param'] 
x = obj.param

```



#### 变量

```JavaScript
// var 声明一个变量，如果再次声明这个变量值不变
# 未赋值的变量实际 = undefined	
var lastname="Doe", age=30, job="carpenter"; 

// 赋值未null来清空变量：
cars=null;

// let 声明一个块级作用域的变量、语句或者表达式。在Function中局部变量推荐使用let变量，避免冲突
// 作用域规则 let 声明的变量只在其声明的块或子块中可用
作用域1 var var1 在其子作用域 var var1=2  则在作用域1的var1也=2
作用域1 let var2 在其子作用域 let var2=2  则在作用域1的var2=undefined


# 全局 JavaScript 变量
// 在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它。
# JavaScript 变量的生存期
// JavaScript 变量的生命期从它们被声明的时间开始。
// 局部变量会在函数运行以后被删除。
// 全局变量会在页面关闭后被删除。
# 如果您把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性。
```



### 对象

```JavaScript
// JavaScript 对象是属性和方法的容器。
// 对象的属性之间一定要用逗号隔开(同名属性只保留最后赋的值,方法也是属性)
// 对象的方法定义了一个函数，并作为对象的属性存储。对象方法通过添加 () 调用 (作为一个函数)。
// 创建一个对象,并且有一个方法:fullname
var person = {
    firstName: "John",
    lastName : "Doe",
    id : 5566,
    fullName : function() 
	{
       return this.firstName + " " + this.lastName;
    }
};


# 对象构造器
function person(firstname,lastname,age,eyecolor)
{
    this.firstname=firstname;
    this.lastname=lastname;
    this.age=age;
    this.eyecolor=eyecolor;
}
var myFather=new person("John","Doe",50,"blue");
//JavaScript中，this通常指向的是我们正在执行的函数本身，或者是指向该函数所属的对象（运行时）

```

### 对象

```javascript
HTML 事件是发生在 HTML 元素上的事情。
HTML 事件可以是浏览器行为，也可以是用户行为。
    HTML 页面完成加载
    HTML input 字段改变时
    HTML 按钮被点击
//HTML 元素中可以添加事件属性，使用 JavaScript 代码来添加 HTML 元素。单引号/双引号:
<some-HTML-element some-event='JavaScript 代码'>
<some-HTML-element some-event="JavaScript 代码">
  
事件可以用于处理表单验证，用户输入，用户行为及浏览器动作:
    页面加载时触发事件
    页面关闭时触发事件
    用户点击按钮执行动作
    验证用户输入内容的合法性
    等等 ...
```

| 常见事件    | 描述                         |
| ----------- | ---------------------------- |
| onchange    | HTML 元素改变                |
| onclick     | 用户点击 HTML 元素           |
| onmouseover | 用户在一个HTML元素上移动鼠标 |
| onmouseout  | 用户从一个HTML元素上移开鼠标 |
| onkeydown   | 用户按下键盘按键             |
| onload      | 浏览器已完成页面的加载       |

更多事件列表: [ JavaScript 参考手册 - HTML DOM 事件](http://www.runoob.com/jsref/dom-obj-event.html)。



#### 浏览器对象模型（Browser Object Model (BOM)）和 HTML DOM Document 对象

```JavaScript

#window 对象。它表示浏览器窗口。
所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。
    全局变量是 window 对象的属性。
    全局函数是 window 对象的方法。
// HTML DOM 的 document 也是 window 对象的属性之一, 下面两条语句相同:
window.document.getElementById("header"); 
document.getElementById("header"); 

// 所有浏览器的窗口宽度和高度（不包括工具栏/滚动条）(兼容)
var w=window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;
var h=window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;

# 注意 window的属性作为保留字,不能定义成变量
//screen 对象包含有关用户屏幕的信息。
    screen.availWidth  //可用的屏幕宽度
    screen.availHeight //可用的屏幕高度
//location 对象用于获得当前页面的地址 (URL)，并把浏览器重定向到新的页面。
    location.hostname  //返回 web 主机的域名
    location.pathname  //返回当前页面的路径和文件名
    location.port 	  //返回 web 主机的端口 （80 或 443）
    location.protocol  //返回所使用的 web 协议（http:// 或 https://）
//history 对象包含浏览器的历史。
Window History
    history.back() //与在浏览器点击后退按钮相同
    history.forward() //与在浏览器中点击向前按钮相同
//navigator 对象包含有关访问者浏览器的信息。

alert("sometext");  //警告框
r=confirm("sometext");  //确认框
p=prompt("请输入你的名字","Harry Potter");  //（提示框） 输入框



#document 对象
当浏览器载入 HTML 文档, 它就会成为 document 对象。
document 对象是HTML文档的根节点与所有其他节点（元素节点，文本节点，属性节点, 注释节点）。
document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。



```





```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>
<h1>我的网页</h1>
  <p id="demo">我的第一个段落。</p>
  <p id="demo2">我的第2个段落。</p>
<script>
  # 向 id="demo" 的 HTML 元素输出文本 "你好 Dolly" ： 
  document.getElementById("demo").innerHTML = "你好 Dolly";
</script>
</body>
</html>
```



#### 调试

```JavaScript
F12 打开浏览器调试器, 控制台查看日志.

console.log('some thing')
```







#### JavaScript 语句标识符 (关键字) ： 

| 语句         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| break        | 用于跳出循环。                                               |
| catch        | 语句块，在 try 语句块执行出错时执行 catch 语句块。           |
| continue     | 跳过循环中的一个迭代。                                       |
| do ... while | 执行一个语句块，在条件语句为 true 时继续执行该语句块。       |
| for          | 在条件语句为 true 时，可以将代码块执行指定的次数。           |
| for ... in   | 用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。 |
| function     | 定义一个函数                                                 |
| if ... else  | 用于基于不同的条件来执行不同的动作。                         |
| return       | 退出函数                                                     |
| switch       | 用于基于不同的条件来执行不同的动作。                         |
| throw        | 抛出（生成）错误 。                                          |
| try          | 实现错误处理，与 catch 一同使用。                            |
| var          | 声明一个变量。                                               |
| while        | 当条件语句为 true 时，执行语句块。                           |