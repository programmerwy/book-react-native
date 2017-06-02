# Tutorial

Hello World（可以使用这个网站直接查看RN效果：[点这里(rn web player)](https://cdn.rawgit.com/dabbott/react-native-web-player/gh-v1.9.1/index.html)）
```
import React, { Component } from 'react';
import { AppRegistry, Text } from 'react-native';

class HelloWorldApp extends Component {
  render() {
    return (
      <Text>Hello world haha!</Text>
    );
  }
}

AppRegistry.registerComponent('HelloWorldApp', () => HelloWorldApp);
```

### 都发生了啥

RN可以平稳过渡到ES6，类似import、from、class、extends还有() => 这种语法都支持。
还有些要注意的就是会有JSX语法，不同于其他框架将code以某种形式嵌入到模板中的方式，
RN反其道的使用JSX将模板语言嵌入到了code中。类似div、span这种，只不过替换成了RN
内建(build-in)的组件。

### Component 和 AppRegistry

上述代码定义了HelloWorldApp这么个Component，并且通过AppRegistry注册。RN就是由一堆
Component组成的。

AppRegistry只是告诉了RN整个App的入口Component是哪个。暂时不用纠结这个，因为你整个
App里面可能只会调一次AppRegistry.registerComponent。

### 上述代码有待完善

在Prop这章会有更多东西帮助你完善这段简单的code [learn about Props](props.md)。