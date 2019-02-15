---
layout: post
title: 'UITextField 在英文输入法状态下的坑'
date: 2019-02-15
cover: '/assets/img/cocoa touch.jpg'
tags: 'UITextField offsetFromPosition selectedTextRange'
---

### 起因
在业务开发中有这样一个需求，一个列表每行文字可以编辑，并且文字可以换行或合并。
当时的实现是这样的，一个 tableView，每一个cell 中持有一个 textField，这个textField 根据光标的位置来决定换行及合并的规则。

### 经过
在输入源为中文(中文键盘下，一切工作正常)，但是切换到英文键盘时，奇怪的事情发生了。每次点选的光标位置，和换行时的分割点，不在同一个位置。
**分析**
这个换行时的分割点的获取时机，是在 - textFieldShouldEndEditing: 这个代理方法里处理的。所以猜测问题很有可能是在按下键盘的 return，到该代理方法被调用的时间里，CocoaTouch 内部针对英文输入源做了处理。也就是说，在这个代理被触发时，光标已经发生了移动。
**验证**
将如下的代码放入 - textFieldShouldEndEditing: 和测试用的按钮点击事件中。
``` objectivec
UITextRange* selectedRange = [self.textField selectedTextRange];
NSInteger cursorOffset = [self.textField offsetFromPosition:0 toPosition:selectedRange.start];
```
1.保持光标在同一位置，使用两种输入源，点击键盘的 return 观察代理方法

可以发现到，在输入源为英文时，代理方法中的 cursorOffset 并不是预期中的值，cursorOffset 发生了偏移（规则大致是光标在单词中间时，按下 return 光标会跳到单词的尾部，英文整个单词，整段字母，符号都有发生偏移）。

2.保持光标在同一位置，使用两种输入源，点击测试按钮，观察测试用点击事件

可以发现，两种输入源对与 cursorOffset 的结果都没有影响，与预期相符。

### 解决方案
这个偏移规则应该属于一个 function ，然而在排查了 UITextFieldDelegate，UITextInputDelegate，UITextInputTraits 之后，并没有发现有对应的属性或方法可以控制这个 function。所以有了下面两个解决方案。

1.使用 UITextView 来处理，这个换行就很简单了，只用查找换行符位置，并且进行了验证可以实现需求。

2.自定义键盘，因为系统提供的代理方法被触发时，实际上已经做了一些微小的工作。而我们需要更早的时机来获取光标位置，类似 textFieldWillReturn 这样的时机。

3.仍然使用 UITextField 来处理，在点击 return 之前，就存储下来 cursorOffset，并根据文字内容的变化以及点击保持更新。在代理方法中将保存好的值重新设置为我们预期的结果。

最终，基于业务和工作量的考量，我们采用了方案三来解决这个问题，在文字内容变化时，根据文字内容的加减来对应调整 cursorOffset，在点击 textField 不同区域时，计算光标位置并更新 cursorOffset。

遗憾的是我们仍然不知道 CocoaTouch 在这里做了什么工作 :)