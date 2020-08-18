
# 语言设置

Sys.getlocale()

Sys.setenv(LANG = "en")


导入包
library(dplyr)


# 导入csv文件

文件名记得加引号 （单引号双引号都可以）

vehicles2 <- read.csv('Downloads/vehicles.csv',header = TRUE)

vehicles <- read.csv("Downloads/vehicles.csv",header = TRUE)


3.数据基本信息
为了检查数据是否已经载入，我们可以在R中展现头几行，使用如下代码：
head(vehicles)
行、列数
查看数据有多少行
nrow(vehicles)
查看有多少个变量（列）
ncol(vehicles)
查看各列的含义，用name()函数
names(vehicles)

x中元素的个数
length(x)

查看变量的维数；或者 重新设置的维数，例如dim(x)=c(3,2)
 dim(x)

summary函数
summary(mtcars)
# Sepal.Length    Sepal.Width     Petal.Length    Petal.Width          Species  
# Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100   setosa    :50  
# 1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300   versicolor:50  
# Median :5.800   Median :3.000   Median :4.350   Median :1.300   virginica :50  
# Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199                  
# 3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800                  
# Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500     

可以看出NA值

最大、最小值(某一列）
min(mtcars[,1])
#[1] 4.3
max(mtcars[,1])
#[1] 7.9

均值、中位数、分位数
度量数据的集中程度
# 均值：mean() 
# 中位数： median()
# 分位数： quantile()

极值、方差、标准差
度量数据集的分散程度
#极值、方差和标准差
#range()、var()、sd()

summarise函数 --dplyr
library(dplyr)

#返回数据框中变量Sepal.Length的均值
summarise(mtcars, mean(Sepal.Length))
#返回数据框中变量Sepal.Length的标准差
summarise(mtcars, sd(Sepal.Length))
#返回数据框中变量Sepal.Length的最大值及最小值
summarise(mtcars, max(Sepal.Length), min(Sepal.Length))
#返回数据框mtcars的行数
summarise(mtcars, n())
#返回unique的Petal.Length数
summarise(mtcars, n_distinct(Petal.Length))
#返回Sepal.Length的第一个值
summarise(mtcars, first(Sepal.Length))
#返回Sepal.Length的最后个值
summarise(mtcars, last(Sepal.Length))

class()/mode()函数 
查看数据类型

table函数 
--分组看频率
table(vehicles$fuelType1)

缺失值处理

缺失值有
某一列中大量缺失值，则可以删去该列
某一行大量缺失，则删除该行
某一列中少量缺失，可酌情填充模拟值


select函数--dplyr
clean1 <- select(vehicles, -contains("eng_dscr"))
nrow(clean1)#还是42445
nrow(vehicles)#42445
ncol(vehicles)#83
ncol(clean1)#减少一个 变成82

clean2 <- select(vehicles, -contains("trans_dscr"))
clean3 <- select(vehicles, -contains("tCharger"))


complete.cases函数
#按行查有没有缺失 没有缺失返回TRUE
complete.cases(vehicles)
complete.cases(clean3)

#这个函数也可以作用在向量上
b <- c(1,2,NA)
complete.cases(b)
#结果是TRUE，TRUE，FALSE

b[complete.cases(b)]
#[1] 1 2

c1 <- c(NA,2,3)
complete.cases(c1,b)
#F,T,T + T,T,F = F,T,F

vehicles.complete <- vehicles[complete.cases(vehicles),]
#注意有逗号
nrow(vehicles.complete)
#得7563行，比原有42445行少太多，因为有些应该删列

vehicles.complete3 <- vehicles[complete.cases(clean3),]
nrow(vehicles.complete3)
#得42202行，比原有42445少200行，可以接受

na.omit函数
vehicles.omit <- na.omit(vehicles)
nrow(vehicles.omit)
#结果是7563

nrow(na.omit(clean3))
#结果是42202

clean.final <- select(vehicles, -c("eng_dscr","trans_dscr","tCharger"))
nrow(na.omit(clean.final))#结果也是42202
