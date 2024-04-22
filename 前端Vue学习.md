# 前端Vue学习

-----------------------



## 1.搭建vue-cli脚手架

##### (1)查看npm版本镜像源

```vue
npm config get registry
```

##### (2)切换npm镜像源

```vue
npm config set registry https://registry.npmmirror.com/
```

##### (3)下载vue-cli脚手架

```vue
yarn global add @vue/cli
```

##### (4)创建项目

```vue
vue create my_app
```

##### (5)运行

```vue
yarn serve  或者  npm run serve
```



------



## 2.Element-ui框架

### 2.1 全局引入

###### （1）首先测试下运行hello world 代码看是否页面布局正常（发现显示错误）

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418134550.png"  />

###### （2）然后在cdn.js网站中输入vue 查看自己的vue版本下载对应的js在线地址

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418133758.png)

###### （3）测试完成，开始安装框架(在自己项目的终端上运行)

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418134849.png" style="zoom:;" />

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418135323.png" style="zoom:;" />

###### （4）引入element-ui 组件库

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418135507.png" style="zoom:;" />

###### （5）现在框架已经形成，但是可能会有代码报错的问题，例如： vue报错：Parsing error: No Babel config file detected for...

解决方案如下:

解决方法：在`package.json`里面添加 `"requireConfigFile": false` 即可。如下图所示:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418140407.png)

###### （6）试着在element-ui组件库里找点组件实现下吧，例如我的：

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418140821.png"  />

实现效果如下:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418141105.png)

------



### 2.2 按需引入

###### （1）运行如下命令:

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418141815.png"  />

###### （2）找到项目中的babel.config.js文件，修改如下：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418141934.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418142316.png)

###### （3）接下来，如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：

```vue
import Vue from 'vue';
import { Button, Select } from 'element-ui';
import App from './App.vue';

Vue.component(Button.name, Button);
Vue.component(Select.name, Select);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Select)
 */

new Vue({
  el: '#app',
  render: h => h(App)
});
```

例如我的项目中：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418143026.png)

###### （4）保存运行： npm run serve ,此时会报错（如果不报错就不管），报错信息如下:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418143152.png)

此时修改方案如下:将之前按需引入的代码中 “es2015” 修改为“@babel/preset-env”即可成功运行.

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418143401.png"  />

此时，项目成功截图如图所示:与之前类似：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418141105.png)

（5）项目打包： 执行npm run build

------



### 2.3 Vue-router的引入

###### （1）在vue.js官网上找到vue-router的安装命令（此时安装的是最新版），若要下载指定版本，则在后面写上@+对应的版本号，例如：

```vue
npm install vue-router@3.6.5
```

注意:查询过往的npm 版本号可直接搜索npm 然后搜vue-router，接着找到以往的版本号即可。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418145024.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418145143.png)

此时查看版本信息，如图所示:

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418145512.png"  />

###### （2）做好vue-router的配置准备工作：

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418145839.png"  />

###### （3）引入vue-router，也就是将下面代码复制到index.js文件中即可。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418150002.png)

###### （4）在页面中配置router

1.在src目录下创建views文件夹用来编写页面，在其下创建Home.vue文件夹和User.vue文件夹，编写下面示例代码如下：

```vue
Home.vue
<template>
  <h1>我是Home</h1>
</template>


<script>
export default{
  data(){
    return {

    }
  }
}
</script>
```

```vue
User.vue
<template>
  <h1>我是User</h1>
</template>


<script>
export default{
  data(){
    return {

    }
  }
}
</script>
```

2.在index.js文件夹下创建路由组件

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418151405.png"  />

3.将路由和组件进行映射

```js
// 3. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
const routes = [
  { path: '/home', component: Home },
  { path: '/user', component: User }
]
```

4.创建router实例

```js
// 4. 创建 router 实例，然后传 `routes` 配置
// 你还可以传别的配置参数, 不过先这么简单着吧。
const router = new VueRouter({
  routes // (缩写) 相当于 routes: routes
})
```

5.挂载

```js
// 5. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')

// 现在，应用已经启动了！
```

注：在 vue eslint 报错 error “Component name “*****“ should always be multi-word”,解决办法：

在根目录下找到 ***vue.config.js*** 文件（如果没有则新建一个，按照示例中的代码进行添加；用 vue-cli 脚手架进行创建的项目都会有 ***vue.config.js*** 文件），添加下面的代码在 **vue.config.js** 文件下，加入以下代码，如图所示:

```js
// 关闭eslint校验
lintOnSave: false 
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418153905.png)

6.上述代码如图所示：

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418153512.png"  />

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418153637.png"  />

7.最后一步就是配置路由出口：在App.vue中写上代码：

```html
<!-- 路由出口 -->
<!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
```

如图所示:

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418154233.png"  />

8.界面效果如图：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418154459.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418154520.png)

------



### 2.4 嵌套路由

###### 1.介绍

<img src="C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418154817.png"  />

###### 2.具体步骤：

（1）在views文件夹下创建Main.vue文件作为主界面，同时在index.js里面书写对应的代码，如图所示：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418155926.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418160147.png)

（2）接着在Main.vue把路由出口写在div中即可。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418160239.png)

（3）如图所示:

User界面：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418160527.png)

Home界面：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418160556.png)

------



### 2.5 整体UI的搭建

###### 1.找到合适的界面样式布局（在elementui组件库寻找合适的），例如：将其代码复制到Main.vue中。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418161116.png)

```html
<el-container>
  <el-aside width="200px">Aside</el-aside>
  <el-container>
    <el-header>Header</el-header>
    <el-main>Main</el-main>
  </el-container>
</el-container>
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418161433.png)

###### 2.做样式

1.创建导航栏组件（在Components文件夹下创建CommonAside.vue文件用来显示导航栏），然后把组件库中合适的导航样式粘贴进去

> [!NOTE]
>
> ##### 注意：创建组件一般在Components文件夹下新建vue文件 = > 组件化封装的思想

````vue
CommonAside.vue文件
<template>
  <el-menu default-active="1-4-1" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose"
    :collapse="isCollapse">
    <el-submenu index="1">
      <template slot="title">
        <i class="el-icon-location"></i>
        <span slot="title">导航一</span>
      </template>
      <el-menu-item-group>
        <span slot="title">分组一</span>
        <el-menu-item index="1-1">选项1</el-menu-item>
        <el-menu-item index="1-2">选项2</el-menu-item>
      </el-menu-item-group>
      <el-menu-item-group title="分组2">
        <el-menu-item index="1-3">选项3</el-menu-item>
      </el-menu-item-group>
      <el-submenu index="1-4">
        <span slot="title">选项4</span>
        <el-menu-item index="1-4-1">选项1</el-menu-item>
      </el-submenu>
    </el-submenu>
    <el-menu-item index="2">
      <i class="el-icon-menu"></i>
      <span slot="title">导航二</span>
    </el-menu-item>
    <el-menu-item index="3" disabled>
      <i class="el-icon-document"></i>
      <span slot="title">导航三</span>
    </el-menu-item>
    <el-menu-item index="4">
      <i class="el-icon-setting"></i>
      <span slot="title">导航四</span>
    </el-menu-item>
  </el-menu>
</template>

<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>

<script>
export default {
  data() {
    return {
      isCollapse: true
    };
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
}
</script>
````

2.在Main.vue中引入组件

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418163614.png)

最后一步就是在template写入已经引入的组件：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418163736.png)

------



## 3.一级菜单的实现

###### 1.先把大致框架整出来：

```vue
<template>
  <el-menu default-active="1-4-1" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose"
    :collapse="isCollapse">
    <el-menu-item index="2">
      <i class="el-icon-menu"></i>
      <span slot="title">导航二</span>
    </el-menu-item>
    <el-submenu index="1">
      <template slot="title">
        <i class="el-icon-location"></i>
        <span slot="title">导航一</span>
      </template>
      <el-menu-item-group>
        <el-menu-item index="1-1">选项1</el-menu-item>
      </el-menu-item-group>
    </el-submenu>

  </el-menu>
</template>

<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>

<script>
export default {
  data() {
    return {
      isCollapse: false
    };
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
}
</script>
```

代码实现效果如图所示:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418165847.png)

###### 2.侧边栏的实现（menu的样式）

```js
menuData: [

        {
          path: '/',
          name: 'home',
          label: '首页',
          icon: 's-home',
          url: 'Home/Home'
        },
        {
          path: '/mall',
          name: 'mall',
          label: '商品管理',
          icon: 'video-play',
          url: 'MallManage/MallManage'
        },
        {
          path: '/user',
          name: 'user',
          label: '用户管理',
          icon: 'user',
          url: 'UserManage/UserManage'
        },
        {
          label: '其他',
          icon: 'location',
          children: [
            {
              path: '/page1',
              name: 'page1',
              label: '页面1',
              icon: 'setting',
              url: 'Other/PageOne'
            },
            {
              path: '/page2',
              name: 'page2',
              label: '页面2',
              icon: 'setting',
              url: 'Other/PageTwo'
            }
          ]
        }
      ]
```

如图所示:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418170215.png)

（1）当多个元素发生变化导致一个结果进行变更的时候可以使用computed（计算属性），如下图所示:

```js
computed:{
	//没有子菜单
    noChildren(){
        return this.menuData.filter(item => !item.children)
    },
    //有子菜单
        hasChildren(){
             return this.menuData.filter(item => item.children)
        }
}
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418171141.png)

（2）使用v-for指令来遍历菜单数据

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418172358.png)

（3）效果显示：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418172441.png)



------



## 4.二级菜单的实现

###### 1.先编写一级菜单的代码实现，同上：

```vue
<el-submenu v-for="item in hasChildren" :key="item.label" :index="item.label">
      <template slot="title">
        <i :class="`el-icon-${item.icon}`"></i>
        <span slot="title">{{ item.label }}</span>
      </template>
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418173416.png)

2.对照着menuData的代码可以书写二级菜单，同一级菜单类似：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418173846.png)

3.效果如图所示:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240418174016.png)

------



## 5.菜单样式与less引入

###### 1.介绍

less就是CSS语法的增强版，可以在项目模块化的过程中快速的创建我们需要的样式。

###### 2.引入less解析器

```js
npm i less@4.1.2
```

###### 3.引入lessloader(lessloader就是less的解析器，可以把less语法转换成css语法)

```js
npm i less-loader@6.0.0
```

###### 4.此时就可以书写less语法

```css
<style lang="less" scope>
.el-menu {
  height: 100vh;

  h3 {
    color: aliceblue;
    text-align: center;
    line-height: 48px;
    font-size: 16px;
    font-weight: 400;
  }
}
注意：scope是只作用于当前页面的作用域生效
```

###### 5.在App.vue清除默认样式

```css
<style lang="less">
html,
body,h3 {
  margin: 0;
  padding: 0;
}
</style>
```

------

## 6.菜单点击跳转功能实现

###### 1.根据CommonAside.vue中menuData的数据，在index.js添加路由配置信息

```js
children:[
      // 子路由(嵌套路由)
      { path: '/home', component: Home },//首页
      { path: '/user', component: User },//用户管理
      { path: '/mall', component: Mall },//商品管理
```

###### 2.在views文件夹下添加对应的页面组件，比如说要显示商品管理的页面，就创建Mall.vue文件夹

```vue
<template>
  <h1>我是Mall</h1>
</template>


<script>
export default{
  data(){
    return {

    }
  }
}
</script>
```

###### 3.在index.js中创建对应的路由组件

```js
import Mall from '../views/Mall.vue'
```

###### 4.其他页面添加步骤一致

###### 5.以下就是我写的页面的步骤：

（1）在views文件夹下创建两个页面信息：

PageOne.vue

```vue
<template>
  <h1>我是PageOne</h1>
</template>


<script>
export default{
  data(){
    return {

    }
  }
}
</script>
```

PageTwo.vue

```vue
<template>
  <h1>我是PageTwo</h1>
</template>


<script>
export default {
  data() {
    return {

    }
  }
}
</script>
```

（2）在index.js文件下创建路由组件：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419130653.png)

（3）在index.js下添加两个路由信息：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419130325.png)

（4）效果显示：

当输入page1的时候，页面跳转到pageOne;

当输入page2的时候，页面跳转到pageTwo;

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419130900.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419131001.png)

###### 6.实现点击事件的跳转

（1）在菜单栏绑定点击事件：@click =  "clickmenu(item)"

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419131300.png)

（2）在methods下添加方法：

这段代码`this.$router.push(item.path)`是在Vue.js中用于程序化地导航到应用程序中的特定路由。

当调用`this.$router.push()`时，它会导航到由`item.path`定义的路由。`item`对象很可能包含与路由相关的信息，如路径、名称或任何额外的参数或查询参数。

通过使用这种方法，应用程序可以导航到不同的路由并相应地更新URL。这通常是作为对用户交互或应用程序事件的响应而使用的。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419131720.png)

> [!NOTE]
>
> 注意:此时已经可以完成基本的首页跳转,但是当点击首页时，发现页面为空，此时的解决办法是：在index.js文件中的主路由下添加    redirect:'/home',表示重定向为主页信息。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419132440.png)

###### 7.同理二级页面跳转步骤一致：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419132729.png)

------



## 7.header组件搭建与样式调整

> [!CAUTION]
>
> 前面已经基本实现路由的跳转功能，但是会发现重复点击页面的时候会发生报错，因为router会限制页面不能重复跳转，为了追求完美，解决方案如下：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419133439.png)

> [!TIP]
>
> 这段代码是一个条件语句，用于判断当前路径是否等于指定路径，然后跳转到指定路径。
>
> 具体解释如下：
> - `this.$route.path` 是当前页面的路径。
> - `item.path` 是指定的路径。
> - `this.$route.path !== item.path` 表示当前路径不等于指定路径。
> - `this.$route.path === '/home'` 表示当前路径等于 "/home"。
> - `item.path === '/'` 表示指定路径等于根路径 "/"。
> - `this.$route.path === '/home' && (item.path === '/')` 表示当前路径等于 "/home" 并且指定路径等于根路径 "/"。
> - `!(this.$route.path === '/home' && (item.path === '/'))` 表示非当前路径等于 "/home" 并且指定路径等于根路径 "/"。
> - `this.$router.push(item.path)` 是跳转到指定路径。
>
> 所以，这段代码的意思是：如果当前路径不等于指定路径，并且当前路径不是 "/home" 或者指定路径不是根路径 "/"，则跳转到指定路径。

###### 1.header组件搭建

①在componens文件夹下创建CommonHeader.vue文件,然后书写页面布局代码：

CommonHeader.vue

```vue
<template>
  <div class="header-container">
    <div class="left-container"></div>
    <div class="right-container"></div>
  </div>
</template>


<script>
export default {
  data() {
    return {

    }
  }
}
</script>

<style lang="less" scoped>
.header-container {
  background-color: #333;
  height: 60px;
}
</style>
```

②在views文件夹下的Main.vue文件中将组件导入：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419134506.png)

③在Main.vue中写入这个组件：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419134809.png)

④基本样式已经出现：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419135012.png)

###### 2.添加button组件及样式

（1）在CommonHeader.vue中添加button组件：

```html
<div class="left-container">
      <el-button icon="el-icon-menu" size="mini"></el-button>
    </div>
```

（2）编写样式：

```css
<style lang="less" scoped>
.header-container {
  padding: 20px;
  background-color: #333;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
```

这是CSS中的属性，用于布局元素的排列方式。`display: flex;` 表示将该元素设置为弹性布局。`justify-content: space-between;` 表示子元素沿主轴（水平方向）对齐，两边的子元素与容器边界保持间距，剩余空间被平均分配给子元素之间的间隔。`align-items: center;` 表示子元素沿交叉轴（垂直方向）对齐，子元素的高度将与容器的高度保持一致。整体上来说，这段样式代码的意思是创建一个弹性布局容器，其中子元素将在主轴上两边对齐，且子元素的高度与容器的高度相等。

（3）面包屑的实现 ---写上首页

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419195352.png)

编写相应的样式属性：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419195432.png)

（4）导航栏右侧实现一个头像加下拉的功能：

> [!NOTE]
>
> 下拉菜单可以在组件库中找到对应样式粘贴即可，然后新建assets文件夹，里面的images文件夹存放图片。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419200355.png)

然后将下拉菜单变成头像的样式，即：先变成图片形式，然后改变样式为圆角

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419201228.png)

css样式为：

```less
 .right-container{
    .logo {
      width: 40px;
      height: 40px;
      border-radius: 50%;
  }
  }
```

页面效果如图:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419201512.png)

## 8.vuex实现左侧折叠

> [!NOTE]
>
> 实现方案:当点击首页左侧按钮时，左侧菜单栏会折叠

###### 1.什么是vuex（详细看官方文档）

​	Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式 + 库**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

###### 2.引入vuex组件

```js
npm i vuex@3.6.2
```

###### 3.在src文件夹下新建一个store文件夹，再在其子文件中新建一个index.js文件，接着在index.js文件中配置vuex的内容：

store文件夹下的index.js文件代码：

```js
import Vue from 'vue'
import Vuex from 'vuex'
import tab from './tab'
Vue.use(Vuex)

// 创建vuex的实例

 export default new Vuex.Store({
  modules:{
    tab
  }
})

这段代码是一个Vuex的配置文件。首先，从Vue库中引入Vue和Vuex插件，并使用Vue.use(Vuex)来安装Vuex插件。

然后，创建一个新的Vuex实例，并将模块tab注册到store中，通过modules对象来指定模块。

最后，通过export default将该实例导出，以便可以在其他地方引入并使用该实例。
```

###### 4.再新建tab.js来管理项目菜单相关数据

tab.js

```js
export default {
  state:{
    isCollapse:false  //控制菜单的展开还是收起
  },
  mutations:{
    // 修改菜单展开收起的方法
    collapseMenu(state){
      state.isCollapse = !state.isCollapse
    }
  }
}

这是一个Vuex的模块配置文件。该模块包含了一个状态state和一个提交mutation的方法。

state对象中包含一个属性isCollapse，用于控制菜单的展开或收起，初始值为false。

mutations对象中包含一个方法collapseMenu，用于修改菜单的展开或收起状态。该方法会将state中的isCollapse属性取反。

当调用collapseMenu方法时，会通过提交mutation的方式来修改state中的isCollapse属性的值。

该模块的作用是用来管理菜单的展开或收起状态。在其他组件中可以通过调用mutation方法来修改该状态的值，从而实现菜单的展开或收起操作。
```

###### 5.最后需要挂载到main.js中

main.js

```js
import Vue from 'vue'
import App from './App.vue'
// 按需引入的组件
// import {Row, Button} from 'element-ui';

// 全局引入
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css';
import router from './router'
import store from './store'
Vue.config.productionTip = false

// 按需引入
// Vue.use(Row);
// Vue.use(Button);

// 全局引入
Vue.use(ElementUI)
new Vue({
  router,
  store,
  render: h => h(App),
}).$mount('#app')

```

###### 6.通过点击按钮触发事件 @click

CommonHeader.vue关键代码：

```vue
<el-button @click="handleMenu" icon="el-icon-menu" size="mini"></el-button>
      <!-- 面包屑 -->
      <span class="text">首页</span>



<script>
export default {
  data() {
    return {}
  },
  methods: {
    handleMenu() {
      this.$store.commit('collapseMenu')
    }
  }
}
</script>


这段代码是一个方法handleMenu()的实现。该方法调用了Vuex的commit方法来提交一个名为'collapseMenu'的mutation。

具体来说，$store是Vue实例中内置的Vuex的store对象，通过commit方法可以提交一个mutation来修改store中的状态。

这里的'collapseMenu'是指向Vuex中的mutation方法，意味着调用这个commit方法会执行该mutation中定义的操作。

通过调用this.$store.commit('collapseMenu')，可以触发Vuex中名为'collapseMenu'的mutation方法，从而修改store中的状态，实现菜单的展开或收起。

需要注意的是，在Vue组件中使用Vuex时，需要在Vue实例中先引入Vuex并安装，才能通过this.$store来访问store对象。
```

CommonAside.vue中书写对应的计算属性：

```js
computed: {
    //没有子菜单
    noChildren() {
      return this.menuData.filter(item => !item.children)
    },
    //有子菜单
    hasChildren() {
      return this.menuData.filter(item => item.children)
    },
    isCollapse() {
      return this.$store.state.tab.isCollapse
    }

  }


这段代码是一个计算属性isCollapse()的实现。该计算属性通过访问Vuex中的状态来获取菜单的展开或收起状态。

通过this.$store.state.tab.isCollapse，可以访问到Vuex中的状态对象state，进而访问到tab模块下的属性isCollapse。

返回的值为菜单的展开或收起状态，即Vuex中存储的isCollapse的值。

在Vue组件中通过调用isCollapse计算属性，可以获取到菜单的展开或收起状态，用于控制菜单的显示与隐藏、样式和交互等操作。
```

###### 实现效果:

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421102523.png)

------

## 9.左侧折叠问题优化

###### 1.当折叠的时候，发现标题并没有被折叠起来

CommonAside.vue

```html
<h3>通用后台管理系统</h3>    修改为：
<h3>{{ isCollapse ? '后台' : '通用后台管理系统' }}</h3>

这段代码是Vue模板中的插值表达式，用于根据isCollapse计算属性的值来显示不同的内容。

具体来说，当isCollapse为true时，即菜单为收起状态，插值表达式的结果为'后台'，则在页面中展示为后台。

当isCollapse为false时，即菜单为展开状态，插值表达式的结果为'通用后台管理系统'，则在页面中展示为通用后台管理系统。

通过这段代码，可以根据菜单的展开或收起状态来动态展示不同的标题内容，增强用户交互和视觉效果。
```

###### 2.观察到侧边栏和导航栏之间有缝隙

CommonAside.vue

```css
<style>
.el-menu {
  border-right: none;
}
</style>
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421104843.png)

------



## 10.home组件布局

###### 1.在el组件库中找到合适的布局效果

```vue
<template>
  <el-row>
  <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
  <el-col :span="16"><div class="grid-content bg-purple-light"></div></el-col>
</el-row>
</template>

这段代码是一个Vue组件的模板部分，同样使用了Element UI中的el-row和el-col组件进行布局。

其中，el-row组件用于创建一个行容器，el-col组件用于创建列容器。通过设置:span属性，可以指定每列占据的格数。

具体来说：
- 第一个el-col组件的:span属性设置为8，表示占据8个格，即占据一行的1/3宽度。
- 第二个el-col组件的:span属性设置为16，表示占据16个格，即占据一行的2/3宽度。

在每个el-col组件中，同样使用了一个div元素作为内容，通过class属性添加了不同的样式类，分别是"bg-purple"和"bg-purple-light"，来实现不同颜色的背景效果。

整个代码段展示了一个行容器，其中包含两列容器，第一列容器占据一行的1/3宽度，第二列容器占据一行的2/3宽度，并且每一列容器都有不同的背景颜色。

这样的布局结构也可以用于实现网格化布局，根据需求将内容划分成不同的宽度，让页面更灵活、美观。
```

###### 2.实现鼠标移入组件有一个阴影的效果（el中的card组件）

```vue
<el-card class="box-card">
        <div class="user">
          <img src="../assets/images/logo2.jpeg" alt="">

          <div class="user-info">
            <p class="name">苏苏</p>
            <p class="access">超级管理员</p>
          </div>
        </div>
      </el-card>

这是一个带有标识和信息的卡片。在该卡片中，有一个用户的图片，用户名为“苏苏”，角色为“超级管理员”。这个卡片可能用于展示用户的信息。
```

编写相应CSS样式：

```less
.user {
  display: flex;
  align-items: center;

  img {
    margin-right: 40px;
    width: 150px;
    height: 150px;
    border-radius: 50%;
  }

  .user-info {
    .name {
      font-size: 32px;
      margin-bottom: 10px;
    }

    .access {
      color: #999999;
    }

这段代码是用来定义一个用户信息的显示样式。首先，使用flex布局来保证用户信息的垂直居中对齐。然后，定义了一个用户头像的样式，包括右边距、宽度、高度和圆角。接着，定义了用户信息的样式，包括姓名的字体大小和底部边距，以及访问权限的文字颜色。
```

###### 3.同理完善相应的内容：

Home.vue

```vue
<template>
  <el-row>
    <el-col :span="8" style="padding-right: 10px">
      <el-card class="box-card">
        <div class="user">
          <img src="../assets/images/logo2.jpeg" alt="">

          <div class="user-info">
            <p class="name">苏苏</p>
            <p class="access">超级管理员</p>
          </div>
        </div>
        <div class="login-info">
          <p>上次登录时间：<span>2024-4-21</span></p>
          <p>上次登录地点：<span>苏州-苏城院</span></p>
        </div>
      </el-card>
    </el-col>
    <el-col :span="16">

    </el-col>
  </el-row>
</template>


<script>
export default {
  data() {
    return {

    }
  }
}
</script>

<style lang="less" scoped>
.user {
  padding-bottom: 20px;
  margin-bottom: 20px;
  border-bottom: 1px solid #ccc;
  display: flex;
  align-items: center;

  img {
    margin-right: 40px;
    width: 150px;
    height: 150px;
    border-radius: 50%;
  }

  .user-info {
    .name {
      font-size: 32px;
      margin-bottom: 10px;
    }

    .access {
      color: #999999;
    }
  }
}

.login-info {
  p {
    line-height: 28px;
    font-size: 14px;
    color: #999999;

    span {
      color: #666666;
      margin-left: 60px;
    }
  }
}
</style>
```

## 11.home购买统计部分

###### 1.表格（el组件库找）

```vue
<el-card style="margin-top: 20px; height: 460px;">
        <el-table :data="tableData" style="width: 100%">
          <el-table-column prop="name" label="型号">
          </el-table-column>
          <el-table-column prop="todayBuy" label="今日购买">
          </el-table-column>
          <el-table-column prop="monthBuy" label="本月购买">
          </el-table-column>
          <el-table-column prop="totalBuy" label="总购买">
          </el-table-column>
        </el-table>
      </el-card>


数据（写死的）
data() {
    return {
      tableData: [
        {
          name: 'oppo',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: 'vivo',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '苹果',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '小米',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '三星',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '魅族',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        }
      ]

    }
  }
```

###### 2.上述代码优化（数组遍历）

```vue
<el-card style="margin-top: 20px; height: 460px;">
        <el-table :data="tableData" style="width: 100%">
          <!-- <el-table-column prop="name" label="型号">
          </el-table-column>
          <el-table-column prop="todayBuy" label="今日购买">
          </el-table-column>
          <el-table-column prop="monthBuy" label="本月购买">
          </el-table-column>
          <el-table-column prop="totalBuy" label="总购买">
          </el-table-column> -->

          <el-table-column v-for="(val, key) in tableLabel" :prop="key" :label="val" />
        </el-table>
      </el-card>


数据（写死的）
data() {
    return {
      tableData: [
        {
          name: 'oppo',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: 'vivo',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '苹果',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '小米',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '三星',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        },
        {
          name: '魅族',
          todayBuy: 100,
          monthBuy: 300,
          totalBuy: 800
        }
      ],
      tableLabel: {
        name: '型号',
        todayBuy: '今日购买',
        monthBuy: '本月购买',
        totalBuy: '总购买'
      }
    }
  }
```

## 12.home订单统计实现

###### 1.首先先写入订单的一些基本Json数据：

```json
countData: [
        {
          name: "今日支付订单",
          value: 1234,
          icon: "success",
          color: "#2ec7c9",
        },
        {
          name: "今日收藏订单",
          value: 210,
          icon: "star-on",
          color: "#ffb980",
        },
        {
          name: "今日未支付订单",
          value: 1234,
          icon: "s-goods",
          color: "#5ab1ef",
        },
        {
          name: "本月支付订单",
          value: 1234,
          icon: "success",
          color: "#2ec7c9",
        },
        {
          name: "本月收藏订单",
          value: 210,
          icon: "star-on",
          color: "#ffb980",
        },
        {
          name: "本月未支付订单",
          value: 1234,
          icon: "s-goods",
          color: "#5ab1ef",
        },
      ],
```

###### 2.在Home.vue中书写右侧的订单界面

Home.vue

```vue
 <div class="num">
      <el-card v-for="item in countData" :key="item.name" :body-style="{ display: 'flex',padding:0}">
        <i class="icon" :class="`el-icon-${item.icon}`" :style="{ background: item.color }"></i>
        <div class="detail">
          <p class="price">￥{{ item.value }}</p>
          <p class="desc">{{ item.name }}</p>
        </div>
      </el-card>
    </div>

这段代码使用了Vue.js和Element UI库来实现一个数值统计的卡片列表。首先，通过v-for循环遍历countData数组中的每个对象，并生成一个el-card组件。每个el-card组件由一个图标和一些详细信息组成。

其中，图标使用了item对象中的icon属性来设置el-icon类名，颜色使用了item对象中的color属性来设置背景色。详细信息部分包括一个显示价格的段落和一个显示描述的段落，分别使用item对象中的value和name属性来显示。整个el-card组件使用flex布局，并设置了padding为0。

最后，整个卡片列表被包裹在一个名为"num"的div元素中。
```

CSS样式：

```less
CSS样式:
.num {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;

  .icon {
    width: 80px;
    height: 80px;
    font-size: 30px;
    color: #fff;
    text-align: center;
    line-height: 80px;
  }

  .detail {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 15px;

    .price {
      font-size: 30px;
      margin-bottom: 10px;
      line-height: 30px;
      height: 30px;
    }

    .desc {
      font-size: 14px;
      color: #999;
      text-align: center;
    }
  }

  .el-card {
    width: 32%;
    margin-bottom: 20px;
  }
}
这段代码定义了一个名为"num"的样式，用于控制数值统计卡片列表的显示样式。具体来说：

1. 使用flex布局使卡片列表垂直排列，并使用flex-wrap: wrap让卡片自动换行。justify-content: space-between将每个卡片在水平方向上均匀分布。

2. icon类的样式设置了宽度、高度、字体大小、颜色、文本居中和行高等属性。

3. detail类的样式使用了flex布局，并设置了垂直居中和左边距。

- price类的样式设置了字体大小、底部边距、行高和高度等属性。
- desc类的样式设置了字体大小、颜色和文本居中等属性。

4. el-card类的样式设置了宽度和底部边距。

总结来说，这些样式定义了卡片列表的整体布局和每个卡片内部元素的样式。通过这些样式，可以实现数值统计卡片列表的合适排列和展示效果。
```

###### 3.界面如图所示：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421125329.png)

------



## 13.axios的基本使用

###### 1.axios是什么？

Axios 是一个基于 *[promise](https://javascript.info/promise-basics)* 网络请求库，作用于[`node.js`](https://nodejs.org/) 和浏览器中。 它是 *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

###### 2.安装axios

```js
npm install axios
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421130407.png)

###### 3.axios的封装

在实际的开发过程中，通常会把axios封看作是当前项目的一个工具方法，除了需要请求的方法以外，可能会还会有对时间的处理、对小数的计算的处理等等之类的逻辑处理，所以一般会把其封装成一个工具方法/工具类。一般放在src下面的utils文件夹下。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421131210.png)

（1）创建实例

src/utils/request.js

```js
import axios from 'axios'

const http = axios.create({
    //通用请求的地址前缀
    baseURL:'/api',
    //超时时间(ms)
    timeout:10000,
})

export default http
```

（2）拦截器

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421131722.png)

```js
import axios from 'axios'

const http = axios.create({
    //通用请求的地址前缀
    baseURL:'/api',
    //超时时间(ms)
    timeout:10000,
})

// 添加请求拦截器
http.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
http.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });

export default http
```

###### 4.api

api指的是接口，一般情况下接口也是也在一个文件夹下，在src文件夹下创建api文件夹，后端接口一般写在api文件夹下。

src/api/index.js

```js
import http from '../utils/request'

//定义请求首页数据接口
export const getData = () => {
    //返回一个promise对象
    return http.get('/home/getData')
}
```

如果接口写好后要进行使用的话，就比如上面写的'/home/getData'，在Home.vue文件中

```js
<script>
import {getData} from '../api'
export default {
  mounted(){
    getData().then((data) => {
      console.log(data)
    })
  }
}
```

网页运行效果如图：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421133252.png)

正常到这里报错是没有问题的，这是因为后端没有回应请求。

## 14.mock数据模拟实战

现在就是后台没有服务器，利用mock进行数据模拟.换句话讲就是当后端还没有完成接口，但是这个时候前端又急需接口来调试的时候用的。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421133632.png)

###### 1.安装mock

````js
npm i mockjs
````

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421134106.png)

###### 2.在api下新建mock.js文件

```js
//1.引入mock
import Mock from 'mockjs'

//2.定义mock请求拦截
Mock.mock('/api/home/getData',function(){
    //拦截到请求后的处理逻辑
    console.log('拦截到了')
})
```

###### 3.在main.js中引入mock

```js
import './api/mock'
```

###### 4.保存运行查看控制台

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421135014.png)

###### 5.在api下新建文件夹mockServeData,在其下创建home.js和permission.js文件用来存储当前首页的数据和后面用户的数据。

mock数据模拟   写入home.js文件中：

```js
// mock数据模拟
import Mock from 'mockjs'

// 图表数据
let List = []
export default {
  getStatisticalData: () => {
    //Mock.Random.float 产生随机数100到8000之间 保留小数 最小0位 最大0位
    for (let i = 0; i < 7; i++) {
      List.push(
        Mock.mock({
          苹果: Mock.Random.float(100, 8000, 0, 0),
          vivo: Mock.Random.float(100, 8000, 0, 0),
          oppo: Mock.Random.float(100, 8000, 0, 0),
          魅族: Mock.Random.float(100, 8000, 0, 0),
          三星: Mock.Random.float(100, 8000, 0, 0),
          小米: Mock.Random.float(100, 8000, 0, 0)
        })
      )
    }
    return {
      code: 20000,
      data: {
        // 饼图
        videoData: [
          {
            name: '小米',
            value: 2999
          },
          {
            name: '苹果',
            value: 5999
          },
          {
            name: 'vivo',
            value: 1500
          },
          {
            name: 'oppo',
            value: 1999
          },
          {
            name: '魅族',
            value: 2200
          },
          {
            name: '三星',
            value: 4500
          }
        ],
        // 柱状图
        userData: [
          {
            date: '周一',
            new: 5,
            active: 200
          },
          {
            date: '周二',
            new: 10,
            active: 500
          },
          {
            date: '周三',
            new: 12,
            active: 550
          },
          {
            date: '周四',
            new: 60,
            active: 800
          },
          {
            date: '周五',
            new: 65,
            active: 550
          },
          {
            date: '周六',
            new: 53,
            active: 770
          },
          {
            date: '周日',
            new: 33,
            active: 170
          }
        ],
        // 折线图
        orderData: {
          date: ['20191001', '20191002', '20191003', '20191004', '20191005', '20191006', '20191007'],
          data: List
        },
        tableData: [
          {
            name: 'oppo',
            todayBuy: 500,
            monthBuy: 3500,
            totalBuy: 22000
          },
          {
            name: 'vivo',
            todayBuy: 300,
            monthBuy: 2200,
            totalBuy: 24000
          },
          {
            name: '苹果',
            todayBuy: 800,
            monthBuy: 4500,
            totalBuy: 65000
          },
          {
            name: '小米',
            todayBuy: 1200,
            monthBuy: 6500,
            totalBuy: 45000
          },
          {
            name: '三星',
            todayBuy: 300,
            monthBuy: 2000,
            totalBuy: 34000
          },
          {
            name: '魅族',
            todayBuy: 350,
            monthBuy: 3000,
            totalBuy: 22000
          }
        ]
      }
    }
  }
}
```

###### 6.在mock.js文件中导入封装的mock数据

```js
//1.引入mock
import Mock from 'mockjs'
import homeApi from './mockServeData/home'

//2.定义mock请求拦截
Mock.mock('/api/home/getData',homeApi.getStatisticalData)
```

###### 7.程序控制台如下：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421140303.png)

------



## 15.首页可视化图表样式调整

##### （1）首先把上述图表写死的数据用mock生成的tableData数据代替：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421140656.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421141021.png)

```js
mounted() {
    getData().then(({ data }) => {
      const { tableData } = data.data
      this.tableData = tableData
    })
  }

这段代码是一个方法（mounted），它调用了一个名为getData的函数，并使用then方法对返回的Promise对象进行处理。当这个Promise对象被解析（即异步操作完成）时，会执行回调函数。回调函数接收一个对象作为参数，该对象的data属性又包含一个data属性。回调函数从这个对象中提取tableData属性，并将其赋值给当前对象（this）的tableData属性。
```



##### (2)运行效果：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421141110.png)

##### （3）实现右侧图表的布局：

Home.vue

```vue
<el-card style="height: 280px">
      <!-- 折线图 -->
    </el-card>

    <div class="graph">
      <el-card style="height: 260px"></el-card>
      <el-card style="height: 260px"></el-card>
    </div>
```

对应的CSS样式：

```less
.graph {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;

  .el-card {
    width: 48%;
  }

}


这段代码是CSS样式代码，它定义了一个类名为"graph"的样式规则。

首先，该样式规则给类名为"graph"的元素的上外边距(margin-top)设置为20像素。

接下来，该规则定义了这个元素的布局方式(display)为flex弹性布局，并设置对齐方式(justify-content)为space-between，即在容器中平均分配空间，并在每两个元素之间留有等宽的间距。

最后是一个嵌套规则(.el-card)，它定义了所有类名为"el-card"的元素的宽度(width)为48%，即将宽度平均分配为容器宽度的48%。这样，在之前定义的容器布局中，两个el-card元素将平分容器的宽度，并且两个元素之间留有间距。

通过这段样式代码，可以实现两个el-card元素水平并排，宽度平分容器，并与上方的元素有一定的间距。
```

##### （4）最后页面布局：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421170507.png)



------



## 16.echarts表格的基本使用

##### 1.安装echarts

```js
npm i echarts@5.1.2
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240421192745.png)

##### 2.引入echarts

在对应的页面中引入echarts,比如说我的图表是在主页中显示，所以在Home.vue中引入：

```js
import * as  echarts from 'echarts'
```

##### 3.编写代码（echarts表格的折线图）

echarts代码的书写位置应该写在mounted的生命周期中。（参考官网文档）

Home.vue

````js
<!-- 折线图 -->
<div ref="echarts1" style="height:280px"></div>
````

对应的js代码：

```js
// 基于准备好的dom,初始化echarts实例
      const line_echarts = echarts.init(this.$refs.echarts1)
      // 指定图表的配置项和数据
      var line_echartsoption = {}
      // 处理数据xAxis
      const { orderData } = data.data
      const xAxis = Object.keys(orderData.data[0])

      const xAxisData = {
        data: xAxis
      }
      line_echartsoption.xAxis = xAxisData
      line_echartsoption.yAxis = {}
      line_echartsoption.legend = xAxisData

      line_echartsoption.series = []

      xAxis.forEach(key => {
        line_echartsoption.series.push({
          name: key,
          data: orderData.data.map(item => item[key]),
          type: 'line'
        })
      })
      //使用刚指定的配置和数据显示图表
      line_echarts.setOption(line_echartsoption)

    这段代码是一个基于Vue.js框架中使用echarts图表库的示例代码。它展示了如何使用预先准备好的DOM元素初始化echarts实例，并为图表定义配置项和数据。

首先，通过`echarts.init(this.$refs.echarts1)`代码初始化了一个echarts实例，这个实例将会在名为`echarts1`的DOM元素上显示出来。

接着定义了一个空的`line_echartsoption`对象，用来存储图表的配置项和数据。然后从接收到的数据中提取出了`orderData`，并将`orderData.data[0]`中的键作为`xAxis`（x轴）的数据。将x轴的数据放入`xAxisData`对象中，然后将其赋值给`line_echartsoption.xAxis`。y轴的定义则直接给`line_echartsoption.yAxis`赋一个空对象。同时，也将x轴的数据定义给`legend`属性，作为图例。

接下来，在`line_echartsoption.series`数组中添加了一些对象。对于这些对象，使用了`xAxis.forEach`循环遍历x轴的每一个数据，并将其加入到`line_echartsoption.series`数组。其中，`name`表示该数据系列的名称，`data`表示该数据系列的具体数据，`type`为'line'表示这是一个线性图表。

最后，使用`line_echarts.setOption(line_echartsoption)`将刚才定义的配置和数据应用到图表中进行显示。

```

##### 4.echarts表格的柱状图

①在第二个表格内引入echarts图表

```vue
<div class="graph">
      <el-card style="height: 260px">
        <div ref="echarts2" style="height: 260px;"></div>
      </el-card>
```

②同样是先基于准备好的dom,初始化echarts实例

```js
//柱状图
const histo_echarts = echarts.init(this.$refs.echarts2)

const histo_echartsOption = {
          legend: {
            // 图例文字颜色
            textStyle: {
              color: "#333",
            },
          },
          grid: {
            left: "20%",
          },
          // 提示框
          tooltip: {
            trigger: "axis",
          },
          xAxis: {
            type: "category", // 类目轴
            data: userData.map(item => item.data),//获取userData的数据
            axisLine: {
              lineStyle: {
                color: "#17b3a3",
              },
            },
            axisLabel: {
              interval: 0,
              color: "#333",
            },
          },
          yAxis: [
            {
              type: "value",
              axisLine: {
                lineStyle: {
                  color: "#17b3a3",
                },
              },
            },
          ],
          color: ["#2ec7c9", "#b6a2de"],
          series: [
              {
                  name:'新增用户',
                  data: userData.map(item => item.new),
                  type:'bar'
              },
              {
                  name:'活跃用户',
                  data: userData.map(item => item.active),
                  type:'bar'
              }
          ],
        },
      
      这段代码是使用ECharts库绘制柱状图的示例。具体解释如下：

1. `histo_echarts` 是一个ECharts实例，使用 `echarts.init` 函数初始化并传入一个DOM元素（通过 `this.$refs.echarts2` 获取）。
2. `histo_echartsOption` 是一个ECharts的配置对象，用来描述图表的属性和数据。
3. `legend` 是图例配置，用来展示数据系列的标识和样式。
4. `grid` 是网格配置，用于调整图表在画布上的位置和大小。
5. `tooltip` 是提示框配置，用于展示用户在图表上的交互操作时的提示信息。
6. `xAxis` 是X轴配置，指定类型为 "category" 表示为类目轴，即横坐标上的数据类型为离散的类目数据。`data` 属性是一个数组，用于设置X轴上的刻度标签，这里的数据来源于 `userData` 数组中的 `data` 属性。
7. `yAxis` 是Y轴配置，指定类型为 "value" 表示为数值轴，即纵坐标上的数据类型为数值。`axisLine` 属性用来设置轴线的样式。
8. `color` 是系列的颜色配置，用于指定不同系列的颜色。
9. `series` 是系列配置，用于描述每个系列的数据和类型。这里定义了两个柱状图系列，分别是 "新增用户" 和 "活跃用户"，数据来源于 `userData` 数组中的 `new` 和 `active` 属性。

最后，通过调用 `histo_echarts.setOption(histo_echartsOption)` 将配置应用到ECharts实例中，从而生成和渲染柱状图。
```

③调用实例对象的Option

````js
//柱状图
const histo_echarts = echarts.init(this.$refs.echarts2)
const histo_echartsOption = {
    ...
}
    histo_echarts.setOption(histo_echartsOption)
````

##### 5.echarts表格的饼状图

①在第三个表格内引入echarts

```vue
<el-card style="height: 260px">
        <!-- 饼状图 -->
        <div ref="echarts3" style="height: 260px;"></div>
      </el-card>
```

②同样是先基于准备好的dom,初始化echarts实例

```js
// 饼状图
      const circle_echarts = echarts.init(this.$refs.echarts3)
      const circle_echartsOption = {
        tooltip: {
          trigger: "item",
        },
        color: [
          "#0f78f4",
          "#dd536b",
          "#9462e5",
          "#a6a6a6",
          "#e1bb22",
          "#39c362",
          "#3ed1cf",
        ],
        series: [
          {
            data: videoData,
            type: 'pie'

          }
        ],
      }
```

③调用实例对象的Option

```js
// 处理数据xAxis
      const { orderData, userData, videoData } = data.data
      
      
circle_echarts.setOption(circle_echartsOption)
```

##### 6.运行效果：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240422125409.png)

## 17.面包屑&tag介绍

##### 1.了解面包屑

> [!NOTE]
>
> 在网站应用中，面包屑导航的作用就是帮助访问者确定自己处在网站中的什么位置以及如何返回到原来的位置。对于用户而言，这个导航辅助工具可以更轻松地在网站上查找内容，帮助用户定位在你网站上的位置，并在需要时帮助用户回到之前页面。对于搜索引擎来讲，面包屑导航会让用户了解你的网站结构，方便爬取索引。

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240422125943.png)

##### 2.element-ui引入面包屑组件

```vue
<el-breadcrumb separator="/">
  <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
  <el-breadcrumb-item><a href="/">活动管理</a></el-breadcrumb-item>
  <el-breadcrumb-item>活动列表</el-breadcrumb-item>
  <el-breadcrumb-item>活动详情</el-breadcrumb-item>
</el-breadcrumb>
```

##### 3.在CommonHeader.vue文件中书写对应代码：

CommonHeader.vue

```vue
 <!-- 面包屑 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item><a href="/">活动管理</a></el-breadcrumb-item>
      <el-breadcrumb-item>活动列表</el-breadcrumb-item>
      <el-breadcrumb-item>活动详情</el-breadcrumb-item>
    </el-breadcrumb>
```

对应界面如下：

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240422130622.png)

##### 4.使用vuex来进行统一的数据存储

src/store/tab.js

```js
state:{
    isCollapse:false,  //控制菜单的展开还是收起
    tabsList:[
      // 面包屑数据
      {
        path:"/",
        name:"home",
        label:"首页",
        icon:"s-home",
        url:"Home/Home",
      }
    ]
  },
```

逻辑处理:就是当点击左侧导航栏时，面包屑的路由也要随之发生变化，也就是components/CommonAside.vue中写入点击事件的处理逻辑，要修改state的数据，首先想到应该在mutation里面去修改，也就是说，当点击菜单的时候，应该是去调用store里面的mutation方法：

①点击事件：

```js
// 点击菜单
    clickmenu(item) {
      // 当页面的路由与跳转的路由不一致才允许跳转
      if (this.$route.path !== item.path && !(this.$route.path === '/home' && (item.path === '/'))) {
        this.$router.push(item.path)
      }
      this.$store.commit('selectMenu',item)
    }
  },
```

②更新面包屑数据,有一个逻辑处理：

```js
```





# 附录：Git的常用命令

###### 1、配置用户名和邮箱(并保存)

```css
git config --global user.name "susu"
git config --global user.email 1983748570@qq.com
git config --global credential.helper store
```

###### 2.查看已配置的信息

```css
git config --global --list
```

###### 3.新建仓库

```css
方法一： git init 
方法二： git clone https://gitee.com/zhang-menglong222/vue2_learning.git
```

###### 4.查看仓库的状态

```css
git status
```

###### 5.添加到暂存区

```css
git add .
```

###### 6.提交

```css
git commit -m "编辑信息"
```

###### 7.SSH配置和克隆仓库

```css
1.首先cd 回车 ，再 cd.ssh 在其目录下敲如下代码：
ssh-keygen -t rsa -b 4096

2.随便写一个文件名  比如说test
3.然后输入ls -ltr查看文件
4.输入vi test.pub查看私钥
5.回到github页面，然后在setting点击SSH and GPG Keys选项,然后新建ssh密钥，此时已经添加完成。
```

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419161100.png)

![](C:\Users\uu\Desktop\vue2学习\images\QQ截图20240419161616.png)

###### 8. add push pull

```css
git add . 
git commit -m "注释"
git push
```

> [!IMPORTANT]
>
> [解决Please make sure you have the correct access rights and the repository exists 问题.]: https://blog.csdn.net/qq_43705131/article/details/107965888
>
> 

###### 9.常用团队之间上传代码（本地上传到远程仓库）

> [!CAUTION]
>
> ①安装完成git后在要上传的文件内部左键Git Bash here
>
> ②将下面配置的命令输入，表示仓库保存位置
>
> git config --global user.name "susu"
>     git config --global user.email 1983748570@qq.com
>
> ③创建git    :  git init
>
> ④查看git状态  ：  git status
>
> ⑤提交文件添加到缓存区   :  git add . 
>
> ⑥提交：   git  commit    -m  "描述信息"
>
> ⑦建立与远程仓库关联：  git remote add origin https://github.com/1983748570zhang/vue3_susu.git
>
> ⑧将本地main分支的更改推送到远程origin仓库：git push -u origin "master"
>
> 



