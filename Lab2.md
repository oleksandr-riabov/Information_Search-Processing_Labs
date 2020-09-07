**#sum**
``` r
list1 <- list(observationA = c(1:5, 7:3), observationB = matrix(1:6, nrow=2))
lapply(list1, sum)
```
```
$observationA
[1] 40

$observationB
[1] 21
```

**#max/min**
``` r
lapply(list1, range)
sapply(list1, range)
```
```
> lapply(list1, range)
$observationA
[1] 1 7

$observationB
[1] 1 6

> sapply(list1, range)
     observationA observationB
[1,]            1            1
[2,]            7            6
```
