# JavaScript SDK 使用手册

## 引入 SDK

```
<script src=".../analytics.js"></script>
<script>
  var analytics = analytics({
    'apiKey': '<提供的Key>',
    // 测试时，需要指定测试环境的postUrl
    // 'postUrl': 'https://api.com/api/v1'
  });
</script>
```

## 使用方式

### 用户登录

用户登录后，直到调用登录接口，所有的事件埋点都会自动打上用户 ID 属性。 并且当用户修改个人信息时，也可以调用该接口以更新用户信息。

```
analytics.identify('user_id', {
  'name': 'test'
});
```

### 用户退出

```
analytics.logout();
```

### 自定义事件

```
// analytics.tack({event}, [properties])
analytics.track('testEvent', {
  'problem_id': '1'
});
```

### 自动采集

默认 SDK 会采集所有浏览页面事件，如不需要，在初始化 SDK 时，设置 `autoPV` 参数即可关闭。

```
var analytics = analytics({
  'apiKey': '<原子钟提供的Key>',
  'autoPV': false
});
```