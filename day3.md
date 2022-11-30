1.XMLHttpRequest的基本使用
    XHR是服务器提供的js对象，通过它可以请求服务器上的数据源 
    可以封装出jq里面的ajax 

 1.1使用xhr发起get 请求
    创建xhr对象 调用xhr.open() -> xhr.send() 监听xhr.onreadystatechange事件
    
    创建对象
    let xhr= new XMLHttpRequest()
    
    指定请求方式和url地址
    xhr.open('get','地址')
    
    发送ajax请求
    xhr.send()
    
    监听事件
    xhr.onreadystatechange = function(){
         xhr对象的请求状态 :readyState 
         与服务器响应状态 status 
         if(xhr.readyState ===4 && xhr.status === 200){
            xhr.respenseText
            打印服务器响应回来的数据
         }
    }
     //xhr.status是数据请求的一部分

 1.2 readystate属性

     0 unsent 已被创建没调用open
     1 opened 已经调用open
     2 headers_received send()方法已被调用，响应头也已经被接受
     3 loading 数据接受中 response 已包含部分数据
     4 done ajax请求完成，意味着数据传输彻底完成/失败
    
    http://www.liulongbin.top:3006/api/getbooks?id=1 
    ?id= 1 =>这属于查询字符串

 1.3 查询字符串

    是指在url的末尾加上用于向服务器发送信息的字符串(变量)
    格式:将英文的 ? 放在url的 末尾，在加上 参数=值 加多个参数用 & 隔开
       相当于 {name:'zs',age:20} == ?name=zs&age=20

 1.4 URL编码

    只能出现英文相关的字母 标点 数字
    中文需要编码转义
    URL:使用安全的字符，去表示那些不安全的字符

  a)如果对URL地址进行编码与解码  
    encodeURL() 编码的函数
    decodeURL() 解码的函数
    里面放字符串就行了

    浏览器会自动对URL地址进行编码的操作，程序员不需要关心URL地址的编码和解码的操作

 1.5 使用xhr发起POST事件
    创建对象 调用open  使用Content-Type属性 (固定写法) 调用send函数，同时指定发送的数据 监听xhr.onreadystatechange事件
    
    xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded')
    send里面要写字符串的 写值 中间用&链接
    
    例子:

<script>    
    let xhr = new XMLHttpRequest()
    xhr.open('post','http://www.liulongbin.top:3006/api/addbook')
    xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded')
    xhr.send('bookname=小墩&author=小墩&publisher=天津出版社')
    xhr.onreadystatechange =function(){
        if(xhr.readyState === 4 && xhr.status === 200){
            console.log(xhr.responseText);
        }
    }
</script>  
2.数据交换格式

  数据交换格式就是服务器端与客户端之间进行数据传输和交换的格式
  两种数据交换 XML和JSON  
  重点学习的数据交换格式就是JSON


  web服务器  -----------   客户端 消费数据资源的    

 2.1 XML
   XML EXtensible Markup Language 可扩展标记语言 因此 XML和HTML 相似 也是一种标记语言
   HTML XML是由标签和内容组成的 也可以写属性

 a)两者的区别
   HTML是被用来设计网页上的内容 是网页内容的载体 
   XML是传输和存储设局 是数据的载体   
例子:
<note>
  <to>ls</to>
  <from>zs</from>
  <heading>通知</heading>
  <body>晚上开会</body>
</note>


 b)XML的缺点
   格式臃肿，和数据无关的代码多 体积大，传输效率低
   在js中解析XML比较麻烦

 2.2JSON
  JSON就是js对象和数组的字符串表示法，他使用文本表示一个JS对象或数组的信息 因此 JSON的本质就是字符串
  JSON是一种轻量级文本数据交换格式 比XML更小更快更容易解析
  JSON已经成了主流的数据交换格式   

  a)json的两种解构
    1)对象结构: 对象结构在JSON中表示为{}括起来的内容  数据结构为{key:value,key:value}的键值对解构，其中，key必须是使用英文的双引号包裹的字符串，value的数据类型可以是数字，字符串 布尔值，数组，对象六种类型 value不可以用function
    键值属性必须用双引号!!!必须全用双引号！！

            {
                "name": "zs",
                "age": 20,
                "gender": "男",
                "address": null,
                "hobby": ["吃饭", "睡觉", "打豆豆"]
            }
    
    2)数组解构 用[]括起来的内容 类型可以是数字 字符串 布尔值 null 数组 对象六种类型
    
        [ "java", "python", "php" ]
        [ 100, 200, 300.5 ]
        [ true, false, null ]
        [ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
        [ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]

 b) JSON语法注意事项
    1.属性名必须使用双引号包裹
    2.字符串类型的值也必须使用双引号包裹
    3.不允许使用单引号表示字符串
    4.JSON不能写注释
    5.JSON的最外层必须是对象/数组的格式
    6.不能使用undefined/函数作为JSON的值

    json的作用：在计算机与网络之间的存储和数据传输
    JSON的本质：用字符串来表示js对象数据/数组数据

  c)JSON和js对象的关系
    JSON是JS对象的字符串表示法，表示一个JS对象的信息 ，本质是字符串

    let obj = {a:'hello',b:'world'}
    let json = '{"a":"hello","b":"world"}'  外部的不是json的内部 所以不用

  d)JSON转换成js对象  JSON.parse()
    <script>
        let jsonstr= '{"a":"hello","b":"world"}'
        let obj = JSON.parse(jsonstr)
        console.log(obj);
    </script>      
​    js对象转换为JSON字符串 就使用JSON.stringify()方法
    <script>
    var json = JSON.stringify({a: 'Hello', b: 'World'})
    console.log(json)
    //结果是 '{"a": "Hello", "b": "World"}'
    </script>     

  e)序列化和反序列化
    把数据对象转换为字符串的过程，叫做序列化 例如 调用JSON.stringify()函数的操作，叫做JSON序列化
    把字符串转成数据对象的过程，叫做反序列化 例如 调用JSON.parse()函数的操作，叫做JSON反序列化

3.封装自己的Ajax的函数

 自定义一个ajax函数 接受一个配置对象作为参数，这个配置对象可以配置如下属性
 method请求类型
 url 请求的URL地址
 data 携带的数据
 success成功后的回调函数

 处理data函数，转化成字符串的格式，从而提交给服务器 提前定义resolveData
<script>
  //1.先处理一下获取的数据 然后先给他们封装函数
//     * @param {data} 需要发送到服务器的数据
//  * @returns {string} 返回拼接好的查询字符串 name=zs&age=10
function resolveData(data){
  let  arr = []
  for(k in data){
    // let str = 'k=value'
    let str = k + '=' +data[k]
    arr.push(str)
  }
  return arr.join('&')  //join是来拼接的
}
 resolveData()

//2.创建xhr对象并监听  option配置选项就相当于$.ajax方法里面的对象 比如说type data url 那些东西
function dun(options){ //options就相当于服务器传来的对象参数 就相当于dun传过来的那个对象 就是自己配置的 就像jq那样 的封装的对象
    let xhr = new XMLHttpRequest()
    //把外界传递过来的参数对象转化为 查询字符串
    let qs =resolveData(options.data)
     if(options.method.toUpperCase()=== 'GET'){
        //发送get请求
        xhr.open(options.method,options.url + '?'+qs)
        xhr.send()
    }else if(options.method.toUpperCase()==='POST'){
        //发送post请求
        xhr.open(options.method,options.url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(qs)
    }
    xhr.onreadystatechange=function(){
        if(xhr.readyState === 4 && xhr.status === 200){
            // xhr.responsText 就是json格式的字符串 转化为对象
            let result = JSON.parse(xhr.responseText)
            options.success(result) //调回去那个之前的数据 一个回调函数
        }
    }

} 
</script>
   3.5判断请求的类型 不同的请求类型，对应xhr对象的不同操作，因此需要对请求类型做if else的判断

4.XMLHttpRequest Level2

 旧版只支持文本数据的传输，无法用来读取和上传文件
 传送和接受数据时，没有进度信息，只能提示有没有完成

 4.1 新功能
    1.设置一个HTTP请求时限
    2.使用FormData对象来管理表单数据
    3.可以上传文件
    4.可以获取数据传输的进度信息

 4.2   设置一个HTTP请求时限 
   用timeout属性来设置HTTP请求的时限:
   记得new
   xhr.timeout = 3000 （单位是毫秒
   有配套事件 超时以后的timeout事件 用来指定回调函数
   xhr.timeout = function(event){
    alert('请求超时')
   }
<script>
let xhr = new XMLHttpRequest()

xhr.timeout =3000  //这里不用加if 就可以用哦
xhr.ontimeout = function(){
    console.log('请求超时了');
}
xhr.open('GET','http://www.liulongbin.top:3006/api/getbooks')
xhr.send()
xhr.onreadystatechange = function(){
    if(xhr.readyState === 4 && xhr.status === 200){
        console.log(xhr.responseText);
    }
}
</script>

  4.3FormData对象管理表单数据
    新增一个Formdata 
    let fd = new FormData()
    fd.append('uname','zs') 实际就是传数据

```
 <script>
      //1.创建一个FormData实例
      let fd = new FormData()
      //2.调用appen 追加数据
      fd.append('uname','zs')
      fd.append('upwd',123)
       let xhr = new XMLHttpRequest()
      xhr.open('POST','http://www.liulongbin.top:3006/api/formdata') //如果content type是默认值写不写都无所谓 
    //!!!content-type是请求头里面的一个属性，与之对应的是send的数据格式 ，如果是采用key=value&的这个格式，则需要修改请求头的这个属性 Form获取的数据格式不是key=value键值对的格式
    //!!!浏览器会自动设置一个合适FormData的请求头
    //!!!data在get请求写在open里面，post写在send里面 get是明文的所以才会看
      xhr.send(fd)  
      xhr.onreadystatechange =function(){
          if(xhr.readyState ===4 && xhr.status === 200){
              console.log(JSON.parse(xhr.responseText));
          }
      }
</script>  
```



    获取网页表单的值


  4.4上传文件
   1.定义ui解构 2.验证是否选择了文件 3.追加到formdata中追加文件 4.使用xhr来上传
   5.onreadystatechange事件  
<body>
        <!-- 1. 文件选择框 -->
        <input type="file" id="file1" />
        <!-- 2. 上传按钮 -->
        <button id="btnUpload">上传文件</button>
        <br />
        <!-- 3. 显示上传到服务器上的图片 -->
        <img src="" alt="" id="img" width="800"/>
<script>
    let btnUpload = document.querySelector('#btnUpload')
    btnUpload.addEventListener('click',function(){
        let files = document.querySelector('#file1').files
        if(files.length <= 0){
            return alert('请选择需要上传的文件')
        }
        let fd = new FormData()
        //将用户选择的文件添加到FormData中
        //fd.append('file',file)
        fd.append('avatar',files[0])//就是给头像传进去
       let xhr =new XMLHttpRequest()
      xhr.open('post','http://www.liulongbin.top:3006/api/upload/avatar')
      xhr.send(fd)
      xhr.onreadystatechange=function(){
          if(xhr.readyState===4 && xhr.status===200){
              let data = JSON.parse(xhr.responseText)
              // 将服务器返回的图片地址，设置为 <img> 标签的 src 属性
              document.querySelector('#img').src='http://www.liulongbin.top:3006'+data.url
          }
          else{ // 上传文件失败
                console.log(data.message)
          }
   }
  })
</script>  

4.5 显示文件的上传速度

  创建对象
  监听 xhr.upload.onprogress 事件

  e.lengthComputable  布尔值(true/false)是否具有可计算的长度
  e.loaded 已传输的字节
  e.total  需要输入的总字节
  Math.ceil(e.loaded/e.total)*100

<script>

    let xhr = new XMLHttpRequest()
    xhr.upload.onprogress=function(e){
      if(e.lengthComputable){ // e.lengthComputable 表示是否具有可计算的长度
          let percentComplete = Math.ceil((e.loaded/e.total)*100) //ceil是向上取整 e.loaded是已经传输的部分 e.total是全部的部分
      }
  }
  style.width =percentComplete+'%'
  div.innerHTML=percentComplete+'%'
  // 把上面的进度条里面的进度改成我们需要的那个进度
  //jq
      如果是jq的话就是需要attr一下 style width里面换一下 html也要换一下

  // 原生写法
  let percent = 0
  function progress(e){
      if(e.lengthComputable){ // e.lengthComputable 表示是否具有可计算的长度
      let percent = Math.ceil((e.loaded/e.total)*100) //ceil是向上取整 e.loaded是已经传输的部分 e.total是全部的部分
  }
    div.style.width=percent+'%'
    div.innerHTML=percent+'%'
  }
</script>

    上传成功之后 移除身上所有的类在添加 别的颜色 removeclass  addclass

5.jq的高级用法

  5.1 实现文件上传
    1.定义UI解构   
    <script>
    $('#btnUpload').on('click',function(){
      //files是原生的 jq对象获取的是一个数组对象
      let files = $('#file1')[0].files   //可能会支持multiple 一次性上传很多的文件 file[0]就是为了证明他有没有的
      if(files.length<=0){
          return alert('请选择图片后上传')
      }
    })
    $(function () {
    // 监听到Ajax请求被发起了
    $(document).ajaxStart(function () { //会监听文档内所有的ajax请求  因为是document监听的
      $('#loading').show()
    }
    // 监听到 Ajax 完成的事件
    $(document).ajaxStop(function () { //结束的时候就hide隐藏就可以了
      $('#loading').hide()
    }))
      var fd = new FormData()
      fd.append('avatar', files[0])
      // 发起 jQuery 的 Ajax 请求，上传文件
      $.ajax({
        method: 'POST',
        url: 'http://www.liulongbin.top:3006/api/upload/avatar',
        data: fd,
        processData: false, //不对formdata里面数据进行url编码 原样发生文件
        contentType: false, //不修改content-type的属性值 使用formdata默认的content type的值 就是再url是否添加http:// 有就false 没有就true
        success: function (res) {
          console.log(res)
        }
      })
      })
</script>

6.axios
  Axios 是专注于网络数据请求的库
  相比于原生的XMLHttpRequst对象 axios简单易懂
  axios更加轻量化 只专注于网络数据请求
     发起get属性的语法 axios.get(('url',{praram:{/*参数*/}}).then(callback)
     发起post请求的语法 axios.post（'url',{/*参数*/}.then(callback)
     直接用axios发起请求
      axios({
        method:'请求类型',
        url:'请求地址'
        data:{请求的数据 post的数据}
        params:{get的参数}
      }).then (callback)  //个人认为有点像promise
      <body>
    <button id="btn1">发动GET请求</button>
    <button id="btn2">发起POST请求</button>
    <button id="btn3">直接使用axios发起GET请求</button>
    <button id="btn4">直接用axios发送post请求</button>

```
<body>
<script>
        // axios发起get请求
        document.querySelector('#btn1').addEventListener('click', function (){
            let url = 'http://www.liulongbin.top:3006/api/get'
            let paramsObj ={name:'zs',age:18}
            axios.get(url,{params:paramsObj}).then(function(res){ //记住里面的url不带'' 因为你前面已经有了地址为啥还要给他带上呢 他就一个url
                console.log(res.data);//res有很多属性 我们只需要res.data 就是服务器响应回来的数据
            })
        })
        //发起post请求
        document.querySelector('#btn2').addEventListener('click',function(){
            let url = 'http://www.liulongbin.top:3006/api/post'
            let dataObj={location:'北京捏',address:'北平'}
            axios.post(url,{dataObj}).then(function(res){
                console.log(res.data);
                // const result = res.data log(result)
            })
        })
        //直接用axios发起get请求
        document.querySelector('#btn3').addEventListener('click',function(){
            let url = 'http://www.liulongbin.top:3006/api/get'
            let paramsData = {name:'钢铁侠',age:35}
            axios({
                method:'GET',
                url:url,
                params:paramsData,
            }).then(function(res){
                console.log(res.data);
            })
        })
        //直接用axios发送post请求
        document.querySelector('#btn4').addEventListener('click',function(){
            let url = 'http://www.liulongbin.top:3006/api/post'
            let data ={ bookname:'今天的我好困',price:6}
            axios({
                method:'POST',
                url:url,
                data:data,
            }).then(function(res){
                console.log(res.data);
            })
        })
    </script>
</body>
```


