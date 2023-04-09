<template>
  <div class="post-main-container" :class="{'sidebar-empty':!cata.menuData.length}">
    <div class="header-container">Article Cover</div>
    <div class="main-container">
      <div class="article-area">
        <div class="markdown-body">
          <h2 id="h2--vite-"><a name="创建vite项目" class="reference-link"></a><span class="header-link octicon octicon-link"></span>创建vite项目</h2><p>根据vite官方文档 来创建一个基础的模板</p>
          <pre><code class="lang-bash">npm create vite@latest
</code></pre>
          <h2 id="h2--vue-router"><a name="安装vue-router" class="reference-link"></a><span class="header-link octicon octicon-link"></span>安装vue-router</h2><pre><code class="lang-bash">npm install vue-router@4
</code></pre>
          <p>使用方式:</p>
          <p>vue-router4+在使用方式上与之前的版本有了些许差别,具体体现在了创建方式,以及模式切换上</p>
          <p>声明方式：</p>
          <pre><code class="lang-js">import { createRouter } from 'vue-router'

// routes的书写形式与之前相比并无变化
const routes = [
  {
    path: '/',
    component: () =&gt; import('../components/HelloWorld.vue')
  }
]

// 新的router采用的导入 createRouter() 的方式来创建router实例
const router = createRouter({
  routes
})
</code></pre>
          <p>模式切换: 对于路由,我们所知是有两种不同的历史记录模式 Hash模式 和 HTML5模式(history模式)</p>
          <pre><code class="lang-js">import { createRouter, createWebHashHistory, createWebHistory } from 'vue-router'

// 同样是以导入的形式,导入 Hash模式createWebHashHistory() 或 HTML5模式createWebHistory() 来进行使用
const router = createRouter({
  history: createWebHashHistory() 或 createWebHistory(),
  routes
})
</code></pre>
          <p>当然创建实例后,需要在main.js里进行挂载才能进行使用</p>
          <h2 id="h2--pinia"><a name="安装pinia" class="reference-link"></a><span class="header-link octicon octicon-link"></span>安装pinia</h2><p>pinia是一个类似vuex的插件。它是最新一代的轻量级状态管理插件,已经正式加入了vue全家桶</p>
          <p>pinia的优点:</p>
          <ul>
            <li><p>非常简便，存储和组件变得很类似，你可以轻松写出优雅的存储。</p>
            </li><li><p>类型安全，通过类型推断，可以提供自动完成的功能。</p>
          </li><li><p>vue devtools 支持，可以方便进行调试。</p>
          </li><li><p>Pinia 支持扩展，可以非常方便地通过本地存储，事物等进行扩展。</p>
          </li><li><p>模块化设计，通过构建多个存储模块，可以让程序自动拆分它们。</p>
          </li><li><p>非常轻巧，只有大约 1kb 的大小。</p>
          </li><li><p>服务器端渲染支持</p>
          </li></ul>
          <p>安装方式：</p>
          <pre><code class="lang-bash">npm install pinia
</code></pre>
          <p>使用方式：</p>
          <p>pinia与vuex一样也有着 state, getters, actions. 在pinia中抛弃了vuex中的mutation,并且action支持同步和异步</p>
          <p>首先修改main.js，引入pinia提供的createPinia方法，创建根存储</p>
          <pre><code class="lang-js">// main.js
import { createPinia } from 'pinia'
app.use(createPinia())
</code></pre>
          <p>store.js中使用pinia提供的 <strong>defineStore()</strong> 来构建一个store,该store用来存放我们需要全局使用的数据</p>
          <pre><code class="lang-js">import { defineStore } from 'pinia'

// defineStore()会接收两个参数：
// name：一个字符串，必传项，该store的唯一id
// options：一个对象，store的配置项,属性包含state,getters,actions
export const useUserStore = defineStore('user', {
  state: ()=&gt; {
    return {
      count: 0
    }
  },
  getters: {
    getCount: (state)=&gt; {
      return state.count + 1
    }
  },
  actions: {
    setCount(count){
      this.count = count
    }
  }
})
</code></pre>
          <h2 id="h2--element-plus"><a name="安装element-plus" class="reference-link"></a><span class="header-link octicon octicon-link"></span>安装element-plus</h2><pre><code class="lang-bash">npm install element-plus --save
</code></pre>
          <p>我这里使用的官方介绍的全局引入的方式</p>
          <pre><code class="lang-js">import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)
// 在引入 Element Plus 时，可以传入一个包含 size 和 zIndex 属性的全局配置对象。
// size 用于设置表单组件的默认尺寸，zIndex 用于设置弹出组件的层级，zIndex 的默认值为 2000。
app.use(ElementPlus, { size: 'small', zIndex: 3000 })
</code></pre>
          <p>特别要注意一点,elementPlus中使用icon不再由element-plus包内提供. 因此,之前通过@element-plus/icons-vue来直接引入使用的方式会发生错误<br>@element-plus/icons-vue被分离出来作为一个单独的包,如果有需要使用icon,那么需要进行安装</p>
          <pre><code class="lang-bash">npm install @element-plus/icons-vue
</code></pre>
          <h2 id="h2--main-js"><a name="完整main.js" class="reference-link"></a><span class="header-link octicon octicon-link"></span>完整main.js</h2><pre><code class="lang-js">import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import router from './router'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import * as ElementPlusIconsVue from '@element-plus/icons-vue'
import { createPinia } from 'pinia'

const app = createApp(App)
// 在引入 Element Plus 时，可以传入一个包含 size 和 zIndex 属性的全局配置对象。
// size 用于设置表单组件的默认尺寸，zIndex 用于设置弹出组件的层级，zIndex 的默认值为 2000。
app.use(ElementPlus, { size: 'small', zIndex: 3000 })
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
  app.component(key, component)
}

app.use(router)

app.use(createPinia())

app.mount('#app')
</code></pre>
        </div>
      </div>
      <div class="sidebar">
        <div class="sticky-block-box post_tree" :style="{ top: anchorPosition.top }">
          <ul class="menu_content">
            <li class="menu_content-item" v-for="(item, key) of cata.menuData" :key="key">
              <a
                :style="menuStyle(item.type)"
                @click="doMenu(item.point)"
                href="javascript:void(0);"
                class="tree_list"
                :title="item.txt"
                :class="{active_tree_item: cata.menuState === item.txt}"
              >
                {{ item.txt }}
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="other-container">Some more markup text so that the affix can reach the end of the content section.</div>
  </div>
</template>

<script>
import Prism from "prismjs";
import "prismjs/themes/prism-okaidia.min.css";
import 'github-markdown-css/github-markdown-dark.css'

export default {
  name: "Article",
  data(){
    return {
      cata: {
        menuData: [],
        menuState: ""
      },
      anchorPosition: {
        top: '0'
      }
    }
  },
  mounted() {
    this.componentDidMount();
    Prism.highlightAll();
  },
  methods: {
    componentDidMount(){
      this.getElement(['H1', 'H2', 'H3', 'H4'])
    },
    getElement(nodeArr){
      let nodeInfo = []
      const dom = document.querySelector('.markdown-body')
      // console.log(dom.childNodes)
      dom?.childNodes.forEach((item, key) => {
        // console.log(item.nodeName)
        if (nodeArr.includes(item.nodeName)) {
          nodeInfo.push({
            type: item.nodeName,
            txt: item.innerText,
            offsetTop: item.offsetTop,
            point: `target_${key}`,
          })
          item.setAttribute('id', `target_${key}`)
          // console.log(item)
        }
      })
      if(!nodeInfo.length) return
      this.cata.menuData = nodeInfo
      this.cata.menuState = nodeInfo[0].txt
      window.addEventListener('scroll', this.onScroll, true)
      // console.log('nodeInfo', nodeInfo)
    },
    onScroll(e){
      const stickyTopVal = '110px'
      // 当前页面滚动的距离
      let scrollTop = e.target.documentElement?.scrollTop || e.target.body?.scrollTop
      // console.log(scrollTop)
      //变量windowHeight是可视区的高度
      let windowHeight = document.documentElement.clientHeight || document.body.clientHeight
      //变量scrollHeight是滚动条的总高度
      let scrollHeight = document.documentElement.scrollHeight || document.body.scrollHeight

      let currentmenu = this.cata.menuData[0].txt // 设置menuState对象默认值第一个标题
      for (let item of this.cata.menuData) {
        // console.log(item.offsetTop)
        if (scrollTop >= item.offsetTop) {
          currentmenu = item.txt
        } else break
      }

      if (currentmenu !== this.cata.menuState) {
        this.cata.menuState = currentmenu
      }

      if(this.anchorPosition.top !== stickyTopVal) {
        this.anchorPosition.top = stickyTopVal
      }

      if (scrollTop === 0) {
        this.anchorPosition.top = '0'
      }
      // 如果到底部，就命中最后一个标题
      if (scrollTop + windowHeight === scrollHeight) {
        console.log('滚动到底部了')
        this.cata.menuState = this.cata.menuData[this.cata.menuData.length - 1].txt
      }
    },
    menuStyle(type){
      let style = {}
      if (type === 'H2') style = { 'padding-left': 10 + 'px' }
      if (type === 'H3') style = { 'padding-left': 20 + 'px' }
      if (type === 'H4') style = { 'padding-left': 30 + 'px' }
      return style
    },
    doMenu(id){
      if(!id) return
      const target = document.querySelector(`#${id}`);
      const targetTop = target.getBoundingClientRect().top + window.scrollY - 80;
      window.scrollTo({
        top: targetTop,
        behavior: 'smooth'
      });
    }
  },
}
</script>

<style scoped>
.post-main-container {
  margin: 0 auto;
  width: 100%;
  max-width: var(--width);
}
.main-container {
  margin-top: 50px;
  display: flex;
  justify-content: space-between;
  position: relative;
}
.header-container {
  text-align: center;
  font-size: 30px;
  height: 300px;
  line-height: 300px;
  color: #fff;
  border: 1px solid #545454;
  margin-top: 50px;
  width: 100%;
}
.other-container {
  text-align: center;
  font-size: 30px;
  height: 650px;
  line-height: 650px;
  color: #fff;
  border: 1px solid #545454;
  margin-top: 50px;
  width: 100%;
}
.article-area {
  width: 81%;
}
.sidebar {
  width: 15.6666666%;
}
.sticky-block-box {
  position: sticky;
  top: 0;
  width: 100%;
  transition: top .3s;
  display: flex;
  flex-direction: column;
}
.post_tree {
  min-height: 400px;
  max-height: 70vh;
  overflow-y: auto;
}

.post_tree .menu_content {
  width: 100%;
  padding: 0;
  margin: 0;
}

.post_tree .menu_content .menu_content-item {
  list-style-type: none;
  text-decoration: none;
  padding: 0 !important;
}

.post_tree .menu_content .tree_list {
  display: block;
  text-decoration: none;
  padding: 5px 0 5px 10px;
  border-left: 1px solid transparent;
  line-height: 20px;
  font-size: 16px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  outline: 0;
  color: #808080;
}

.post_tree .menu_content .tree_list:hover {
  color: #3c93f8;
}

.post_tree .menu_content .active_tree_item {
  position: relative;
  color: #3c93f8;
}

.post_tree .menu_content .active_tree_item::before {
  content: '';
  height: 20px;
  width: 5px;
  background: #3c93f8;
  position: absolute;
  left: -17px;
  top: 50%;
  border-radius: 0 5px 5px 0;
  transform: translate(-50%, -50%);
}
</style>
