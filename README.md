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
