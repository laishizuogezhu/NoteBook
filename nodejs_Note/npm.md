## npm简介

1. npm是Node Package Manager，是包管理器或者包管理系统

2. npm命令

   - npm -v            查看当前npm版本

   - npm version       查看所有模块的版本

   - npm search 包名    搜索模块包

   - npm install/i 包名 安装包

   - npm init          初始化，主要用来创建                       

     ​                  package.json 文件

   - node JS文件名      执行JS文件

   - npm remove/r 包名    删除包

   - `npm install/i 包名 --save`

      `安装包并添加到依赖中`

   - npm install       下载当前项目所依赖的包

   - npm install 包名 -g  全局安装包（一般都是  

      ​                    一些工具）

   - cd 文件夹名称         进入文件夹

3. 如果没有package.json文件，包可能会安装不成功

4. npm是国外的，服务器在国外，下载包会很慢 

5. 镜像服务器，就是在自己国内安装一个服务器，然后把国外服务器上的信息都下载，搬到自己的服务器上  

6. 通过npm下载的模块，不用写路径，直接写模块名

7. node在使用模块名引入模块时，他首先会在当前目录下的node_modules中寻找是否有此模块，如果有则直接使用，否则去上一级目录寻找，直到找到磁盘的根目录，没有则报错

## 配置cnpm

1. 安装cnpm

   ```
   npm install -g cnpm --registry=http://registry.npm.taobao.org
   ```

   

