##模块化
- 什么是模块化
  + 模块化是指解决一个复杂问题时自顶向下逐层把系统划分成若干模块的过程，有多种属性，分别反映其内部特性。
  + 解决复杂问题的一种方式而已
 - 使用模块化开发的方式带来的好处
   + 生产效率高
   + 可维护性高

- 问题：
 ```
 ;(function (形参模块名, 依赖项, 依赖项) {
   // 通过 形参模块名 修改模块
 
   // 如果需要，可以通过给 window 对象挂载属性对外暴露内部成员
   window.模块名 = 形参模块名
 })(window.模块名 || {}, 依赖项, 依赖项)
```

>+ 分号是什么意思
   * 目的是为了防止前面的代码没有加分号导致语法错误
 + 为什么要给代码加一个匿名自执行函数
   * 避免全局命名空间污染，核心是利用函数的私有作用域
 + 为什么要把使用的依赖作为参数传递进来
   * 目的是减少作用域查找机制，提高代码运行效率
   
---
##Seajs
 + **Seajs介绍**
 
   - SeaJS 带来的最大好处是：提升代码的可维护性。 如果一个网站的 JS 文件超过 3 个，就适合用 SeaJS 来组织和维护代码。 涉及的 JS 文件越多，SeaJS 就越适合。
   - SeaJS 是一个适用于浏览器环境的javascript的模块加载器
     * 一个库文件，类似于jQuery
     * 使用这个库提个的规范的模块化的方式来编写JavaScript代码
     * 只关心JavaScript文件代码如何组织、相互协议、引用、依赖
   - SeaJS 的作者是阿里巴巴支付宝前端架构师，花名：玉伯，玉伯也叫射雕
   
 + **SeaJS的优点**
   - **简单友好的模块定义规范：**SeaJS 遵循 CMD 规范，可以像 Node 一样书写模块代码
   - **自然直观的代码组织方式：**依赖的自动加载、配置简洁清晰，可以让我们更多的享受编码的乐趣
   - SeaJS兼容性非常好，几乎可以运行在任何浏览器引擎上
   - SeaJS 只是实现模块化开发的一种方式或者说一种工具而已，重在模块化思想的理解
   - 因为 SeaJS 采用的 CMD 模块规范和 Node 中的 CommonJS 模块规范非常一致，所以有利于我们学习 Node 中的模块化编程
 使用场景
   - SeaJS 不提供任何功能性 API，只提供了解决 JavaScript 代码的命名污染和文件依赖的问题
   - 所以 SeaJS 可以和 jQuery、underscore 等库结合使用
   - 例如 只写写 原生 JavaScript 或者用了一些第三方库
   
 + **使用方法**
   1. 下载 sea.js 库文件
     - bower install seajs
     - npm install seajs
   2. 在页面中引入 sea.js
   3. 使用`define`函数定义模块
   4. 使用`require`函数加载模块
   5. 使用`module.exports`对外暴露接口对象
   6. 使用`seajs.ues`函数启动模块系统
  --- 
 + **API详解**
 
   **1. seajs.use**
   加载模块，启动模块系统
    - 加载一个模块`seajs.use('id')`
    - 加载一个模块，在加载完成时，执行回调`seajs.use('id',callback)`
    - 加载多个模块，加载完成时，执行回调函数`seajs.use(['id1','id2',...],callback)`
    - **注意**
      + 在调用 seajs.use 之前，需要先引入 sea.js 文件
      + seajs.use 与 `DOM ready` 事件没有任何关系。如果某些操作要确保在 `DOM ready` 后执行，需要使用 jquery 等类库来保证
      + seajs.use 理论上只用于加载启动，不应该出现在 `define` 中的模块代码里
      
   **2. define(factory)**
   
       `define`是一个全局函数，用来定义模块
       
       `define`接受`factory`参数，`factory`可以是一个函数，也可以是一个字符串
       `factory`为对象、字符串时，表示模块的接口就是该对象或字符串。
        + factory 是一个对象时：
          * `define({})`
        + factory 是一个字符串时：
          * `define('hello')`
        + factory 是一个函数时： 
          * `define(function(require,exports,module){})`
          
   **3. require**
   
    require 用来加载一个js文件模块，require 用来获取指定模块的接口对象`module.exports`
    
    require 在加载和执行的时候，js会按照同步的方式和执行。
    
     **使用注意：**
     >>
      - 正确拼写
        + 模块 factory 构造方法的第一个参数必须命名为require
      - 不要修改
        + 不要重命名 require 函数，或在任何作用域中给 require 重新赋值
      - 使用字符串直接量
        + require 的参数值 必须 是字符串直接量
        
      Tips: 把 require 看做是语法关键字就好啦

  **4. exports**
      - 每个模块内部对外的接口都是 `module.exports`
      - 可以修改 `module.exports` 或给它赋值改变模块接口对象
      - `exports` 就是` module.exports `的一个引用，就好比在每一个模块定义最开始的地方写了 `var exports=module.exports`
      - **注意**
        + 可以给exports点属性赋值，但是不能直接给exports直接赋值。
        类似于：
      ```  
      function fn() {
              var a = {};
              var b = a;
              b.name = 1;
      
              b = {aa: 2};
              console.log(b);
              console.log(a);
              return a;
          }
      ```
      - 为什么还要使用 `exports`
        + 只是为了开发体验，API更友好，少写几个字母
 ---
 + **jQuery如何兼容CMD**       
 ```
if (typeof define === 'function' && define.cmd) {
	define(function (require, exports, module) {
	  module.exports = jQuery;
	});
}

 ```
 ---
+ **常见的JavaScript模块化规范**
    - 什么是规范
      * 定义模块的书写格式
      * 定义模块之间的交互规则
    - Node环境
      * CommonJS
    - 浏览器环境
      * AMD
      
        **1. RequireJS**
        
      * CMD
      
        **1. SeaJS**
    - ECMAScript
    
      **1. ECMAScript**  
    - UMD
    
**AMD、CommonJS 都是社区制定出来的模块规范，他们的目的都是为了解决 JavaScript 没有模块化系统的问题。 他们都有如何定义模块成员，以及模块成员之间如何进行通信交互的规则。**