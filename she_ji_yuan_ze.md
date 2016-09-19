# 设计原则

### 把UI拆分为一个组件的层级
但是你如何知道什么东西应该是独立的组件？只需在你创建一个函数或者对象时，根据是否使用过相同技术来做决定。一种这样的技术是单一功能原则（single responsibility principle），也就是一个组件在理想情况下只做一件事情。如果它最终增长了，它就应该被分解为更小的组件。

例如：
* FilterableProductTable
 * SearchBar
 * ProductTable
   * ProductCategoryRow
   * ProductRow

### 用React创建一个静态版本
要构建一个静态版本 app 来渲染你的数据模型，你将会想到构建一个重用其它组件并利用 props 传递数据的组件。props 是一种从父级传递数据到子级的方式。

### 确定最小（但完备）的 UI state 表达
要正确的构建你的 app，你首先需要思考你的 app 需要的可变 state 的最小组。这里的关键是 DRY 原则：Don't Repeat Yourself(不要重复自己)。想出哪些是你的应用需要的绝对最小 state 表达，并按需计算其他任何数据。
