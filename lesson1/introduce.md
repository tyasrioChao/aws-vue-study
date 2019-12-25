# 1.vue介绍

看下面来自官网的介绍，可以知道vue本体只是针对于HTML视图(类比于SpringMVC框架中的thymeleaf模板，只不过vue在前端进行，但是vue也有服务器端渲染，有时间的话进行介绍)

```text
Vue是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图。
```

让我们看一个简单的例子：  

<p class="codepen" data-height="240" data-theme-id="default" data-default-tab="html,result" data-user="tyasriochao" data-slug-hash="jOEwyPe" style="height: 120px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lesson1-introduce">
  <span>See the Pen <a href="https://codepen.io/tyasriochao/pen/jOEwyPe">
  Lesson1-introduce</a> by Tyasrio 畢建超 (<a href="https://codepen.io/tyasriochao">@tyasriochao</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

修改`input`中的值可以实时修改`<p>`标签中的文本值，这是怎么做到的呢？  
使用的是`Javascript`的[`Object.defineProperty`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)方法。

看一下下面这个例子：  

<p class="codepen" data-height="240" data-theme-id="default" data-default-tab="html,result" data-user="tyasriochao" data-slug-hash="KKwqagb" style="height: 120x; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lesson1-introduce(02)">
  <span>See the Pen <a href="https://codepen.io/tyasriochao/pen/KKwqagb">
  Lesson1-introduce(02)</a> by Tyasrio 畢建超 (<a href="https://codepen.io/tyasriochao">@tyasriochao</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>



