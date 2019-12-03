# 状态加载窗口

```
class AppLoadingDialog {
  static bool isLoading = false;

  static void show(BuildContext context, String txt) {
    if (!isLoading) {
      isLoading = true;
      showGeneralDialog(
          context: context,
          barrierDismissible: false,
          barrierLabel:
              MaterialLocalizations.of(context).modalBarrierDismissLabel,
          transitionDuration: const Duration(milliseconds: 150),
          pageBuilder: (BuildContext context, Animation animation,
              Animation secondaryAnimation) {
            return Align(
              child: ClipRRect(
                borderRadius: BorderRadius.circular(10),
                child: Container(
                  width: AppScreenUtil.setWidth(220),
                  height: AppScreenUtil.setWidth(220),
                  color: Colors.black.withOpacity(0.5),
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      CupertinoActivityIndicator(radius: AppScreenUtil.setWidth(35)),
                      SizedBox(height: AppScreenUtil.setWidth(40)),
                      Text(
                        txt,
                        style: TextStyle(
                            decoration: TextDecoration.none,
                            color: Colors.white,
                            fontSize: AppScreenUtil.setSp(28),
                            fontWeight: FontWeight.w400),
                      )
                    ],
                  ),
                ),
              ),
            );
          }).then((v) {
        isLoading = false;
      });
    }
  }

  static void dismiss(BuildContext context) {
    if (isLoading) {
      Navigator.of(context).pop();
    }
  }
}
```