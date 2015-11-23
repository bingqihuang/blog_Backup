title: "Assertion failure in -[UITableView layoutSublayersOfLayer:]" error in iOS7
tags: [iOS7, UITableView, layoutSublayersOfLayer]
date: 2015-11-11

## 问题来源

　　起初的想法是，在**UITableViewController**中，如果加载没有数据，则显示一个没有数据的提示***TipView***。在添加的过程中，都对TipView以及TipView的子View添加了约束。结果导致了Crash。但是这些在iOS8洗头版本以上是运行正常的。

报错的log如下：

```bash
Assertion failure in -[UITableView layoutSublayersOfLayer:], /SourceCache/UIKit_Sim/UIKit-2935.137/UIView.m:8794　	

```

## 追根溯源

对于这个问题，网上也有很多说法。比如有人说UITableView在iOS7下是不能addSubView的的。还有因为之前使用的第三方库Masonry来约束的，于是也尝试着用系统自带的约束来布局。但都没有解决问题。

经过测试，才发现在iOS7中，向UITableView添加子View时如果使用自动布局，就会报这个错。没办法，***只能放弃使用AutoLayout，通过设置frame来实现。***这就是最后的解决方案。




