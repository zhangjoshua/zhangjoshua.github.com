---
layout: post
title: 第八章 继承 练习7
category: Objective-C
tags:
- obj学习

---

>编写一个名为 intersect: 的 Rectangle 方法，该方法使用一个矩形作为参数，并返回代表两个矩形的重叠区域。
>
>如果矩形没有相交，返回宽度与高度均为零的矩形，其原点位（0，0）。

判断返回值应该为（Rectangle *）,在 Rectangle.h 中加入：

		-(Rectangle *) intersect: (Rectangle *) newRec;

在 Rectangle.m 中加入：

	-(Rectangle *) intersect: (Rectangle *) newRec{

    Rectangle *intersectRec = [Rectangle new];
    XYpoint *origIntersectRec = [XYpoint new];
    
    float maxLeft = (origin.x > intersectRec.origin.x) ? origin.x : intersectRec.origin.x;
    float minRight = ((origin.x + width ) < (intersectRec.origin.x + intersectRec.width)) ? (origin.x + width) : (intersectRec.origin.x + intersectRec.width);
    float maxBottom = (origin.y > intersectRec.origin.y) ? origin.y : intersectRec.origin.y;
    float minTop = ((origin.y + height) < (intersectRec.origin.y + intersectRec.height)) ? (origin.y + height) : (intersectRec.origin.y + intersectRec.height);
    
    if ((maxLeft < minRight) && (maxBottom < minTop)) {
        
        [origIntersectRec setX: maxLeft andY:maxBottom];
        [intersectRec setWidth:(minRight - maxLeft) andHeight:(minTop - maxBottom)];
        [intersectRec setOrigin:origIntersectRec];
        return intersectRec;
	    }
    else {
        
        [origIntersectRec setX: 0 andY: 0];
        //intersectRec.origin = origIntersectRec;
        [intersectRec setOrigin:origIntersectRec];
        [intersectRec setWidth:0 andHeight:0];
        return intersectRec;
	    }
	}

main.m 中的实现：

	#import "Rectangle.h"
	#import "XYpoint.h"


	int main(int argc, const char * argv[])
	{
    @autoreleasepool {
     
        Rectangle *myRec1 = [Rectangle new];
        XYpoint *myPoint1 = [XYpoint new];
        
        [myRec1 setWidth:250 andHeight:75];
        [myPoint1 setX:200 andY:420];
        //myRec1.origin = myPoint1;
        [myRec1 setOrigin:myPoint1];
        
        
        Rectangle *myRec2 = [Rectangle new];
        XYpoint *myPoint2 = [XYpoint new];
        
        [myRec2 setWidth:100 andHeight:180];
        [myPoint2 setX:400 andY:300];
        //myRec2.origin = myPoint2;
        [myRec2 setOrigin:myPoint2];
        
        Rectangle *inter = [Rectangle new];
        
        inter = [myRec1 intersect: myRec2];
        
        NSLog(@"the Rec's point is (%.2f,%.2f),the width and height is %.2f %.2f",inter.origin.x,inter.origin.y,inter.width,inter.height);
        
-输出的结果不是很正确，但是找不出问题。待解-

找到原因了，intersect: 方法的实例变量出了问题，

将 Rectangle.m 进行如下修改即可：

	-(Rectangle *) intersect: (Rectangle *) intersectRec{

    //Rectangle *intersectRec = [Rectangle new];
    XYpoint *origIntersectRec = [XYpoint new];

当然，最好接口中保持同步
	
	-(Rectangle *) intersect: (Rectangle *) intersectRec;
	
输出：

	2014-03-29 16:01:40.291 Rectangle[12826:303] the Rec's point is (400.00,420.00),the width and height is 50.00 60.00

