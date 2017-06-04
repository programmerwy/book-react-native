{% extends "../tpls/base.md" %}

{% block title %}
# Layout with Flexbox
{% endblock %}

{% block pageContent %}
一个组件可以通过flexbox方法来处理子组件的布局。flexbox可以用来开发出兼容各种
尺寸屏幕的布局。

你一般需要煎饼果子来一套的使用`flexDirection`，`alignItems`和`justifyContent`
之类的来共同实现一个可用的布局方案。

> flexbox与css在web中呈现出的效果一致，不过会有一些小不同。一些默认值是不一样的，
> flexDirection的默认值是column(css中是row)，还有flex参数只接受数字。

### Flex Direction

给一个组件的style设置flexDirection属性，可以改变这个组件布局的主轴（primary axis）。
也就决定了它的子组件的组织方式，即水平(row)分布还是垂直(column)分布（默认垂直分布）。

{% raw %}
```
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

class FlexDirectionBasics extends Component {
  render() {
    return (
      // Try setting `flexDirection` to `column`.
      <View style={{flex: 1, flexDirection: 'row'}}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

AppRegistry.registerComponent('AwesomeProject', () => FlexDirectionBasics);
```
{% endraw %}

### Justify Content

设置这个属性，会影响它的子组件沿它的主轴的分布方式（翻译的有点绕，看例子）。
比如子组件是按照起始位置，中间，末端还是均分空隙的方式分布。可取的值有：`flex-start`，
`center`，`flex-end`，`space-around`和`space-between`。

{% raw %}
```
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

class JustifyContentBasics extends Component {
  render() {
    return (
      // Try setting `justifyContent` to `center`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'space-between',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

AppRegistry.registerComponent('AwesomeProject', () => JustifyContentBasics);
```
{% endraw %}

### Align Items

设置这个属性，会影响它的子组件沿它的副轴的对齐方式（如果主轴是垂直方向，那副轴就是水
平方向，反之亦然）。比如子组件是按照起始，中间，末端对齐还是拉伸填充。可取值有：`flex-start`，
`center`，`flex-end`和`stretch`。

> 为了让`stretch`生效，子组件中不能设置副轴方向的fixed尺寸。比如在设置`alginItems: stretch`的组件
> 中不能有设置`width: 50`的子组件，否则`alignItems`属性会失效。

{% raw %}
```
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

class AlignItemsBasics extends Component {
  render() {
    return (
      // Try setting `alignItems` to 'flex-start'
      // Try setting `justifyContent` to `flex-end`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'center',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

AppRegistry.registerComponent('AwesomeProject', () => AlignItemsBasics);
```
{% endraw %}

### 搞深一点

基本的flexbox我们差不多撸了一遍，但是实战中可能会用到更多。控制布局的props全集[点击这里（官方）](https://facebook.github.io/react-native/docs/layout-props.html)。

学到这里就快能搞si情了（写个app :)）。不过还差个事：[处理用户输入](handling-text-input.md)。
{% endblock %}