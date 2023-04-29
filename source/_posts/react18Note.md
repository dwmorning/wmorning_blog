---
title: react 18 笔记
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 入门React
categories:
  - react
tags:
  - react
  - note
date: 2023-04-25 23:41:45
keywords: 
toc: true
---

# React18核心概念与类组件使用 – 入门React18第一步
## props细节详解及注意事项

### 构造器中获取props数据

props是我们React父子组件之间通信的对象，那么这个对象在构造器`constructor`中是获取不到的。

```jsx
class Welcome extends React.Component {
    constructor(){
        super();
        console.log( this.props.msg )   // undefined
    }
    render(){
        return (
            <div>hello world, {this.props.msg}</div>
        );
    }
}
let element = (
    <Welcome msg="hi react" />
);
```

可以通过给`super()`传递props参数是可以做到的，代码如下：

```jsx
constructor(props){
    super(props);
    console.log( this.props.msg )   // hi react
}
```

那么React类组件是如何设计的呢？就要对面向对象非常的熟悉，原理分析如下：

```jsx
class Foo {
    constructor(props){
        this.props = props;
    }
}
class Bar extends Foo {
    constructor(props){
        super(props);
        console.log(this.props);
    }
    render(){
        console.log(this.props);
        return '';
    }
}
let props = {
    msg: 'hello world'
};
let b = new Bar(props);
b.props = props;
b.render();
```

### 多属性的传递

当有非常多的属性要传递的时候，那么会比较麻烦，所以可通过扩展运算形式进行简写。

```jsx
class Welcome extends React.Component {
    render(){
        let { msg, username, age } = this.props;
        console.log( isChecked );
        return (
            <div>hello world, {msg}, {username}, {age}</div>
        );
    }
}
let info = {
    msg: 'hi react',
    username: 'xiaoming',
    age: 20
};
let element = (
    <Welcome {...info} />
);
```

### 给属性添加默认值与类型

```jsx
import PropTypes from 'prop-types'
class Welcome extends React.Component {
    static defaultProps = {
        age: 0
    }
    static propTypes = {
        age: PropTypes.number
    }
    ...
}
```

这里的类型需要引入第三方模块才可以生效。

当父子通信的时候，如果只写属性，不写值的话，那么对应的值就是布尔值true。

## 类组件中事件的使用详解

首先React中的事件都是采用事件委托的形式，所有的事件都挂载到组件容器上，其次event对象是合成处理过的。一般情况下这些都是内部完成的，我们在使用的时候并不会有什么影响，作为了解即可。

### 事件中this的处理

在事件中最重要的就是处理this指向问题了，这里我们推荐采用面向对象中的`public class fields`语法。

```jsx
 class Welcome extends React.Component {
    handleClick = (ev) => {  //推荐 public class fields
        console.log(this);   //对象
    }
    handleClick(){   		 //不推荐 要注意修正指向
        console.log(this);   //按钮 
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                hello world
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```

### 事件传参处理

推荐采用函数的高阶方式，具体代码如下：

```jsx
class Welcome extends React.Component {
    handleClick = (num) => {   // 高阶函数
        return (ev) => {
            console.log(num);
        }
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick(123)}>点击</button>
                hello world
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```
## state细节详解及React18的自动批处理

### 自动批处理

自动批处理，即有助于减少在状态更改时发生的重新渲染次数。在React18之前也有批处理的，但是在Promise、setTimeout、原生事件中是不起作用的。

实际上自动批处理指的是，同一时机多次调用`setState()`方法的一种处理机制。

```jsx
handleClick = () => {  
    this.setState({
        msg: 'hi'
    });
    this.setState({
        count: 1
    });
}
```

这里的代码当点击触发后，虽然调用了两次`setState()`方法，但是只会触发一次`render()`方法的重新执行。那么这就是所谓的自动批处理机制，这样是有助于性能的，减少重新执行的次数。

而且不管在什么时机下，都不会有问题的，这个在React18版本之前并不是所有的情况都好用的，比如：定时器。

```jsx
handleClick = () => {  
    setTimeout(()=>{
        this.setState({
            msg: 'hi'
        });
        this.setState({
            count: 1
        });
    }, 2000)
}
```

上面代码在React18之前的版本中，将会触发两次`render()`方法。默认是自动批处理的，当然也可以改成不是自动批处理的方式，通过`ReactDOM.flushSync`这个方法。

```jsx
handleClick = () => {  
    ReactDOM.flushSync(()=>{
        this.setState({
            msg: 'hi'
        });
    })
    ReactDOM.flushSync(()=>{
        this.setState({
            count: 1
        });
    }) 
}
```

### 异步处理

既然React18对多次调用采用的是自动批处理机制，那么就说明这个`setState()`方法是异步的，所以要注意方法调用完后，我们的state数据并不会立即发生变化，因为state可能会被先执行了。

```jsx
handleClick = () => {  
    /* this.setState({
          count: this.state.count + 1
        });
        console.log( this.state.count ); */
    this.setState({
        count: this.state.count + 1
    }, ()=>{  //异步执行结束后的回调函数
        console.log( this.state.count );
    });
}
```

可利用`setState()`方法的第二个参数来保证数据更新后再去执行。这里还要注意同样的数据修改只会修改一次，可利用`setState()`的回调函数写法来保证每一次都能触发。

```jsx
handleClick = () => {  
    /* this.setState({
          count: this.state.count + 1
        });
        this.setState({
          count: this.state.count + 1
        });
        this.setState({
          count: this.state.count + 1
        }); */
    this.setState((state)=> ({count: state.count + 1}));
    this.setState((state)=> ({count: state.count + 1}));
    this.setState((state)=> ({count: state.count + 1}));
}
```

这样页面按钮点击一次，count会从0直接变成了3。

## PureComponent与shouldComponentUpdate

PureComponent与shouldComponentUpdate这两个方法都是为了减少没必要的渲染，React给开发者提供了改善渲染的优化方法。

### shouldComponentUpdate

当我们在调用`setState()`方法的时候，如果数据没有改变，实际上也会重新触发`render()`方法。

```jsx
class Welcome extends React.PureComponent {
    state = {
        msg: 'hello',
        count: 0
    }
    handleClick = () => {  
        this.setState({
            msg: 'hello'
        });
    }
    render(){
        console.log('render');
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                {this.state.msg}, {this.state.count}
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```

上面的`render()`方法还是会不断的触发，但是实际上这些render触发是没有意义的，所以可以通过`shouldComponentUpdate`钩子函数进行性能优化处理。

```jsx
class Welcome extends React.Component {
    state = {
        msg: 'hello',
        count: 0
    }
    handleClick = () => {  
        this.setState({
            msg: 'hi'
        });
    }
    shouldComponentUpdate = (nextProps, nextState) => {
        if(this.state.msg === nextState.msg){
            return false;
        }
        else{
            return true;
        }
    }
    render(){
        console.log('render');
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                {this.state.msg}, {this.state.count}
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```

shouldComponentUpdate()方法的返回值，如果返回false就不进行界面的更新，如果返回true就会进行界面的更新。这样就可以根据传递的值有没有改变来决定是否进行重新的渲染。

### PureComponent

PureComponent表示纯组件，当监控的值比较多的时候，自己去完成判断实在是太麻烦了，所以可以通过PureComponent这个内置的纯组件来自动完成选择性的渲染，即数据改变了重新渲染，数据没改变就不重新渲染。

```jsx
class Welcome extends React.PureComponent {
    state = {
        msg: 'hello',
        count: 0
    }
    handleClick = () => {  
        this.setState({
            msg: 'hi'
        });
    }
    render(){
        console.log('render');
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                {this.state.msg}, {this.state.count}
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```

改成了纯组件后，记得不要直接对数据进行修改，必须通过`setState()`来完成数据的改变，不然纯组件的特性就会失效。

```jsx
class Welcome extends React.PureComponent {
    state = {
        msg: 'hello',
        count: 0,
        list: ['a', 'b', 'c']
    }
    handleClick = () => {  
        /* this.setState({
          list: [...this.state.list, 'd']
        }); */
        //错误✖
        /* this.state.list.push('d');
        this.setState({
          list: this.state.list
        }) */
    }
    render(){
        console.log('render');
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <ul>
                    {
                        this.state.list.map((v, i)=> <li key={i}>{v}</li>)
                    }
                </ul>
            </div>
        );
    }
}
let element = (
    <Welcome />
);
```
## immutable.js不可变数据集合

在上一个小节中，我们对数组进行了浅拷贝处理，这样可以防止直接修改数组的引用地址。但是对于深层次的对象就不行了，需要进行深拷贝处理。

但是常见的深拷贝处理机制，对于性能或功能性上都有一定的制约性，所以不复杂的数据，我们直接就可以选择用`lodash`库中提供的深拷贝方法处理就可以了。但是对于复杂的对象就需要拷贝性能问题，这就可以用到本小节中介绍的immutable.js不可变数据集合。

### immutable.js库

Immutable 是 Facebook 开发的不可变数据集合。不可变数据一旦创建就不能被修改，使得应用开发更简单，允许使用函数式编程技术，比如惰性评估。Immutable JS 提供一个惰性 `Sequence，`允许高效的队列方法链，类似 `map` 和 `filter` ，不用创建中间代表。

具体是如何做到高效的，可以参考图示。

<div align=center>
    <img src="/image/react18Note/immutablejs.gif" />
    <div>immutablejs</div>
</div>

下面就来看一下immutable.js的基本使用吧，代码如下：

```jsx
import Immutable from 'immutable'

class Head extends React.PureComponent {
    render(){
        console.log('render');
        return (
            <div>head component, {this.props.item.get('text')} </div>
        );
    }
}
class Welcome extends React.PureComponent {
    state = {
        msg: 'hello',
        count: 0,
        list: Immutable.fromJS([
            { id: 1, text: 'aaa' }
        ])
    }
    handleClick = () => {  
        let list = this.state.list.setIn([0, 'text'], 'bbb');
        this.setState({
            list
        });
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <Head item={this.state.list.get(0)} />
            </div>
        );
    }
}
```

主要就是通过Immutable.fromJS()先把对象转成immutable对象，再通过setIn()方法来设置数据，get()方法来获取数据。

## Refs操作DOM及操作类组件

React操作原生DOM跟Vue框架是类似的，都是通过ref属性来完成的，主要使用`React.createRef()`这个方法和`callbackRef()`这个回调函数写法。

### React.createRef()

这个方法可以创建一个ref对象，然后把这个ref对象添加到对应的JSX元素的ref属性中，就可以控制原生DOM了。

```jsx
class Welcome extends React.Component {
    myRef = React.createRef()
    handleClick = () => {   
        //console.log(this.myRef.current);  // 原生DOM 
        this.myRef.current.focus();
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <input type="text" ref={this.myRef} />
            </div>
        );
    }
}
```

### 回调函数写法

还可以编写一个回调函数来完成，原生DOM的操作。

```jsx
class Welcome extends React.Component {
    callbackRef = (element) => {
        element.focus();
    }
    handleClick = () => {   
        this.myRef.focus();
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <input type="text" ref={this.callbackRef} />
            </div>
        );
    }
}
```

### Ref操作类组件

除了可以把ref属性添加到JSX元素上，还可以把ref属性添加到类组件上，那么这样可以拿到类组件的实例对象。

```jsx
class Head extends React.Component {
    username = 'xiaoming';
    render(){
        return (
            <div>head component</div>
        );
    }
}

class Welcome extends React.Component {
    myRef = React.createRef()
    handleClick = () => {   
        console.log(this.myRef.current);   //组件的实例对象
        console.log(this.myRef.current.username);
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <Head ref={this.myRef} />
            </div>
        );
    }
}
```

这样可以间接的实现父子组件之间的数据通信。

ref属性还可以进行转发操作，可以把ref传递到组件内，获取到子组件的DOM元素。

```jsx
class Head extends React.Component {
    render(){
        return (
            <div ref={this.props.myRef}>head component</div>
        );
    }
}
class Welcome extends React.Component {
    myRef = React.createRef()
    handleClick = () => {   
        console.log(this.myRef.current);
    }
    render(){
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                <Head myRef={this.myRef} />
            </div>
        );
    }
}
```

## 详解常见生命周期钩子函数

在学习Vue的时候，我们就已经介绍了生命周期钩子函数的概念，React中也存在一些钩子函数。我们可以为类组件声明一些特殊的方法，当组件挂载、更新或卸载时就会去执行这些函数。

要想学习React类组件的生命周期钩子函数，可以参考生命周期图谱。地址：https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

<div align=center>
    <img src="image/react18Note/14-03-常见生命周期图谱.png" />
    <div>常见生命周期图谱</div>
</div>

生命周期主要分为三个阶段：

- 挂载时
- 更新时
- 卸载时

挂载时对应的钩子函数有：`constructor`，`render`，`componentDidMount`。

更新时对应的钩子函数有：`render`，`componentDidUpdate`

卸载时对应的钩子函数有：`componentWillUnmount`

可以看到挂载时和更新时都有`render`这个方法。这就是为什么state改变的时候，会触发`render`重渲染操作。

```jsx
class Welcome extends React.Component {
    state = {
        msg: 'hello world'
    }
    constructor(props){
        super(props);
        console.log('constructor');
    }
    componentDidMount = () => {
        // react中发起ajax请求的初始操作，在这个钩子中完成
        console.log('componentDidMount');
    }
    componentDidUpdate = () => {
        // 等DOM更新后触发的钩子
        console.log('componentDidUpdate');
    }
    componentWillUnmount = () => {
        console.log('componentWillUnmount');
    }
    handleClick = () => {  
        /* this.setState({
          msg: 'hi react'
        }); */
        //this.forceUpdate();
        root.unmount();   // 触发卸载组件
    }
    render(){
        console.log('render');
        return (
            <div>
                <button onClick={this.handleClick}>点击</button>
                { this.state.msg }
            </div>
        );
    }
}
```




