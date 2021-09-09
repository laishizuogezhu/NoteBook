# 模块化

1. 方便维护

2. 便于复用

3. 一个JS文件就是一个模块

4. 在node中通过require（）函数来引入外部模块

5. require函数可以传递一个文件的路径作为参数，node将会自动根据该路径来引入外部模块

6. 这里的路径，如果使用相对路径，必须于.或..开头

   ```javascript
   require("./02.module.js")
   是相同目录下的一个文件
   ./ 是当前目录
   ../ 是上一级目录
   //js可以省略
   ```

7. require函数引入一个模块之后会返回一个对象，这个对象是代表引入的模块

   ```javascript
   var dm = require(./02.module.js);
   console.log(dm)//是{}
   ```

8. 在node中，每一个JS文件中的JS代码都独立运行在一个函数中，而不是全局作用域，所以一个模块中的变量和函数在其他模块中无法访问

   ```javascript
   console.log("hahaha");
   var x = 10;
   var y = 20;
   相当于一个函数的自调用
   (function(){
    console.log("hahaha");
    var x = 10;
    var y = 20;
   })()
   ```

## 向外部暴露属性和方法

可以通过exports 来向外部暴露变量和方法，只需要将需要暴露给外部的变量或方法设置为exports的属性即可

```javascript
exports.x = "我是02.module.js中的x";
exports.y = "我是y";
exports.fn = function(){
    
}
```

## 模块标识

我们使用require引入外部模块时，使用的就是模块标识，比如文件的路径，我可以通过模块的标识找到指定的模块

- 模块的分类

  1. 核心模块

     - 由node引擎提供的模块

     - 核心模块的标识就是模块的名字

       ```javascript
       var fs = require("fs");
       //是node提供的文件模块
       ```

  2. 文件模块

     - 由用户自己创建的模块
     - 文件模块的标识就是文件的路径

  