{% extends "../tpls/base.md" %}

{% block title %}
# Style
{% endblock %}

{% block pageContent %}
在RN里面，可以直接用js写样式（style）。所有核心组件都可以用`style`属性（prop）来指定样式。
style內的属性名和取值与css基本一致，只是RN里面使用驼峰命名法（css: `background-color`/
RN: `backgroundColor`）。

一般比较常用的是直接传一个简单js对象，也可以传一个数组进来，如果有重复会覆盖，最后面的优先级最高。

有时组件可能hin复杂，这时候一般使用`StyleSheet.create`将样式定义在一起：
```
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  bigblue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

AppRegistry.registerComponent('LotsOfStyles', () => LotsOfStyles);
```

比较常用的使用方式是，通过在当前组件上定义style来作用到子组件上。可以使用这个方式来模拟css上的层叠用法（One common pattern is to make your component accept a style prop which in turn is used to style subcomponents. You can use this to make styles "cascade" the way they do in CSS.）。
> 注：CSS(Cascade Style Sheet[(MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade))

这里有Text的更多style用法：[戳这里（官方）](https://facebook.github.io/react-native/docs/text.html)。

查看更多关于控制组件尺寸的：[戳这里](height-and-width.md)。
{% endblock %}