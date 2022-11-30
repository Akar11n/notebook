1.了解同源和跨域
 
 1.1 同源策略
    1.什么是同源
      如果两个页面你的协议，域名，和端口都相同 则两个页面具有相同的源 如果没写数字就默认80

        例如，下表给出了相对于 http://www.test.com/index.html 页面的同源检测：

            URL	是否同源	原因
        http://www.test.com/other.html	是	同源（协议、域名、端口相同）
        https://www.test.com/about.html	否	协议不同（http 与 https）
        http://blog.test.com/movie.html	否	域名不同（www.test.com 与 blog.test.com）
        http://www.test.com:7001/home.html	否	端口不同（默认的 80 端口与 7001 端口）
        http://www.test.com:80/main.html	是	同源（协议、域名、端口相同）

    2.什么是同源策略 Same origin policy
     同源策略是浏览器提供的一个安全功能
     限制了同一个源加载的文档和脚本如何与来自另一个源的资源进行交互
      A网站的JavaScript 不能和非同源的网站C之间的自愿交互
       无法读取cookie localstorage indexedb
       无法读取 DOM ajax    

 1.2跨域

    同源指的是两个的URL的协议 域名 端口一致 反之就是跨域
    出现跨域的根本原因 浏览器的同源策略不允许非同源的url之间进行资源的交互

    2.对跨域请求的拦截
     存在跨域问题 
     跨域请求可以正常发起 ---> 服务器处理请求 ------>浏览器能正常接受到跨域相应的数据 ---->先被同源策略所拦截

    3.实现跨域数据请求 
    两种解决方案 JSONP 和CORS
    JSONP 兼容性好 缺点是只支持GET请求，不支持POST请求
    CORS 官方解决的方案，支持post get 不兼容低版本浏览器

2.JSONP
  JSONP(JSON with Padding) 是JSON的一种使用模式 可用于解决主流浏览器的跨域数据和访问的问题
  script标签不受浏览器同源策略的影响 可以通过src 来请求非同源的js
  通过函数调用的形式 接受跨域借口相应过来的数据
    //之前的都已经社配好的当前可以跨域

  2.1自己实现一个简单的JSONP
      在页面中 无论定义多少个script标签，他们里面的代码都是共享的 
<body>
    <script>
        function success(data){
            console.log('打印一个data数据');
            console.log(data);
        }
    </script>
    <script>
        success ({name:"zs",age:10})
    </script>
</body>
      在外面定义一个.js 然后用script src = 地址 如果函数不是一个地址  在后面?callback=success=abc 回调函数的名字是success
    abc({name:'困困',age：18})
     
    定义一个success回调函数 再通过success标签请求JSONP的接口
    ?callback=success&name=zs&age=10

    只支持GET数据请求 不支持POST数据请求
    !!!JSONP是src属性 他跟AJAX没有任何关系 不能把JSONP请求数据方式叫做Ajax 因为JSONP没有用到XMLHttpRequest

 2.2JQ中的JSONP
    $.ajax({
        url:地址 后面?name=zs&age=20
        dataType:'jsonp'
        success:function(res){
            log(res)
        }
    })             
    查找jsonp  Network中的js

    ajax不能跨域 Ajax通过jsonp来进行跨域
    默认情况下 JQ发起jsonp请求会自动携带一个callback =Jquery的参数 是随机生成的一个回调函数名称
    函数名只跟你本地定义的有关 跟服务器没关系 服务器会根据函数生成对应函数调用，并携带data参数返回到一个页面上然后调用对应方法 success不是函数名啊喂！！

 2.3自定义函数参数及回调函数名称  一般不会修改服务器名称
    callback这个很乱 很随机生成的 如果想自我定义的话通过两个参数来指定
    
    //发送到服务器的参数名称，默认值为callback
    jsonp:'callback', 默认callback   发送到服务器端参数的名称 把里面换名字

    //自定义回调函数名称，默认值为JQxxx格式
    jsonCallback:'abc',  这个是jsonp里面的那个后面=的值

                jq把success放在回调函数里面了

  2.4 jq中发起ajax请求原理
    动态创建和动态移除
       在发起jsonp请求的时候 向header中append一个script标签
       在请求成功后再移除刚才append加进去的script标签
<body>
<button id="btnJSONP">发起JSONP数据请求</button>

<script>
    $(function () {
        $('#btnJSONP').on('click', function () {
        $.ajax({
        url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?address=北京&location=顺义',
        dataType: 'jsonp',
        jsonpCallback: 'abc',
        success: function (res) {
        console.log(res)
          }
        })
      })
    })
  </script>
</body>

   2.5什么是防抖
    防抖策略(debounce)是当事件被触发后，延迟n秒在进行回调，如果在这n秒内事件又被触发  则重新计时  ps:感觉跟定时器还是不一样哦  就像那种自动回城B

    防抖应用的场景  
        用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源

   实现防抖的步骤
    1.防抖动的timer timer=null  settimeout来做
    2.定义防抖的函数
    3.在触发keyup事件时，立刻清空timer cleartimeout 再调用这个函数
  1.定义演示器的id
  let timer = null 
  function debounceSearch(kw){
    timer=settimeout (function(){
      getSuggestList(kw)
    },500)
    触发keyup的时候清空timer 
    在调用debounceSearch
  }

    2.6根据缓存来弄 因为你搜索两个Apple 他占两个格子 还不如缓存看只有一个对象
       当用户输入的内容当做键 将数据作为值 进行缓存

    2.7节流
     节流(throttle),减少一段时间内事件触发的频率 技能cd
     应用场景
        连续不断触发某时间但只会在单位时间内触发一次
        懒加载时要监听计算滚动条的位置，但不必要每次滑动都触发，可以降低计算的频率而不必去浪费cpu的资源

    2.8 节流阀的概念
    节流阀为空 可以执行下一次操作 不为空 不能执行
    操作完之后 必须重置节流阀为空 表示可以执行下一次操作
    settimeout是延迟启动 setinterval是周期启动


    防抖和节流的区别
      如果事件被频繁触发 防抖只有最有一次触发生效
      节流是减少事件触发的频率 有选择性执行一部分
