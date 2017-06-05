{% extends "../tpls/base.md" %}

{% block title %}
# Handling Text Input
{% endblock %}

{% block pageContent %}
`TextInput`是一个允许用户输入文本的基础组件。它有个`onChangeText`属性（prop），会在
每次text改变的时候调用，然后在输入提交时调用`onSubmitEditing`。

举个栗子：对于用户输入，我们假设这样的场景，我们会把用户的每个输入转换成另一种“语言”——
每个单词都会被转换成一个🍕。如果输入"hello there bob"，则会输出"🍕🍕🍕"。

```
import React, { Component } from 'react';
import { AppRegistry, Text, TextInput, View } from 'react-native';

class PizzaTranslator extends Component {
  constructor(props) {
    super(props);
    this.state = {text: ''};
  }

  render() {
    return (
      <View style={{padding: 10}}>
        <TextInput
          style={{height: 40}}
          placeholder="Type here to translate!"
          onChangeText={(text) => this.setState({text})}
        />
        <Text style={{padding: 10, fontSize: 42}}>
          {this.state.text.split(' ').map((word) => word && '🍕').join(' ')}
        </Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('PizzaTranslator', () => PizzaTranslator);
```

在上面这个例子中，我们将`text`存入state，因为可能会有变动。

当然对于文本输入，我们还可以做很多事情。比如验证用户输入的有效性。更多详细内容
看这里[React docs on controlled components（官方）](https://facebook.github.io/react/docs/forms.html)，
或者这里[reference docs for TextInput（官方）](https://facebook.github.io/react-native/docs/textinput.html)。

text input可能是state自然改变的组件中最简单的一个实例。接下来，我们来看另一种控制布局的组件[ScrollView](scrollview.md)。
{% endblock %}