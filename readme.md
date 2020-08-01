
# 语言设置

Sys.getlocale()

Sys.setenv(LANG = "en")


导入包
library(dplyr)


# 导入csv文件

文件名记得加引号 （单引号双引号都可以）

vehicles2 <- read.csv('Downloads/vehicles.csv',header = TRUE)

vehicles <- read.csv("Downloads/vehicles.csv",header = TRUE)
