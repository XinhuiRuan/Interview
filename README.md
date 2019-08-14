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
