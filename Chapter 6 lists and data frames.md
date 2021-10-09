# Chapter 6 lists and data frames
[原书链接](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf)  
### lists
list里包含很多components，它们不需要是相同类型。  
list()：定义list
length(list name)：计算list的长度
```r
> l<-list('Re',3,c(3,54,33),'wq',TRUE)
> l
[[1]]
[1] "Re"

[[2]]
[1] 3

[[3]]
[1]  3 54 33

[[4]]
[1] "wq"

[[5]]
[1] TRUE

> length(l)
[1] 5

> l[[2]]
[1] 3
```
list里的元素可以命名：
```r
> a<-list(name='Mike',age=22,gender='male',height=177)
> a
$name
[1] "Mike"

$age
[1] 22

$gender
[1] "male"

$height
[1] 177

> a$age
[1] 22
> a[['gender']]
[1] "male"
```
有趣的是，通过listname$component_name来提取component时，component_name可以简写，只要这个简写足以和其他的name区别开来就好：
```r
> a$n
[1] "Mike"
```

### modifying lists
```r
> a<-list(name='Mike',age=22,gender='male',height=177)
> a[[5]]<-9
> a
$name
[1] "Mike"

$age
[1] 22

$gender
[1] "male"

$height
[1] 177

[[5]]
[1] 9
```

### data frames
A data frame is a list with class"data.frames".
#### makeing data frames
data.frame()
```r
> a<-data.frame(name=c('Mike','Mary','Jack'),gender=c('M','F','M'),height=c(177,164,182))
> a
    name gender height
1   Mike      M    177
2   Mary      F    164
3   Jack      M    182
```
同一列的数据类型相同，每列的长度一致。  
nrow()可以得到数据框的行数，ncol()或者length()可以得到数据框的列数，每一列是一个变量。
#### attach() and detach()
attach()函数帮助更方便地调用数据框里的元素,该函数将数据框添加到R的搜索路径中。
```r
> a<-data.frame(name=c('Mike','Mary','Jack'),gender=c('M','F','M'),height=c(177,164,182))
> a
  name gender height
1 Mike      M    177
2 Mary      F    164
3 Jack      M    182
> a$gender
[1] "M" "F" "M"
> a$gender[2]
[1] "F"
> attach(a)
> gender[2]
[1] "F"
> name[3]
[1] "Jack"
> detach(a)
> name[3]
错误: 找不到对象'name'
```
