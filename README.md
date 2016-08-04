## 一个项目运行前所必须的配置

```
git clone 项目地址；
```
把项目整个拿到本地，放到xampp的htdocs下，项目文件夹命名为rent

此时直接在地址栏里输入localhost/rent就能访问整个项目

C:/windows/System32/drivers/etc

可以在上述路径下找到hosts文件

```
127.0.0.1       localhost
```
127.0.0.1是本机ip地址，这句话就说明localhost和127.0.0.1是等价的。

同样的可以设置127.0.0.1为别的地址，比如dev.m.daba.cn

```
127.0.0.1       dev.m.daba.cn
```
此时输入dev.m.daba.cn/rent就可以直接访问项目
### fis的安装
fis3安装之前确保已经安装了node和npm ,然后执行下面的指令
```
npm install -g fis3
```
### 如何用fis编译

```
fis3 release -r <path>
```
指定需要编译的项目根目录

```
fis3 release  -d <path>
```
指定编译产出到的特定目录

```
fis3 release -w
```
启动文件监听，当文件变化时会编译发布变化了的文件以及依赖它的文件。

命令也可以合并 直接用一个命令行就可以完成以上三个功能

```
fis3 release -r <path> -d  <path> -w
```
- 栗子
A/B/C
我们在B里执行fis3指令，根目录指定为C，编译后的文件放在A里，启动文件监听

```
fis3 release -r C -d ../A -w
```

### Apache 配置 http.conf
**apache配置严格区分大小写**
Apache 基本配置：\xampp\apache\conf

```
ServerRoot "C:/xampp/apache"
```
- Apache软件安装的位置，其他指定目录如果没有指定绝对路径，则目录相对于该目录。

```
Listen 80
```
- 服务器端监听的端口号。


```
ServerName localhost:80
```
- 主站点名称

```
DocumentRoot "C:/xampp/htdocs"
```
- 默认情况下，所有的请求都从这个目录中取的，所以需要把整个项目放在此目录下。

```
<Directory "C:/xampp/cgi-bin">
    AllowOverride All
    Options None
    Require all granted
</Directory>
```
- AllowOverride :允许存在于.htaccess文件中的指令类型（.htaccess 是对于系统目录设置各种规则权限的文件，一般放在根目录中）All:在.htaccess文件中可以使用所有指令。
- Require all granted 允许所有的访问。不加这句话会报403错误。
- options:None 没有任何额外权限。

```
LoadModule
LoadModule rewrite_module modules/mod_rewrite.so
```
- 加载相关模块

```
ErrorLog logs/error_log
```
- 错误日志的保存位置

`<IfMOdule>`,作用于模块，首先判断模块是否被载入，然后再进行处理。

