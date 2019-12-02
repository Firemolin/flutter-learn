# 点击空白收起键盘

**思路1：**在布局最外层包裹手势widget，在onTap方法中执行键盘收回的操作。
```
@override
Widget build(BuildContext context) {
return Scaffold(
    appBar: AppBar(
      title: Text(widget.title),
    ),
    body: SafeArea(
      child: GestureDetector(
          behavior: HitTestBehavior.translucent,
          onTap: () {
            FocusScope.of(context).requestFocus(FocusNode());
          },
          child: Container(
              color: Colors.grey,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[TextField()],
              ))),
    ));
}
```
**思路2：**在布局最外层包裹手势widget，监听输入框焦点，在onTap方法中执行输入框失去焦点的操作。
```
FocusNode _focusNode = FocusNode();

@override
Widget build(BuildContext context) {
return Scaffold(
    appBar: AppBar(
      title: Text(widget.title),
    ),
    body: SafeArea(
      child: GestureDetector(
          behavior: HitTestBehavior.translucent,
          onTap: () {
            if (_focusNode.hasFocus) {
              _focusNode.unfocus();
            }
          },
          child: Container(
              color: Colors.grey,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  TextField(
                    focusNode: _focusNode,
                  )
                ],
              ))),
    ));
}
```