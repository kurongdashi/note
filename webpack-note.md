 ## webpack 
 webpack.config.js 文件导出一个对象
 [webpack文档](https://www.webpackjs.com/concepts/)
 
 - output 出口 ，entry 入口
  * 多个出入口 使用占位符 [name] 代表模块名称
  [占位符](https://www.webpackjs.com/configuration/output/#output-filename)
  ``` 
  {
    entry: {
      app: './src/app.js',
      search: './src/search.js'
    },
    output: {
      filename: '[name].js',
      path: __dirname + '/dist'
    }
  }

  
  ```
  * 单个出入口
 ``` 
 module.exports = {
   entry: './path/to/my/entry/file.js',
   output: {
     path: path.resolve(__dirname, 'dist'),
     filename: 'my-first-webpack.bundle.js'
   }
 };
 
 ```
 - mode 不同的模式下启用不同的功能插件
 ``` 
   mode: "production", // "production" | "development" | "none"
 ```
 
 - loader   
 webpack自身只理解.js 文件，其他文件打包需要使用loader进行转化
使用loader 必须写在module.rules 里面

1. test 标识要转化类型
2. use 使用loader

 ``` 
 const config = {
   output: {
     filename: 'my-first-webpack.bundle.js'
   },
   module: {
     rules: [
       { test: /\.txt$/, use: 'raw-loader' }
     ]
   }
 };
 
 ```
 
 3. use 可以配置数组
 ``` 
  module: {
     rules: [
       {
         test: /\.css$/,
         use: [
           { loader: 'style-loader' },
           {
             loader: 'css-loader',
             options: {
               modules: true
             }
           }
         ]
       }
     ]
   }
 
 ```
 
 4. 内联使用loader
 
 - plugins 完成loader无法完成的任务，配置使用数组[],传入new 对象
 ``` 
 plugins: [
     new webpack.optimize.UglifyJsPlugin(),
     new HtmlWebpackPlugin({template: './src/index.html'})
   ]
 
 ```
 
 - resolve  是一个库(library)，用于帮助找到模块的绝对路径
 
 ``` 
 resolve: {
     extensions: ['.js', '.vue', '.json'],
     alias: {
       'vue$': 'vue/dist/vue.esm.js',
       '@': resolve('src'),
     }
   },
 ```
 - target 用于设置webpack 打包环境 由node 和web 两种，默认是web环境
 
 
 ## CommonJS、CMD、AMD 理解
 
 [CommonJS理解](https://www.cnblogs.com/chenguangliang/p/5856701.html)
 
 ### commoneJS 解决的是模块化加载的问题（同步加载），是适应于后台的规范（本地加载本地），同步加载模块 实现node.js
 
 1. require()
 
 2. module.exports.xxx
 

 
 ### AMD (Asynchronous Module Definition) 是解决异步模块化加载问题，适应于前端规范（客户端加载远程模块），防止客户端卡住，假死.实现框架有requireJS
 
 1. require(['module'],callback)
 
  ``` 
  require(['math'], function (math){
  
  　　　　alert(math.add(1,1));
  
  　　});
  ```
 
 2. 定义模块 
    a.直接定义 define(fn)
    b. 依赖其他模块 define(['module'],fn)
    
    
### CMD (通用模块定义) 也是异步模块加载  实现由seaJS  
    
   1. seaJS 和requireJS [区别](https://www.douban.com/note/283566440/)
   
   requireJS 是将所有依赖模块优先加载，不管是否使用到
   seaJS 是模块按需加载，也就是按顺序执行代码  
    
    
 
                                   
   
 