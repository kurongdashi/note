
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
2. 手机软键盘问题

软键盘唤起后，页面fixed 元素失效，变成absolute，将滚动区域和input区域分离

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
 3. 300ms 延时，fastclick
 
 4. ios 下对非可点击元素，不会触发点击事件，so,需要规范标签的语义化
 
 5.关闭window问题
 [关闭window问题](https://www.jianshu.com/p/9dc2752194b8)
 
 ``` 
  window.location.href="about:blank";
  window.close();
 ```
 
     


## css 
 - overflow 属性误区 推荐使用auto,不用scroll

[overflow 属性误区](http://www.w3school.com.cn/cssref/pr_pos_overflow.asp)
[生效](https://blog.csdn.net/diudiu5201/article/details/54666809)
 - 怎么应用vertical-align，才能生效,父元素设置line-height
 
 ``` 
 img 标签和文字使用 vertical-align：top
 背景图和文字使用 vertical-align：middle
 
 <div class="filter-box">
     <span class="text">筛选</span>
     <span class="icon"></span>
 </div>
 
 ```
 
 
 
 - placeholder 是input元素的伪类，可以通过伪类方式设置属性
 ``` 
     &::placeholder{
          font-size: 16px;
     }
 ```
 - 浏览器滚动条，也是
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
  
- 手机屏幕适配方案，rem 方案
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
 
 

  
  
 
 
    
 
 
 