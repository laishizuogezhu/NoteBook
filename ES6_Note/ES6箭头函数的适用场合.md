## ES6箭头函数的适用场合

1. 箭头函数适用于与this无关的回调，比如定时器，数组的方法回调
2. 箭头函数不适用于与this有关的回调，比如事件的回调，对象的方法

## 给函数参数赋初始值

1. 形参初始值,具有默认值的参数，一般位置要靠后

```javascript
 function add(a,b,c=10) {
            return a+b+c;
        }
        let result = add(1,2);
        console.log(result);
```

2. 与解构赋值相结合

```javascript
function connect({host="127.0.0.1",username,password,port}) {
            console.log(host),
            console.log(username),
            console.log(password),
            console.log(port)
        }
        connect({
            host:'localhost',
            username:'root',
            password:'1234abc',
            port:3306
        })
 // 如果实参有值，则使用实参的值，否则使用形参的默认值

```

## ES6引入 rest 参数

1. 用于获取函数的实参，用来代替 arguments

2. rest参数必须要放到参数最后

```javascript
function date(...args){
	console.log(args);
	//args是数组，不是对象
}
date("阿娇",'白芷','思慧')；
```

## 扩展运算符

1. 声明一个数组

```javascript
const tfboys = ['王源','王俊凯','易烊千玺']
```

2. 声明一个函数

```javascript
function chunwan(){
	console.log(arguments);
    //此时arguments是一个对象	
}
chunwan(tfboys);
---------------------------------------------
function chunwan(){
	console.log(arguments);
    //此时arguments是一个数组	
}
chunwan(...tfboys);
```

3. 数组的合并

```javascript
const kuaizi = ['王太利','肖央'];
const fenghuang = ['曾毅','玲花']；
const connect = [...kuaizi,...fenghuang];
```

4. 数组的克隆

```javascript
const san = ['E','G','M'];
const sanclone = [...san];
```

5. 将伪数组转为正真的数组

```javascript
const divs = document.querySelectorAll('div')
const divarr = [...divs];
```

## Symbol基本使用

1. Symbol是一种原始的数据类型，表示独一无二的值，通常用于给对象添加属性和方法
2. 特点
   - symbol的值是唯一的，用来解决命名冲突的问题
   - 不能与其它数据进行运算,也不能跟自身
   - symbol定义的对象属性不能使用for...in循环遍历，但是可以使用Reflect.ownKeys来获取所有键名
3. 创建symbol

```javascript
// 创建symbol
        // 方式一
        let s = Symbol();
        // 方式二 创建的symbol值不是唯一的
        let s2 = Symbol('张三');
        let s3 = Symbol('张三');
        console.log(s2===s3);//false
        // 方式三 创建的symbol值是唯一的
        let s4 = Symbol.for('张三');
        let s5 = Symbol.for('张三');
        console.log(s4===s5);//true
```

4. 向对象中添加方法

```javascript
 let game = {
          up:function(){
           console.log("我可以上升！")
          },
          down:function(){
              console.log("我可以下降！");
          },
          name:'张三'
       }
       let method = {
           up:Symbol(),
           down:Symbol()
       }
       game[method.up] = function(){
           console.log("我可以快速上升！")
       };
       game[method.down] = function(){
           console.log("我可以快速下降！")
       }
       console.log(game);
```

```javascript
  //    或者通过以下方法
    let youxi = {
        name:'狼人杀',
        [Symbol('say')]:function(){
            console.log("我可以说话")
        },
        [Symbol('zibao')]:function(){
            console.log("我可以自爆")
        }
    }
    console.log(youxi);
```

## 迭代器

1. 迭代器是一种接口，为各种不同数据结构提供统一的访问机制，任何数据结构只要部署iterator接口，就可以完成遍历操作，相当于对象中的一个属性
2. ES6创建了一种新的遍历命令for···of循环iterator接口主要供for···of消费
3. 原生具备iterator接口命令的数据
   1. Array
   2. Arguments
   3. Set
   4. Map
   5. String
   6. TypeArray
   7. NodeList

4. 使用

```javascript
 const xiyou = ['唐僧','孙悟空','猪八戒','沙和尚','白龙'];
        for(v of xiyou){
            console.log(v);
        }
// for...of循环是数组的每个元素,for...in循环是数组元素的下标
```

5. 给没有迭代器的对象增加迭代器

```javascript
 let clazz = {
 name: '终极一班',
 stus: ['小明', '小张', '小李', '小吴', '小赵'],
[Symbol.iterator]() {
     let index = 0;
     return {
        next: () => {
          if (index < this.stus.length) {
             const result = {
               value: this.stus[index],
               done: false
              };
              index++;
              return result;
           } else {
               return {
                 value: undefined,
                 done: true
                };
            }
         }
     }
   }
}
  for (v of clazz) {
     console.log(v);
        }
```

## 生成器

1. 生成器其实就是一种特殊的函数，专门针对异步编程，异步编程主要有文件操作，网络操作，和数据库操作
2. 生成器要在function和函数名中间添加一个‘*’
3. 生成器不能直接执行，要调用迭代器的next方法

```javascript
function* gen() {
            console.log("哈哈，我是卖报的小行家")
        }
        let iterator = gen();
        iterator.next();
```

4. yield 是函数代码的分隔符

```javascript
function* gen2(params) {
      console.log(111);
      yield 'aaa'; 
    //这行之前的为一块，调用next时执行到这里
      console.log(222);
      yield 'aaa'; //这行和222为一块
      console.log(333);
      yield 'aaa'; //这行和333为一块
      console.log(444);
      yield 'aaa'; //这行和444为一块
      console.log(555); //这行到最后为一块
        }
let iterator = gen2();
iterator.next();//111
iterator.next();//222
iterator.next();//333
iterator.next();//444
iterator.next();//555
for (v of gen2()) {
      console.log(v);//yield后面的字符串
}
```

5. iterator.next()的返回值是一个对象，执行了第几次返回的对象里面的值就是第几个yield后面的值
6. iterator.next()可以传递参数，所传递的参数就是前一个yield语句的返回值

```javascript
function* gen(params) {
    console.log(params);
    let one = yield 111;
    console.log(one);
    yield 222;
    yield 333;
    yield 444;
}
let iterator = gen('AAA');
console.log(iterator.next());
console.log(iterator.next('BBB'));
//BBB传递的是第一个yield语句的返回值
```

7. 实例

```javascript
function one() {
    setTimeout(() => {
        console.log(111);
        iterator.next();
    }, 1000)
}
function two() {
    setTimeout(() => {
        console.log(222);
        iterator.next();
    }, 2000)
}
function three() {
    setTimeout(() => {
        console.log(333);
        iterator.next();
    }, 3000)
}
function* gen() {
    yield one();
    yield two();
    yield three()
}
let iterator = gen();
iterator.next();
```

