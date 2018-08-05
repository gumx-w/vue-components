# vue-components


一些 vue 组件的实现。以 JS 的实现为主，尽量剥离样式。默认情况下以 bootstrap 样式为基础样例。

项目演示地址：https://git.gumx.top/#vue_components


起因：

1. 在 Vue 和 bootstrap 混合使用的情况下，很多事件的响应会变得混乱，甚至不可用。

2. 在 Vue 的单页面应用下，由于 bootstrap 不考虑单页面问题，对于事件监听的监听只负责创建不负责移除，所以会导致严重的内存泄漏问题。

3. bootstrap 的功能实现都是基于样式的， 不具有扩展性。

4. bootstrap 的一些功能对于组件化的不友好。


基于以上4条原因，而项目的开发中又大量的使用了 bootstrap 。为了解决这些问题，对一些功能实现了组件化的封装，以解决这些问题。

希望能帮助到 同时使用 bootstrap 和 vue 做开发的同学们，特别是单页面开发。





