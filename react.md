 ## React 
 
 - 生命周期
 [生命周期](https://www.cnblogs.com/qiaojie/p/6135180.html)
 
 1. componentWillReceiveProps 使用
``` 
 //组件props 更新时调用
    componentWillReceiveProps(nextProps){

        if(this.props.showTime){
            document.body.style.overflow='hidden'
        }else{
            document.body.style.overflow='auto'
        }
    }
```
 
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
 
 - props 验证和使用默认属性
 [验证和使用默认属性](https://react.docschina.org/docs/typechecking-with-proptypes.html)
``` 
//使用默认属性
    static defaultProps={
        btnType:'',
        leftBtnText:'放弃',
        rightBtnText:'确认购买',
    }

```
## React 使用

1. 弹窗关闭事件处理

``` 

 this.state={
            show:this.props.show,
            dialogType:'DEF',
            title:'新人领劵'

        }

//因为该弹窗只弹一次，所以关闭弹窗交由内部处理，如果是和外组件有交互，则必须由外组件处理
    closeDialog=()=>{
        this.setState({show:false})
    }


```

 
 
 ## redux 结合react使用
 
 1. 安装 redux ，react-redux (连接react和redux)，redux-logger
    
 - redux 和DOM 无关的
  
 - react-redux 和DOM 相关的操作，方法都从这里引用
 
    [react-redux](https://www.npmjs.com/package/react-redux)
 
 2. 创建store文件夹，创建对应文件
 
 - action.js 主要用来写动作和type,每个action 必须包含一个type
 
 
 ``` 
export const type={
    USER_LOGIN:'USER_LOGIN',
    USER_OPTION:'USER_OPTION'
}
//用户登陆action
export function loginAction(data) {
    return {
        type:type.USER_LOGIN,
        userInfo:data
    }
}
//用户配置
export function optionAction(data) {
    return {
        type:type.USER_OPTION,
        userOption:data
    }
}

 
 ```
 - reducer.js 主要用来定义规则，就是操作state
 
 ``` 
 import {type} from './action'
 import {combineReducers} from 'redux'
 
  //登陆
  function loginReducer(state={},action) {
     switch (action.type){
         case type.USER_LOGIN:
            let obj=Object.assign({},state,action.userInfo)
             return obj;
         default:
             return state;
     }
 }
 
 function optionReducer(state={},action) {
     switch (action.type){
         case type.USER_OPTION:
             let obj=Object.assign({},state,action.userOption)
             return obj;
         default:
             return state;
     }
 }
 
 //合并所有的reducer
 let reducer=combineReducers({
     loginReducer,optionReducer
 })
 
 export default reducer
 
 ```
 
 - store.js 主要用来生成store，和使用一些插件，例如logger
``` 
//applyMiddleware 允许使用redux-devtools

import {createStore,applyMiddleware} from 'redux';

import reducer from './reducer';
//使用logger
import {createLogger} from 'redux-logger'


let logger=createLogger({collapsed:true})

// import {composeWithDevTools} from 'redux-devtools-extension'

const store=createStore(reducer,applyMiddleware(logger))

export default store

```        
3. 在react项目入口（index.js），引入redux使用

``` 
import {Provider} from 'react-redux'
import store from './store/store'

ReactDOM.render(
    <Provider store={store}>
        <App></App>
    </Provider>

    , document.getElementById('root'));

registerServiceWorker();

```

4. 在react项目具体某个页面中使用redux，例如在home.js 页面

``` 
// 将redux 中reducer 结果绑定到props
let mapStateToProps=(state)=>{
    //state 包含的是所有的reducer
    console.log('home--state==',state)
    return {
        userInfo:state.loginReducer,
        userOption:state.optionReducer
    }
}
//将action 方法绑定到props 上
let mapDispatchToProps=(dispatch)=>{
        return {
            loginAction:bindActionCreators(myselfAction.loginAction,dispatch),
            optionAction:bindActionCreators(myselfAction.optionAction,dispatch),
        }
}
// connect将 redux 中的reducer，和action 方法绑定到props上
export default connect(mapStateToProps,mapDispatchToProps)(Index);

```    
 
 ## React-router 4.x 
 - 详细 包括4个包，每个包要另外安装
 [React-router4.x](https://github.com/ReactTraining/react-router)
 react-router，react-router-dom (我们用这个就行)
 
 ### react-router-dom 使用
 
 - HashRouter作为外层，只能有一个children
 
 ``` 
 <HashRouter>
             <div>
                 <Route path="/" exact component={Index}></Route>
                 <Route path="/second" component={Second}></Route>
             </div>
 
         </HashRouter>
 
 ```
 - 子路由嵌套
  ``` 
  <HashRouter>
              <div>
                  <Route path="/" exact component={MyRouter}></Route>
              </div>
  
          </HashRouter>
  
  ```
- hash路由使用微信分享问题，微信会截取掉 #，导致路由只能跳转到首页(android正常，ios异常)
[hashRouter微信分享](https://www.cnblogs.com/xyyt/p/7533091.html)
``` 

```

 
 
 
 
 
  
  
## create-react-app 

[create-react-app 配置](https://www.jianshu.com/p/e09b2c57cf20)

1. 配置代理proxy
``` 
package.js 中加入

"proxy":{
    "/api":{
      "target":"http://10.101.222.10",
    }
  },

```
2. 使用antd [使用antd](https://ant.design/docs/react/use-with-create-react-app-cn)

``` 
/ package.json 文件
  "babel": {
    "presets": [
      "react-app"
    ],
    // 加入配置
    "plugins": [
    // 如果使用了 定制颜色功能 将 "css" => true 同时需要配置 less
      ["import", { "libraryName": "antd-mobile", "style": "css" }]
    ]
  }
```
  
 ## antd 使用
1. webpack 按需加载配置
 [按需加载配置](https://www.cnblogs.com/camille666/p/webpack_antd.html)
 
 
 
 ## swiper使用
 
 1. 初始化swiper必须等待数据加载完成，将列表dom全部渲染完成后，执行
 ``` 
 initSwiper() {
         let mySwiper = new Swiper('.swiper-container', {
             slidesPerView: "auto",
             spaceBetween: 0,
         });
     }
 ```
  
  ## jsx 开发中
  
  - 使用marquee 标签时，无法设置属性，需要动态设置
  ``` 
  //设置marquee,因为jsx不支持marquee标签设置属性
      setMarquee(){
          let domMar=document.getElementById('marquee');
          domMar.scrollAmount='3'
      }
  
  ```