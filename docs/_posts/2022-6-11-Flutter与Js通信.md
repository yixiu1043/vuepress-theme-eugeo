---
title: Flutter与Js通信
date: 2022-6-11
tags:
  - flutter
category: 前端
banner: /img/banner/62.jpeg
---

# Flutter 代码示例
### 接收消息
```dart
Scaffold(
  appBar: AppBar(title: const Text('WebView页面')),
  body: WebView(
    initialUrl: 'http://127.0.0.1:5500/index.html',
    javascriptMode: JavascriptMode.unrestricted,
    javascriptChannels: <JavascriptChannel>{
      JavascriptChannel(
        name: "FlutterBridge", // js 通信管道
        onMessageReceived: (JavascriptMessage javascriptMessage) {
          /// 接收js发来的消息
          final message = jsonDecode(javascriptMessage.message);
          final method = message['method'];
          final data = message['data'];
          switch(method) {
            case: 'back':
            	Get.back();
            	break;
            	...
          }
        },
      )
    },
  ),
)
```























# Web前端代码

### Js发送消息
```javascript
 <body>
  <button onclick="onButtonClick()" style="width: 200px; height: 60px">
    发送消息
  </button>

  <script>
    function onButtonClick() {
      console.log("onButtonClick");
      var data = {
        method: "back",
        data: "aaaa",
      };
      // 发送消息
      FlutterBridge.postMessage(JSON.stringify(data));
    }
  </script>
</body
```