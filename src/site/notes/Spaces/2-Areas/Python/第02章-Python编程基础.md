---
{"dg-publish":true,"dg-path":"Python/第02章-Python编程基础.md","permalink":"/Python/第02章-Python编程基础/"}
---

# 一、IPO编程方式
IPO（<font color="red">l</font>nput,<font color="red">P</font>rocess,<font color="red">O</font>utput）
![../../../Extras/Media/media-第02章-Python编程基础-1.png](/img/user/Extras/Media/media-%E7%AC%AC02%E7%AB%A0-Python%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80-1.png)
# 二、基本的输出函数print
语法结构：  
```python
print(输出内容)
```
`输出内容`外面可以是单引号、双引号、三个单引号、三个双引号

print()函数完整的语法格式：  
```python
print(value,...,sep=' ',end='\n',file=None)
```
-  解释：sep分隔符号（separator），end结束符，file输出到什么文件
## 1.使用连接符连接多个字符串
多个值之间，只能是字符串与字符串之间使用`+`连接，别的不行（如：字符串与整型数值之间就不行）
```python
print('北京欢迎你'+'2023') # 只能是字符串和字符串之间连接，别的不行  
#print('北京欢迎你'+2023) # TypeError: can only concatenate str (not "int") to str
```
## 2.使用print函数将内容输出到文件
```python
fp=open('note.txt','w') # 打开文件 w-->write
print('北京欢迎你',file=fp) # 将"北京欢迎你"输出(写入)到note.txt文件中  
fp.close() # 关闭文件
```
# 三、chr函数
语法结构：
```python
chr(x)
```
将整数x转换为一个字符
# 四、org函数
语法结构：
```python
org(x)
```
将一个字符x转换为其对应的整数值
# 五、基本的输入函数input
语法结构：  
```python
x=input('提示文字')
```
- 注意事项：无论输入的数据是什么，x的数据类型都是字符串类型
# 六、注释
1. 单行注释用`#`；
2. 多行注释使用三个单引号或者三个双引号包裹起来；
3. 中文声明注释应在第一行输入，如下
```python
# coding=utf-8
```
或者
```python
# coding=gbk
```
# 七、缩进
1. 缩进是指每行语句开始前的空白区域
2. 用来表示Python程序间的包含和层次关系
3. 类定义、函数定义、流程控制语句以及异常处理语句等行尾的<font color="purple">**冒号**</font>和<font color="purple">**下一行的缩进**</font>表示一个代码块的开始，而缩进结束，则表示一个代码块的结束
4. 通常情况下采用4个空格作为一个缩进量
***
# 参考文献
[1] 杨淑娟.花了2万多买的Python教程全套，现在分享给大家，入门到精通(Python全栈开发教程)\_哔哩哔哩\_bilibili\[EB/OL\].\[2025-09-14\].[花了2万多买的Python教程全套，现在分享给大家，入门到精通(Python全栈开发教程)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1wD4y1o7AS/)