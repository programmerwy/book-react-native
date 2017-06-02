{% extends "../tpls/base.md" %}

{% block title %}
# State
{% endblock %}

{% block pageContent %}
一共有两类数据用来控制Component：props和state。props由父级设定，并且在Component的
整个生命周期里面都是固定的。如果有数据的变更，就要使用state了。

通常会在构造函数里面就初始化好state，然后在需要变动的时候调用setState。

举个栗子，现在要搞个blingbling的闪动text，text只要设置一次，所以使用props，但是控制一闪一闪的
特性要使用state。
```
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = {showText: true};

    // Toggle the state every second
    setInterval(() => {
      this.setState({ showText: !this.state.showText });
    }, 1000);
  }

  render() {
    let display = this.state.showText ? this.props.text : ' ';
    return (
      <Text>{display}</Text>
    );
  }
}

class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

AppRegistry.registerComponent('BlinkApp', () => BlinkApp);
```
实际项目中不一定像这样靠timer来设置state，可能还会有类似异步请求或者用户输入这样的。
也可以使用[Redux](http://redux.js.org/index.html)这种state容器（state container）来
控制数据流（data flow）的。要是Redux这种，可能就直接用容器自带的api了。

每次调用setState的时候，Blink App都会重新渲染（re-render），机制和React一致，有兴趣
[戳这里(React.Component API)](https://facebook.github.io/react/docs/react-component.html)。

感觉代码执行效果都是白底黑字很无聊？[learn about Style](style.md)。
{% endblock %}