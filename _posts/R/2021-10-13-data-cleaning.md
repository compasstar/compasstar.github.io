---
layout: post
title:  "[R] 6. data cleaning"
subtitle:   "data cleaning"
categories: R
tags: R
comments: true
date: 2021-10-13 00:15:28
---


# 1. 결측값 관리

***

```
x <- c(1,2,3,4, NA, 6,7, NA, 9)
is.na(x) # 데이터에 na가 있는지 확인
sum(is.na(x)) # data에 na가 몇개인가?  --> 2
sum(x, na.rm = T) # na를 제외하고 합해줘 remove=T
mean(x, na.rm = T) # na를 제외하고 평균
```

### 결측값[NA] :  값이 없는 빈 부분  <br><br>

`is.na(x)` 출력
> FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE

`sum(x, na.rm = T)` 출력
> 32

`mean(x, na.rm = T)` 출력
>4.571429

<br>

```
y <- c(1,2,3,4, NA, 6, NA)
y1 <- as.vector(na.omit(y))
y[is.na(y)] <- 0 
```

`as.vector(na.omit(y))` 
>NA를 제거하고 새 집합을 만듭니다

`y[is.na(y)] <- 0`
> y에 있는 결측값들을 0으로 교체합니다

`y1`
> 1 2 3 4 6

`y`
> 1 2 3 4 0 6 0

<br>

```
women[1,2] <- NA
women[10,1] <- NA
women[13,2] <- NA
colSums(is.na(women)) # women데이터 각 열에 결측값 개수
rowSums(is.na(women)) # 각 행의 결측값 개수
sum(is.na(women)) # 모든 결측값 개수
```

`colSums(is.na(women))`
> 1 2

`rowSums(is.na(women))`
> 1 0 0 0 0 0 0 0 0 1 0 0 1 0 0

`sum(is.na(women))`
> 3




# 2. 이상치[outlier] 제거 

***


```
boxplot(iris$Sepal.Width)
out.value <- boxplot.stats(iris$Sepal.Width)$out # 아웃라이어 값
out.value
```

![outlier](https://user-images.githubusercontent.com/55419868/137080981-3fdf7e2f-b703-4e46-93ae-a39e66c465ea.png)

그래프 상에 이상치가 4개 있는 것을 확인할 수 있습니다. <br>

`out.value` 
> 4.4 4.1 4.2 2.0

<br>

```
iris$Sepal.Width[iris$Sepal.Width %in% out.value] <- NA

iris.new <- iris[complete.cases(iris), ]

boxplot(iris.new$Sepal.Width)
```

`iris$Sepal.Width[iris$Sepal.Width %in% out.value] <- NA`
> `Sepal.Width` 안에 있는 `out.value` 값을 `NA` 로 바꾸어 줍니다.

`iris[complete.cases(iris), ]`
> `iris` 에서 결측값이 포함된 행을 제거합니다

<br>

![outlier remove](https://user-images.githubusercontent.com/55419868/137082133-9a5aee9b-e639-4386-a358-65845ce5a62c.png)

이상치가 사라진 것을 확인할 수 있습니다



# 3. 데이터 분리하기 합하기

```
x1 <- split(iris, iris$Species) # Species에 따라 데이터분리
x1 # setosa versicolor virginica 로 분리됨

# 조건에 따라 부분적으로 출력
subset(iris, Species == "versicolor") # versicolor 만 출력
subset(iris, Petal.Width > 2.0)
subset(iris, Petal.Width > 2.0 & Petal.Length > 5.5)
```

```
# 데이터 합하기
a <- data.frame(id=c(1,2,3), math1=c(80,70,95))
b <- data.frame(id=c(1,2,3), math2=c(55,40,20))

merge(a,b,by='id') #id 기준으로 a b 병합
```


