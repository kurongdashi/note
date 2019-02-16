
## angular 

- 强制刷新Dom ,$apply()使用 
``` 
 //强制刷新变量
  $scope.$apply(function () {
      $scope.showSelect=false;
   })

```
- $event 事件获取

``` 
点击时，传入$event
ng-click="searchParkName($event)"

```

- ui-router

[ui-router 入门](https://www.cnblogs.com/VictorYe/p/7099165.html)
[ui-router 深入](https://www.cnblogs.com/haogj/p/4885928.html)




## React 

- jsx ,类似模版引擎 ``,可以在代码中直接jsx 变量赋值

``` 
if(type==1)
{
   dom=<span className="type owe">欠费待补交</span>
}
```

- 绑定事件，传参

``` 
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>

<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>

```

- 组件必须大写（和java 类同），属性驼峰写法,例如className,区分html原生标签

``` 
// 函数组建记得引入react
import React from 'react' 


```

- props(纯函数，无法修改值) 自带一个children 属性，代表现在组件里的元素
类似vue slot 插槽
``` 
 <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>

```

- 如果有多个插槽，不是用children，因为自定义属性可以传入一个组件作为属性值 

``` 
<SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
```

- setState(param) 方法 参数接收一个函数，该函数的第一个参数是要更新对象
的前一个状态

``` 
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}))
```

- 表单有受控组件，和非受控（ref）
 
 ``` 
 //受控写法
 <input type="text" value={this.state.value} onChange={this.handleChange} />
 //非受控
 <input type="text" ref='xxx' onChange={this.handleChange} />
 
 ```

- ref 的最新写法,接收一个函数
``` 
<input type="text" ref={(input)=>input} onChange={this.handleChange} />

```
- mixin 使用



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

## css 
 - overflow 属性误区 推荐使用auto,不用scroll

[overflow 属性误区](http://www.w3school.com.cn/cssref/pr_pos_overflow.asp)

 - 怎么应用vertical-align，才能生效,父元素设置line-height
 
 ``` 
 img 标签和文字使用 vertical-align：top
 背景图和文字使用 vertical-align：middle
 
 <div class="filter-box">
     <span class="text">筛选</span>
     <span class="icon"></span>
 </div>
 
 ```
 
 [生效](https://blog.csdn.net/diudiu5201/article/details/54666809)
 
 - placeholder 是input元素的伪类，可以通过伪类方式设置属性
 ``` 
     &::placeholder{
          font-size: 16px;
     }
 ```
 - 浏览器滚动条，也是
 [滚动条样式](https://www.cnblogs.com/yclblog/p/6806496.html)
  ``` 
      &::scrollbar{
           font-size: 16px;
      }
  ```
  
- 手机屏幕适配方案，rem 方案

 ``` 
  设计稿一般以iphone6 屏幕作为参考，当为iphone 屏幕宽度时
  设置,html根标签font-size 为某个基准值,其他屏幕按照这个比值设置
  
 window.onresize=function(){
     
     window.clientWidth / 100 
 }
 
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
 

 
 
 
 
 ## 框架适用目录结构
 
 - 外层总路由，内层每个菜单，一个子路由
 
 

  
  
 
 
    
 
 
 