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
