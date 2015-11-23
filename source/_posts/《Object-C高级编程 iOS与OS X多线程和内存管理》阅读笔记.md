title:《Object-C高级编程 iOS与OS X多线程和内存管理》阅读笔记
tags: [iOS, 多线程, 内存管理]
date: 2015-11-04

----

## 自动引用计数

### 1.1 内存管理的思考方式

* 自己生成的对象，自己持有。
* 非自己生成的对象，自己也能持有。
* 自己持有的对象不再需要时释放。
* 非自己持有的对象无法释放。

### 1.2 权限修饰符

#### 1.2.1 _strong
* _strong修饰符是id类型和对象类型默认的所有权修饰符。
* _strong修饰符表示对对象的“强引用”。持有强引用的变量在超出其作用域时被废弃，随着强引用的失效，引用的对象会被释放。
* 附有_strong修饰符的的变量之间可以相互赋值。

#### 1.2.2 _weak
* _weak修饰符和_strong修饰符相反，提供弱引用。它的出现是为了解决循环引用的问题。
* **循环引用**一般有两种：对象之间的强引用；对象自身的强引用。
* _weak修饰符的变量不持有对象，在超出对象的作用域时，对象即被释放。
* _weak修饰符在持有某对象的弱引用时，若该对象被废弃，则此弱引用将自动失效且被赋值为nil。


代码示例：

``` bash
@interface Test : NSObject
{
    id __strong obj_;
}

- (void)setObject:(id __strong)obj;

@end

@implementation Test

- (void)setObject:(id)obj {
    obj_ = obj;
}
@end
```
对象之间的循环引用代码示例：

``` bash
{
	id test0 = [[Test alloc] init]; // 生成对象A，test0持有Test对象A的强引	用。
	id test1 = [[Test alloc] init]; // 生成对象B，test0持有Test对象B的强引	用。

	[test0 setObject:test1];
	/*
		Test对象A的obj_成员变量持有Test对象B的强引用。
	
		此时持有Test对象B的强引用变量为：Test对象A的obj_和test1;
	*/

	[test1 setObject:test0];
	/*
		Test对象B的obj_成员变量持有Test对象A的强引用。
	
		此时持有Test对象A的强引用变量为：Test对象B的obj_和test0;
	*/
}
/*
	因为test0变量超出作用域，强引用失效，
	所以自动释放Test对象A。
	
	因为test1变量超出作用域，强引用失效，
	所以自动释放Test对象B。
	
	此时持有对象A的强引用变量为：Test对象B的obj_。
	
	此时持有对象A的强引用变量为：Test对象A的obj_。
	
	发生内存泄露。
*/
@end
```

对象自身强引用引起的循环应用代码示例：

``` bash
{
	id test = [[Test alloc] init];
	
	[test setObject:test];
}
@end
```

#### 1.3 ARC的规则
* 不能使用retain/release/retainCount/autorelease方法。
* 不能使用NSAllocateObject/NSDellocateObject
* 必须遵循内存管理的方法命名规则。
* 不要显式调用dealloc。
* 使用@autoreleasepool块 替代 NSAutoreleasePool。 同样可以嵌套使用。
* 对象型变量不能作为C语言结构体(stuct/union)的成员。
* 显式转换"id" 和"void *"。

