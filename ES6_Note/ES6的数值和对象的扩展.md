## ES6的数值扩展

### Number的最小精度

1. Number.EPSILON是JS表示的最小精度

```javascript
console.log(0.1 + 0.2 === 0.3);//false
function equal(a, b) {
    if (Math.abs(a - b) < Number.EPSILON) {
        return true;
    } else {
        return false;
    }
}
console.log(equal(0.1 + 0.2, 0.3));//true
```

### 进制表示

1. `0b`表示二进制
2. `0o`表示八进制
3. `0x`表示十六进制

```javascript
let b = 0b1010;
let o = 0o777;
let x = 0xff;
let s = 100;
console.log(b);//10
console.log(o);//511
console.log(x);//255
console.log(s);//100
```

### Number.isFinite

1. 这个主要用来检测一个数值是否为有限数

```javascript
console.log(Number.isFinite(100));//true
console.log(Number.isFinite(100 / 0));/false
console.log(Number.isFinite(Infinity));//false
```

### Number.isNaN

1. 主要用来检测一个数值是否为NaN

### Number.parseInt和Numbe.parseFloat

1. 将一个字符串转换为整数或者浮点数

```javascript
console.log(Number.parseInt('455love'));
//455
console.log(Number.parseFloat('3.234深浅'));
//3.234
```

### Number.isInteger 判断一个数是否为整数

### Math.trunc 将数字的小数部分抹掉

### Math.sign 判断一个数到底为正数 负数 还是零

1. 正数返回 1 ，负数返回 -1 ，零返回 0

## 对象方法扩展

### Object.is 判断两个值是否完全相等

```javascript
console.log(Object.is(NaN, NaN));//true
 console.log(NaN === NaN);//false
```

`Object.is `的作用与 `===`类似，但是不同的是针对NaN有不同的作用

### Object.assign 对象的合并

```javascript
const config1 = {
    host: 'localhost',
    user: 'root',
    password: '123abc',
    port: 3306,
    test: 'test'
}
const config2 = {
    host: '127.0.0.1',
    user: 'root',
    password: '123abc',
    port: 8000,
    test2: 'test2'
}
console.log(Object.assign(config1, config2));
```

> 两个对象的合并，如果有相同的项，那么第二个参数会将第一个参数的项进行覆盖，其他不同的项，都会合并成一个对象内的属性

### Object.setPrototypeOf 设置原型对象

### Object.getPrototypeOf 获取原型对象

```javascript
const school = {
    name: '希望小学'
}
const area = {
    name: ['广州', '深圳', '上海', '北京', '浙江']
}
Object.setPrototypeOf(school, area);
console.log(school);
console.log(Object.getPrototypeOf(school));
```

