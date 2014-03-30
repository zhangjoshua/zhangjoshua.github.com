---
layout: post
title: 第八章 继承 练习8
category: Objective-C
tags:
- obj学习

---

>为 Rectangle 类编写一个名位 draw 的方法，此方法使用虚线和垂直的条形字符绘制矩形。以下代码序列：
>
	Rectangle *myRect = [[Rectangle alloc] init];
	[myRect setWidth:10 andHeight:3];
	[myRect draw];
>	
>注意：应该使用 printf 绘制字符，因为每次调用 NSLog 时都会显示一个新行。

draw 方法：

	-(void) draw{
    
    //Rectangle *mydraw = [Rectangle new];
    
    for(int i = 0; i < self.width ; i++ ) {
        
        printf("-");
    }
        printf("\n");
    
    for (int i = 0; i < self.height; i++) {
        
        printf("|");
        
        for (int j = 0; j < (self.width - 1); j++) {
        printf(" ");
        }
        printf("\n");
    }
    for(int i = 0; i < self.width ; i++ ) {
        
        printf("-");
    }

	}
	
输入结果：


	----------
	|        |
	|        |
	|        |
	----------Program ended with exit code: 0