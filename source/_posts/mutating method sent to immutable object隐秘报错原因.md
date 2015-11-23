title: mutating method sent to immutable object</font>的隐秘报错原因
tags: [iOS开发, mutating method]
date: 2015-08-26

---

虽说<font color="#45903" size="4px">mutating method sent to immutable object</font>这个错误在iOS开发中不是很难解决，但是有时候这个报错会非常隐秘，这回碰到一个，详情且看下文。

## 报错

下面就是报错内容：

``` bash
Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: '-[__NSCFArray removeObjectAtIndex:]: mutating method sent to immutable object'
```

接着是报错的代码：

``` bash
[self.dataList removeAllObjects]; // self.dataList 类型是NSMutableArray
if (isMessage) {
   self.dataList = (NSMutableArray *)[result objectForKey:News];
} else {
   self.dataList = (NSMutableArray *)[result objectForKey:Note];
}
```

## 报错代码分析

看报错的提示，意思就是把一个可变量对应的方法让一个不可变量来调用。

<font color="#45903">mutating method</font>（可变量对应的方法）:是那些在创建后可以被更改的变量所拥有的method，比如NSMutableArray,NSMutableDictionary 等。

<font color="#45903">immutable object</font>(不可改变的变量):就是那些被创建后不能被改变的变量:比如　NSArray　NSDictionary等。

很迷惑的是，我明明初始化的是NSMutableArray，在运行以上代码后，self.dataList的类型变成了NSArray。

分析后才发现，
self.dataList = (NSMutableArray *)[result objectForKey:News];这句代码并没有如我所想转换成NSMutableArray，而是将self.dataList 类型改成了NSArray。

## 解决Bug

通过以上代码分析，知道报错原因后，剩下的就是解决<font color="#45903" size="3px">如何将result里的数据获取而不改变self.dataList的数据类型</font>的问题了。其实很简单，修改成以下代码就行了。

``` bash
if (isMessage) {
    self.dataList = [[result objectForKey:News] mutableCopy];
} else {
    self.dataList = [[result objectForKey:Note] mutableCopy];
}
```

<center>
	<font color="#ff0000" size="5px">
		The End!
	</font>
</center>






