## 移动端慎用fixed！
    在移动端使用fixed可能引起很多奇葩的为题，这里总结一下我在工作中遇到的关于fixed的问题，并给出了经实践，已解决问题的解决方案。

> Q：在ios中，fixed会让input聚焦时，光标不显示 或者 显示错位。

A：讲fixed改为absolute处理。

 
> Q：在安卓中，被设置fixed的元素A，显示在底部。当手机键盘弹出时，A的子元素会被键盘顶到上面去。

A：将fixed布局使用其他布局形式，比如min-height 结合 flex去布局