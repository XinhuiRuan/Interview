# Vue
Q1: v-show 与 v-if 区别

1.相同点：v-show和v-if都能控制元素的显示和隐藏。

2.不同点：

实现本质方法不同：
v-show本质就是通过设置css中的display设置为none，控制隐藏；
v-if是动态的向DOM树内添加或者删除DOM元素。

编译的区别：
v-show其实就是在控制css；
v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件。

编译的条件：
v-show都会编译，初始值为false，只是将display设为none，但它也编译了；
v-if初始值为false，就不会编译了。

性能：
v-show只编译一次，后面其实就是控制css，而v-if不停的销毁和创建，故v-show性能更好一点。

注意点：因为v-show实际是操作display:" "或者none，当css本身有display：none时，v-show无法让显示。

总结：
如果要频繁切换某节点时，使用v-show（无论true或者false初始都会进行渲染，此后通过css来控制显示隐藏，因此切换开销比较小，初始开销较大）；
如果不需要频繁切换某节点时，使用v-if（因为懒加载，初始为false时，不会渲染，但是因为它是通过添加和删除dom元素来控制显示和隐藏的，因此初始渲染开销较小，切换开销比较大）。

参考：https://www.cnblogs.com/liutianzeng/p/10978890.html


Q2: methods(方法)、computed(计算属性)、watch(侦听器)的区别

1、computed和methods

共同点：computed能现实的methods也能实现；

不同点：computed是基于它的依赖进行缓存的。computed只有在它的相关依赖发生变化才会重新计算求值。 而只要它的相关依赖没有发生变化，多次访问会立即返回之前的计算结果，而不必再次执行计算。相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。也就是说当我们不希望有缓存，用方法来替代。（关于缓存和重新渲染，看详解：https://www.jb51.net/article/138743.htm）

2、watch和computed

共同点：以 Vue 的依赖追踪机制为基础，当某个依赖数据发生变化时，所有依赖这个数据的相关数据或函数都会自动发生变化或调用；

不同点：computed是自动监听依赖值的变化，从而动态返回内容；watch是一个过程，在监听的值变化时，可以触发一个回调，并做一些事情。所以区别来源于用法，只是需要动态值，那就用计算属性；需要知道值的改变后执行业务逻辑，才用 watch，用反或混用虽然可行，但都是不正确的用法。
使用 watch 选项允许我们执行异步操作（访问一个 API）或高消耗性能的操作，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态，而这些都是计算属性无法做到的。

另外总结了几点关于 computed 和 watch 的差异：

  1. computed 是计算一个新的属性，并将该属性挂载到 vm（Vue 实例）上，而 watch 是监听已经存在且已挂载到 vm 上的数据，所以用 watch 同样可以监听  
      computed 计算属性的变化（其它还有 data、props）;

  2. computed 本质是一个惰性求值的观察者，具有缓存性，只有当依赖变化后，第一次访问 computed 属性，才会计算新的值，而 watch 则是当数据发生变化便会调
      用执行函数;
      
  3. 从使用场景上说，computed 适用一个数据被多个数据影响，而 watch 适用一个数据影响多个数据；
  
  参考：https://segmentfault.com/a/1190000016387717

Q2扩展问题：

Q2-1： computed 是一个对象时，它有哪些选项？

有 get 和 set 两个选项。

get是当该对象所依赖的变量发生变化是执行，重新return computed结果。

set是该对象的值变化时会执行，并且将变化的结果作为参数传进set里，然后可以根据传进的值来处理。

Q2-2：computed 是否能依赖其它组件的数据？

computed 可以依赖其它 computed，甚至是其它组件的 data。

Q2-3：watch 是一个对象时，它有哪些选项？

handler方法：watch中需要具体执行的方法；

immediate属性：为true时则立即先去执行里面的handler方法；如果为false，不会在绑定的时候就执行。

deep属性：默认值是 false，代表是否深度监听。当需要监听一个对象的改变时，普通的watch方法无法监听到对象内部属性的改变，此时就需要deep属性对对象进行深度监听，也就是在对象中层层遍历，并在监听对象上的每一个属性上都添加监听，固然也会损耗性能。（如果只需要监听对象中的一个属性值，则可以做以下优化：使用字符串的形式监听对象属性）

注意点：

1. 如果在handler函数中使用了箭头函数，改变了this指向，就无法获取到Vue实例，则为undifined。

2. 对于父子组件传参，异步获取数据有时会存在获取不到值的情况。这时候watch就派上用场，适当的时候要配合immediate或者deep属性配合使用。

参考资料：https://blog.csdn.net/Amanda_wmy/article/details/83749560

         https://blog.csdn.net/yangdengcheng/article/details/90479976


Q3：事件修饰符

Vue提供事件修饰符是因为：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

1. .stop：阻止冒泡（通俗讲就是阻止事件向上级DOM元素传递）；

2. .prevent：阻止默认事件的发生（默认事件比如点击超链接的时候会进行页面的跳转，点击表单提交按钮时会重新加载页面等）；

3. .capture：捕获冒泡，即有冒泡发生时，有该修饰符的dom元素会先执行，如果有多个，从外到内依次执行，然后再按自然顺序执行触发的事件；
    （详解请看：https://www.cnblogs.com/xiaozhang666/p/10430059.html）
    
4. .self：将事件绑定到自身，只当在 event.target 是当前元素自身时触发处理函数，即事件不是从内部元素触发的，通常用于避免冒泡事件的影响；

5. .once：设置事件只能触发一次，比如按钮的点击等。

6. .passive：用于对DOM的默认事件进行性能优化，默认行为将会立即触发,对应 addEventListener 中的 passive 选项（详情请看：https://blog.csdn.net/wildye/article/details/80223679）。

注意点：

1. 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。

2. 不要把 .passive 和 .prevent 一起使用，因为 .prevent 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，.passive 会告诉浏览器你不想阻止事件的默认行为。

参考资料：https://www.cnblogs.com/Delo/articles/10475634.html


Q4：双向绑定的原理

vue.js 是采用数据劫持结合发布者-订阅者模式的方式，核心的 API 是通过Object.defineProperty()来劫持各个属性的setter / getter，在数据变动时发布消息给订阅者，触发相应的监听回调，这也是为什么 Vue.js 2.x不支持IE8的原因。

解释一：
要实现双向绑定，首先进行数据劫持，所以需要设置一个监听器Observer，用来监听所有属性。如果属性发生变化，就需要告诉订阅者Watcher看是否需要更新。因为订阅者很多，所以需要一个消息订阅器Dep来专门收集这些订阅者，然后在监听器和订阅者之间进行统一管理，最后需要一个指令解析器Compile，对每个节点元素进行扫描和解析，将相关指令（v-model，v-on）对应初始化一个订阅者Watcheer，并替换模板数据或绑定相应函数。

解释二：
首先我们为每个vue属性用Object.defineProperty()实现数据劫持，为每个属性分配一个订阅者集合的管理数组dep；然后在编译的时候在该属性的数组dep中添加订阅者，v-model会添加一个订阅者，{{}}也会，v-bind也会，只要用到该属性的指令理论上都会，接着比如为input会添加监听事件，修改值就会为该属性赋值，触发该属性的set方法，在set方法内通知订阅者数组dep，订阅者数组循环调用各订阅者的update方法更新视图。

参考资料：https://www.cnblogs.com/zhenfei-jiang/p/7542900.html

         https://www.jianshu.com/p/bb5d1bede3ea
         
        
Q5：怎么理解单项数据流

深入了解前提：

1、v-model 用在 input 元素上
  v-model在使用的时候很像双向绑定的（实际上也是。。。），但是 Vue 是单项数据流，v-model 只是语法糖而已。
  
  <input v-model="something" />
  <input v-bind:value="something" v-on:input="something = $event.target.value" />
  第一行的代码其实只是第二行的语法糖。
  在给 input 元素添加 v-model 属性时，默认会把 value 作为元素的属性，然后把 'input' 事件作为实时传递 value 的触发事件。
  
2、v-model 用在组件上
  v-model 不仅仅能在 input 上用，在组件上也能使用。
  
  <currency-input v-model="price"></currency-input>
  所以在组件中使用时，它相当于下面的简写：
  //上行代码是下行的语法糖
  <currency-input :value="price" @input="price = arguments[0]"></currency-input>
  所以，给组件添加 v-model 属性时，默认会把 value 作为组件的属性，然后把 'input' 值作为给组件绑定事件时的事件名。这在写组件时特别有用。
  
单项数据流详解：

3.vue 组件数据流

  从上面 v-model 的分析我们可以这么理解，双向数据绑定就是在单向绑定的基础上给可输入元素（input、textare等）添加了 change(input) 事件，来动态修改 model 和 view ，即通过触发（$emit）父组件的事件来修改mv来达到 mvvm 的效果。

  而 vue 组件间传递数据是单向的，即数据总是由父组件传递到子组件，子组件在其内部可以有自己维护的数据，但它无权修改父组件传递给它的数据，当开发者尝试这样做的时候，vue 将会报错。
  
  这样做是为了组件间更好的解耦，在开发中可能有多个子组件依赖于父组件的某个数据，假如子组件可以修改父组件数据的话，一个子组件变化会引发所有依赖这个数据的子组件发生变化，所以 vue 不推荐子组件修改父组件的数据，直接修改 props 会抛出警告。
  
  所以，有两种常见的试图改变一个 prop 的情形：
  
  1、这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。 
      => 定义一个局部变量，并用 prop 的值初始化它。  
      props: ['initialCounter'],
      data: function () {
        return {
          counter: this.initialCounter
        }
      }
        
  2、这个 prop 以一种原始的值传入且需要进行转换。
      => 使用这个 prop 的值来定义一个计算属性。
      props: ['size'],
      computed: {
        normalizedSize: function () {
          return this.size.trim().toLowerCase()
        }
      }
     
注意点：
  在JS中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变这个对象或数组本身将会影响到父组件的状态。
  
  //如此解决引用传递  
　1：var newObject = jQuery.extend(true, {}, oldObject); 
  2：var obj={};
     obj=JSON.parse(JSON.stringify(oldObject));
  
参考资源：https://www.jianshu.com/p/8b4f4c2f75e4
          
         https://www.cnblogs.com/em2464/p/10418535.html
         
    
Q6：简述下生命周期钩子




  
