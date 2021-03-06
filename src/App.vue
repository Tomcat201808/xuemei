<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by 缘分
* 
*
*
* 雪梅，我是福君————
* 一个很喜欢你，但是又不知如何表达的呆子
* 作为程序员，我写一份自我介绍，以表达爱慕之情，慰藉相思之苦
* 方便你了解更真实的我
*
*
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始写咯... */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
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
`, `/* 最后，
 * 感谢命运，安排你我相遇相知相恋，在茫茫人海之中邂逅你。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `福君
====

坐标：深圳福田。

Java架构师，大数据项目经理，机器学习算法工程师

技能
====

数据库设计
----
  - 结构化数据库设计
  - 数据仓库模型设计

后端开发
----
  - 用户管理
  - 多点登录，消息漫游
  - 交易系统
  - 支付系统
  - 公众号开发

前端开发
----
  - Web前端开发

产品设计
----
  - 省级银行大数据平台
  - 某县城电子政务平台
  - 天眼监控平台
  - CMCC-BOSS(中国移动运营支撑管理系统)

技术及语言
----
  - Java:      JVM, Springboot, MyBatis
  - Big Data:  Hadoop, Zookeeper, Hive, Spark, Storm, Flink，Apache Beam
  - Python:    pandas, numpy, matplotlib,sklearn
  - DataBase:  Oracle, MySQL, GreenPlum, Hbase, Redis
  - WebServer: Tomcat, nginx
  - OS:        CentOS, UNIX, Windows
  - Others:    git, Xmind

工作经历
----

1. 中国移动通信集团广西有限公司
2. 中国银行深圳分行


教育经历
----

1. 广西大学 计算机科学与技术学士



文章
====

* [读《亲密关系》 ](https://mp.weixin.qq.com/s/PIlYV_v0ZI2L6H2EQv2anw)
* [寻找那些长期对你好的人](https://mp.weixin.qq.com/s/6BFAY1p1U4Is7cTopyhdfg)
* [数据库老头儿的独孤九剑](https://mp.weixin.qq.com/s/LVWEAcw1rlT2BfhDZ-qDBQ)
* [太史公的智慧——也谈谈《货殖列传》](https://mp.weixin.qq.com/s/HYrTyjTXp3oOs-_sJm8ytw)
* [深度学习——卷积神经网络的奇妙](https://mp.weixin.qq.com/s/lPrM-HelOBrb0MwlJ65NOw)
* [关于三个概况人类文明公式的感悟](https://mp.weixin.qq.com/s/4okM9FeGKE5_IZ8lM4OJFg)
* [精神资源与深度关系](https://mp.weixin.qq.com/s/mtVVuJU9Pqel4ehfuv__qQ)

链接
====

* 
* [微信公众号](概率邦)
* 


勾引方式
====

* 微信：weifujun2

`, thanksMarkdown: `

感恩
----

* 感谢命运，感恩你我相遇，相知，相恋，你于我，独一无二，无人能取代————
* 1.有幸看到你的执念，也看到了我自己，我们前世一定有着海誓山盟的缔约;
* 2.因为你对人生的不卑不亢、从容优雅，早已认你是个知己；
* 3.你的独立，你的优雅，你的气质，时时刻刻都牵动着我的思绪，魂牵梦萦；
* 4.人生苦短，佳音难觅，我们应开启这段亲密的关系之旅；
* 5.某年某月某日，江南，雪里，赏评风雪中的一枝梅，余生不枉费；
* 6.路，仍不长不短，却越走越远；风，已不变不依，情愈来越浓；眼，是不偏不倚，想望穿秋水；手，也不温不热，盼与雪梅相携人生。
* ...
* 未完待续...


  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) {
              return
            }
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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
  }

  html {
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>
