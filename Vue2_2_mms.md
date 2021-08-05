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
        <meta name="viewport" content="width=device-width,initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
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
    <head>
        <title>Vue2</title>
        
        <meta name="viewport" content="width=device-width,initial-scale=1.0"/>
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

        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
             <!--告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面
                 类似的还有：<meta http-equiv="X-UA-Compatible" content="IE=8">
                            告诉IE浏览器，IE8/9都会以IE8引擎来渲染页面。  -->
        <link rel="stylesheet" href="./css/index.css"/>
                <!--告诉浏览器你将采用什么编码来对下面的内容进行处理 -->
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



## 本地应用-各种指令🚌

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

事件绑定的方法写成函数调用的形式，可以传入自定义参数

定义方法时需要定义形参来接受传入的实参

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



### v-bind

v-bind:属性名=表达式

设置元素的属性（比如：src，title，class）

简写只需要写冒号：

```html
<!DOCTYPE html> 
<html lang="en">
    <head>
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">

        <title>Vue2</title>
        <style>
            .active{
                border:10px solid royalblue;
            }
        </style>
    </head>
</html>

<body>
    <div id="id_app">
        <img :src="imgSrc" alt="百度" :title="imgTitle+'!!!!!'" :class="{active:isActive}" @click="toggleActive">
     </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#id_app",
            data:{
                imgSrc:"https://www.baidu.com/img/flexible/logo/pc/result.png",
                imgTitle:"title",
                isActive:false
            },
            methods:{
                toggleActive:function(){
                    this.isActive=!this.isActive;
                }
            }
        })
    </script>
</body>
```



### v-for

根据数据生成列表结构

```html
<body>
    <div id="app">
        <ul>
            <li v-for="(item,index) in arr">
                {{index+1}} : {{arr[index]}}  {{item}}
            </li>
            
            <input type="button" value="添加" @click="add">

            <h3 v-for="item in objArr">
                {{item.name}}
            </h3>
        </ul>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#app",
            data:{
                arr:["harry","ron","hermione"],
                objArr:[
                    {name:"gry"},
                    {name:"rav"}
                ]
            },
            methods:{
                add:function(){
                    this.objArr.push({name:"+1"});
                }
            }
        })
    </script>
</body>
```



### v-model

获取和设置表单元素的值（双向数据绑定，同时改变绑定的数据 和 表单元素的值）

```html
<body>
    <div id="app">
        <input type="text" v-model="message">
        <h2>{{message}}</h2>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#app",
            data:{
                message:"hogwards"
            },
            methods:{
                add:function(){
                    this.objArr.push({name:"+1"});
                }
            }
        })
    </script>
</body>
```





## 应用实例代码🚍

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



### 图片切换

```html
<body>
    <div id="mask">
        <div class="center">
            <!-- 左箭头 -->
            <a href="javascript:void(0)" v-show="index!=0" @click="prev" class="left">
                <img src="https://pic2.zhimg.com/50/v2-2b08ad9fcb1860412e359e95299efbfc_720w.jpg?source=1940ef5c"/>
            </a>
            <!-- 图片 -->
            <img src="imgArr[index]" alt="123456">
            <!-- 右箭头 -->
            <a href="javascript:void(0)" v-show="index<imgArr.length-1" @click="next" class="right">
                <img src="https://pic2.zhimg.com/50/v2-2b08ad9fcb1860412e359e95299efbfc_720w.jpg?source=1940ef5c "/>
            </a>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app=new Vue({
            el:"#mask",
            data:{
                imgArr:[
                    "https://pic1.zhimg.com/50/v2-48bcff5660d1a93e181b6408e4a916c2_720w.jpg?source=1940ef5c",
                    "https://pic1.zhimg.com/50/v2-48bcff5660d1a93e181b6408e4a916c2_720w.jpg?source=1940ef5c",
                    "https://pic1.zhimg.com/50/v2-8b8587363e69acb8ded6fc6e61106530_720w.jpg?source=1940ef5c"
                ],
                index:0
            },
            methods:{
                prev:function(){
                    this.index--;
                },
                next:function(){
                    this.index++;
                }
            }
        })
    </script>
</body>
```



### 记事本

```html
<!DOCTYPE html>
<html lang="en">        
    <head>
        <title>Vue2</title>

        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <meta name="robots" content="noindex,nofollow"/>
            <!--设置网页的搜索引擎规则
                content包括：是否允许索引（index/noindex）
                             是否跟踪链接（follow/nofollow，也可以理解为是否允许沿着网页中的超级链接继续抓取）-->
        <meta name="googlebot" content="noindex,nofollow"/>
            <!--指定搜索引擎  具体同上-->
    </head>
</html>

<body>
    <section id="todoapp">
        <header class="header">
            <h1>记事本</h1>
            <input v-model="inputValue" @keyup.enter="add" autofocus="autofocus" autocomplete="on" placeholder="请输入" class="new_todo"/>
                <!--autofocus: 在页面加载时自动获得焦点 在移动版 Safari 上不工作 也可以直接写autofocus不赋值
                    autocomplete: 属性规定输入字段是否应该启用自动完成功能
                    placeholder：当没有内容的时候输入框里面灰色的文字-->
        </header>
        <section class="main">
            <ul class="todo_list">
                <li class="todo" v-for="(item,index) in list">
                    <div class="index">
                        <span class="index">{{index+1}} . </span>
                        <label>{{item}}</label>
                        <button class="destroy" @click="remove(index)"></button>
                    </div>
                </li>
            </ul>
        </section>
        <footer class="footer" v-show="list.length!=0">
            <span class="todo_count" v-if="list.length!=0">还有<strong>{{list.length}}</strong>个！</span>
            <button v-show="list.length!=0" class="clear_completed" @click="clear">clear</button>
        </footer>
            <!-- <footer> 标签定义文档或节的页脚 -->
    </section>

    <footer class="info">到最后啦</footer>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script>
        var app =new Vue({
            el:"#todoapp",
            data:{
                list:["first","second","third"],
                inputValue:"increaseing"
            },
            methods:{
                add:function(){
                    this.list.push(this.inputValue);
                },
                remove:function(index){
                    this.list.splice(index,1);
                },
                clear:function(){
                    this.list=[];
                }
            }
        })
    </script>
</body>
```

## 
