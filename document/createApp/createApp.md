### rootComponent

```
rootComponent = {
    data: () => ({
        title: '标题title'
    }),
    template: 'hello'
}
```

# Vue.createApp

```js

let app =  Vue.createApp({
    data: () => ({
        title: '标题title'
    }),
    template: 'hello'
})
```

渲染器对象 app 真正的 创建过程 位于apiCreateApp.ts 中的 createAppAPI 方法

## app 实例的样子: 

```js
component: ƒ component(name, component)
config: Object
directive: ƒ directive(name, directive)
mixin: ƒ mixin(mixin)
mount: (containerOrSelector) => {…}
provide: ƒ provide(key, value)
unmount: ƒ unmount()
use: ƒ use(plugin, ...options)
version: "3.2.27"
_component: {data: ƒ}
_container: null
_context: {app: {…}, config: {…}, mixins: Array(0), components: {…}, directives: {…}, …}
_instance: null
_props: null
_uid: 0
```

## vnode 的样子:

```
anchor: null
appContext: {app: {…}, config: {…}, mixins: Array(0), components: {…}, directives: {…}, …}
children: null
component: {uid: 0, vnode: {…}, type: {…}, parent: null, appContext: {…}, …}
dirs: null
dynamicChildren: null
dynamicProps: null
el: p
key: null
patchFlag: 0
props: null
ref: null
scopeId: null
shapeFlag: 4
slotScopeIds: null
ssContent: null
ssFallback: null
staticCount: 0
suspense: null
target: null
targetAnchor: null
transition: null
type: {template: '\n        <p>{{title}}</p>\n    ', data: ƒ, render: ƒ}
__v_isVNode: true
__v_skip: true
```

# mount('#app') 的过程

```js
const vnode = createVNode(
  rootComponent as ConcreteComponent,
  rootProps // 根props
)
render(vnode, rootContainer, isSVG)
```

在 render => patch => processComponent => mountComponent 

初次时, 无旧节点, 故直接挂载组件

mountComponent 里 三步骤:

## mountComponent 

1. 创建组件实例 createComponentInstance
2. 初始化实例, 初始化插槽, props, 相应依赖
   setupComponent(instance)
3. 为组件实例安装渲染函数的副作用
   setupRenderEffect

setupRenderEffect 里的update 中完成了**虚拟dom vnode 到真实dom** 的过程