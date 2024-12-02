---
title: Vue2
date: 2024-10-26 20:43:57
tags:
---

## VUE2

### 1.初识Vue
- 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象
- root容器里面的代码一九符合html规范，只不过混入了一些特殊的Vue语法
- root容器里的代码被称为【Vue模板】
- Vue实例和容器是一一对应的
- 真实的开发中只有一个Vue实例，并且会配合着组件使用
- {{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性
- 一旦data中的数据发生变化，那么页面中用到该数据的地方也会自动更新
----
>`注意区分：js表达式和js代码（语句）`
>>`1.表达式：一个表达式会生成一个值，可以放在任何一个需要值的地方 `
>>>`(1). a `
>>>`(2). b + 1 `
>>>`(3). demo(1) `
>>>`(4). x===y?'a':'b' `
>>>
>>`2.代码（语句）：`
>>>`(1). if(a>b)`
>>>`(2). for(let i=0;i<10;i++)`
----

### 2.Vue模板
- 插值语法：
    - 功能：用于解析标签体内容
    - 写法：{{xxx}}，xxx可以是任何js表达式，会自动读取到data中的所有属性
- 指令语法：
    - 功能：用于解析标签（包括：标签属性，标签体内容，绑定事件....）
    - 举例：v-bind：herf="xxx"  或简写为：  ：herf="xxx"
    - 备注：Vue中有很多的指令，且形式都是：v-????，此处我们拿v-bind举例

### 3.数据绑定
- v-bind:单向数据绑定
- v-model:双向数据绑定，只能用在表单元素上（输入类元素）
    - v-modle:value可以简写为v-model

### 4.el与data的两种写法
- el:
    - 创建Vue实例时，可以传入el参数，指定容器元素；
    - 也可以创建v=new Vue()，v.$mount('#root')指定容器元素
- data:
    - 对象式
    - 函数式，组件学习后，使用函数式

### 5.MVVM模式
- Model-View-ViewModel模式
- Model：数据模型，即data中的数据
- View：视图，即页面显示的部分，由HTML模板和指令组成
- ViewModel：视图模型，即Vue实例，负责处理数据和视图间的交互
- data中所有的属性，最后都出现在vm上A
- vm身上的所有属性 及 Vue原型上的所有属性，在Vue模板中都可以直接使用

### 6.Object.defineProperty()
- ![数据代理](Vue2-6.1.png)


### 7.数据代理
- 通过一个对象对另一个对象中属性的操作

### 8.Vue中的数据代理
- 通过vm对象来代理data对象中属性的操作（读/写）
- 好处：更加方便的操作data中的数据
- 原理：
    - 通过Object.defineProperty()方法把data对象中所有属性添加到vm上，为每一个添加到vm上的属性，都指定一个getter和setter方法，当vm上属性被访问或修改时，会自动调用getters和setters方法，从而实现双向数据绑定

### 9.事件处理
- 使用v-on指令绑定事件，或者@xxx绑定事件（其中xxx是事件名）
- 事件的回调需要配置在methods中
- methods中配置函数时，不要使用箭头函数
- 函数中this指向vm实例
- @click="demo"与@click="demo($event)"一致，但是后者可以传参

### 10.事件修饰符
- .stop：阻止事件冒泡
- .prevent：阻止默认事件
- .once：只执行一次
- .capture：使用事件捕获模式
- .self：只有event.target是当前操作元素时，才触发事件
- .passive：事件的默认行为立即执行，不会等待事件回调函数执行完毕
- 修饰符可以链式使用
- ![事件修饰符1](/images/Vue2-10.1.png)
- ![事件修饰符2](/images/Vue2-10.2.png)

### 11.键盘事件
- 常用按键别名：
    - 回车 ==> enter
    - 删除 ==> delete(退格/delete)
    - 退出 ==> esc
    - 空格 ==> space
    - 换行 ==> tab(特殊，配合keydown)
    - 上 ==> up
    - 下 ==> down
    - 左 ==> left
    - 右 ==> right
- Vue中未提供别名的案件，可以用原始key值去绑定
- 系统修饰键（用法特殊）：ctrl / alt / shift /meta(win健)
    - 配合keyup：按下后，同时按住其余按键，松开其他按键
    - 配合keydown：正常触发事件
- 利用keyCode绑定事件（不推荐）
- 自己定义别名  Vue.config.keyCodes.xxx = yyy（xxx为自定义按键名，yyy为原始按键值）
`键盘事件也可以链式使用（不常见）`

### 12.计算属性
- 计算属性是一种特殊的属性，它依赖于已有的属性，并返回一个值
- 语法：computed:{属性名：函数}
- 计算属性的函数中，this指向vm实例
- 计算属性的返回值会被缓存，只有当依赖的数据发生变化时，才会重新计算
- 计算属性的返回值可以直接用在模板中，也可以用在其他地方


### 13.监视属性
- 监视属性是一种特殊的属性，它依赖于已有的属性，并在属性值发生变化时，执行一个函数
- 监视属性必须存在
- 两种写法：
    - 1.watch:{属性名：函数}
    - 2.vm.$watch('属性名',函数)
- 深度监视：deep:true,监视多级结构中所有属性的变化，watch默认不检测多级结构内部的变化
- immediate:true 初始化时，会执行一次回调函数

### 14.computed和watch的区别
- 区别：
    - 1.computed能够完成的功能，watch都可以做到
    - 2.watch可以做到的功能，computed不一定能完成，例如watch可以进行异步操作
- 两个重要小原则：
    - 1.所有被Vue管理的函数，最好使用普通函数，这样this才是指向vm实例或者组件实例
    - 2.所有不被Vue所管理的函数（定时器回调函数，ajax回调函数），最好写成箭头函数，这样this的指向才会是vm或者实例组件 

### 15.绑定class样式
- 字符串形式< ：class="xxx"> 适用于样式名不确定，需要动态指定
- 数组写法：<:class="[xxx,yyy]"> 适用于样式名不确定，名字也不确定
- 对象写法：<:class="{xxx:true,yyy:false}"> 适用于样式名确定，名字也确定，但要动态决定状态

### 16.style绑定
- 对象写法：style="{color:red,fontSize:16px}"
- 数组写法：style="[style1,style2]"

### 17.条件渲染
- v-show：根据条件，决定是否渲染标签
- v-if：根据条件，决定是否渲染标签及其子元素
- v-else-if：等价于python中的elif
- v-else：等价于python中的else
- 后面三者不能分割使用

### 18.列表渲染
- v-for：
    - 1.用于展示列表数据
    - 2.语法：v-for="(item,index) in item :key=index"
    - 可遍历对象： 数组、对象、字符串、指定次数（后两者用的很少）
- key的原理：
    - key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据新数据生成新的虚拟DOM，随后将新旧DOM 进行比较，找出需要更新的部分，然后进行局部更新
    - 开发中最好使用每条数据的唯一标识作为key，如果不存在逆序添加则用index作为key也没有问题
- 列表过滤:
    - filter()实现 
    - watch实现：
    - ![列表过滤1](/images/Vue2-18.1.png)
    - computed实现：
    - ![列表过滤2](/images/Vue2-18.2.png)
- 列表排序：
    - sort(val1，val2 )实现
        - val1-val2 升序
        - val2-val1 降序

### 19.vue.set()
- 作用：动态添加属性到data中
- 语法：Vue.set(对象，'属性名',值)
- 注意：
    - 1.对象必须是data中的对象
    - 2.属性名必须是字符串
    - 3.值可以是任意类型
`局限：只能给vm._data中的对象实行动态添加，不能直接给vm._data添加属性`

### 20.vm.$set()
- 作用：动态添加属性到data中
- 语法：vm.$set(对象，'属性名',值)
- 注意：
    - 1.对象可以是data中的对象，也可以是vm实例
    - 2.属性名必须是字符串
    - 3.值可以是任意类型
`局限：只能给vm._data中的对象实行动态添加，不能直接给vm._data添加属性`

### 21.Vue检测数据的原理
- Vue会监视data中所有层次的数据
- 如何实现监测对象中的数据:
    - 通过setter实现监视，且要在new Vue()时，就传入要监测的数据
        - （1）对象中后追加的属性，Vue默认不做响应式处理
        - （2）如果需要给后面添加的属性做响应式，需要使用Vue.set()或者vm.$set()方法
- 如何实现监测数组中的数据：
    - 通过包裹数组更新元素的方法实现，本质就是做了两件事
        - （1）调用原生对应的方法对数组进行更新
        - （2）重新解析模板，进而更新页面
- 在Vue修改数组中的某个元素一定要用如下方法：
    - 使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
    - Vue.set()、vm.$set()

`特别注意：Vue.set()、vm.$set()只能给data中的对象添加属性，不能给vm或者vm的根数据添加属性`

### 22.表单收集
- 若`<input type="text">`，则v-model收集的是value值，用户输入的也是value值
- 若`<input type="radio">`，则v-model收集的是value值，要给标签配置value值，用户选择哪个，v-model会更新为相应的value值
- 若`<input type="checkbox">`
    - 没有配置value值，则v-model收集的是布尔值，用户勾选，v-model会更新为true
    - 配置了value值，且初始值为数组，那么收集的就是由value组成的数组
    - 配置了value值，且初始值为非数组，那么收集的就是布尔值
- v-modle的修饰符：
    - .lazy：默认情况下，v-model在每次input事件触发时，都会更新数据，加上.lazy修饰符，则只在输入框失去焦点时，才会更新数据
    - .number：将用户输入的字符串转换为数字类型
    - .trim：自动去除用户输入的首尾空格

### 23.过滤器
- 定义：对要显示的数据进行特定格式化之后再显示（适用于一些简单逻辑）
- 语法：
`    - 注册过滤器：Vue.filter('过滤器名',函数)`
`    - 使用过滤器：{{xxx|yyy}}(yyy为过滤器名)`

- 备注：
    - 1.过滤器可以链式使用
    - 2.未改变原本的元素

### 24.内置指令
- v-bind:单向数据绑定，简写--- ：xxx
- v-model:双向数据绑定
- v-for: 遍历数组对象字符串
- v-on : 绑定事件监听，简写---- @xxx
- v-if: 条件渲染
- v-else: 条件渲染
- v-show: 条件渲染，与v-if的区别是，v-show会始终渲染标签，只是改变display:none/block
- v-text: 显示文本内容，与插值语法的区别是，v-text不会解析表达式，直接显示文本内容,不可以进行文本拼接
- v-html:支持结构解析，可以解析html代码，不建议使用
- v-cloak: 解决闪烁问题，在页面加载时，隐藏标签（配合css），等Vue实例创建完成，再显示标签（无需赋值）
- v-once：只渲染一次，数据变化时，不会重新渲染（无需赋值）
- v-pre：跳过当前元素和子元素的编译过程，直到遇到v-cloak指令才开始编译


### 25.自定义指令
- 定义：自定义指令，可以绑定到元素上，实现一些特殊功能
- 语法：
    - 注册指令：Vue.directive()或者derectives
    - 函数式：Vue.directive('指令名':function(el,binding,vnode){})
    - 对象式：Vue.directive('指令名':{
        bind:function(el,binding,vnode){},---一开始就执行
        update:function(el,binding,vnode){},---数据更新时执行
        inserted:function(el,binding,vnode){},---插入DOM时执行
    })
- 备注：
    - 定义时不加v，使用时要加v
    - 指令名是多个单词，那么需要用-连接


### 26.生命周期
- 又名生命周期函数、生命周期钩子，名字不可更改，this指向vm
- 四对生命周期函数：
    - beforeCreate：实例刚被创建，数据观测和事件配置还未开始
    - created：实例创建完成，数据观测和事件配置已完成，但还没有挂载到实例上，$el还不存在
    - beforeMount：实例开始挂载，$el已存在，但还没有开始渲染
    - mounted：实例挂载完成，$el已渲染完成
    - beforeUpdate：数据更新时调用，发生在虚拟DOM重新渲染和打补丁之前
    - updated：数据更新时调用，发生在虚拟DOM重新渲染和打补丁之后
    - beforeDestroy：实例销毁之前调用
    - destroyed：实例销毁之后调用

### 27.组件
-  三大步骤：
    - 1.定义组件
    - 2.注册组件Vue.component()注册组件
    - 3.使用组件
- 定义组件：
    - 组件是一个对象，包含三个选项：
        - template：组件的模板
        - data：组件的属性
        - methods：组件的方法
- 注册组件：
    - 局部注册：new Vue的时候传入components选项，注册局部组件
    - 全局注册：Vue.component()注册全局组件
- 使用组件：
    -  <组件名>< /组件名>
`注意：`
>`关于组件名：`
>>`一个单词组成的：`
>>>`首字母小写、首字母大写`
>>
>>`多个单词组成的：`
>>>`短横线连接`
>>>`CamelCase写法，两个单词首字母大写`

### 28.单文件组件
- vue文件
- 一个文件就是一个组件，包含template、script、style三个部分
- 同时一个大组件可以包含多个小组件
- 有一个名为APP的组件管理所有组件
- 组件需要export default导出，才能在其他组件中使用
  

### 29.ref
- 作用：获取组件实例或元素
- 语法：ref="xxx"
- 备注：
    - 1.用在标签元素上，与id属性类似，可以获取元素
    - 2.用在组件上，可以获取组件实例vm

### 30.props
- 简单接收:
    props:['name','age']
- 对象接收(接收+限制):
    - props:{
        name:String,
        age:Number
      }
- 接收+限制+默认值:
    - props:{
        name:{
            type:String,
            required:true,
            default:'默认值'
        }
    }

### 31.mixin
- 能够将重复的代码抽取到一个文件中，然后在多个组件中使用
- 语法：
    - 1.定义mixin：
        - 定义一个对象，包含多个选项
        - 选项可以是data、methods、computed、watch等
    - 2.使用mixin：
        - 直接在组件中使用mixins选项，传入mixin对象
        - 也可以在组件中使用mixins选项，传入多个mixin对象
- 注意：
    - 1.mixin对象中的选项，会覆盖组件自身的同名选项
    - 2.mixin对象中的选项，不会影响组件的生命周期
    - 3.mixin对象中的选项，不会影响父组件和子组件的通信


### 32.插件
- 作用：扩展Vue的功能
- 语法：
    - 1.定义插件：
        - 定义一个对象，包含install方法
        - install方法接收Vue构造函数和options对象
        - install方法的作用：
            - 1.`全局过滤器 Vue.filter()`
            - 2.`全局指令 Vue.directive()`
            - 3.`全局混入 Vue.mixin()`
            - 4.`全局实例方法 Vue.prototype.$xxx()`
    - 2.使用插件：
        - 直接使用插件，传入Vue构造函数和options对象
        - 也可以在Vue.use()方法中传入插件对象


### 33.scoped样式
- 作用：隔离样式，防止样式污染
- 语法：
    - 1.在style标签上添加scoped属性
    

### 34.案例分析
- 组件化编码流程
    - 1.拆分静态组件：组件按照功能拆分，不易过于粗糙，也不宜过于细致，命名不要与html元素重复
    - 2.实现动态组件：考虑好数据的存放位置，数据是一个组件在使用，还是一系列组件在使用
        - 1）一个组件使用，放在自己内部就好
        - 2）一系列组件使用，放在他们的父组件中，通过props传递数据
    - 3.实现交互：从绑定事件开始
- props适用于：
    - 1.父组件==>子组件传值
    - 2.子组件==>父组件传值（需要先在父组件定义一个方法，然后在子组件调用）
- v-model的注意事项：v-model绑定的值不可以是props传过来的值，因为props传值不可以修改
- props传值时，若是对象类型，修改对象的属性时，Vue不会报错，但是不推荐这样做，毕竟不合规则

### 35.WebStorage
- setItem(key,value)：设置存储项
- getItem(key)：获取存储项
- removeItem(key)：删除存储项
- clear()：清空存储
- sessionStorage：只在当前会话（窗口）有效，关闭浏览器窗口后，数据清空
- localStorage：除非手动删除，否则数据永久保存
- 注意：
    - 1.存储内容大小一般支持5M左右
    - 2.存储内容只能是字符串
    - 3.存储内容只能存储在同源的域名下

### 36.组件自定义事件
- 组件间的通信方式：适用于子组件==>父组件
- 在父组件中绑定组件自定义事件，在子组件中触发组件自定义事件
- 绑定方式：
    - 1.`<demo @xxx="test">`
    - 2.`<demo ref="demo">`.....`mounted(){this.$refs.demo.$on('xxx',this.test)}`
    - 若要求只能触发一次，可以使用once修饰符，或者$once()方法
- 触发自定义事件：`this.$emit('xxx',参数)`
- 解绑自定义事件：`this.$off('xxx')`
- 使用原生事件，可以用native修饰符

### 37.全局事件总线
- 安装全局事件总线：
`new Vue({`
`.......`
`beforeCreate(){`
`    Vue.prototype.$bus = new Vue()`
`}`
`})`
- 使用全局事件总线：
    - 接收数据
    `methods:{`
    `demo(){}`
    `}`
    `mounted(){`
    `    this.$bus.$on('xxx',this.demo)`
    `}`
    - 发送数据
    `this.$bus.$emit('xxx',参数)`
- 注意：
    - 1.全局事件总线，可以跨组件通信
    - 2.全局事件总线，可以实现跨越多层级的通信
    - 3.全局事件总线，不建议过度使用，会造成命名冲突，可读性差

### 38.消息的订阅与发布
- 一种组件间通信的方式，适合于任意组件间通信
- 使用步骤：
    - 1.安装：`npm i pubsub-js`
    - 2.导入：`import PubSub from 'pubsub-js'`
    - 3.订阅：`PubSub.subscribe('主题名',function(msg,data){})`
    - 4.发布：`PubSub.publish('主题名',参数)`
    - 5.注销：`PubSub.unsubscribe('主题id')`


### 39.动画效果
- 作用：在插入，更新或者移除DOM元素时，在合适的时候给元素添加样式类名
- 语法：
    - Enter:`v-enter-active` `v-enter;v-enter-to`
    - Leave:`v-leave-active` `v-leave;v-leave-to`
- 写法：
    - 1.准备好样式：
        1）元素进入的样式
        2）元素离开的样式
    - 2.使用`<transition>`包裹要过度的元素，并且配置name属性
    `<transition name="xxx">`
    `    <div v-if="show">`
    `        内容`
    `    </div>`
    `</transition>`
    - 3.备注：
        多个元素过度，使用transition-group组件，并且指定key属性

### 40.配置技术(代理)
- 方法一：
    在vue.config.js中配置
    `devServer:{`
    `    proxy:http://localhost:5000`
    `}`
- 说明：
    - 1.优点：简单
    - 2.缺点：无法配置多个代理，不能灵活的控制请求是否代理
    - 3.工作方式：请求时优先请求前端资源，若自身没有此项资源，再向外请求
- 方法二：
    在vue.config.js中配置
    ` devServer:{`
    `    devServer:{`
    `    proxy:{`
    `        '/api':{`
    `            target:'http://localhost:5000',`
    `            pathRewrite:{'^/api':''}`
    `            changeOrigin:true`
    `             }`
    `        }`
    `    }`
    `}`
- 说明：
    - 1.优点：可以配置多项代理，可以灵活控制是否代理
    - 2.缺点：配置稍微繁琐，请求时必须加前缀

### 40.插槽
- 作用：让父组件可以向子组件插入html结构，也是一种组件间通信的方式，适用于父组件==>子组件
- 分类：默认插槽、具名插槽、作用域插槽

### 41.路由
- 理解：一个路由就是一组映射关系，多个路由需要路由器进行管理
- 前端路由：key是路径，value是组件
- 安装：`npm i vue-router`
- 应用：`Vue.use(VueRouter){routers:[]}`
- 路由组件一般放在pages文件夹下，每个页面一个组件；一般组件放在components文件夹下
- 切换是将组件销毁，需要时在进行挂载
- 每个组件都有`自己的$route`属性，存储自己的路由信息
- 整个应用只有一个router，可以通过组件的`$router`获取

### 42.多级路由
- 配置在一级路由的children选项中
- 跳转规则要写完整

### 43.路由query参数
- 路由路径中带有参数，可以通过`$route.query`获取
- 跳转时，可以通过`:to="{path:'路径',query:{参数名:参数值}}`传递参数

### 44.命名路由
- 在配置路由时，给路由添加name属性
- 配置后，可以在跳转时用name属性，代替path属性，简化跳转路径

### 45.路由params参数
- 配置在路由路径中，通过`/:参数名`获取
- 跳转时，可以通过`:to="{name:'路由名',params:{参数名:参数值}}`传递参数（路径只能通过name属性跳转，不可以用path属性）

### 46.路由的props
- 1.第一种写法：对象形式`props:{a:1,b:"hello"}`，都会以props形式传递给组件
- 2.第二种写法：布尔值形式`props:ture`，会把该路由收到的所有`params`参数，以props形式传递给组件
- 3.第三种写法：函数形式`props:function($route){return {a:$route.quary.a}}`，

### 47.路由replace
- 作用：替换当前路由，不会留下历史记录
- 在router-link上添加replace属性

### 48.编程式路由导航 
- 作用：通过代码控制路由的跳转
- 跳转语法：`this.$router.push()`或者`this.$router.replace()`
- 回退和前进：`this.$router.back()`或者`this.$router.forward()`
- go方法：`this.$router.go(n)`n为正数，向前走n步；n为负数，向后走n步

### 49.缓存路由
- 作用：在切换路由时，缓存当前路由组件，下次进入时直接渲染缓存的组件
- 实现：用`keep-alive`元素包裹`router-view`，并设置`include`属性，值为要缓存的组件名

### 50.两个新的生命周期函数
- activated：组件激活时调用，只调用一次（从无到有）
- deactivated：组件失活时调用，只调用一次（从有到无）

### 51.路由工作的模式
![路由工作的模式](../images/Vue2-51.1.png)