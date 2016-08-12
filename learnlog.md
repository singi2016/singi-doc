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
3. self.view.frame获取最外层View的frame对象,frame.size.width获取当前view的宽度。

##2016-8-12
1. 点击表格某一行时，弹出UIAlertController，点击UIAlertController时，执行特定的动作，这里选择了某一行，并会打钩。
2. 当某一行被选择时触发的方法是tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath)，然后在这个方法里面弹出UIAlertController。
3. UIAlertController产生到显示的一般步骤：先生成一个UIAlertController对象，保存为optionMenu，然后生成一个UIAlertAction对象，这个是设置用户能看到的弹层内容的对象。接着调用optionMenu.addAction(UIAlertAction),将UIAlertAction加入到UIAlertController中，最后调用顶层TableViewController的presentViewController方法将UIAlertController显示在表格中。
4. 改变cell状态时，需要借助第三方变量来记录当前状态，然后改变时还需要刷新，从新载入已经改变的状态。