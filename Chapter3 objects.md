# Chapter 3 Objects
[原书链接](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf)
### intrinsic attributes: mode and length
R所操作的对象包括：
* vectors
    * vector内的value必须属于同样的mode（原子结构），即logical、complex、numeric、character、raw。
* lists
    * lists的mode即为list，lists内部的对象可以属于任何mode。lists属于递归结构而非原子结构。
* function
* expression

任何对象包含以下property(其中mode和length被称为intrinsic attributes)：
* mode
    * logical
    * complex
    * numeric
    * character
    * raw
    * list
    * ……
* length
* attributes
* class

```
> a<-c(4,3)
> mode(a)
[1] "numeric"
> length(a)
[1] 2
```
as.*mode*()可以转换对象mode：
```
> a<-c(3,5)
> mode(a)
[1] "numeric"
> b<-as.complex(a)
> b
[1] 3+0i 5+0i
> mode(b)
[1] "complex"
> c<-as.numeric(b)
> c
[1] 3 5
> mode(c)
[1] "numeric"
```
## changing the length of an object
增加长度：
```
> e<-numeric()
> e
numeric(0)
> e[2]<-3
> e
[1] NA  3
```
缩短长度
```
> a<-c('e','t','f','d','s','b','c','a','j','v')
> length(a)<-4
> a
[1] "e" "t" "f" "d"
```
还有一个有趣的缩短长度的方法，比如字符向量a的长度为6，通过改变索引内的数字可以提取出不同长度的字符向量。如果索引数字为[2*1:3]，即提取2、4、6位置上的字符。
```
> a<-c('e','f','h','x','j','q')
> a
[1] "e" "f" "h" "x" "j" "q"
> a<-a[2*1:3]
> a
[1] "f" "x" "q"
```
如果将索引更改为[3*1:2]，即提取3和6位置上的字符。
```
> a<-c('e','f','h','x','j','q')
> a<-a[3*1:2]
> a
[1] "h" "q"
```
## getting and setting attributes
这里的attributes指的是non-intrinsic attributes，因此：
**getting attributes:**
```
> a<-4
> attributes(a)
NULL
```
**setting attributes:**  
attr(*object*,*name*)
## the class of an object
每个对象都有自己的*class*，对于简单的向量来说就相当于*mode*，但是也有其他的*class*，比如*data.frame*、*factor*……

通过class()可以获取对象的class，通过unclass()可以暂时移除对象的class，详细内容等读到了对应章节再写^.^
