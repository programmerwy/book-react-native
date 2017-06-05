{% extends "../tpls/base.md" %}

{% block title %}
# Using a ListView
{% endblock %}

{% block pageContent %}
`ListView`组件用于展现一组可变的，但是数据结构统一的可滚动列表。

`ListView`适合用于列表项可变的长列表。不同于`ScrollView`，`ListView`只会渲染出现在
屏幕可视范围内的元素，不会一次性都渲染出来。

`ListView`需要传入两个属性(prop)：`dataSource`和`renderRow`。`dataSource`是列表的信息源。
`renderRow`会取出源的每一项并返回一个格式化的可渲染组件。

下面的栗子是一个使用固定数据数据的`ListView`。它会初始化`dataSource`来填充`ListView`。
'dataSource'中的每一项都会被渲染成一个`Text`组件，并最终渲染所有`Text`组件组成一个`ListView`。

> 使用`ListView`时需要传入`rowHasChanged`。我们定义一个rowchange为：当前row与上一个row不同时，
> 则row发生了change（mlgb，翻译的想死:(Here we just say a row has changed if the row we are on is not the same as the previous row.）。

{% raw %}
```
import React, { Component } from 'react';
import { AppRegistry, ListView, Text, View } from 'react-native';

class ListViewBasics extends Component {
  // Initialize the hardcoded data
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
    this.state = {
      dataSource: ds.cloneWithRows([
        'John', 'Joel', 'James', 'Jimmy', 'Jackson', 'Jillian', 'Julie', 'Devin'
      ])
    };
  }
  render() {
    return (
      <View style={{flex: 1, paddingTop: 22}}>
        <ListView
          dataSource={this.state.dataSource}
          renderRow={(rowData) => <Text>{rowData}</Text>}
        />
      </View>
    );
  }
}

// App registration and rendering
AppRegistry.registerComponent('ListViewBasics', () => ListViewBasics);
```
{% endraw %}

使用`ListView`的一个最常用的场景，就是从服务器获取数据来展现的时候。为了实现这个，
需要看这里[learn about networking in RN](networking.md)。
{% endblock %}