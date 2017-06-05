{% extends "../tpls/base.md" %}

{% block title %}
# Using a ScrollView
{% endblock %}

{% block pageContent %}
`ScrollView`是个通用的可容纳多个组件(components)和视图(views)的可滚动容器。
可滚动的item不必同属一种类型，scrollview还可以设置为水平滚动或垂直滚动。

下面这个栗子是一个混合容纳images和text的垂直方向可滚动的`ScrollView`。
```
import React, { Component } from 'react';
import { AppRegistry, ScrollView, Image, Text } from 'react-native'

class IScrolledDownAndWhatHappenedNextShockedMe extends Component {
  render() {
      return (
        <ScrollView>
          <Text style={{fontSize:96}}>Scroll me plz</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>If you like</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>Scrolling down</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>What's the best</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>Framework around?</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:80}}>React Native</Text>
        </ScrollView>
    );
  }
}


AppRegistry.registerComponent(
  'IScrolledDownAndWhatHappenedNextShockedMe',
  () => IScrolledDownAndWhatHappenedNextShockedMe);
```

`ScrollView`比较适合有限的短列表。`ScrollView`里面的所有元素都会一次性的渲染出来（
即使还没有出现在屏幕的可视范围内）。如果你想要处理长列表，需要用到`ListView`。详情
[戳这里](listview.md)。
{% endblock %}