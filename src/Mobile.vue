<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 40,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
/*
* 你好，我是毕国康
* 本人正在找工作，所以我现在在写一份在线简历！
* 感谢您花时间阅读我的在线简历，期待能有机会和您共事
* pc大屏幕看效果最佳
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: rgb(105,105,105);
}
/* 文字离边框太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  overflow: auto;
  background-color: #303030;
  width: 90vw;
  margin: 2.5vh 5vw;
  height: 90vh;
}
/* 太高了 */
.styleEditor {
  height: 45vh;
}
/* 代码高亮 */
.token.selector{
  color: rgb(255,0,0);
}
.token.property{
  color: rgb(187,137,0);
}
.token.punctuation{
  color: yellow;
}
.token.function{
  color: rgb(42,161,152);
}

/* 加点 3D 效果呗 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  transform: rotateX(-10deg) translateZ(-50px) ;
}

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed;
  top: 50%; left: 0;
  padding: .5em;  margin: 2.5vh;
  width: 95vw; height: 45vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,
          `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`
          ,
          `
/* 再对 HTML 加点样式 */
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `
# 毕国康的在线个人简历

感谢您花时间阅读我的简历，期待能有机会和您共事，想了解更多信息可以面谈


## 个人信息
 - **毕国康**/男/1995
 - **本科**/韶关学院 物联网工程
 - **期望职位**：web前端开发、node.js开发
 - **期望城市**：广州、深圳
 - **手机**：17666503029
 - **邮箱**：bi@guokang.email
 - **微信**：workbiguokang
 - **Github**：https://github.com/biguokang
 - **个人网站**：https://biguokang.cn



## 技术栈清单
以下均为我熟练使用的技能，均用来做过东西

* **web开发**：html5+css+JavaScript三件套，熟悉es6，掌握闭包、原型链、异步概念
* **Web框架和库**：React.js/Vue.js/Bootstrap/ElementUI/jQuery/live2d.js
* **前端工具**：npm包管理器/webpack/create-react-app/Vue-cli/Dva
* **状态管理**：Redux/react-redux/vuex
* **网络请求**：ajax/fetch/vue-resource/axios
* **异步编程**：callback/Promise/Generator/async
* **后台技术**：node.js/express框架/cookies-session
* **服务器**：nginx/nginx反向代理/nginx转发
* **数据库**：MySQL
* **版本管理**：git
* **操作系统**：windows/macos/Ubuntu/Centos
* **其他（略懂）**：php/python3/java/wxpy/c/http协议

## 开源项目和作品
1. [基于react框架开发的单页博客系统](https://biguokang.cn)
2. [基于vue框架开发的单页博客系统](http://vue.biguokang.cn)
3. [基于node.js的express框架开发的博客后台系统](https://biguokang.cn/#/backstage)
4. [基于live2d.js的web嵌入式人工智能，拥有聊天和图片识别功能](http://live2d.biguokang.cn)
5. [基于wxpy的微信智能ai，拥有聊天和图片识别功能，ai微信号biguokang，欢迎调戏](https://github.com/biguokang/bgk_weixin_bot)
6. [基于wxpy和百度审核ai的的微信智能语言图片审核，能够识别微信对话内容和图片是否存在违规情况](https://github.com/biguokang/bgk-wechat-cleaner)


## 博客文章：
* [本人对于JavaScript原型和原型链的理解](https://biguokang.cn/#/article/66)
* [JavaScript异步编程技术方法总结](https://biguokang.cn/#/article/68)

## 自我评价：
- 技术：
   - js自认中等水平吧，作用域、闭包、原型链、异步、es6还是能吹上几分钟的；
   - css一般只记得常用的属性，不常用的要翻文档，会写响应式页面；
   - 框架方面对React比较熟，平时React用的也比较多；
   - 当然了Vue我也会用，也能用Vue造出东西，不过没有React那么熟；
   - 因为自己买了服务器搭过项目，自认为it知识广度比较广；
- 个人：
   - 为人乐观，性格开朗
   - 热爱it技术，业余喜欢搞点有趣的线上项目，喜欢动手。
   - 热爱学习，热衷接触新技术新事物。
   - 能接受加班


> 如果你想知道更多详细信息，<a href="resume.txt" download="简历">点击这里</a>下载pdf版简历
`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          this.$nextTick(() => {
            this.$refs.resumeEditor.goTop()
          })
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-height: 100vh; position: relative;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }

</style>
