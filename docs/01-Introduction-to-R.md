# Introduction to R

We will go over some of the basic R operations in this chapter.

If you have questions, you should check [Chris Bilder's website](http://www.chrisbilder.com/stat878/sections.html) for full information.

## Basic Operation


```r
2+2
```

```
## [1] 4
```


```r
2^3
```

```
## [1] 8
```


```r
# calculate the cdf of std. normal
pnorm(1.96) # 1.96 is the quantile
```

```
## [1] 0.9750021
```


```r
log(1)
```

```
## [1] 0
```


```r
sin(pi/2)
```

```
## [1] 1
```


```r
3/4
```

```
## [1] 0.75
```


```r
save <- 2+2
save
```

```
## [1] 4
```


```r
objects()
```

```
## [1] "save"
```


```r
ls()
```

```
## [1] "save"
```


```r
# quit operaiton
# q() 
```

## Vectors


```r
x <- c(1,2,3,4,5)
x
```

```
## [1] 1 2 3 4 5
```


```r
sd(x)
```

```
## [1] 1.581139
```


```r
mysd <- function(x){
  cat(" My data \n", x, "\n has std deviation",sqrt(var(x)))
}


mysd(x)
```

```
##  My data 
##  1 2 3 4 5 
##  has std deviation 1.581139
```


```r
pnorm(q=1.96, mean=1.96, sd=1)
```

```
## [1] 0.5
```

The full syntax for `pnorm()` is `pnorm(q, mean = 0, sd = 1, lower.tail = TRUE, log.p = FALSE)`


```r
pnorm(q=c(-1.96,1.96))
```

```
## [1] 0.0249979 0.9750021
```


```r
x <- c(3.68, -3.63, 0.80, 3.03, -9.86, -8.66, 
    -2.38, 8.94, 0.52, 1.25) 

y <- c(0.55, 1.65, 0.98, -0.07, -0.01, -0.31, 
    -0.34, -1.38, -1.32, 0.53)

x+y
```

```
##  [1]  4.23 -1.98  1.78  2.96 -9.87 -8.97 -2.72  7.56 -0.80  1.78
```

```r
x*y
```

```
##  [1]   2.0240  -5.9895   0.7840  -0.2121   0.0986   2.6846   0.8092 -12.3372
##  [9]  -0.6864   0.6625
```


```r
mean(x)
```

```
## [1] -0.631
```

```r
x-mean(x)
```

```
##  [1]  4.311 -2.999  1.431  3.661 -9.229 -8.029 -1.749  9.571  1.151  1.881
```

```r
x*2
```

```
##  [1]   7.36  -7.26   1.60   6.06 -19.72 -17.32  -4.76  17.88   1.04   2.50
```
The element(elt)-wise operation makes our life easier.

## Files

Click [gpa.csv](http://www.chrisbilder.com/stat878/sections/1/gpa.csv) to download the GPA csv file.

Click [gpa.txt](http://www.chrisbilder.com/stat878/sections/1/gpa.txt) to download the GPA txt file.


```r
getwd()
```

```
## [1] "/Users/weishangjie/Documents/GitHub/Time_Series_Analysis/Book/Time_Series_Analysis"
```



```r
gpatxt <- read.table("gpa.txt", header=TRUE, sep="")
gpacsv <- read.csv("gpa.csv")

#write.table(x = gpacsv, file = "gpa-out1.csv", quote = FALSE, row.names =
#  FALSE, sep  =",")
#write.csv(x = gpacsv, file = "gpa-out2.csv")
```


```r
gpacsv$HSGPA
```

```
##  [1] 3.04 2.35 2.70 2.55 2.83 4.32 3.39 2.32 2.69 2.83 2.39 3.65 2.85 3.83 2.22
## [16] 1.98 2.88 4.00 2.28 2.88
```


```r
gpacsv$CollegeGPA
```

```
##  [1] 3.10 2.30 3.00 2.45 2.50 3.70 3.40 2.60 2.80 3.60 2.00 2.90 3.30 3.20 2.80
## [16] 2.40 2.60 3.80 2.20 2.60
```


```r
gpacsv[1,1] # [row, col]
```

```
## [1] 3.04
```


```r
gpacsv[,1]
```

```
##  [1] 3.04 2.35 2.70 2.55 2.83 4.32 3.39 2.32 2.69 2.83 2.39 3.65 2.85 3.83 2.22
## [16] 1.98 2.88 4.00 2.28 2.88
```


```r
gpacsv[c(1,3,5),2]
```

```
## [1] 3.1 3.0 2.5
```


```r
gpacsv[,"HSGPA"]
```

```
##  [1] 3.04 2.35 2.70 2.55 2.83 4.32 3.39 2.32 2.69 2.83 2.39 3.65 2.85 3.83 2.22
## [16] 1.98 2.88 4.00 2.28 2.88
```


```r
summary(gpacsv)
```

```
##      HSGPA         CollegeGPA   
##  Min.   :1.980   Min.   :2.000  
##  1st Qu.:2.380   1st Qu.:2.487  
##  Median :2.830   Median :2.800  
##  Mean   :2.899   Mean   :2.862  
##  3rd Qu.:3.127   3rd Qu.:3.225  
##  Max.   :4.320   Max.   :3.800
```

```r
names(gpacsv)
```

```
## [1] "HSGPA"      "CollegeGPA"
```


```r
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA,
     xlab = "HS GPA", ylab = "College GPA", 
     main = "College GPA vs. HS GPA", 
     xlim = c(0,4.5), ylim = c(0,4.5), col = "red", 
    pch = 1, cex = 1.0, panel.first = grid(col = "gray", lty 
    = "dotted"))
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-27-1.pdf)<!-- --> 
The `plot()` function creates a two dimensional plot of data. 

Here are descriptions of its arguments:

- x specifies what is plotted for the x-axis.  

- y specifies what is plotted for the y-axis.  

- xlab and ylab specify the x-axis and y-axis labels, respectively.

- main  specifies the main title of the plot.

- xlim and ylim specify the x-axis and y-axis limits, respectively.
  - Notice the use of the c() function. 
  
- col specifies the color of the plotting points. 
  - Run the `colors()` function to see what possible colors can be     used. 
  - Also, you can see [Here](https://github.com/EarlGlynn/colorchart/wiki/Color-Chart-in-R) for the colors from colors(). 
  
- `pch` specifies the plotting characters.

- `cex`specifies the height of the plotting characters. 
   The value 1.0 is the default.
   
- `panel.first = grid()` specifies grid lines will be plotted.

- The line types can be specified as follows: 
`1=solid, 2=dashed, 3=dotted, 4=dotdash, 5=longdash, 6=twodash` or as one of the character strings `"blank", "solid", "dashed", "dotted",  "dotdash", "longdash"`, or `"twodash"`.  
  These line type specifications can be used in other functions.    
- The `par()`(parameter) function’s Help contains more information about the different plotting options!

## Regression

Our model is:$$CollegeGPA=\beta_0+\beta_1HSGPA+\epsilon$$


```r
mod.fit <- lm(formula= CollegeGPA~ HSGPA, data=gpacsv)
mod.fit
```

```
## 
## Call:
## lm(formula = CollegeGPA ~ HSGPA, data = gpacsv)
## 
## Coefficients:
## (Intercept)        HSGPA  
##      1.0869       0.6125
```


```r
names(mod.fit)
```

```
##  [1] "coefficients"  "residuals"     "effects"       "rank"         
##  [5] "fitted.values" "assign"        "qr"            "df.residual"  
##  [9] "xlevels"       "call"          "terms"         "model"
```



```r
mod.fit$coefficients
```

```
## (Intercept)       HSGPA 
##   1.0868795   0.6124941
```


```r
round(mod.fit$residuals[1:5],2)
```

```
##     1     2     3     4     5 
##  0.15 -0.23  0.26 -0.20 -0.32
```
   

```r
library(tidyverse)
```

```
## -- Attaching core tidyverse packages ------------------------ tidyverse 2.0.0 --
## v dplyr     1.1.1     v readr     2.1.4
## v forcats   1.0.0     v stringr   1.5.0
## v ggplot2   3.4.1     v tibble    3.2.1
## v lubridate 1.9.2     v tidyr     1.3.0
## v purrr     1.0.1     
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
## i Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
save.fit <- data.frame(gpacsv, C.GPA.hat = 
    round(mod.fit$fitted.values,2), residuals = 
    round(mod.fit$residuals,2))

save.fit %>% head()
```

```
##   HSGPA CollegeGPA C.GPA.hat residuals
## 1  3.04       3.10      2.95      0.15
## 2  2.35       2.30      2.53     -0.23
## 3  2.70       3.00      2.74      0.26
## 4  2.55       2.45      2.65     -0.20
## 5  2.83       2.50      2.82     -0.32
## 6  4.32       3.70      3.73     -0.03
```


```r
summary(mod.fit)
```

```
## 
## Call:
## lm(formula = CollegeGPA ~ HSGPA, data = gpacsv)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -0.55074 -0.25086  0.01633  0.24242  0.77976 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   1.0869     0.3666   2.965 0.008299 ** 
## HSGPA         0.6125     0.1237   4.953 0.000103 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.3437 on 18 degrees of freedom
## Multiple R-squared:  0.5768,	Adjusted R-squared:  0.5533 
## F-statistic: 24.54 on 1 and 18 DF,  p-value: 0.0001027
```

```r
class(mod.fit)
```

```
## [1] "lm"
```


Hence, our estimated regression model is$$ \hat{collge.GPA}=\hat{\beta_0}+\hat{\beta_1}HS.GPA
=1.0869+0.6125HS.GPA$$


```r
# Open a new graphics window 
# device new
dev.new(width = 8, height = 6, pointsize = 10)


# 1 row and 2 columns of plots
par(mfrow = c(1,2))
# par= graphic parameter
# mfrow= make a frame by row

# Same scatter plot as before
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS 
    GPA", ylab = "College GPA", main = "College GPA vs. 
    HS GPA", xlim = c(0,4.5), ylim = c(0,4.5), col = 
    "red", pch = 1, cex = 1.0, panel.first = grid(col = 
    "gray", lty = "dotted"))
    
# Puts the line y = a + bx on the plot
abline(a = mod.fit$coefficients[1], b = 
    mod.fit$coefficients[2], lty = "solid", col = 
    "blue", lwd = 2)
```


```r
# Same scatter plot as before
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS 
    GPA", ylab = "College GPA", main = "College GPA vs. 
    HS GPA", xlim = c(0,4.5), ylim = c(0,4.5), col = 
    "red", pch = 1, cex = 1.0, panel.first = grid(col = 
    "gray", lty = "dotted"))


# Add line
# expr= math expression
curve(expr = mod.fit$coefficients[1] + 
    mod.fit$coefficients[2]*x, 
    xlim = c(min(gpacsv$HSGPA),max(gpacsv$HSGPA)), 
    col= "blue", add = TRUE, lwd = 2)


# Draw a line from (x0, y0) to (x1, y1)
  segments(x0 = min(gpacsv$HSGPA), y0 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*min(gpacsv$HSGPA),
           x1 = max(gpacsv$HSGPA), y1 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*max(gpacsv$HSGPA),
           lty = 1, col = "blue", lwd = 2)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-35-1.pdf)<!-- --> 


- The `dev.new()` function can be used to open a new plotting window. 
- The `abline()` function can be used to draw straight lines on a plot. In the format used here, the line y = a + bx was drawn where a was the (intercept) and b was the (slope).  

- In the second plot, the curve() function was used to draw the line on the plot. This was done to have the line within the range of the high school GPA values.  

Let's use function to automate what we have done.


```r
my.reg.func <- function(x, y, data) {

    # Fit the simple linear regression model and save the results in mod.fit
    mod.fit <- lm(formula = y ~ x, data = data)

    #Open a new graphics window - do not need to
    dev.new(width = 6, height = 6, pointsize = 10)

    # Same scatter plot as before
    plot(x = x, y = y, xlab = "x", ylab = "y", main = "y vs. x", panel.first=grid(col = "gray", lty = 
      "dotted"))

    # Plot model
    curve(expr = mod.fit$coefficients[1] + 
      mod.fit$coefficients[2]*x, xlim = c(min(x),max(x)), 
      col = "blue", add = TRUE)
    
    segments(x0 = min(x), y0 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*min(x),
             x1 = max(x), y1 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*max(x),
             lty = 1, col = "blue", lwd = 2)

    # This is the object returned
    mod.fit
  }
```


```r
save.it <- my.reg.func(x = gpacsv$HSGPA, y = 
    gpacsv$CollegeGPA, data = gpacsv)
```
To get specific x-axis or y-axis tick marks on a plot, use the `axis()` function. For example, 

```r
#Note that xaxt = "n" tells R to not give any labels on the 
#  x-axis (yaxt = "n" works for y-axis)
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS GPA", 
     ylab = "College GPA", main = "College GPA vs. HS GPA", 
     xaxt = "n", xlim = c(0, 4.5), ylim = c(0, 4.5), col = 
     "red", pch = 1)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-38-1.pdf)<!-- --> 


```r
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS GPA", 
     ylab = "College GPA", main = "College GPA vs. HS GPA", 
     xaxt = "n", xlim = c(0, 4.5), ylim = c(0, 4.5), col = 
     "red", pch = 1)
     
#Major tick marks
axis(side = 1, at = seq(from = 0, to = 4.5, by = 0.5)) 
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-39-1.pdf)<!-- --> 


```r
plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS GPA", 
     ylab = "College GPA", main = "College GPA vs. HS GPA", 
     xaxt = "n", xlim = c(0, 4.5), ylim = c(0, 4.5), col = 
     "red", pch = 1)
     
#Major tick marks
axis(side = 1, at = seq(from = 0, to = 4.5, by = 0.5)) 

#Minor tick marks
axis(side = 1, at = seq(from = 0, to = 4.5, by = 0.1), tck 
      = 0.01, labels = FALSE) 
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-40-1.pdf)<!-- --> 


```r
 plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS GPA", ylab = "College GPA",
      main = expression(hat(Y) == hat(beta)[0] + hat(beta)[1]*x),
      xlim = c(0,4.5), ylim = c(0,4.5), col = "red", pch = 1, cex = 1.0, panel.first=grid(col = "gray", lty = "dotted"))

  #Draw a line from (x0, y0) to (x1, y1)
  segments(x0 = min(gpacsv$HSGPA), y0 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*min(gpacsv$HSGPA),
           x1 = max(gpacsv$HSGPA), y1 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*max(gpacsv$HSGPA),
           lty = 1, col = "blue", lwd = 2)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-41-1.pdf)<!-- --> 

```r
  plot(x = gpacsv$HSGPA, y = gpacsv$CollegeGPA, xlab = "HS GPA", ylab = "College GPA",
      main = expression(paste("College GPA vs. HS GPA and ", widehat(CollegeGPA) == hat(beta)[0] + hat(beta)[1]*HSGPA)),
      xlim = c(0,4.5), ylim = c(0,4.5), col = "red", pch = 1, cex = 1.0, panel.first=grid(col = "gray", lty = "dotted"))
  
  #Draw a line from (x0, y0) to (x1, y1)
  segments(x0 = min(gpacsv$HSGPA), y0 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*min(gpacsv$HSGPA),
           x1 = max(gpacsv$HSGPA), y1 = mod.fit$coefficients[1] + mod.fit$coefficients[2]*max(gpacsv$HSGPA),
           lty = 1, col = "blue", lwd = 2)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-41-2.pdf)<!-- --> 


```r
demo(plotmath) #Run this to see examples
```

```
## 
## 
## 	demo(plotmath)
## 	---- ~~~~~~~~
## 
## > #  Copyright (C) 2002-2016 The R Core Team
## > 
## > require(datasets)
## 
## > require(grDevices); require(graphics)
## 
## > ## --- "math annotation" in plots :
## > 
## > ######
## > # create tables of mathematical annotation functionality
## > ######
## > make.table <- function(nr, nc) {
## +     savepar <- par(mar=rep(0, 4), pty="s")
## +     plot(c(0, nc*2 + 1), c(0, -(nr + 1)),
## +          type="n", xlab="", ylab="", axes=FALSE)
## +     savepar
## + }
## 
## > get.r <- function(i, nr) {
## +     i %% nr + 1
## + }
## 
## > get.c <- function(i, nr) {
## +     i %/% nr + 1
## + }
## 
## > draw.title.cell <- function(title, i, nr) {
## +     r <- get.r(i, nr)
## +     c <- get.c(i, nr)
## +     text(2*c - .5, -r, title)
## +     rect((2*(c - 1) + .5), -(r - .5), (2*c + .5), -(r + .5))
## + }
## 
## > draw.plotmath.cell <- function(expr, i, nr, string = NULL) {
## +     r <- get.r(i, nr)
## +     c <- get.c(i, nr)
## +     if (is.null(string)) {
## +         string <- deparse(expr)
## +         string <- substr(string, 12, nchar(string) - 1)
## +     }
## +     text((2*(c - 1) + 1), -r, string, col="grey50")
## +     text((2*c), -r, expr, adj=c(.5,.5))
## +     rect((2*(c - 1) + .5), -(r - .5), (2*c + .5), -(r + .5), border="grey")
## + }
## 
## > nr <- 20
## 
## > nc <- 2
## 
## > oldpar <- make.table(nr, nc)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-42-1.pdf)<!-- --> 

```
## 
## > i <- 0
## 
## > draw.title.cell("Arithmetic Operators", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x + y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x - y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x * y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x / y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %+-% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %/% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %*% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %.% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(-x), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(+x), i, nr); i <- i + 1
## 
## > draw.title.cell("Sub/Superscripts", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x[i]), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x^2), i, nr); i <- i + 1
## 
## > draw.title.cell("Juxtaposition", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x * y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(paste(x, y, z)), i, nr); i <- i + 1
## 
## > draw.title.cell("Radicals", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(sqrt(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(sqrt(x, y)), i, nr); i <- i + 1
## 
## > draw.title.cell("Lists", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(list(x, y, z)), i, nr); i <- i + 1
## 
## > draw.title.cell("Relations", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x == y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x != y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x < y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x <= y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x > y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x >= y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %~~% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %=~% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %==% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %prop% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %~% y), i, nr); i <- i + 1
## 
## > draw.title.cell("Typeface", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(plain(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(italic(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(bold(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(bolditalic(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(underline(x)), i, nr); i <- i + 1
## 
## > # Need fewer, wider columns for ellipsis ...
## > nr <- 20
## 
## > nc <- 2
## 
## > make.table(nr, nc)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-42-2.pdf)<!-- --> 

```
## $mar
## [1] 0 0 0 0
## 
## $pty
## [1] "s"
## 
## 
## > i <- 0
## 
## > draw.title.cell("Ellipsis", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(list(x[1], ..., x[n])), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x[1] + ... + x[n]), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(list(x[1], cdots, x[n])), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x[1] + ldots + x[n]), i, nr); i <- i + 1
## 
## > draw.title.cell("Set Relations", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %subset% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %subseteq% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %supset% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %supseteq% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %notsubset% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %in% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %notin% y), i, nr); i <- i + 1
## 
## > draw.title.cell("Accents", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(hat(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(tilde(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(ring(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(bar(xy)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(widehat(xy)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(widetilde(xy)), i, nr); i <- i + 1
## 
## > draw.title.cell("Arrows", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %<->% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %->% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %<-% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %up% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %down% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %<=>% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %=>% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %<=% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %dblup% y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x %dbldown% y), i, nr); i <- i + 1
## 
## > draw.title.cell("Symbolic Names", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(Alpha - Omega), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(alpha - omega), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(phi1 + sigma1), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(Upsilon1), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(infinity), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(32 * degree), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(60 * minute), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(30 * second), i, nr); i <- i + 1
## 
## > # Need even fewer, wider columns for typeface and style ...
## > nr <- 20
## 
## > nc <- 1
## 
## > make.table(nr, nc)
```

```
## $mar
## [1] 0 0 0 0
## 
## $pty
## [1] "s"
## 
## 
## > i <- 0
## 
## > draw.title.cell("Style", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(displaystyle(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(textstyle(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(scriptstyle(x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(scriptscriptstyle(x)), i, nr); i <- i + 1
## 
## > draw.title.cell("Spacing", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x ~~ y), i, nr); i <- i + 1
## 
## > # Need fewer, taller rows for fractions ...
## > # cheat a bit to save pages
## > par(new = TRUE)
## 
## > nr <- 10
## 
## > nc <- 1
## 
## > make.table(nr, nc)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-42-3.pdf)<!-- --> 

```
## $mar
## [1] 0 0 0 0
## 
## $pty
## [1] "s"
## 
## 
## > i <- 4
## 
## > draw.plotmath.cell(expression(x + phantom(0) + y), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x + over(1, phantom(0))), i, nr); i <- i + 1
## 
## > draw.title.cell("Fractions", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(frac(x, y)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(over(x, y)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(atop(x, y)), i, nr); i <- i + 1
## 
## > # Need fewer, taller rows and fewer, wider columns for big operators ...
## > nr <- 10
## 
## > nc <- 1
## 
## > make.table(nr, nc)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-42-4.pdf)<!-- --> 

```
## $mar
## [1] 0 0 0 0
## 
## $pty
## [1] "s"
## 
## 
## > i <- 0
## 
## > draw.title.cell("Big Operators", i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(sum(x[i], i=1, n)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(prod(plain(P)(X == x), x)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(integral(f(x) * dx, a, b)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(union(A[i], i==1, n)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(intersect(A[i], i==1, n)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(lim(f(x), x %->% 0)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(min(g(x), x >= 0)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(inf(S)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(sup(S)), i, nr); i <- i + 1
## 
## > nr <- 12
## 
## > nc <- 1
## 
## > make.table(nr, nc)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-42-5.pdf)<!-- --> 

```
## $mar
## [1] 0 0 0 0
## 
## $pty
## [1] "s"
## 
## 
## > i <- 0
## 
## > draw.title.cell("Grouping", i, nr); i <- i + 1
## 
## > # Those involving '{ . }' have to be done "by hand"
## > draw.plotmath.cell(expression({}(x , y)), i, nr, string="{}(x, y)"); i <- i + 1
## 
## > draw.plotmath.cell(expression((x + y)*z), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x^y + z),   i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x^(y + z)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(x^{y + z}), i, nr, string="x^{y + z}"); i <- i + 1
## 
## > draw.plotmath.cell(expression(group("(", list(a, b), "]")), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(bgroup("(", atop(x, y), ")")), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(group(lceil, x, rceil)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(group(lfloor, x, rfloor)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(group(langle, list(x, y), rangle)), i, nr); i <- i + 1
## 
## > draw.plotmath.cell(expression(group("|", x, "|")), i, nr); i <- i + 1
## 
## > par(oldpar)
```

## Object-Oriented Language

Functions are typically designed to operate on only one or very few classes of objects. However, some functions, like `summary()`, are **generic**, in the sense that essentially different versions of them have been constructed to work with different classes of objects. 

When a generic function is run with an object, R first checks the object's class type and then looks to find a method function with the name format `<generic function>.<class name>`. Below are examples for `summary()`: 

- summary(mod.fit) – The function `summary.lm()` summarizes the regression model
- summary(gpacsv) – The function `summary.data.frame()` summarizes the data frame’s contents
- summary.default() – R attempts to run this function if there is no method function for a class

There are many generic functions! For example, `plot()` is a generic function (try` plot(mod.fit)` to see what happens!). We will also see other generic functions like `predict()` later in the notes.


```r
plot(mod.fit)
```

![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-43-1.pdf)<!-- --> ![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-43-2.pdf)<!-- --> ![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-43-3.pdf)<!-- --> ![](01-Introduction-to-R_files/figure-latex/unnamed-chunk-43-4.pdf)<!-- --> 

The purpose of generic functions is to use a familiar language set with any object. So it is convenient to use the same language set no matter the application. This is why R is referred to as an object-oriented language.

To see a list of all method functions associated with a class, use `methods(class = <class name>)`. For the regression example, the method functions associated with the `lm` class are:


```r
methods(class="lm") %>% head()
```

```
## [1] "add1.lm"                   "alias.lm"                 
## [3] "anova.lm"                  "case.names.lm"            
## [5] "coerce,oldClass,S3-method" "confint.lm"
```

To see a list of all method functions for a generic function, use `methods(generic.function = <generic function name>)`


```r
methods(generic.function = "summary") %>% head()
```

```
## [1] "summary.aov"                   "summary.aovlist"              
## [3] "summary.aspell"                "summary.check_packages_in_dir"
## [5] "summary.connection"            "summary.data.frame"
```

Knowing what a name of a particular method function can be helpful to find help on it. For example, the help for `summary()` alone is not very helpful! However, the help for `summary.lm() `provides a lot of useful information about what is summarized for a regression model.
