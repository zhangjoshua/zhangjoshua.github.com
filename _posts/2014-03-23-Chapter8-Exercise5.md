---
layout: post
title: 第八章 继承 练习5
category: Objective-C
tags:
- obj学习

---

>定义一个名为 GraphicObject 的新类，使其成为 NSObject 的子类。在新类中定义如下一些实例变量：
>
>int fillColor; // 32位颜色
>
>int filled; //是否为对象填充了？
>
>int lineColor; // 32位线的颜色
>
>编写一个方法，设定并检索前面定义的变量。使 Rectangle 类成为 GraphicObject 的子类。

创建 GraphicObject.h 

	#import <Foundation/Foundation.h>

		@interface GraphicObject : NSObject{
    
		    int fillColor;
		    int lineColor;
		    bool filled;
		}

		@property int fillColor , lineColor ;
		@property bool filled;

		-(void) setFillColor:(int)fc;
		-(void) setLineColor:(int)lc;

	@end
		
创建 GraphicObject.m
		
	#import "GraphicObject.h"

		@implementation GraphicObject

		@synthesize fillColor ,lineColor ;
		@synthesize filled;

		-(int)fillColor{
	        return fillColor;
		}

		-(int)lineColor{
	        return lineColor;
		}

		-(void) setFillColor:(int)fc{
    
		    fillColor = fc;
		    self.filled = YES;
		}

		-(void) setLineColor:(int)lc{
    
		    lineColor = lc;
		    self.filled = YES;
		}

	@end
		
使得 Rectangle 类成为 GraphicObject 的子类：

		@interface Rectangle : GraphicObject
		
main.m 中的使用：

		
		[myRect setFillColor:0x00FF0000];
        
		NSLog(@"IS IT FILLED? %s",[myRect filled]?"YES":"NO");
		
输出结果

2014-03-24 22:27:08.542 Rectangle[25269:303] IS IT FILLED? YES


