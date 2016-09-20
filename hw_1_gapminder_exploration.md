# RMarkdown Gapminder exploration
Emma Graham  
September 19, 2016  

This is an R Markdown file that attempts to explore the Gapminder data.
First, let's install the package and inport it into R

Let's load the gapminder data and look at the first few rows and columns of the data

```r
library(gapminder)
head(gapminder)
```

```
##       country continent year lifeExp      pop gdpPercap
## 1 Afghanistan      Asia 1952  28.801  8425333  779.4453
## 2 Afghanistan      Asia 1957  30.332  9240934  820.8530
## 3 Afghanistan      Asia 1962  31.997 10267083  853.1007
## 4 Afghanistan      Asia 1967  34.020 11537966  836.1971
## 5 Afghanistan      Asia 1972  36.088 13079460  739.9811
## 6 Afghanistan      Asia 1977  38.438 14880372  786.1134
```

Let's make a histogram of the life expectancy of all people included in the dataset. 


```r
hist(gapminder$lifeExp)
```

![](hw_1_gapminder_exploration_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

Let's look at how many individuals are from each continent


```r
summary(gapminder$continent)
```

```
##   Africa Americas     Asia   Europe  Oceania 
##      624      300      396      360       24
```

Let's make a plot using ggplot2 that shows the relationship between country GDP and life expectancy. This was taken from Jenny Bryan's "care feeding data into R" html file on stat545.com


```r
library(ggplot2)
p <- ggplot(subset(gapminder, continent != "Oceania"),
            aes(x = gdpPercap, y = lifeExp))
p <- p + scale_x_log10() # log the x axis the right way
p + geom_point() # scatterplot
```

![](hw_1_gapminder_exploration_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
p + geom_point(aes(color = continent)) # map continent to color
```

![](hw_1_gapminder_exploration_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

```r
p + geom_point(alpha = (1/3), size = 3) + geom_smooth(lwd = 3, se = FALSE)
```

![](hw_1_gapminder_exploration_files/figure-html/unnamed-chunk-4-3.png)<!-- -->

```r
p + geom_point(alpha = (1/3), size = 3) + facet_wrap(~ continent) +
  geom_smooth(lwd = 1.5, se = FALSE)
```

![](hw_1_gapminder_exploration_files/figure-html/unnamed-chunk-4-4.png)<!-- -->
