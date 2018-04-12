
node-day1:

// 在文件中打印this不是global属性，node自带模块化功能 一个js文件就是一个模块，模块this不是global （闭包）

// process 进程 设置环境变量
process.env.NODE_ENV == 'dev'

// 异步的，在当前队列的底部
process.nextTick(function ()

// 第二个队列中的
setImmediate( ()=> {

setTimeout((...args)=> {

// 形参（剩余运算符） 将剩余的内容放到一个数组中,args中['吃饭']
// 拓展运算符 展开运算符

// this指向的是timeout自己,箭头函数中没有this指向没有arguments

// exports导出
// require引用 导入
// module 代表当前模块
// __filename当前的文件的绝对路径
// __dirname 当前的文件夹的目录的绝对路径

// node基于规范commonjs 文件的读写，node天生自带模块化
// 1.定义如何创建一个模块 一个js文件就是一个模块
// 2.如果使用一个模块 require 你要使用一个文件只需要require一个文件
// 3.如何导出一个模块 exports / module.exports


// require方法具有缓存功能，多次引用只执行依次

// 调用写好的方法
// 如果自己写的文件 要通过./的方式，文件模块,如果是js，node，json后缀可以省略，他会自动添加.js .json .node依次匹配
// 如果异步方法一般会有回调函数

## nodejs
- 主线程是单线程(异步)callback，将后续的逻辑写成函数，传入到当前执行的函数中，当执行的函数得到了结果后，执行传入的函数(回调函数)
- 五个人同时吃一碗饭(异步)
- 阻塞不能异步（阻塞是针对内核说的）
- i/o操作 读写操作，异步读写（能用异步绝不用同步）
- event-driven 事件驱动（发布订阅）

//util 工具模块 核心模块/内置模块，不需要安装直接使用

// util.inherits
// util.isArray,isFunction
// util.promisify 把方法转化成promise

// fileSystem 文件系统

// promise 用法，promise的实例就具备了then方法
let read = util.promisify(fs.readFile); // 把一个函数promise化

read('./2.es6.js','utf8').then(


### 全局安装 -g (只能在"命令行"中使用) 默认的安装路径是(npm root -g) 不会自动加入环境变量中 而是通过npm进行映射

npm install nrm -g 安装nrm
nrm test 测试链接时间
nrm ls 显示所有的可用源
nrm use 源的名字 使用源
npm uninstall nrm -g 卸载nrm


### 本地安装
- 没有-g参数，安装之前需要初始化,记录安装依赖的

npm init -y

> package.json，目录不能有中文，特殊字符，大写，默认先找当前目录下的package.json，如果当前木没有会去上级查找，找不到才认为在当前目录下安装


#### 项目依赖
- 开发时使用，上线还需要
```
npm install jquery@1.8.3
npm uninstall jquery
```

#### 开发依赖
- 开发时使用，线上不使用
```
npm install less --save-dev
npm uninstall less --save-dev

## yarn安装
- npm install -g yarn (回家要安装)
```
yarn init
yarn add 包
yarn remove 包 删除包
yarn add less --dev 安装开发依赖
yarn install 安装依赖包


// 第三方模块不需要./的形式引入 可以直接通过包名将文件引入,找package.json中的main对应的文件运行,如果当前目录下没找会像上一级查找，找到计算机的根目录为止


......................................................................................................................................

node-day2:

## buffer（16进制）
## 字节
- 1024b = 1k
- 8bit(8个二进制) = 1b
- 1个汉字(3个b)
- 1个字节转化成十进制是255
- 1个字节最大转换成16进制是ff

// 1.通过长度创建

Buffer.alloc(100); // 相对这种方法比较耗性能
Buffer.allocUnsafe(100);

Buffer.from([17,18,19,0x11]);// 会自动把10进制转化成16进制

buffer.slice(0,1); // 拷贝出来的存放的是内存地址空间

buf1.copy(buf,0);
targetBuffer目标buffer, targetStart目标的开始, sourceStart源的开始, sourceEnd源的结束 this.length

//1.把16进制转化成2进制 toString()
(0xe7).toString(2)

//2.将这些值转化成10进制 去可见编码中取值 parseInt
parseInt('00111001', 2)


// fileSystem 文件系统 文件的读写
let fs = require('fs');
// 既有同步又有异步方法，异步有callback

// 同步的读取
// 1.读取文件 文件必须存在。不能通过/读取内容 /表示的是根目录
// 2.读取的默认类型是buffer

fs.readFileSync('3.fs.js','utf8');


// 异步的方案 会导致回调地狱，不方便维护

fs.readFile('./1.txt','utf8',function (err,data) { // err错误第一

//如果第一个promise中返回了一个promise实例，会把当前执行的结果传到下一个then中

  // 如果你返回的不是promise 会把结果结果继续向下传递

  // 处理错误,如果写了错误callback走自己的，没写同一走catch

// await后面只能跟随promise 终极解决方案
async function result () {
    let content1 = await read('./1.txt','utf8')
}
result();

// 调用all方法后 会返回一个新的promise的实例
async function result() {

await Promise.all([read('x.txt','utf8'),read('y.txt','utf8')]);

// promise解决的问题 1.回调地狱 2.合并异步的返回结果 3.async，await 简化promise写法的 （语法糖）

//1.回调地狱 链式写法then
//2.解决同步异步的结果 Promise.all，如果都成功才算成功，有一个失败了就失败了,Promise.race(),谁快以谁为准，得到结果以后就结束了


// Promise类上拥有两个方法可以把结果保证成promise对象 reject resolve（上来就失败或者成功）

Promise.reject('123').then(function (data) {

// 如果程序 只开始执行一次 可以同步。readFile会把内容读到内存中，用这种方式会导致淹没可用内存。

// 读取都是类型都是buffer 写入的时候utf8
// 读取的文件必须存在，写的时候文件不存在会自动创建，里面有内容会覆盖掉
// 默认会调用toString方法

fs.writeFile('1.txt','{name:1,age:2}',function (err) {

fs.writeFile(target,data,callback)

fs.stat('/',function (err,stats) {
    if(err){/!*文件不存在*!/}
    console.log(stats.isFile()); //判断是不是文件
    console.log(stats.isDirectory()); // 判断是不是文件夹
});

fs.mkdir(p,function (err) {
创建文件夹


// 拼一个路径出来
path.join(__dirname, './a','./b')

// 解析一个绝对路径出来
path.resolve('./a','./b')

let EventEmitter = require('events');

// removeListener once on emit


// 流 可读流和可写流
// 流：边读边写 不是疯狂的读

// highWaterMark 每次能读取多少 默认64k我们默认不需要更改
// 读取默认时buffer类型
let rs = fs.createReadStream('1.txt',{highWaterMark:1});

// 需要监听事件 数据到来的事件 rs.emit('data',数据);
// 默认叫非流动模式 => 流动模式

 rs.pause(); // 暂停 暂停是on('data')的触发

rs.resume(); // 恢复data事件的触发

rs.on('data',function (chunk) { chunk读取的数据

// 默认data事件是不停的触发，直到文件中的数据全部读出来

rs.on('end',function () {

rs.on('err',function (err) {
    // 文件不存在 错误

// on('data') on('err') on('end') resume() pause()
// http 增删改查 fetch


。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。

node-day3:


// 可写流 默认要占用16384 = 16k

fs.createWriteStream('./1.txt',{highWaterMark:2});

// 可写流有两个方法 write end

var flag = ws.write(1+''); // 可写流来些数据必须时字符串类型或者buffer类型

ws.end('吃饱了'); // end调用后会把所有的write中的内容以最快速度写入文件

//ws.write(1+''); //write after end 调用end后不能在用write

ws.on('drain',function () { // 当读入的文件 全部写入后 就恢复读取

rs.pipe(ws); // 可读流.pipe(可写流),会自动调用write和end方法



http.createServer((req,res)=>{ // 监听函数，当请求到来时会执行回调函数

// req代表的是客户端 他是一个可读流
    // res代表的是服务端 他是一个可写流

 res.setHeader('Content-Type','text/plain;charset=utf8');
    res.end('你好');//调用end后结束响应


.listen(port,()=>{
// 端口号尽量使用3000以上端口

<!--不支持../路径 ./路径-->
  <link rel="stylesheet" href="/index.css">


// 跨域：协议 端口号 域名 有一个不相同就是跨域

// fetch 基于promise的


 res.setHeader('Content-type','text/html;charset=utf-8');
    fs.createReadStream('index.html').pipe(res)

url.parse(req.url,true); // true的作用是将query转化成一个对象

//实现类型转化
mime.getType(pathname)

stats.isFile()){ // /index.css  /index.js /index.html
            res.setHeader('Content-Type',mime.getType(pathname)+';charset=utf8');


<!--jsonp script没有跨域的问题  jsonp和ajax json jsonp 没关系-->

// 必须是一个全局函数
 oScript.src = 'http://localhost:3000/jsonp?cb=c';

 if(pathname === '/jsonp'){
        res.end(`${query.cb}(1)`);


  fetch('/user',{
       method:'POST',
       body:JSON.stringify( )

 fetch(`/user?id=${id}`,{
         method:'DELETE'


ajax:跨域：
xhr.open('PUT','http://localhost:5000/clock',true);

res.header("Access-Control-Allow-Origin", "*");

 if(req.method === 'OPTIONS'){
        res.end();
    }

 if(pathname === '/clock'){




..............................................................................................................
node-day5:

let express = require('express');
// 引用express模块,express是一个函数

let app = express(); //express函数执行后，返回的是一个http的监听函数,就是http.createServer中的函数

// 在此函数上扩展了一个listen可以监听端口

// app.listen就是基于以前封装的
app.listen(8080);

// app监听函数上 扩展了很多方法 包括get post delete put,RESTful风格中的动词
// app.方法名('路径名',fn)
// 从上到下匹配如果匹配到了并且结束响应 就不会继续向下走
// 路径指的是pathname 没有问号后面的内容
// express 重点 扩展req和res的属性

// all表示所有的方法 * 表示所有的路径，一般放到最后
app.all('*',function (req,res) {

req.query.id; // express扩展的属性

req.url; // 获取整个路径包括问号的

req.path; // express扩展的属性
req.headers);// 所有的都是小写
req.method); // 请求的方法，所有的方法都是大写的

// 表示id是占位符 必须有 但是可以随机
// /user/1/2 => {id:1,name:2} = params 一一对应的关系
app.get('/user/:id/:name/a',function (req,res) {

req.params.id

// 拦截功能 在这里的req和res都是同一个
// 当调用next后 可以继续向下执行

app.param('id',callback(req,res,next) )

//调用了next就可以向下匹配,如果在这里结束了请求那就不走了(res.end())

// 中间件 当我们访问到最终目标之前执行的内容

//1.中间件的第一个功能 可以进行权限判断
//2.可以进行对req和res的属性进行扩充
//3.中间件放在要执行路径的上面
//4.中间默认情况下都匹配，可以指定匹配什么开头的

app.use('url',callback (req,res,next))

// 错误中间件拥有四个参数 fn.length == 4

app.use(callback(err,req,res,next))


let end = res.end;
res.end =fn;
res.end('water'); // 装饰模式

// 不能直接返回对象 res.json() // 返回json的
// 返回html页面 res.sendFile() // 返回文件
// res.statusCode res.end => res.sendStatus();
// res.end() res.header();  => res.send();

 // 不能通过../查找(root是不支持的)想读取到确切的文件 用path模块进行拼接即可

res.sendFile(require('path').join(__dirname,'..','index.html'));

// 解析表单格式 把表单内的数据 解析后放在req.body上

// 解析json格式 把json字符串转化成对象 解析后放在req.body上
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended:false}));

路由：
1 let router = express.Router(); // 创建一个路由池子

2 router.get('/login',callback(req,res))

3，module.exports = router;

4，let user = require('./routes/user');

5，app.use('/user',user);

// 告诉他页面上所有render方法中的html 都用ejs模板来渲染
app.engine('html',require('ejs').__express);
// 更改模板路径,默认叫views
app.set('views','static');
// 配置默认模板后缀名字
app.set('view engine','html');

<!--引用某个模板-->
<%include ../header.ejs%>

<!--取值表达式-->
<h1><%=username%></h1>

<!--js语法-->
<%arr.map((item)=>{%>
    <li><%=item+1%></li>
<%})%>

<!--转译html-->
<%-html%>

 console.log(require('querystring').parse(str)); // node自带的模块（解析路径参数）

处理静态文件：
app.use(express.static('dist'));
app.use(express.static('public'));

重定向：
 res.redirect('http://www.zhufengpeixun.cn')

++++++++++++++++++++++++++++++++++++++++++++++


## express搭建服务
```
let express = express();
let app = express();
app.listen(8080);
```

## express路由
- 必须method和path全都匹配上执行对应的callback
```
app[method](path,function(){});
app.all('*',function(){})
```

## 路径参数路由
- 将匹配到的结果生成一个对象放到req.params上
```
app.get('/user/:id/name')
```

## req上的属性
```
req.params 路径参数
req.url 整个的路径
req.path pathname路径
req.headers 请求头
req.method 请求的方法
req.query 获取请求的参数 问号后面的参数
```

## middleware
- 中间件的作用
    - 处理公共逻辑,扩展req,res
    - 可以决定是否继续执行
    - 开头匹配到就会执行中间件
    - 错误中间件，在页面的最后，参数是4个，第一个参数中是错误

## res新增的方法
- res.json()
- res.sendFile() 绝对路径 path.join/ path.resolve
- res.sendStatus();
- res.send();

## 用户管理模块
- 登陆 /login
- 注册 /reg
## 文章管理模块
- 发表文章 /post
- 删除文章 /delete

## 路由拆分
```
let express = require('express');
let app = express();
let router = express.Router();
router.get('/login',fn)
app.use('/user',router);
```

## bodyParser
```
app.use(bodyParser.json()); // 解析json application/json
app.use(bodyParser.urlencoded({extented:true})); // 解析表单 application/x-www-form-urlencoded
```

## ejs（前后端分离不使用ejs）
```
app.set('view engine','html');
app.set('views','static');
app.engine('html',require('ejs').__express);
res.render('index',渲染的数据)
```
- ejs用法
```
<%include '文件名'%>
<%=变量%>
<%-转义变量%>
<%for(var i = 0; i<10;i++){%>
    <li><%=i%></li>
<%}%>
```

## 静态服务中间件
```
app.use(express.static('文件夹'))
```

## 重定向
```
res.redirect('路径');
```
