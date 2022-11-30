1.客户端和服务器

    1.1服务器的概念:上网过程中，负责存放和对外提供资源的电脑，叫做服务器
    1.2客户端的概念:负责获取和消费资源电脑叫做客户端

2.URL地址

    URL地址:统一资源定位符，只有通过URL地址 才能正确定位资源存放的位置，从而成功访问到对应的资源
    URL例子 : http  :// www.baidu.com  
             通信协议 -   服务器名称     具体的存放位置  
    由三部分组成 1 客户端与服务器之间的通信协议 2 存有该资源的服务器名称 3 具体存放的位置

3.客户端与服务器的通信过程

    客户端请求服务器  
    服务器处理资源请求  1.接收到请求 2.处理资源请求 3.找到的资源发送给客户端
    服务器响应客户端  
    
    网页中的每一个资源 都是通过这个 客户端与服务器的通信过程，分为请求 处理 响应三个步骤
    
    3.1 打开Chrome浏览器 F12 network header response看到响应的

4.服务器对外提供了哪些资源

    4.1数据也是对外提供的资源
    
    4.2网页如何请求数据 资源 :请求 处理 响应 的方式来获取
        在网页上请求服务器的数据资源，需要XMLhttpRequest对象(XHR)是浏览器提供的js成员
        let xhrObj = new XMLHttpRequest()
    
    4.3资源的请求方式 get 和 post 请求
        get请求 获取服务器资源(向服务器要资源) 比如 HTML文件 css js 那种
        post请求 向服务器提交数据(向服务器发资源) 数据提交操作
5.Ajax 
    5.1 ajax实现网页与服务器之间的数据交互
    用户   ->交互->  网页  -> 数据传输-> 服务器

    5.2 应用场景 检测用户名是否被占用 先查重 返回你一个结果 然后提示你 //正则而是说这个名称符合不符合规范 而不是你重复不重复数据
                根据页码动态刷新表格的数据 
                增删改查的操作 都需要用ajax的形式来进行数据的交互
    
    **需要数据的传输就一定会用到Ajax     

6.JQ中的Ajax
   6.1三种方法：$.get()获取数据   $.post()提交数据  $.ajax() 两者都可以

   6.2 a)$.get()

        $.get(url,[data],[callback]) //中括号是[可选参数]
    
        参数名      参数类型  是否必选   说明
        url         string     是       要请求的地址资源
        data        object     否       要携带的参数
        callback   function    否       请求成功后的回调函数
    
       b) $.get() 不带参数的请求
        url地址和回调函数就行
        $.get('http://www.baidu.com',function(res){console.log(res)})
    
        <body>
        <button id="btnGET">发起不带参数的get请求</button>
        <script>
        $(function(){  //这个就是属于 给function(){} 
            $('#btnGET').on('click',function(){ //里面不需要直接获取 直接拿id就能获取 然后onclick function
                $.get('http://www.liulongbin.top:3006/api/getbooks', function (res) { //res代表服务器回来相应的数据
            console.log(res)})
            })
        })
        </script>
        </body>

   6.3 $.post()函数的语法

         $.post(url,[data],[callback]) //中括号是[可选参数]
    
            参数名      参数类型  是否必选   说明
            url         string     是       要请求的地址资源
            data        object     否       要携带的参数
            callback   function    否       请求成功后的回调函数
    
        $(function () {
            $('#btnPOST').on('click', function () {
            $.post('http://www.liulongbin.top:3006/api/addbook', { bookname: '简爱', author: '施耐庵', publisher: '天津图书出版社' }, function (res) {
            console.log(res)
            })
        })
        }) 

   6.4 $.ajax()函数用法
        $.ajax({
            type:'',//请求的方式 例如 GET POST
            url:'',//请求的url地址
            data:'',//请求要携带的数据
            success:function(res){}  //请求成功后的回调函数
            })

        get请求
    
        $(function(){
            $('#btnGET').on('click',function(){
                $.ajax({
                    type:'GET', //大小写都可以
                    url:'http://www.liulongbin.top:3006/api/getbooks',
                    data:{id : 1},
                    success:function(res){
                        console.log(res);
                    }
                })
            })
        })
        把刚刚的get改成post
        
         $(function () {
        $('#btnPOST').on('click', function () {
          $.ajax({
            type: 'POST',
            url: 'http://www.liulongbin.top:3006/api/addbook',
            data: {
              bookname: '史记',
              author: '司马迁',
              publisher: '上海图书出版社'
            },
            success: function (res) {
              console.log(res)
            }
          })
        })
      })


7.接口

  7.1 接口的概念

    使用ajax请求数据的时候，被请求的url地址，就叫做数据接口(接口)，每个接口必须有请求方式
    
    例如:'http://www.liulongbin.top:3006/api/getbooks' 获取图书列表的接口
        'http://www.liulongbin.top:3006/api/postbooks' 添加图书的接口

  7.2 通过get方式请求接口的过程

    用户 <-交互> 网页 ajax载体 ——>发送post请求 客户端 ——>响应给post请求 给ajax 网页

  7.3接口测试工具
    不写代码也可以对接口进行调用和调试 postman
    get请求
    选择请求方式， 然后填写url地址
    ?用这个来添加 例如 ?id=1 查找id为1的

    post请求 可以填完地址再body里面填写
    然后点击x-www-form-urlencoded
  7.4接口文档
    接口的说明文档 它是我们调用接口的依据， 包含 url 参数 输出内容的说明
    参考接口文档就可以知道接口的作用和接口的调用
    1.接口名称:用来标识各个接口的简单说明
    2.接口url
    3.调用方式:post /get
    4.参数格式:参数名称 参数类型 是否必选 参数说明
    5.相应格式:数据名称 数据类型 说明
    6.返回示例(可选): 通过对象的形式，例举服务器返回数据的结构
    
8.案例-图书管理
​	   用css库 bootstrap.css
    js jq .js
    vscode bootstrap 3 Snippets

机器人接口http://www.liulongbin.top:3006/api/robot能用
机器人对应的语音接口http://www.liulongbin.top:3006/api/synthesize

资料里机器人接口失效解决方法:
打开文件chat.js
getMsg(text)里的url换成 http://www.liulongbin.top:3006/api/robot
getVoice(text)  里的语音url换成 http://www.liulongbin.top:3006/api/synthesize


