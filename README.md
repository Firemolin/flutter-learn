# 项目总结  
## Scaffold常用属性：
* appBar：设置应用栏，显示在脚手架顶部
```
appBar: AppBar( title: Text('Sample Code'), )
```
* body： 设置脚手架内容区域控件
```
body: Center(child: Text('Hello'),)
```
* floatingActionButton:设置显示在上层区域的按钮，默认位置位于右下角       
```
 floatingActionButton: FloatingActionButton(
   onPressed: null,
   child: Icon(Icons.add),
 )
```
* floatingActionButtonLocation:设置floatingActionButton的位置
```
floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked 
```
* floatingActionButtonAnimator:设置floatingActionButton的动画
```
floatingActionButtonAnimator:FloatingActionButtonAnimator.scaling
```
* persistentFooterButtons:一组显示在脚手架底部的按钮(在bottomNavigationBar底部导航栏的上面)
```
persistentFooterButtons: <Widget>[
  RaisedButton(
    onPressed: null,
    child: Text('Click1'),
  ),
  RaisedButton(
    onPressed: null,
    child: Text('Click2'),
  ),
]
```
* drawer:设置左边侧边栏
```
drawer: Drawer(
    child: Center(
      child: Text('left drawer'),
    ),
  )
```
* endDrawer: 设置右边侧边栏
```
endDrawer: Drawer(
    child: Center(
      child: Text('right drawer'),
    ),
  )
```
* bottomNavigationBar: 设置脚手架 底部导航栏
```
bottomNavigationBar: BottomAppBar(
    child: Container(height: 50.0,),
  )
```
* backgroundColor: 设置脚手架内容区域的颜色
```
backgroundColor: Colors.yellow
```
* resizeToAvoidBottomPadding: 控制界面内容 body 是否重新布局来避免底部被覆盖，比如当键盘显示的时候，重新布局避免被键盘盖住内容
```
resizeToAvoidBottomPadding: false
```
### SafeArea
**用来适配不规则的屏幕。**
```
SafeArea(
  child: Center(
    child: Text('Hello Tifor'),
)),
```
* 仅指定特定的某一位置
```
SafeArea(
  top: false,
  bottom: true,
  left: true,
  right: false,
),
```



