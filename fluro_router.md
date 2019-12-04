# 路由管理解决方案

## 安装

```
fluro: ^1.5.1
```

## 配置

### application.dart

```
class Application {
  static Router router;
}
```

### routes.dart

```
class Routes {
  static String root = "/";
  static String home = "/home";

  static void configureRoutes(Router router) {
    router.define(root, handler: splashHandler);

    router.define(home, handler: homeHandler);
  }
}
```

### route_handlers.dart

```
var splashHandler = new Handler(
    handlerFunc: (BuildContext context, Map<String, List<String>> params) {
  return new SplashPage();
});

var homeHandler = new Handler(
    handlerFunc: (BuildContext context, Map<String, List<String>> params) {
  return new HomePage();
});
```

### navigator_util.dart

```
class NavigatorUtil {
  static void goHomePage(BuildContext context) {
    Application.router.navigateTo(context, Routes.home, replace: true);
  }
}
```

### main.dart

```
void main() {
  // 注册 fluro routes
  Router router = Router();
  Routes.configureRoutes(router);
  Application.router = router;

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      onGenerateRoute: Application.router.generator,
    );
  }
}
```

## 传递参数

*Fluro路由地址，只能传递String类型（并且不支持中文），所以需要对 中文，int,double,bool,自定义类型进行一个转换 , 写了一个 转换类 fluro_convert_util.dart。*

```
import 'dart:convert';

/// fluro 参数编码解码工具类
class FluroConvertUtils {
  /// fluro 传递中文参数前，先转换，fluro 不支持中文传递
  static String fluroCnParamsEncode(String originalCn) {
    return jsonEncode(Utf8Encoder().convert(originalCn));
  }

  /// fluro 传递后取出参数，解析
  static String fluroCnParamsDecode(String encodeCn) {
    var list = List<int>();

    ///字符串解码
    jsonDecode(encodeCn).forEach(list.add);
    String value = Utf8Decoder().convert(list);
    return value;
  }

  /// string 转为 int
  static int string2int(String str) {
    return int.parse(str);
  }

  /// string 转为 double
  static double string2double(String str) {
    return double.parse(str);
  }

  /// string 转为 bool
  static bool string2bool(String str) {
    if (str == 'true') {
      return true;
    } else {
      return false;
    }
  }

  /// object 转为 string json
  static String object2string<T>(T t) {
    return fluroCnParamsEncode(jsonEncode(t));
  }

  /// string json 转为 map
  static Map<String, dynamic> string2map(String str) {
    return json.decode(fluroCnParamsDecode(str));
  }
}

```

*配置*

```
class Routes {
  static String root = "/";
  static String home = "/home";
  static String params = "/params";

  static void configureRoutes(Router router) {
    router.define(root, handler: splashHandler);

    router.define(home, handler: homeHandler);

    router.define(params, handler: paramsHandler);
  }
}
```

*处理*

```
var paramsHandler = new Handler(
    handlerFunc: (BuildContext context, Map<String, List<String>> params) {
  var p = params['p']?.first;
  Person person = Person.fromJson(FluroConvertUtils.string2map(p));
  String cn = FluroConvertUtils.fluroCnParamsDecode(params['cn']?.first);

  return new ParamsPage(
    p: person,
    cn: cn,
  );
});
```

*跳转*

```
static void goParams(BuildContext context, Person p, String cn) {
    String mCn = FluroConvertUtils.fluroCnParamsEncode(cn);
    String mP = FluroConvertUtils.object2string(p);
    Application.router.navigateTo(context, Routes.params + '?p=$mP&cn=$mCn');
  }
```

## 参考
[https://juejin.im/post/5d051a5b6fb9a07ec07fbdc5#heading-21]
