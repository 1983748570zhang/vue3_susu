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

CommonHeader.vue

```vue
<template>
  <div class="header-container">
    <div class="left-container">
      <el-button icon="el-icon-menu" size="mini"></el-button>
    </div>
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
  padding: 20px;
  background-color: #333;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
```

------



## 附录：Git的常用命令

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
git add
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

###### 8.push pull

```
git push
```

