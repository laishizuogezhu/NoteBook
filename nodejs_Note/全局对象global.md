## 全局对象global

1. 在node中有一个全局对象global，它的作用和网页中的window类似

2. 在全局中创建的变量都会作为global的属性保存

3. 在全局中创建的函数都会作为global的方法保存

4. 通过删除var可以创建全局变量和方法

   ```javascript
   var a  = 20;
   console.log(a)//undefined
   -------------------------------
   a = 10
   console.log(a)//10
   ```

5. 当node在执行模块中的代码时，它会首先在代码的最顶部，添加如下代码：

   ```javascript
   function(exports,require,module,_filename,_dirname){
   //在代码的最底部添加如下代码
   }
   ```

   ```javascript
   console.log(arguments.calle+"");
   // argument.calle 这个属性保存的是当前执行的函数的对象
   //argument是伪数组元素，是传递过来的实参数组
   ```

6. 实际上模块中的代码都是包装在一个函数中执行的，并且在函数执行时，同时传递了5个实参exports，require，module，_filename,_dirname

   ```javascript
   console.log(argument.length);//5
   ```

7. exports该对象用来将变量或函数暴露到函数外部

8. require函数用来引进外部的模块

9. module代表的是当前模块本身，exports就是module的属性

   ```javascript
   console.log(exports == module.exports)
   //true
   ```

10. _filename：当前模块的完整路径

11. _dirname:当前模块所在文件夹的完整路径

### module.exports和exports差别

1. 本来exports = module.exports将module的exports属性赋值给了exports

   ```javascript
   module.exports = {
   	name:"猪八戒",
   	age:18,
   	sayName:function(){
   		console.log("我是猪八戒");
   	}
   }
   //与下面的不一样
   exports = {
   	name:"猪八戒",
   	age:18,
   	sayName:function(){
   		console.log("我是猪八戒");
   	}
   }
   ```

2. module.exports是改变了exports属性，就像`obj.name='孙悟空'`一样，改变的是属性

3. exports修改的是exports变量，不在指向module.exports

4. exports只能通过.的方式向外暴露属性，module.exports可以通过.或者直接赋值

