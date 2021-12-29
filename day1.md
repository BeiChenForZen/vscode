创建项目  vue create app

1： vue-cli脚手架初始化项目
    node + webpack + 淘宝镜像
    node_modules 文件夹 ： 项目的依赖的文件夹
    public 文件夹 ： 一般放置一些静态资源（图片） 需要注意 放在public文件夹中的静态资源 webpack 进行打包的时候 会原封不动的打包到dist文件夹中
    src 文件夹（程序员源代码文件夹）： 
        assets文件夹 ： 一般也是放置的是静态资源 （一般放置的是多个组件公用的静态资源） 需要注意 放置在assets文件架里面的静态资源，
        在webpack打包的时候，webpack会把静态资源当做一个模块 打包到js文件里面

        components文件夹： 一般放置的是非路由组件（全局组件）

        App.vue : 唯一的根组件

        main.js ： 程序入口文件，也是整个程序当中最先执行的组件

babel.config.js：配置文件 （babel相关）

package.json文件 ： 认为是项目的身份证  记录了项目叫做什么  项目中有那些依赖

package-lock.json文件： 缓存性的文件

README.md文件： 说明性的文件

2： 项目的其他配置 
    2.1 ： 项目运行起来的时候 让浏览器自动打开
        --- package.json 文件 
              "scripts": {
                "serve": "vue-cli-service serve --open", // --open 浏览器自动打开
                "build": "vue-cli-service build",
                "lint": "vue-cli-service lint"
            }


    2.2 eslint校验功能关闭
        --- 在根目录下，创建一个vue.config.js文件
        比如：申明变量但是没有使用，eslint校验工具报错。
            module.exports = {
            //关闭eslint
            lintOnSave: false
            }


    2.3 src文件夹目录的简写,配置别名 @
        jsconfig.json 配置别名@提示 [@代表的是src文件夹，这样将来文件过多，找的时候方便很多]
        {
            "compilerOptions": {
                "baseUrl": "./",
                "paths": {
                    "@/*": ["src/*"]
                }
            },
            "exclude": ["node_modules","dist"]
        }

    3. 项目路由的分析
        vue-router 
        前端有所谓的路由: KV键值对。
        key: URL（地址栏中的路径）
        value: 相应的路由组件

        注意： 项目上中下结构
        路由组件：
            home首页的路由、search 搜索页的路由、login登录路由、register注册路由
        非路由组件：
            Header、Footer 在首页、搜索页是有的   在登录页、注册页是没有的 

    4、 完成非路由组件Header与 Footer的业务
        在咱们的项目中  不再以html + css为主，主要搞业务 逻辑 
        4.1 书写静态页面 （HTML+CSS）
        4.2 拆分组件
        4.3 获取服务器的数据动态展示
        4.4 完成相应的动态业务逻辑
        
        注意1： 创建组件的时候 组件结构+组件的样式+组件需要的图片资源
        注意2： 咱们的项目采用的是less的样式 浏览器不识别less样式  需要通过less、less-loader进行处理less，把less样式变成css样式 浏览器才可以识别
        使用的是less5版本
        注意3： 如果想让组件识别less样式，需要 在style标签的身上的身上加上lang=less

        4.5 使用组件的步骤 （非路由组建）
            -创建或者定义
            -引入
            -注册
            -使用

    5、路由组件的搭建
        在上面分析的时候 路由组件应该有四个 Home Search Login Register
        -components文件夹 经常放置的非路由组件（共用全局组件）
        -pages|views文件夹 经常防止路由组件    
        5.1 配置路由
            项目当中配置的路由 一般放在router文件夹中
        5.2 总结
            路由组件与非路由组件的区别
            1： 路由组件一般放置在pages|views文件夹，非路由组件一般放置在components文件夹中
            2： 路由组件一般需要在router文件夹中进行注册（使用的即为组件的名字），非路由组件一般以标签的形式使用
            3:  注册完路由 不管路由组件 还是非路由组件身上都有$route\$router属性

            $route： 一般获取路由信息【路径 query params等等】
            $router: 一般进行编程式导航进行路由跳转【push|replace】

        5.3 路由的跳转 
            路由的跳转有两种形式 ： 
                声明式导航router-link ， 可以进行路由的跳转
                编程式导航push|replace， 可以进行路由跳转

                编程式导航 ： 声明式导航能做的 编程式导航都能做
                但是编程式导航除了可以进行路由跳转，还可以做一些其他的业务逻辑。（比如登录时候，账号密码提交的业务逻辑）


    6、Footer组件显示与隐藏： v-if （频繁操作dom，耗性能）| v-show
            Footer组件： 在Home、Search显示Footer组件
            Footer组件： 在Login、Register时候是隐藏的 
            6.1 我们可以根据组件身上的$route获取当前路由的信息，通过路由的路径判断Footer的显示与隐藏
                    <!-- 在Home、Search下显示的  在登录、注册时隐藏 -->
                    <Footer v-show="$route.path=='/home' || $route.path=='/search'"></Footer>
            6.2 配置的路由的时候，可以给路由添加路由元信息【meta】，路由需要配置对象，他的key不能瞎写、胡写、乱写

    8、路由传参
            8.1 路由跳转有几种方式？
                比如A->B
                声明式导航：<router-link to="组件名"> （务必要有to属性） ，可以实现路由的跳转。
                编程式导航：利用的是组件实例的$route.push | replace方法，可以实现路由的跳转。 （这种方式更好，在跳转之前可以实现自己的业务，再跳转）

            8.2 路由传参，参数有几种写法？
                params参数，属于路径中的一部分，需要注意，再配置路由的时候，需要占位
                query参数：不属于路径当中的一部分，类似于ajax中的queryString /home?k=v    
