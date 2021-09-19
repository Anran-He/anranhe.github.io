# Chapter 2
[原书链接](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf)
### vectors and assignment
在学习R之前，我只接触过C和Python两种语言，因此会觉得R的赋值
（assignment）很特殊。R有四种赋值方式：  
```r
# assignment statements

> x<-4
> 4->x
> assign("x",4)
> x=4
```
"<-"和“=”在大部分情况下作用相同，但也有一些情景中
它们俩不能替换。具体的区别书里还没讲，打算多学一点
后再去研究^o^

在R语言里，*vector*是最简单的数据结构。新建一个*vector*的代码如下：
```r
# set up a vector named x

> x<-c(2,5,3)
> x
[1] 2 5 3
```
这里的c函数c()可以把括号里的多个对象连接在一起，
组成向量*vector*。

*vector*还可以继续进行赋值和运算，比如：  

```r
# assignment

> x<-c(2,5,3)
> y<-c(1,x,2)
> y
[1] 1 2 5 3 2

# addition

> z<-x+1
> z
[1] 3 6 4

#mulplication

> t<-2*x
> t
[1]  4 10  6
```
接下来是关于两个向量之间的运算，这就比较有意思了。
如果两个向量的长度相等，它们之间的运算就很好理解，
对应位置上的数字进项运算即可。比如：
