1. 模块在第一次加载后会被缓存。这也意味着多次调用 require() 不会导致模块代码被执行多次。
2. 内置模块的加载优先级最高
3. 使用 require() 加载自定义模块时，必须指定以./或../开头的路径标识符，否则会被node当作内置模块或者第三方模块加载
4. 使用 require() 导入自定义模块时，如果省略了文件扩展名，则nodejs会安装顺序分别尝试加载以下文件：
（1）安装确切的文件名进行加载
（2）补全.js扩展名进行加载
（3）补全.json扩展名进行加载
（4）补全.node扩展名进行加载
（5）报错


第三方模块加载机制：
如果传递给 require() 的模块标识符不是一个内置模块，也没有./ 或../开头，则会从当前的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块；如果没有找到，则会移动到再上一层父母录中进行加载，直到文件系统的根目录。


目录作为模块：
当把目录作为模块标识符，传递给 require() 进行加载时，有三种方式
（1）在被加载的目录下查找 package.json 文件，并寻找 main 属性，作为 require() 加载路径
（2）如果目录中没有 package.json 文件，或者 main 属性不存在，则会试图加载目录下的 index.js文件
（3）上面两步失败， 报错