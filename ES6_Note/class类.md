## Class类

1. **声明**

```javascript
class Phone {
    // 构造方法，名字不能修改
    constructor(brand, price) {
        this.brand = brand;
        this.price = price
    }
    // 方法必须使用该语法，方法名+小括号，不能使用ES5的完整语法
    call() {
        console.log("我可以讲话！");
    }
    // 错误写法
    // call:function () { 
    // }
}
// 实例化
let huawei = new Phone("华为", 5999);
console.log(huawei);
huawei.call();
ript>
```

2. **类的静态成员**

   1. 在ES5中，直接给类添加成员方法和成员变量是静态的
   2. 通过类的实例化对象调用是不行的
   3. 如果想要调用，那么要在prototype中定义

   ```javascript
   function Phone() {
   }
   Phone.name = '手机';
   Phone.change = function () {
       console.log("我可以改变这个世界");
   }
   Phone.prototype.size = '5.12inch';
   let ph = new Phone();
   console.log(ph.name);//undefined
   ph.change();//报错
   console.log(ph.size);//5.12inch
   ```

   - 在ES6中，类的静态成员属于类，可以通过类调用

   ```javascript
   class Phone {
       static name = '手机';
       static change() {
           console.log("我可以改变这个世界");
       }
   }
   let ph = new Phone();
   console.log(ph.name);//undefined
   console.log(Phone.name);//手机
   Phone.change();//我可以改变这个世界
   ```

3. **对象的继承**

   - ES5

   ```javascript
   function Phone(brand, price) {
       this.brand = brand;
       this.price = price;
   }
   Phone.prototype.call = function () {
       console.log("我可以打电话");
   }
   function SmartPhone(brand, price, color, size) {
       Phone.call(this, brand, price);
       this.color = color;
       this.size = size;
   }
   // 设置子级构造函数的原型
   SmartPhone.prototype = new Phone;
   SmartPhone.prototype.constructor = SmartPhone;
   // 声明子类的方法
   SmartPhone.prototype.photo = function () {
       console.log("我可以拍照");
   }
   let apple = new SmartPhone('苹果', 4999, '黑灰色', '6.2inch');
   console.log(apple);
   ```

   - ES6

   ```javascript
   class Phone {
       constructor(brand, price) {
           this.brand = brand;
           this.price = price;
       }
       // 父类的成员方法
       call() {
           console.log("我可以打电话！");
       }
   }
   class SmartPhone extends Phone {
       constructor(brand, price, color, size) {
           super(brand, price);
           this.color = color;
           this.size = size;
       }
       photo() {
           console.log("我可以拍照！");
       }
   }
   let zi = new SmartPhone('苹果', 4999, '黑灰色', '6.2inch');
   console.log(zi);
   zi.photo();
   zi.call();
   ```

4. **子类对父类方法的重写**

   ```javascript
   class Phone {
       call() {
           console.log("我可以打电话！");
       }
   }
   class SmartPhone extends Phone {
       photo() {
           console.log("我可以拍照！");
       }
       call() {
           super.call();
           console.log("我可以打视频通话！");
       }
   }
   let zi = new SmartPhone();
   zi.photo();
   zi.call();
   ```

5. **类中的get和set**

   ```javascript
   class Phone {
       price = 0;
       set price(price) {
           this.price = price;
       }
       get price() {
           return this.price;
       }
   }
   let ph = new Phone();
   console.log(ph.price);
   ph.price = 5000;
   console.log(ph.price);
   ```

   

