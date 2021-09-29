# Chapter 4 ordered and unordered factors
[原书链接](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf)  
这一章原文讲的很少，然后我没看懂，所以我在百度上学习了这一章。。。找到一个[宝藏文档](https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/prog-type-fact.html)。
### 因子
因子分为有序因子和无序因子，有序因子指的是可以连续性量化的量度，其他的就是无序因子啦。
factor()函数可以将字符型向量转化为因子：
```r
> x<-c("BJ","SH","HK","SZ","HK","SZ","SH","SH","BJ","GZ")
> city<-factor(x)
> city
 [1] BJ SH HK SZ HK SZ SH SH BJ GZ
Levels: BJ GZ HK SH SZ
```
通过attributes()函数可以获得因子的non-intrinsic attributes：
```r
> attributes(city)
$levels
[1] "BJ" "GZ" "HK" "SH" "SZ"

$class
[1] "factor"
```
可以看出因子有两个属性:
* levels
    * 我所理解的levels是因子内变量的所有取值，通过levels()函数可以获取因子的该属性值。
* class
    * class自然就是factor

levels与整数值1,2,3,4,……一一对应，因子内部保存的实际就是整数值，而非上文输入的字符，这样可以节省存储空间。通过as.numeric()可以将因子转化为整数值：
```r
> as.numeric(city)
 [1] 1 4 3 5 3 5 4 4 1 2
```
通过as.character()可以将因子转化为字符型：
```r
> as.character(city)
 [1] "BJ" "SH" "HK" "SZ" "HK" "SZ" "SH" "SH" "BJ" "GZ"
```
### table()
table()函数可以统计因子各水平(levels)的出现次数，也可以统计向量内部各元素的出现次数。
```r
> x<-c("BJ","SH","HK","SZ","HK","SZ","SH","SH","BJ","GZ")
> city<-factor(x)
> table(city)
city
BJ GZ HK SH SZ
 2  1  2  3  2
```
### tapply()
tapply()函数的格式为：tapply(vector1,vector2,运算类型)，其中vector1和vector2最好要等长。看个例子：
```r
# 计算不同性别内部的最高身高

> height<-c(155,174,170,168,164,185,159)
> sex<-c("女","女","男","女","男","男","女")
> tapply(height,sex,max)
 男  女
185 174
```
