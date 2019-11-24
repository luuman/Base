## 添加Mackdown 文件解析
### 标签

```javascript
<vue-markdown v-highlight :source="markdown"></vue-markdown>
```

### main.js 全局方式

```javascript
import hljs from 'highlight.js'
import 'highlight.js/styles/solarized-dark.css'
Vue.directive('highlight', (el) => {
  let blocks = el.querySelectorAll('pre code')
  blocks.forEach((block) => {
    hljs.highlightBlock(block)
  })
})
```
![](./_image/2019-08-05/2019-08-11-23-48-50.jpg)
```javascript
import VueMarkdown from 'vue-markdown'
import hljs from 'highlight.js'
import 'highlight.js/styles/solarized-dark.css'

# 延迟渲染
markdownShow () {
  setTimeout(() => {
    let blocks = document.getElementById('api1').querySelectorAll('pre code')
    blocks.forEach((block) => {
      hljs.highlightBlock(block)
    })
  }, 1000)
}
```

## 在线编辑Markdown
### 标签
```javascript
<mark-down @on-paste-image="handlePasteImage" @on-save="save" :theme="theme" :initialValue="markdown" :markedOptions="{baseUrl:'http://smalleyes.oss-cn-shanghai.aliyuncs.com/'}"></mark-down>
```

### 配置
```javascript
// 开发文件
import MarkDown from 'SRC/markdown/index'
// Demo文档
import doc from 'SRC/doc'

mounted () {
  setTimeout(() => {
    this.initialValue = doc
  }, 1000)
},
data: () => ({
  initialValue: '',
  theme: 'OneDark'
})
save (res) {
  console.log(res)
},
handlePasteImage (res) {
  console.log(res)
},
```