{% extends "../tpls/base.md" %}

{% block title %}
# Props
{% endblock %}

{% block pageContent %}
大部分`Component`在创建的时候都能设置一堆参数，也就是`props`（应该就是property吧，下面直接用“属性”）。

举个栗子，创建一个`image`，你需要设置它的`source`来控制显示啥。
```
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

AppRegistry.registerComponent('Bananas', () => Bananas);
```
注意`{pic}`这种将变量扔到`{}`的JSX用法。`{}`在JSX里面类似exec，可以把任何js表达式扔进去执行。

自定义的组件也可以设置`props`。只需要在你的render函数里面写上this.props这种形式。
```
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <Text>Hello {this.props.name}!</Text>
    );
  }
}

class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

AppRegistry.registerComponent('LotsOfGreetings', () => LotsOfGreetings);
```
输出结果：
```
Hello Rexxar!
Hello Jaina!
Hello Valeera!
```
只用props和一些内建组件，就基本能cover住一般的静态页了，但是要想变的话，
还得看看这个 [learn about State](state.md)。
{% endblock %}