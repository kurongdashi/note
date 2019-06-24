
## JS 
- 光标移动行末，或选中文字
``` 
//将光标位置移动至输入字符后面
    cursorEnd(e){
        let dom=e.target;
        //设置选中字符位置，如果起始位置==结束位置，则光标就在该位置
        dom.setSelectionRange(0,1)//选中0~1字符
        dom.setSelectionRange(1,1)

    }

```
- 正则常用方法

[正则使用](http://javascript.ruanyifeng.com/stdlib/regexp.html#toc3)

1. string.replace(),脱敏,第二个参数中用$,代表捕获的分组
``` 
'13423882680'.replace(/^(\d{3})\w+(\w{4})$/,'$1****$2')

"134****2680"

```
2. 常用预定义

``` 
大写取反
\d [0-9] 
\D [^0-9]
\s 空格、换行
\w 字母、数字、下划线

{n} 正好n次
{n,m} >n <m
{n,} >n


* 0个或多个
+ 1个或多个
? 0 或者1个

```
3. 模式，默认是匹配到第一个就停止


``` 
i ignorecase 忽略大小写
g global   全局匹配
m mutilline 多行（跳过换行符继续匹配）

```
### JS 面向对象

- 对象的深拷贝
``` 
for ...in 会遍历对象继承的属性（前提这些属性可以被遍历）
Obj.hasOwnProperty(),判断是否是自身的属性

function deepCopy(obj){
    // 判断要拷贝的对象是数组
    let result=Array.isArray(obj)?[]:{};
    for(let key in obj){
        if(obj.hasOwnProperty(key)){
            // 对象的属性是否是对象
            if(typeof obj[key]==='object'){
                result[key]=deepCopy(obj[key])
            }else{
                result[key]=obj[key];
            }
        
        }
    
    }
    return result;

}


```

- 双向数据绑定原理

[双向数据绑定原理](https://www.cnblogs.com/lvmylife/p/7474374.html)

1. Object.defineProperty(obj,attr,{set(nVal),get())

- 判断变量是否为对象
1. Object(param),将参数包装成对象，如果参数是对象则直接返回

``` 
function isObject(value) {
  return value === Object(value);
}

```
2. 对象属性数量
``` 
Object.keys(obj).length;

```            
3. new 命令原理解析
``` 
new 创建一个空对象，然后将空对象的原型指向构造函数的prototype，将空对象赋值给this
function getMessage() {
  return 'this is a message';
}

var msg = new getMessage();

msg // {}
typeof msg 

new 命令创建对象，函数内部会有new.target==函数名

```
4. 内层（2层及以上）函数的this其实是指向顶层window对象的

5. 避免对象实例方法覆盖原型对象方法，将直接调用原型方法，绑定对象就行
``` 
Object.prototype.hasOwnProperty.call(obj, 'toString') //

```
6. 取数组中最大值

``` 
var a = [10, 2, 4, 15, 9];
Math.max.apply(null, a) // 15

```
7. prototype指向原型对象

``` 
var MyArray = function () {};
MyArray.prototype = new Array();
MyArray.prototype.constructor = MyArray;

#constructor属性表示原型对象与构造函数之间的关联关系，如果修改了原型对象，一般会同时修改

```
8. instanceof 判断对象是否来着构造函数new出来的，但是由于instanceof检查整个原型链

9.  创建对象Object.create(A)，参数A可以是普通对象，也可以是原型对象，生成的对象继承参数对象

10. __proto__ ,浏览器私有属性，指向对象原型，可读写

11. 模块化设计原理，利用立即指向函数封装私有方法
``` 
var moudel=(function($,window){
    a(){}
    b(){}
    
    return {
        a:a(),
        b:b()
    }

})(jQuery,window)

```

### 网络通信ajax

``` 
//创建请求对象 status=0
var xhr=new XMLHttpRequest();
//监听readyState状态
xhr.onreadystatechange=change;

function change(){
    //通信成功
    if(xhr.readystate==4){
        //返回成功
        if(xhr.status==200){
            console.log(xhr.responseText)
        }
    }
}
xhr.onerror=err;
// status=1
xhr.open('get',http://xxxx)
// status=2
xhr.send()

```


###  兼容性问题

### 手机端 IOS,android 浏览器

[兼容性问题](https://www.jianshu.com/p/31e53df2ecce)

[汇总](https://efe.baidu.com/blog/mobile-fixed-layout)

1. ios 浏览器获取时间不支持 （2019-3-12 09:05:09） 带-方式，
应该使用（2019/3/12 09:05:09），以后所有格式化获取时间全部使用 / 替换-

``` 
// 以后所有格式化获取时间全部使用 / 替换-
 inTime=inTime.replace(/-/g,'/');
  let time=new Date(inTime).getTime();
``` 
2. 手机软键盘问题,ios下fixed定位缺陷，尽量使用absolute

* 问题1：软键盘唤起后，将页面顶上去，留出一个软件盘的位置，页面其他元素位置错误

 ``` 
 <body class="layout-scroll-fixed">
     <!-- fixed定位的头部 -->
     <header>
         
     </header>
     
     <!-- 可以滚动的区域 -->
     <main>
         <div class="content">
         <!-- 内容在这里... -->
         </div>
     </main>
     
     <!-- fixed定位的底部 -->
     <footer>
         <input type="text" placeholder="Footer..."/>
         <button class="submit">提交</button>
     </footer>
 </body>
 
 ```
 * 问题2：软件盘结束后，页面留白问题,需要监听input的onblur事件，js控制页面滚动到原点
 
 [页面留白问题](https://www.jianshu.com/p/0953157ca407)
 ``` 
  onBlur () {
         window.scrollTo(0,0)
       }
 ```
 
 3. 300ms 延时，fastclick
 
 4. ios 下对非可点击元素，不会触发点击事件，so,需要规范标签的语义化
 
 5.关闭window问题
 [关闭window问题](https://www.jianshu.com/p/9dc2752194b8)
 
 ``` 
  window.location.href="about:blank";
  window.close();
 ```
 6. IE浏览器兼容问题
 [IE浏览器兼容问题](https://www.cnblogs.com/cxyc/p/10592957.html)
 
 ``` 
 IE9 以下都使用 注释
 <!-- [if lte IE 9 ]> 处理xxx <!endif>
 
 <!--[if lt IE 9]> 
 <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
 <![endif]-->
 ```
 7. 微信中对img 标签点击放大问题：Android底层默认支持点击放大，ios中无此问题
 [img 标签点击放大问题](https://www.jianshu.com/p/78af66ca9149)
 ``` 
  if(e){
            e.preventDefault();
       }
 ```    
   


## css 
 - overflow 属性误区 推荐使用auto,不用scroll

[overflow 属性误区](http://www.w3school.com.cn/cssref/pr_pos_overflow.asp)
[生效](https://blog.csdn.net/diudiu5201/article/details/54666809)
 1. 怎么应用vertical-align，才能生效,父元素设置line-height
 
 ``` 
 img 标签和文字使用 vertical-align：top
 背景图和文字使用 vertical-align：middle
 
 <div class="filter-box">
     <span class="text">筛选</span>
     <span class="icon"></span>
 </div>
 
 ```
 
 
 
 2. placeholder 是input元素的伪类，可以通过伪类方式设置属性
 ``` 
     &::placeholder{
          font-size: 16px;
     }
 ```
 3. 浏览器滚动条，也是
 [滚动条样式](https://www.cnblogs.com/yclblog/p/6806496.html)
 [滚动条样式](https://segmentfault.com/a/1190000012800450)
  ``` 
     /*定义滚动条高宽及背景
      高宽分别对应横竖滚动条的尺寸*/
     ::-webkit-scrollbar
     {
         width:16px;
         height:16px;
         background-color:#F5F5F5;
     }
     /*定义滚动条轨道
      内阴影+圆角*/
     ::-webkit-scrollbar-track
     {
         -webkit-box-shadow:inset 0 0 6px rgba(0,0,0,0.3);
         border-radius:10px;
         background-color:#F5F5F5;
     }
     /*定义滑块
      内阴影+圆角*/
     ::-webkit-scrollbar-thumb
     {
         border-radius:10px;
         -webkit-box-shadow:inset 0 0 6px rgba(0,0,0,.3);
         background-color:#555;
     }

  ```
  4. 文字换行和空白换行控制
      [文字换行](https://www.cnblogs.com/dfyg-xiaoxiao/p/9640422.html)  
  
  
### 手机屏幕适配方案，rem 方案
    [rem 方案](https://www.cnblogs.com/dannyxie/p/6640903.html)
1.  根元素size（rem） = (实际文档宽/设计稿宽) * 50 = (实际尺寸/设计尺寸) *50  
x50是为了根元素最小尺寸大于12px,所以实际尺寸= 设计尺寸/50 *rem
    
 ``` 
 <meta name="viewport" content="initial-scale=1,maximum-scale=1, minimum-scale=1">
 
  <script>
        window.onresize=function () {
            document.documentElement.style.fontSize = document.documentElement.clientWidth / 375*50 + 'px';
        }
    </script>
 
 ```
 - 隐藏input 光标，显示文字,用文字阴影替代颜色
    
 ``` 
 <style>
     input{
       color: transparent;
       text-shadow: 0 0 0 #000;
     }
   </style>
 ```
 - 阻止遮罩层下list 滚动，直接设置body的overflow属性
 
 [阻止遮罩层下滚动](https://www.cnblogs.com/licf/p/4691556.html)
 
 ``` 
if(props.showTime){
        document.body.style.overflow='hidden'
    }else{
        document.body.style.overflow='auto'
}
 
 ```
 - css 按钮按下样式，:active
 
 
 -  line-height 属性和pading-top 有冲突，实现文字居中，推荐选择padding，line-height
 会被子元素继承，导致样式混乱，解决方案
 ``` 
 //子元素
  line-height: normal;
 
 ```
 
 - 父元素与子元素之间的margin-top问题,同级或者嵌套的盒元素，
 并且它们之间没有非空内容、Padding或Border分隔,他们合并margin
  [margin-top](https://www.cnblogs.com/ranyonsue/p/5461749.html)
  ``` 
  
  .fu{
       overflow：hidden；
       .zi{
        
       }
  }
  
  ```
 
## Html,html5
- 元标签的使用
[元标签的使用](https://www.cnblogs.com/yumo1627129/p/7198968.html)
 ``` 
  meta 标签 name content 属性
  name属性，和网页本身有关,keywords,description
  
  meta 标签 http-equiv content 属性
  
  http-equiv属性，和http请求有关，例如设置缓存，请求头，解析
  //注意是key中的值是大写开头
  <meta http-equiv="Content-Type" content="text/html;charset=信息参数"/> 
  //不使用缓存
  <meta http-equiv="Cache-Control"content="no-cache"/>
      
  
  
  ```  


 
 
## flex 布局

  [flex布局](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
 
 1. item 平均分布，给父级设置 justify-content:space-between; flex-wrap:wrap;
 
 ``` 
    .list {
          display: flex;
          justify-content: space-between;//空隙均分
          flex-wrap:wrap;//换行
          li {
             display: inline-block;
            }
 ```
 
 
 
 ## 框架适用目录结构
 
 - 外层总路由，内层每个菜单，一个子路由
 
 ## 微信公众号开发
 
 - 微信分享地址，如果是路由方式，则会被微信修改地址，会去掉#/后面参数
  a.处理方式，在进入主页面是，重新组装路由
  b.独立url,不适应路由方式
  
 - 微信中识别图片，只能是img标签，背景图无法识别
 
 
 
 

  
  
 
 
    
 
 
 