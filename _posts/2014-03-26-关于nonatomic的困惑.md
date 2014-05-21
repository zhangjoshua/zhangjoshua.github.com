---
layout: post
title: 关于nonatomic的困惑
category: Objective-C
tags:
- obj学习

---


通过 @property 和 @synthesize 来实现存取方法:

	@property double real ,imaginary ;
	
	--
	@synthesize real , imaginary;

但却报警告：

	warning:  Writable atomic property 'real' cannot pair a synthesized getter with a user defined setter
	warning:  Writable atomic property 'imaginary' cannot pair a synthesized getter with a user defined setter
	
修复建议：

	 fix-it Setter and getter must both be synthesized,or both be user defined,or the property must be nonatomic
	
	
搜了下，获得几种解决办法：

1. 声明属性为nonatomic，即我上面的修改方法。
2. @synthesize合成用getter/setter方法（即自己手动定义getter/setter方法)。
3. 用@dynamic来代替@synthesize。
4. 直接不用属性@property。