# Vue2🦓

> 写在前面🐤
>
> Vue3之前准备还是先过一下Vue2
>
> 主要是代码为主，看代码过知识点，如果需要某个具体知识点查找就下载后Ctrl+F吧
>
> 有的批注写的比较长，建议CV到VScode等里面看，都是排版好的



## 第一个代码_Hello World

```html
<!DOCTYPE html><!--声明了这是html5的文档规范-->
<html lang="en">
    <head>
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Vue2</title>
    </head>
</html>

<body>
    <div id="app">
        {{message}}
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    <script>
        var app=new Vue({
            el:"#app",
            data:{
                message:"Hello World"
            }
        })
    </script>
</body>
```

下面开始详细解释

```html
<!DOCTYPE html>     <!--声明了这是html5的文档规范-->
<html lang="en">    <!--lang是language的缩写，代表该网页属于哪一个国家或是地区的网页
                        常用:en-US 英国(美国)
                            zh-CN 中文(简体，中国大陆) 
                        比如必应搜索有国内版/国际版两种选项，即在zh-CN和全部当中搜索-->

        <meta name="viewport" content="width=device-width,initial-scale=1.0">
            <!--viewport：  设备的屏幕上能用来显示我们的网页的那一块区域
                            用于指定用户是否可以缩放Web页面，并对相关的选项进行设定。

                content属性值:  width和height: 指定视区的逻辑宽度和高度
                                              它们的值可以是以像素为单位的数字，也可以是一个特殊的标记符号
                                                要注意：css中的1px并不等于设备的1px
                                              如上文代码中device-width即表示，视区宽度应为设备的屏幕宽度
                                              类似的，device-height即表示设备的屏幕高度

                                intial-scale:   页面首次被显示是可视区域的缩放级别
                                                取值1.0则页面按实际尺寸显示，无任何缩放

                                maximum-scale=1.0 和 minimum-scale=1.0: 可视区域的缩放级别
                                                                        值的范围为0.25~10.0之间

                                user-scalable:  是否可对页面进行缩放，no禁止缩放 -->

        <meta http-equiv="X-UA-Compatible" content="ie=edge">
             <!--告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面
                 类似的还有：<meta http-equiv="X-UA-Compatible" content="IE=8">
                            告诉IE浏览器，IE8/9都会以IE8引擎来渲染页面。  -->
        <link rel="stylesheet" href="./css/index.css"/>
                <!--告诉浏览器你将采用什么编码来对下面的内容进行处理 -->
    <head>
        <title>Vue2</title>
    </head>
</html>

<body>
    {{message}} <!-- 这里只会在页面中打印出来"{{message}}" -->

    <div id="id_app" class="class_app">
        {{school.college[1]}}   <!-- 可以打出来G -->
        <span>{{message}}</span><!-- 可以打出来hello world -->
        <span>{message}</span>  <!-- 只能打出来"{message}"-->
    </div>

    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",       //#是id选择器，让其管理一个id叫id_app的元素
                                //这种办法仅支持部分双标签，比如<body>和<HTML>就不支持
/*          el:".class_app",    //.是class选择器，让其管理一个class叫class_app的元素
            el:"div",           //管理<div>标签
        上面三句话等价，推荐使用id选择器   */
            
            data:{
                message:"Hello World",
                school:{
                    name:"Hogwarts",
                    college:["R","G","S"]
                }
            }
        })
    </script>
</body>
```



## 本地应用-各种指令

### v-test

设置标签的文本值

```html
<!--两种使用方法-->
<body>
    <div id="id_app" class="class_app">
         <h2>Hey！{{message+" is here"}}</h2>   <!-- 打印出Hey！Harry Potter is here! -->
         <h2 v-text="message+' is here!'"></h2> <!-- 打印出Harry Potter is here! -->
<!--     <h2 v-text="message">is here</h2>            但这样用 只能打印出Harry Potter -->
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                message:"Harry Potter",
            }
        })
    </script>
</body>
```



### v-html

文本 -> 同v-test

超链接

```html
<body>
    <div id="id_app" class="class_app">
         <p v-text="message"></p> <!-- 打印出Harry Potter-->
         <p v-html="message"></p> <!-- 打印出Harry Potter 同v-text-->
         <p v-html="website"></p> <!-- 打印出蓝色"百度"的超链接-->
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                message:"Harry Potter",
                website:"<a href='https://www.baidu.com/'>百度</a>"
            }
        })
    </script>
</body>
```



### v-on

为元素绑定事件

```html
<body>
    <div id="id_app" class="class_app">
         <input type="button" value="单击按钮" @click="doIt">   <!-- 点击方法 @click也可以写成 v-on:click -->
         <input type="button" value="双击按钮" @dblclick="doIt"><!-- 双击方法 @dblclick也可以写成v-on:dblclick-->
            <!-- button表面字符为value值 -->
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            methods:{
                doIt:function(){
                    alert("Hogwarts！");
                }
            }
        })
    </script>
</body>
```

### 计数器

```html
<body>
    <div id="id_app">
        <div class="input-num">
            <button @click="sub">-</button>
            <span>{{num}}</span>
            <button @click="add">+</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                num:1
            },
            methods:{
                add:function(){
                    this.num++;
                },
                sub:function(){
                    this.num--;
                }
            }
        })
    </script>
</body>
```



### v-show

根据表达式的真假，切换元素的显示和隐藏

```html
<body>
    <div id="id_app">
        <input type="button" value="切换显示状态" @click="changeisShow">
        <input type="button" value="增加年龄" @click="addAge">
        <img src="https://www.baidu.com/img/flexible/logo/pc/result.png" v-show="true" alt="百度">
        <img src="https://www.baidu.com/img/flexible/logo/pc/result.png" v-show="isShow" alt="百度">
        <img src="https://www.baidu.com/img/flexible/logo/pc/result.png" v-show="age>=18" alt="百度">
            <!-- alt：如果无法显示图像，浏览器将显示替代文本 -->
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                isShow:false,
                age:16
            },
            methods:{
                changeisShow:function(){
                    this.isShow=!this.isShow;
                },
                addAge:function(){
                    this.age++;
                }
            }
        })
    </script>
</body>
```



### v-if

根据表达式的真假，切换元素的显示和隐藏 (操纵dom元素)

当表达式的值为true，元素存在于dom中，为false中，从dom中移除

```html
<body>
    <div id="id_app">
        <input type="button" @click="changeisShow" value="通过我来控制">
        <p v-if="true">我是一个始终显示的P标签</p>
        <p v-if="isShow">我一会显示一会不显示</p>
     </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                isShow:false,
            },
            methods:{
                changeisShow:function(){
                    this.isShow=!this.isShow;
                },
            }
        })
    </script>
</body>
```

