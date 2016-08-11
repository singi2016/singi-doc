# ios8-swift 学习记录

##2016-8-10
1. `ViewController` 需要在`Custom Class`绑定
2. `storyboard`中的元素可以按住`Ctrl`,然后拖动到`ViewController`上，释放鼠标左键，然后可以选择需要绑定的方法(如果代码已经有了的话。)
3. aotu layout,在main.storyboard->preview，记得同时按住shift+option，点击previw，然后，点击+,打开一个预览窗口就可以预览到界面了，左下脚的+可以选择不同尺寸的屏幕，屏幕下方的按钮，可以横屏竖屏你的设备。
4. prototype原型，开始一个app之前，先画好原型，工具sketch
5. UITableView 需要实现两个接口：UITableViewDelegate(控制表格样式)，UITableViewDataSource(负责处理数据并显示)；

##2016-8-11
1. 添加元素的时候，需要注意元素的类型，ViewController是ViewController，TableViewController是TableViewController;
2. 关于绑定，首先绑定类，然后绑定类的属性