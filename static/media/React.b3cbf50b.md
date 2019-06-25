## 10. React

### 10.0 Links

- [浅析前端开发中的 MVC/MVP/MVVM 模式
](https://www.cnblogs.com/zhouyangla/p/6936455.html) —— 架构模式

### 10.1 React相关基本概念

#### 10.1.1. MVC、MVP和MVVM模式

MVC、MVP和MVVM都是常见的软件架构设计模式，其相同点和不同点在于：

- 相同点：MV(Model-View)

- 不同点：C(controller)、P(Presenter)、VM(View-Model)

（1）MVC

<center>

![10-1](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-1.png)

</center>

- MVC(Model-View-Controller)架构模式，用户对View的操作交给了Controller处理，在Controller中响应View的事件调用Model的接口对数据进行操作，Model发生变化后，通知相关的视图进行更新。

- MVC架构模式核心在于Controller，View的每个事件流经Controller，其View和Controller一般为一一对应，如果想多个View公用一个Controller即为MVP架构模式。

（2）MVP

<center>

![10-2](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-2.png)

</center>

- MVP(Model-View-Presenter)为MVC的改良，通过解耦View和Model，Presenter负责业务逻辑、Model管理数据、View负责显示

- 视图和模型职责划分更清晰，可将View抽离出来作为组件

（3）MVVM

<center>

![10-3](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-3.png)

</center>

- MVVM(Model-View-ViewModel)将View和Model的同步逻辑自动化

- ViewModel核心为数据绑定，Model发生变化，ViewModel就会自动更新，Model也会更新

- 不同的MVVM框架，实现双向数据绑定技术有所不同，主流前端框架数据绑定方式：

数据劫持（Vue）

发布-订阅模式（Knockout、BackBone）

脏值检查（Angular）

#### 10.1.2 Virtual DOM

1. React产生虚拟DOM的过程

（1）state 数据

（2）JSX 模板

（3）数据 + 模板 生成虚拟DOM（虚拟DOM就是一个JS对象，用它来描述真实的DOM）虚拟DOM的结构类似于：

```
['div', {id: 'abc'}, ['span', {}, 'hello world']]
```

（4）用虚拟DOM的结构生成真实的DOM，来显示：

```html
<div id='abc'><span>hello world></span></div>
```

（5）state 发生变化

（6）数据 + 模板 生成新的虚拟DOM（极大的提升性能，因为虚拟DOM就是JS对象，相对于使用API来产生真实的DOM，性能极大提高）

（7）比较原始虚拟DOM和新的虚拟DOM的区别，找到区别是span中内容（极大提升性能）

（8）直接操作DOM，改变span中的内容

2. 优点：

（1）性能提升了

（2）**使得跨端应用得以实现。React Native原生应用（除了网页以外的原生应用，如安卓之类的，因为虚拟DOM的本质是JS对象）**

> react-native口号：Learn Once, Write Anywhere

3. React定义标签时候，只允许被一个标签包裹：原因是JSX会转译为JS语言，在转译时候，会调用React.createElement方法，因此需要进行包裹。

#### 10.1.3 为什么不用传统的操作DOM方式？

- 传统的组件封装的基本思路是面向对象思想，交互操作主要以**操作DOM为主**

- 传统操作DOM的方式导致存在大量的HTML结构和style样式的拼装，如果逻辑复杂，就会存在大量的DOM操作。

#### 10.1.4 虚拟DOM中的Diff算法

1. Diff：difference

2. setState: 异步的方法，提升React底层性能。比如有连续三次setState，那么React将三次setState合并成一次setState，只需一次虚拟DOM比对。

<center>

![10-4](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-4.png)

</center>

3. 虚拟DOM比对的原则：同级比较，从上到下，如果第一层的DOM节点出现不一样，那么从该层开始到下面的子节点，都会进行替换。同层比对，比对的速度会更快

4. 虚拟DOM值的比对会根据Key值来进行比对。因此不建议使用index来作为Key值使用。index会导致key值不稳定。=> **使用稳定的值作为key值**

#### 10.1.5 React中的ref使用

ref可以用来获取dom上的元素

React建议以数据驱动的方式来实现界面的更新，使用ref去直接操作DOM不是React建议的方式。

***setState是一种异步的方式，如果一个函数中有setState的话，如果该函数被调用，那么setState不会被立即执行，解决的办法是setState有第二个函数，即为回调函数。如：***


```javaScript
handleButtonClick(){
    this.setState((prevState) => ({
        list: [...prevState.list, prevState.inputValue],
        inputValue: ''
    }), () => {
        // 异步
        console.log(this.ul.querySelectorAll('div').length)
    })
}
```

#### 10.1.6 React生命周期
<center>

![10-5](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-5.png)

</center>
- 生命周期函数指在某一个时刻组件会自动调用执行的函数

- render、componentWillMount、componentDidMount等都是生命周期函数

1. Initialization: 初始化

2. Mounting: 挂载

- componentWillMount: 在组件即将被挂载到页面的时候自动执行

- render: 该函数会被反复的执行

- componentDidMount: 在组件被挂载到页面之后，自动被执行

***componentDidMount只会执行一次，就是组件被挂载到页面上之后，因此，接收Ajax请求通常放到该函数中***

3. Updating

（1）props

- componentWillReceiveProps: 当一个组件要从父组件接收参数，只要父组件的render函数被重新执行了，子组件的这个生命周期函数就会被执行。

需要注意的是，如果这个组件第一次存在于父组件中，不会执行；如果这个组件之前已经存在于父组件中，才会执行

- **shouldComponentUpdate**: 组件被更新之前，自动执行

***借助shouldComponentUpdate的功能，可以提高React组件的性能，因为可以避免组件无谓的render函数的运行。默认的情况下，父组件更新，自组件也会进行更新，如***


```
// 为了降低性能损耗，因为父组件在执行render的时候，子组件也会执行render，那么会导致性能损耗
// 添加了shouldComponentUpdate后，只有在传值之后更新
shouldComponentUpdate(nextProps, nextState) {
    if (nextProps.content !== this.props.content) {
        return true;
    }else{
        return false;
    }
}
```

- **componentWillUpdate**: 组件被更新之前，它会自动执行，但是它在shouldComponentUpdate之后执行。如果shouldComponentUpdate返回为true，它才会执行，如果为false，就不会执行。

**componentWillUpdate中不能执行setState**

- **render**: 开始渲染

- **componentDidUpdate**: 组件更新完毕之后，才会执行。

（2）states

- **shouldComponentUpdate**:

- **componentWillUpdate**:

- **render**:

- **componnetDidUpdate**:

4. Unmounting

- componentWillUnmount: 当这个组件即将被从页面剔除的时候，会被执行

### 10.2 Redux

#### 10.2.1 Redux概念

<center>

![10-6](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-6.png)

</center>
1. Redux将各个组件的数据放入公用的Store中去存储，其他组件也会感知Store

2. Redux = Reducer + Flux

- Flux: 存在弊端，如公共存储区域Store中可以有很多个Store去组成，数据存储可能会存在数据依赖的问题

#### 10.2.2 Redux的工作流程

<center>

![10-7](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-7.png)

</center>

1. Store(管理员): 存放所有的数据的公共区域

2. React Component(借书的人): React的组件

3. Action Creators(借书的请求): 请求数据的语句

4. Reducers(记录本): 将组件的请求与Store中的数据对应起来

#### 10.2.3 Redux设计和使用的三项原则

1. store是唯一的

2. 只有store能够改变自己的内容

3. reducer必须是纯函数

- 纯函数：给定固定的输入，就一定会有固定的输出，而且不会有任何的副作用

（1）也就是说函数内部不能有异步的操作，也不能有和时间相关的操作

（2）副作用指的是，如果在函数内部对接收的参数进行了修改，则该函数就有一定的副作用。

#### 10.2.4 Redux核心API

1. createStore: 创建一个store

2. store.dispatch: 帮助派发action，将action传递给store

3. store.getState: 帮助获取store中的数据内容

4. store.subscribe: 只要store内容改变，store.subscribe接收的回调函数就会执行

### 10.3 UI组件与逻辑组件

- **UI组件通常用于页面的渲染，逻辑组件用于页面的逻辑**

- 无状态组件：组件只有render函数的时候，即为无状态组件。当一个组件只有render()函数的时候，可以通过无状态组件去替换普通的组件

- **无状态组件的性能更高**，因为一个无状态组件没有生命周期函数，render()等

- 一般情况下，一般的UI组件，在没有逻辑代码的情况下，可以用无状态组件进行替换

### 10.4 Redux-thunk中间件

- **Redux-thunk用于解决系统中异步的内容**，将其放入Action中，避免将其放入生命周期，造成系统的臃肿。

- Redux-thunk的使用流程

（1）配置store中的index.js

```javascript
import { createStore, applyMiddleware, compose } from 'redux';
import reducer from './reducer';
import thunk from 'redux-thunk';

const composeEnhancers =
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?   
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose;

const enhancer = composeEnhancers(
  applyMiddleware(thunk),
);
const store = createStore(reducer, enhancer);

export default store
```

（2）配置ActionCreators.js

```javascript
export const getTodoList = () => {
    return (dispatch) => {
        axios.get('/list.json').then((res) => {
            const data = res.data;
            console.log(data);
            const action = initListAction(data);
            dispatch(action);
        }) 
    }
}
```

（3）配置Todolist_antd.js

```javascript
import {getTodoList, getInputChangeAction, getAddItemAction, getDeleteItemAction } from './store/actionCreators';

componentDidMount() {
    const action = getTodoList();
    store.dispatch(action)
}
```

- Redux-thunk作为中间件的工作原理：

<center>

![10-8](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/10React/10-8.png)

</center>

（1）在引入Redux-thunk之前，Action只能够Dispatch对象，在引入Redux-thunk之后，则可以引入异步函数。其工作机制就是，在dispatch之前，会将函数执行。

（2）Redux-thunk作为中间件，其实就是对Dispatch这个方法进行封装与升级，如果Dispatch方法是一个对象，那么就不变，作为一个对象直接传给Store。如果Dispatch方法是一个函数的时候，那么由于这个中间件，则不会直接传递函数，而是将这个函数先执行，执行完后，如果需要，再调给Store。

（3）类似于Redux-thunk的中间件的还有 Redux-logger、Redux-saga（解决React异步问题，与Redux-thunk不同的是，Redux-thunk是将异步操作放入Action进行操作，而Redux-saga的思想是单独的将异步的逻辑拆分出来，放到另一个文件中进行管理。）等

### 10.5 Redux-saga中间件

- 创建&使用流程

（1）在store文件夹下的index.js中引入Redux-saga中间件，配置

```javascript
import { createStore, applyMiddleware, compose } from 'redux';
import reducer from './reducer';
import createSagaMiddleware from 'redux-saga'
import todoSagas from './sagas'

const sagaMiddleware = createSagaMiddleware();

const composeEnhancers =
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?   
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose;

const enhancer = composeEnhancers(
    applyMiddleware(sagaMiddleware)
);
const store = createStore(reducer, enhancer);

sagaMiddleware.run(todoSagas)

export default store
```

（2）在store文件夹下新建sagas.js

```javascript
import { takeEvery, put } from 'redux-saga/effects'
import { GET_INIT_LIST } from './actionTypes'
import { initListAction } from './actionCreators'
import axios from 'axios';

function* getInitList() {
    try {
        // 在generator函数中，做异步请求的时候，不要使用Promise的形式
        const res = yield axios.get('/list.json');
        const action = initListAction(res.data);
        yield put(action);
    }catch(e) {
        console.log('list.json网络请求失败')
    }
}

// ES6中的generator函数
function* todoSaga() {
    yield takeEvery(GET_INIT_LIST, getInitList);
}

export default todoSaga
```

（3）reducer部分定义INIT_LIST_ACTION

```javascript
if (action.type === INIT_LIST_ACTION) {
    const newState = JSON.parse(JSON.stringify(state));
    newState.list = action.data;
    return newState;
}
```

### 10.6 React的事件系统

#### 10.6.1 合成事件实现机制

1. React的底层对合成事件做了两件事：**事件委派**和**事件绑定**。

2. **事件委派**

- React的事件代理机制，不是将事件处理函数直接绑定到真实的HTML的节点上，而是将事件绑定到结构的最外层，使用一个统一的事件监听器。

- 通过统一的事件监听器去处理，在映射里找到真正的事件处理函数并调用。

3. 事件绑定

（1）bind方法

```javascript
return(<button onClick={this.handleClick.bind(this, 'test')}>Test</botton>)
```

（2）构造器内声明

```javascript
constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this)
}
```

（3）箭头函数

```javascript
return <button onClick={() => this.handleClick()}>Test</botton>
```