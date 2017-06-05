{% extends "../tpls/base.md" %}

{% block title %}
# Networking
{% endblock %}

{% block pageContent %}
很多app都会从远程地址请求资源。你可能想发起个POST去请求一个REST API，或者单纯的从另一个server
那里获取静态数据。

### 使用Fetch

RN提供了一个[Fetch API(官方)](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)来处理
你的网络需求。如果你以前用过XHR或者其他网络的api，你可能会觉得Fetch有点眼熟。你可以从MDN上查阅到
更多内容[戳这里(官方)](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)。

#### 发请求

想要获取任意URL的内容，可以直接这么搞：

```
fetch('https://mywebsite.com/mydata.json')
```

也可以为Fetch传入可选的第二个参数来更加定制化的设置你的http请求。比如定义额外的header或者构建一个POST请求：
```
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue',
  })
})
```
更多Fetch的详细配置可以[看这里(官方)](https://developer.mozilla.org/en-US/docs/Web/API/Request)。

#### 处理响应

上面的例子展示了如何发起一个请求。但有时你也需要对response搞些si情。

网络有着它固有的异步特性。Fetch方法会返回一个[Promise(MDN官方)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)来代码可读性更友好地进行异步编程：
```
function getMoviesFromApiAsync() {
  return fetch('https://facebook.github.io/react-native/movies.json')
    .then((response) => response.json())
    .then((responseJson) => {
      return responseJson.movies;
    })
    .catch((error) => {
      console.error(error);
    });
}
```
你也可以在RN app里面使用ES2017的async/await：
```
async function getMoviesFromApi() {
  try {
    let response = await fetch('https://facebook.github.io/react-native/movies.json');
    let responseJson = await response.json();
    return responseJson.movies;
  } catch(error) {
    console.error(error);
  }
}
```
如果不catch fetch的错误，这些错误就会被丢弃掉。

> IOS会阻塞掉所有未使用ssl加密的请求。如果你想发送一个http的请求，则首先要添加一个App Transport Security exception项。如果发送请求时，你能确定请求的域名，则可以更详细的添加exception(也就是具体的域名要比*这类的通配设置)要更加安全。如果运行时仍无法确定域名，可以尝试[完全禁用ATS(官方)](https://facebook.github.io/react-native/docs/integration-with-existing-apps.html#app-transport-security)。还要注意一点，自2017年1月开始，苹果App store审核会要求提供禁用ATS的合理原因[了解详细(官方)](https://forums.developer.apple.com/thread/48979)。查看更多信息[Apple's documentation(官方)](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33)。

### 使用其他网络库

[XMLHttpRequest API(官方)](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)是RN的内建API。这意味着你可以使用基于它构建的第三方库[frisbee](https://github.com/niftylettuce/frisbee)或者[axios](https://github.com/mzabriskie/axios)，如果你想的话也可以直接用XMLHttpRequest API。

```
var request = new XMLHttpRequest();
request.onreadystatechange = (e) => {
  if (request.readyState !== 4) {
    return;
  }

  if (request.status === 200) {
    console.log('success', request.responseText);
  } else {
    console.warn('error');
  }
};

request.open('GET', 'https://mywebsite.com/endpoint/');
request.send();
```

由于安全模型的不同，客户端app的XHR中没有web开发中的CORS概念。

### WebSocket

RN同样支持[WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)，一个可以提供全双工交互的TCP连接。

```
var ws = new WebSocket('ws://host.com/path');

ws.onopen = () => {
  // connection opened

  ws.send('something'); // send a message
};

ws.onmessage = (e) => {
  // a message was received
  console.log(e.data);
};

ws.onerror = (e) => {
  // an error occurred
  console.log(e.message);
};

ws.onclose = (e) => {
  // connection closed
  console.log(e.code, e.reason);
};
```

现在你的app可以展现任何形式的数据了，接下来你可能会开始需要在几个屏幕间来组织数据。
想要管理屏幕间的传递，你需要看看这个：[navigators(官方)](https://facebook.github.io/react-native/docs/using-navigators.html)。
{% endblock %}