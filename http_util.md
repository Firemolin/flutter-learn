# 网络请求封装

## 添加依赖

```
dependencies:
  dio: ^3.0.7
```

## 封装
```
import 'package:dio/dio.dart';

class HttpRequest {
  Dio _dio;

  HttpRequest() {
    _dio = Dio();
    _setConfig();
    _setInterceptors();
  }

  void _setConfig() {
    _dio.options.baseUrl = "https://jsonplaceholder.typicode.com";
    _dio.options.connectTimeout = 5000; //5s
    _dio.options.receiveTimeout = 3000;
  }

  void _setInterceptors() {
    _dio.interceptors
        .add(InterceptorsWrapper(onRequest: (RequestOptions options) async {
      // 在请求被发送之前做一些事情
      var token;
      if (token != null) {
        options.headers = token;
      }
      print('RquestHeader:::::::${options.headers.toString()}');
      return options; //continue
      // 如果你想完成请求并返回一些自定义数据，可以返回一个`Response`对象或返回`dio.resolve(data)`。
      // 这样请求将会被终止，上层then会被调用，then中返回的数据将是你的自定义数据data.
      //
      // 如果你想终止请求并触发一个错误,你可以返回一个`DioError`对象，或返回`dio.reject(errMsg)`，
      // 这样请求将被中止并触发异常，上层catchError会被调用。
    }, onResponse: (Response response) async {
      // 在返回响应数据之前做一些预处理
//      if (response.data.code == 200) {
//        return response.data;
//      } else {
//        return _dio.reject('BusinessErr:::::');
//      }
      return response.data;
    }, onError: (DioError e) async {
      // 当请求失败时做一些预处理
      return e; //continue
    }));
  }

  // General network request
  request(String path, String method,
      {Map<String, dynamic> data, Map<String, dynamic> queryParameters}) async {
    print('url:::::$path');
    print('method:::::$method');
    return await _dio.request(path,
        queryParameters: queryParameters,
        data: data,
        options: Options(method: method));
  }
}

final httpRequest = HttpRequest();

```

## 使用

```
httpRequest.request('/posts/1', 'get',
  queryParameters: {'id': '999'}).then((res) {
    print('res====>$res');
    _entity = TestEntity.fromJson(json.decode(res.toString()));
    setState(() {});
});
```

**注意**:在initState初始化方法中进行网络请求，需要使用SchedulerBinding。
```
SchedulerBinding.instance.addPostFrameCallback((_) {
  httpRequest.request('/posts/1', 'get',
      queryParameters: {'id': '999'}).then((res) {
    print('res====>$res');
    _entity = TestEntity.fromJson(json.decode(res.toString()));
    setState(() {});
  });
});
```

