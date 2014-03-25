---
layout: post
title: 第八章 继承 练习6
category: Objective-C
tags:
- obj学习

---

>编写一个名为 containsPoint: 的 Rectangle 方法，使用 XYpoint对象作为参数
>	
> -（BOOL）containsPoint: (XYpoint \*) aPoint;
>	
> 这个方法返回 BOOL 值，如果矩形包含有这个点，返回 YES，否则返回 NO。
	
	
在 Rectangle.h 添加

		-(BOOL) containsPoint:(XYpoint *) aPoint;

在 Rectangle.m 添加

		-(BOOL) containsPoint:(XYpoint *) aPoint{
		if ((aPoint.x >= origin.x) && (aPoint.x <= origin.x + width) && (aPoint.y >= origin.y) && (aPoint.y <= origin.y + height)) {
             return YES;
	    }else{
             return NO;
             }
		}
		
在 main.m 中的代码为


		#import "Rectangle.h"
		#import "XYpoint.h"
		
		int main(int argc, const char * argv[]){
		  @autoreleasepool {
		  
        Rectangle *myRec = [Rectangle new]; //建立矩形
        XYpoint *point1 = [XYpoint new]; //给矩形设原点
        XYpoint *point2 = [XYpoint new]; //判断点1
        XYpoint *point3 = [XYpoint new]; //判断点2
        
        [myRec setWidth:5 andHeight:8]; 
        [point1 setX:3 andY:5];
        
        myRec.origin = point1; //aka [myRec setOrigin:point1]; 
        
        [point2 setX:3 andY:5];
        [point3 setX:5 andY:18];
        
        if ([myRec containsPoint:point2]) {
            NSLog(@"YES,it Contain the point (%.2f,%.2f)",point2.x , point2.y);
        }else {
            
            NSLog(@"NO,it is not contain the point (%.2f,%.2f)",point2.x,point2.y);
        }
        
        if ([myRec containsPoint:point3]) {
            NSLog(@"YES,it Contain the point (%.2f,%.2f)",point3.x , point3.y);
        }else {
            
            NSLog(@"NO,it is not contain the point (%.2f,%.2f)",point3.x,point3.y);    
        }
        } 
        return 0;
		}
        
调试结果

2014-03-24 22:27:08.541 Rectangle[25269:303] YES,it Contain the point (3.00,5.00)

2014-03-24 22:27:08.541 Rectangle[25269:303] NO,it is not contain the point (5.00,18.00)

注意
* if else 后面的{} 不能丢失
* BOOL 返回值为 YES 或者 NO，被 if 语句用做判断
* 


发散思维
这个只是判断点在矩形范围内，如果判断点是否在矩形的线条上，containsPoint:方法该如何改？

		((aPoint.x = origin.x) || ((aPoint.y >= origin.y) &&(aPoint.y <= origin.y + height))) && ((aPoint.x = origin.x + width) || ((aPoint.y >= origin.y) &&(aPoint.y <= origin.y + height))) && ((aPoint.y = origin.y) || ((aPoint.x >= origin.x) &&(aPoint.x <= origin.x + width))) && ((aPoint.y = origin.y + height) || ((aPoint.x >= origin.x) &&(aPoint.x <= origin.x + width)))