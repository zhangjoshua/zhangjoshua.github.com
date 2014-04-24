---
layout: post
title: Assignment 1 Extra Credit 1、2
category: Objective-C
tags:
- obj学习

---

> Implement a “backspace” button for the user to press if they hit the wrong digit button. This is not intended to be “undo,” so if they hit the wrong operation button, they are out of luck! It’s up to you to decided how to handle the case where they backspace away the entire number they are in the middle of entering, but having the display go completely blank is probably not very user-friendly.
	
	

	-(IBAction)clearPressed {
    
    self.display.text =[self.display.text substringToIndex:[self.display.text length] - 1];
    self.allDisplay.text =[self.allDisplay.text substringToIndex:[self.allDisplay.text length] - 1];
    
    if ([self.display.text isEqualToString:@""])  {
        self.display.text = @"0";
        self.userIsInMiddleOfEnteringANumber = NO;   
    }
    if ([self.allDisplay.text isEqualToString:@""]) {
        self.allDisplay.text = @"0";   
    }
    
重点：

- substringToIndex:(NSUInteger)anIndex 方法应用
- 及时将用户输入状态调零，解决输入默认0的问题
- allDisplay 需要在digitPressed:中增加恢复@“”的判断，不然输出也会出现默认0


> When the user hits an operation button, put an = on the end of the text label that is showing what was sent to the brain (required task #4). Thus the user will be able to tell whether the number in the Calculator’s display is the result of a calculation or a number that the user has just entered.

step1: 在 operationPressed: 方法中增加“=”

	self.allDisplay.text = [self.allDisplay.text stringByAppendingString:@"="];
	
step2：在 digitPressed: 方法中除去“=”

	if (self.userIsInMiddleOfEnteringANumber) {
        self.display.text = [self.display.text stringByAppendingString:digit];
        
    } else {
        self.display.text = digit;
        
        if ([self.allDisplay.text isEqual:@""]) {
        }else {self.allDisplay.text =[self.allDisplay.text substringToIndex:[self.allDisplay.text length] - 1];
        }

注意： 这里用了一个反判断，没有直接判断self.allDisplay.text 有值时就除去“=”。（但这里有一种情况没有考虑：点击两次运算符的时候）

	if ([self.allDisplay.text isEqual:@""]) {
        }else {self.allDisplay.text =[self.allDisplay.text substringToIndex:[self.allDisplay.text length] - 1];
        }
        
以下这种情况走不通

	if (self.allDisplay.text){
	    self.allDisplay.text =[self.allDisplay.text substringToIndex:[self.allDisplay.text length] - 1];
        }