# 底部导航栏

## 主页面

```
  // current show page index
  int _currentIndex = 0;

  // page list
  List<Widget> _pages = [H1(), H2(), H3()];

  final pageController = PageController();

  // lick on the bottomNav event
  void _bottomNavOnTap(int index) {
    if (index == _currentIndex) return;
    pageController.jumpToPage(index);
  }

  // page view change call
  void onPageChanged(int index) {
    if (index == _currentIndex) return;
    setState(() {
      _currentIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      resizeToAvoidBottomPadding: false,
      body: PageView(
        controller: pageController,
        onPageChanged: onPageChanged,
        children: _pages,
        physics: NeverScrollableScrollPhysics(),
      ),
      bottomNavigationBar: BottomNavigationWidget(
        currentIndex: _currentIndex,
        onTap: _bottomNavOnTap,
      ),
    );
  }
```

## BottomNavigationWidget

```
import 'package:flutter/material.dart';

class BottomNavigationWidget extends StatelessWidget {
  final int currentIndex;

  final ValueChanged<int> onTap;

  BottomNavigationWidget({this.currentIndex, this.onTap});

  @override
  Widget build(BuildContext context) {
    return Theme(
      data: ThemeData(primarySwatch: Colors.orange),
      child: BottomNavigationBar(
        currentIndex: this.currentIndex,
        type: BottomNavigationBarType.fixed,
        selectedFontSize: 12,
        unselectedFontSize: 12,
        unselectedIconTheme: IconThemeData(color: Colors.black),
        selectedIconTheme: IconThemeData(color: Colors.red),
        unselectedItemColor: Colors.grey,
        selectedItemColor: Colors.greenAccent,
        onTap: (index) {
          this.onTap(index);
        },
        items: [
//          _BottomNavigationBarItem.item(
//              imagePath: 'assets/images/icon-zoom.png', title: '案内'),
//          _BottomNavigationBarItem.item(
//              imagePath: 'assets/images/icon-ticket.png', title: 'クーポン'),
//          _BottomNavigationBarItem.item(
//              imagePath: 'assets/images/icon-me.png', title: 'アカウント'),
          _BottomNavigationBarItem.icon(icon: Icons.search, title: 'h1'),
          _BottomNavigationBarItem.icon(
              icon: Icons.account_balance_wallet, title: 'h2'),
          _BottomNavigationBarItem.icon(icon: Icons.perm_identity, title: 'h3'),
        ],
      ),
    );
  }
}

class _BottomNavigationBarItem {
  static BottomNavigationBarItem icon({IconData icon, String title}) {
    return BottomNavigationBarItem(
        icon: Icon(
          icon,
          size: 22,
        ),
        activeIcon: Icon(
          icon,
          size: 22,
        ),
        title: Container(
          padding: const EdgeInsets.only(top: 4.0),
          child: Text(title),
        ));
  }

  static BottomNavigationBarItem item(
      {String imagePath, String title, bool isTransparent = false}) {
    return BottomNavigationBarItem(
        icon: Image.asset(
          imagePath,
          width: 30,
          height: 30,
          color: isTransparent ? Colors.transparent : Colors.black,
        ),
        activeIcon: Image.asset(
          imagePath,
          width: 30,
          height: 30,
          color: isTransparent ? Colors.transparent : Colors.black,
        ),
        title: Container(
          padding: const EdgeInsets.only(top: 2.0),
          child: Text(title),
        ));
  }
}

```