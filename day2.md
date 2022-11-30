这是第二天的笔记(＾U＾)ノ~yoho

1 form表单的基本使用

 1.1什么是表单
 表单在网页中主要负责 数据采集 功能，html的form标签就是用于采集用户输入的信息，并通过form表单的提交操作，把采集到的信息提交到服务器端进行处理
 
 1.2表单的组成部分
    表单标签 form
    表单域 input text password 就比如 文本框 密码框 隐藏域 多行文本框 复选框 单选框 下拉选择框和文件上传框
    表单按钮!! btn sumbit

 1.3 form标签的属性 
    form标签的属性是用来规定如何把采集到的数据发送给服务器


    属性                            值                             描述
    action                       url地址                    提交表单时，向何处发送数据表单

    method                       get/post                   用哪种方式把表单数据提交到action URL

    enctype                      application/               规定在发送表单数据之前如何对其进行编码
                                x-www-form-urlencoded
                                multipart/form-data 
                                text/plain   

    target                      _blank 新窗口 _self默认  _parent 父级          规定在何处打开action URL
                                _top整个窗口  framename指定的框架 


   1.当form表单没有指定action属性值的情况下，action的默认值为当前页面的url地址 就好比你输入form的各种数据他会在后面提示出来
       提交表单后，页面会立马跳转到action的那个地址

   2.target  在何处打开 默认属性_self 在相同的框架中打开actionURL
        _blank	在新窗口中打开。
        _self	默认。在相同的框架中打开。
        _parent	在父框架集中打开。（很少用）
        _top	在整个窗口中打开。（很少用）
        framename	在指定的框架中打开。（很少用）


   3.method属性 以何种方式把表单提交给action URL      
    最好把method添加给post 因为这样更加的安全一点
    post方式适合提交大量的复杂的 文件上传的数据
    get适合提交少量的 简单的数据

   4.enctype 默认值application/x-www-form-urlencoded 发送数据之前编码所有的字符串
                multipart/form-data 不对字符编码 上传控件的表单时，必须使用该值
                text/plain 空格转换为+加好，但不对特殊字符编码(很少用)
     文件上传     multipart/form-data 

 1.4表单的同步提交以及缺点
    点击submit按钮 触发表单提交操作 使页面跳转到action URL的行为，叫做表单的同步提交
    form表单同步提交后，页面的状态和数据会丢失

    如何解决上述问题
    (感觉可以用那个比如 阻止默认行为)
    表单只负责采集数据，ajax负责将数据提交到服务器


2.通过ajax提交表单数据
    2.1监听表单提交事件
        jq可以用两种方式
    $('#form1').submit(function(e){

    })

        或者

    $('#form1').on('submit',function(e){
        
    })

 2.1 快速获取表单中的数据   
    1)serialize()函数
    
    jq提供的函数

    $(selector).serialize()    //选择器获取元素.serialize()
    
    <form id="form1">
        <input type="text" name="username" />
        <input type="password" name="password" />
        <button type="submit">提交</button>
    </form>
    <script>
        $('#form1').serialize()
        //调用的结果 uername = 用户名的值& password=密码值
        //必须为每个表单添加name属性
    好处:可以一次性获取到表单中的所有数据  得到一个键值对 也就是key&value的组合 key是值得名称，value存的是值得内容
    !必须为每个表单添加name属性

    formData: form.onsubmit中 构造forData对象 new FormData (formElement)
    form.elements 遍历，利用e.type判断类型再获取e.name,e.value
    Vue 通过v-model表单输入绑定或原生js 手动获取 推荐1和3   

    jq转dom对象 $('#f1')[0].reset
    reset() 重置事件 就清空了


什么叫做隐式迭代?
在方法的内部会为匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用,这就叫做隐式迭代　　
我想把ul下的每个li都加个样式jquery写法就是:$("ul li").addClass("test"),就是把ul下的每一个li都加了test的样式，我们并没有去取得所有li然后循环加样式
如果获取的是多元素的值，大部分情况下返回的是第一个元素的值

each方法：大部分情况下是不需要使用each方法的，因为jquery有隐式迭代的特性，但是如果要对每个元素做不同的处理就要用到each方法了 

4.如果ui解构复杂
  最好被用字符串拼接的解构
 
  模板引擎:指定的模板结构和数据 自动生成一个完整的html的页面

            数据 
                                模板引擎  HTML页面
            模板解构
  好处:1.减少字符串拼接的操作 2.让代码的解构更加清晰 3.使代码更容易阅读和维护

5.art-template 
  art-template 是一个简约、超快的模板引擎。中文官网首页为 http://aui.github.io/art-template/zh-cn/index.html

  导入art template 定义数据 定义模板 调用template函数 渲染HTML结构
     //1.导入模板引擎 在window全局就多一个函数叫template ('模板的id'，需要渲染的数据)
     //2.定义需要渲染的数据
     //3.定义模板 HTML结构 必须定义到script标签中
    <script type="text/HTML"> //把里面的内容当做html来填写
     //4.调用template函数
     模板id 设一个id 渲染数据   
     {{}}这属于双发占位符
     //5.渲染HTML结构 
       二三的顺序不能乱 先HTML再JS
       原生就需要获取id container.innerHTML =str
 
 5.1 art-template标准语法

  art-template提供了{{}}这种语法，在{{}}内可以进行变量输出/循环数组等操作，这种{{}}语法在art-template中被称为标准语法   

    {{value}}
    {{obj.key}}
    {{obj['key']}}
    {{a ? b : c}}
    {{a || b}}
    {{a + b}}

    在 {{ }} 语法中，可以进行变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出
 2) 原文输出
    {{@ value}}
    如果要输出的value值中 包含了html标签结构，则需要原文输出语法，才能保证HTML标签被正常渲染

    Eg :{{@ test}}
 3)条件输出
    用if...else if.../if的方式 进行按需输出

    {{if value}} 按需输出的内容 {{/if}}

    {{if v1}} 按需输出的内容 {{else if v2}} 按需输出的内容 {{/if}}

 4)循环输出
  如果要实现循环输出，则可以在 {{ }} 内，通过 each 语法循环数组，当前循环的索引使用 $index 进行访问，当前的循环项使用 $value 进行访问。

    {{each arr}}
    {{$index}} {{$value}}
    {{/each}}
 5)过滤器
    
    需要处理的值 参数-> 过滤器参数 ->返回值 输出新值
    {{value| filterName}} 
    管道符 | 他的上一个输出作为下一个输入
    template.defaults.imports.filterName=function(value){/*return处理的结果*/}

6.正则和字符串的操作
    exec() 用来检索字符串中正则表达式的匹配 如果没有匹配的就是test    
    replace() 函数用于在字符串中用一些字符替换另一些字符，语法格式如下：
        var str = '<div>我是{{name}}</div>'
        var pattern = /{{([a-zA-Z]+)}}/
                    ()是为了提取出来name对应的值
        var patternResult = pattern.exec(str)
        str = str.replace(patternResult[0], patternResult[1]) // replace 函数返回值为替换后的新字符串
        // 输出的内容是：<div>我是name</div>
        console.log(str)

JS对样式的修改相当于行内式 优先级高于内嵌式