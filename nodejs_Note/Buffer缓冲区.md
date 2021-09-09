## Buffer缓冲区

1. buffer结构与数组类似，操作方法也类似

2. 数组不能存储二进制数据，而buffer是专门用来存储二进制数据的

3. buffer的元素是16进制的两位数

4. 一个元素就是内存中的一个字节

5. 使用buffer不需要引入模块，直接使用即可

   ```javascript
   var str = "hello hahaha";
   //将一个字符串保存到buffer中
   var buf = Buffer.from(str);
   //<Buffer 68 65 6c 6c 6f 20 68 61 68 61 68 61>
   console.log(buf);
   console.log(buf.length);
   //12个字节，占用内存的大小
   console.log(str.length);
   //12 字符串的长度
   //英语字符在内存中占用一个字节，中文字符占用三个字节
   var str1 = "hello 赵晓明";
   var buf1 = Buffer.from(str1);
   console.log(buf1.length);//15
   console.log(str1.length);//9
   ```

6. 在buffer中存储的都是二进制数据，但是是以16进制形式显示的

7. 创建一个指定大小的字节

   ```js
   var buffer3 =  new Buffer(10)//10个字节的buffer
   console.log(buffer3.length);
   ```

8. buffer所有构造函数都已经被废弃，不推荐使用

9. Buffer.alloc

   ```js
   const buf4 = Buffer.alloc(10);//10字节
   console.log(buf4.length);//10
   buf4[0] = 88;//58
   buf4[1] = 255;//ff
   buf4[2] = 0xaa;//aa
   buf4[10] = 15;//不会显示，但是也不会报错
   buf4[3] = 256;//还是显示00
   buf4[4] = 556;//2c
   //556转为二进制1000101100，然后去后面8位
   //00101100 -> 2c
   console.log(buf4[0]);//88
   console.log(buf4[0].toString(16));//58
   console.log(buf4[0].toString(2));
   //1011000
   ```

10. **buffer的大小一旦确定，就不能修改，实际上是对底层内存的操作**

11. 只要数字在控制台或页面输出一定是10进制