---
layout: article
title: "iOS Development Tips"
categories: iOS
excerpt: "DevelopTips"
ads: true
share: false
image:
---

#### 数组拼接字符串

```
NSArray *arr = [NSArray arrayWithObjects:@"I", @"love", @"you", nil];
NSLog(@"%@",[arr componentsJoinedByString:@""]);//打印Iloveyou
NSLog(@"%@",[arr componentsJoinedByString:@" "]);//打印I love you
```
`- (NSArray<NSString *> *)componentsSeparatedByCharactersInSet:(NSCharacterSet *)separator`方法的而作用是通过set来进行分割字符串，返回分割后的数组。

```
NSCharacterSet *set = [NSCharacterSet characterSetWithCharactersInString:@"0123456"];
NSString *nam = @"1g2h45j3d688";
NSLog(@"%@",[nam componentsSeparatedByCharactersInSet:set]);
```

#### 输入框只能输入字母和数字

```
- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string {
    NSCharacterSet *charSet = [[NSCharacterSet characterSetWithCharactersInString:@"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"] invertedSet];
    NSString *filteredStr = [[string componentsSeparatedByCharactersInSet:charSet] componentsJoinedByString:@""];
    if ([string isEqualToString:filteredStr]) {
        return YES;
    }
    return NO;
}
```

#### 限制输入框输入长度

```
#define MAXLENGTH 10

- (BOOL)textField:(UITextField *) textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string {

    NSUInteger oldLength = [textField.text length];
    NSUInteger replacementLength = [string length];
    NSUInteger rangeLength = range.length;

    NSUInteger newLength = oldLength - rangeLength + replacementLength;

    BOOL returnKey = [string rangeOfString: @"\n"].location != NSNotFound;

    return newLength <= MAXLENGTH || returnKey;
}

// 对于能输入中文的输入框 还要增加方法
- (void)textFieldDidChange:(UITextField *)textField
{
    if (textField == self.titleField) {
        if (textField.text.length > MAXLENGTH) {
            textField.text = [textField.text substringToIndex:MAXLENGTH];
        }
    }
}
```

#### 金额输入框 只能输入一个小数点，小数点后只能输入两位

```
- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string{
    //控制输入框输入长度
    NSInteger maxLength = 11;
    NSUInteger oldLength = [textField.text length];
    NSUInteger replacementLength = [string length];
    NSUInteger rangeLength = range.length;
    NSUInteger newLength = oldLength - rangeLength + replacementLength;
    BOOL returnKey = [string rangeOfString: @"\n"].location != NSNotFound;
    if (range.location==0 && [string isEqualToString:@"."])
    {
        return NO;
    }
    if ([string isEqualToString:@""]) {
        return YES;
    }
    NSString *checkStr = [textField.text stringByReplacingCharactersInRange:range withString:string];
    //正则表达式 数字或小数点后两位
    NSString *regex = @"^\\-?([1-9]\\d*|0)(\\.\\d{0,2})?$";
    return (newLength <= maxLength || returnKey) && [self isValid:checkStr withRegex:regex];
}

//检测改变过的文本是否匹配正则表达式，如果匹配表示可以键入，否则不能键入
- (BOOL) isValid:(NSString*)checkStr withRegex:(NSString*)regex{
    NSPredicate *predicte = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex];
    return [predicte evaluateWithObject:checkStr];
}
```

#### 沙盒机制

沙盒根目录结构：Documents、Library、temp。

1. Documents：用于存储用户数据，iTunes备份和恢复的时候会包括此目录，所以，苹果建议将程序中建立的或在程序中浏览到的文件数据保存在该目录下。

2. Library：包含两个子目录：Caches和Preferences。Caches用来存放用户需要换成的文件。Preferences是APP的偏好设置，可以通过NSUserDefaults来读取和设置。

3. tmp：用于存放临时文件，这个可以放一些当APP退出后不再需要的文件。

#### 获取键盘高度

```
[[NSNotificationCenter defaultCenter] addObserver:self
                                     selector:@selector(keyboardWasShown:)
                                         name:UIKeyboardDidShowNotification
                                       object:nil];

- (void)keyboardWasShown:(NSNotification *)notification
{

// Get the size of the keyboard.
CGSize keyboardSize = [[[notification userInfo] objectForKey:UIKeyboardFrameBeginUserInfoKey] CGRectValue].size;

//Given size may not account for screen rotation
int height = MIN(keyboardSize.height,keyboardSize.width);
int width = MAX(keyboardSize.height,keyboardSize.width);

//your other code here..........
}
```

#### UILabel lineBreakMode

```
lineBreakMode：设置标签文字过长时的显示方式。   
label.lineBreakMode = NSLineBreakByCharWrapping;    //以字符为显示单位显示，后面部分省略不显示。   
label.lineBreakMode = NSLineBreakByClipping;        //剪切与文本宽度相同的内容长度，后半部分被删除。   
label.lineBreakMode = NSLineBreakByTruncatingHead;  //前面部分文字以……方式省略，显示尾部文字内容。   
label.lineBreakMode = NSLineBreakByTruncatingMiddle;    //中间的内容以……方式省略，显示头尾的文字内容。   
label.lineBreakMode = NSLineBreakByTruncatingTail;  //结尾部分的内容以……方式省略，显示头的文字内容。   
label.lineBreakMode = NSLineBreakByWordWrapping;    //以单词为显示单位显示，后面部分省略不显示。
```

#### UIBarButtonItem 左右距离

```
//左右边距调整增加空的按钮即可
UIBarButtonItem *rightBtn = [[UIBarButtonItem alloc] init];
UIButton *rgbtn = [[UIButton alloc] initWithFrame:CGRectMake(80, 10, 80, 13)];
[rgbtn setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
[rgbtn setTitle:btnTitle forState:UIControlStateNormal];
rgbtn.titleLabel.font = [UIFont systemFontOfSize:BTN_FONT];
[rgbtn addTarget:self action:@selector(switchTrafic) forControlEvents:UIControlEventTouchUpInside];
rightBtn.customView = rgbtn;
UIBarButtonItem *negativeSpacer = [[UIBarButtonItem alloc]
                                       initWithBarButtonSystemItem:UIBarButtonSystemItemFixedSpace
                                       target:nil action:nil];
negativeSpacer.width = -18;
self.navigationItem.rightBarButtonItems = [NSArray arrayWithObjects:negativeSpacer,rightBtn, nil];
[negativeSpacer release];
[rightBtn release];
[rgbtn release];
```

#### UISearchBar的背景设置为透明

```
[self.mySearchBar setBackgroundColor:[UIColor clearColor]];
[self.mySearchBar setBackgroundImage:[UIImage new]];
[self.mySearchBar setTranslucent:YES];
```

#### 根据颜色生成图片

```
- (UIImage *) createImageWithColor: (UIColor *) color{
    CGRect rect=CGRectMake(0.0f, 0.0f, 1.0f, 1.0f);
    UIGraphicsBeginImageContext(rect.size);
    CGContextRef context = UIGraphicsGetCurrentContext();
    CGContextSetFillColorWithColor(context, [color CGColor]);
    CGContextFillRect(context, rect);

    UIImage *theImage = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    return theImage;
}
```

#### dyld: Library not loaded: @rpath/XCTest.framework/XCTest

解决办法：工程－>targets－>Bulid Phases－>complie Sources 搜索一下是否有test，有的话，删除一下即可。

#### 版本更新跳转到AppStore显示“打开”而不是“更新”的问题

>原因：AppStore有缓存，导致即使不是最新版app也显示”打开“，不显示”更新“
>
>解决方法：杀死AppStore，重新打开即可

#### 把定时器加到runloop

```
[[NSRunLoop currentRunLoop] addTimer:timer forMode:NSRunLoopCommonModes];
```

#### 定时器更新按钮title闪烁的问题

把按钮设置成custom，不要用system，然后用下面的方法

```
[UIView setAnimationsEnabled:NO];
[self.btnGetCode setTitle:[NSString stringWithFormat:@"%ds",second] forState:UIControlStateNormal];
[UIView setAnimationsEnabled:YES];
```