## css小记！

> Q：设置height: 100%，没有效果。

A：在给块级元素设置高度100%时，父级一定要有 **显式** 定义的高度。

当父级元素的高度设置了min-height，用来控制元素的最小高度，子元素使用height:100%是无法获取高度的。如果想要子元素是父元素的100%：

**方法一**（父元素显示定义高度）： 父元素:设置height，删除min-height。

**方法二**（绝对定位）：父元素设置position: relative，子元素设置position: absolute。


> Q：transform导致字体模糊

A：当元素渲染时，若transform值函数(如translate3d(), scale(), rotate()等)中的参数为非整数，在使用iScroll模拟滚动的项目中会出现字体模糊。

解决方法：将包含文字块级元素的高设置为偶数。