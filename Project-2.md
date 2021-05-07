Project 2: Airquality seasonality
================
Hye Jeong Lee
4/13/2021

### 1. Introduction

``` r
# dataset
aq<- airquality

# dimension of dataset
dim(aq)
```

    ## [1] 153   6

``` r
# change numerical month to categorical month
aq$month <- month.abb[aq$Month]
aq <- aq %>%
  select(-Month) %>%
  rename ("Month" = month) %>%
  mutate(Temp=(aq$Temp -32)*(5/9))
```

The data set ‘air quality’ is one of built-in R studio which contains
153 observations and 5 variables. Month is the only categorical variable
and the rests are numeric variables.

The purpose of this analysis is to test if there is a significant
difference in means of ozone concentration between months, and to build
a linear regression model to predict ozone based on variables as well as
to build a logistic regression model that predict if the ozone
concentration is permissible based on other variables.

I expect to find that there is a significant difference in mean of ozone
concentration between months, and there is a significant effect of solar
radiation and month on ozone concentration. In addition, I expect to
find that there is a significant effect of solar radiation, month,
temperature on predicting if the ozone concentration is permissible (
&lt; 100 ppb).

I chose this dataset because everyone on earth is affected by the
outside air quality and air quality related diseases are increasing with
time. Finding any pattern or seasonality in the air quality would be
important for improving air quality.

**Variables**

1.  ozone: mean ozone in parts per billion from 1300 to 1500 hours at
    Roosevelt Island (ppb)

2.  Solar.R: solar radiation in Langleys in frequency band 4000 - 7700
    Angstroms from 0800 to 1200 hours at central park (lang)

3.  wind: average wind speed in miles per hour at 0700 and 1000 hours at
    LaGuardia Airport (mph)

4.  temp: maximum daily temperature in degrees Farenheit at La Guardia
    Airport (Farenheit)

5.  month: abbreviated character Month

6.  day: numeric day of month (1-31)

### 2. EDA

``` r
# correlation heatmap to visualize overall correlation to pick variables
cor(airquality, use = "pairwise.complete.obs") %>%
  # Save as a data frame
  as.data.frame %>%
  # Convert row names to an explicit variable
  rownames_to_column %>%
  # Pivot so that all correlations appear in the same column
  pivot_longer(-1, names_to = "other_var", values_to = "correlation") %>%
  ggplot(aes(rowname, other_var, fill=correlation)) +
  # Heatmap with geom_tile
  geom_tile() +
    theme(axis.text.x=element_text(angle=90,hjust=1))+
  # Change the scale to make the middle appear neutral
  scale_fill_gradient2(low="red",mid="white",high="blue") +
  # Overlay values
  geom_text(aes(label = round(correlation,2)), color = "black", size = 5) +
  # Give title and labels
  labs(title = "Correlation matrix for the dataset airquality", x = "variable 1", y = "variable 2")
```

![](Project-2_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
# summary of each variables  into a table
aq_sd <- airquality %>%
  summarize_all(sd,na.rm=T)%>%
  pivot_longer(cols=c(Ozone:Day), names_to="Variables", values_to="sd")
aq_sd <-data.frame(aq_sd)
## remove white space
library(stringr)
remove_all_ws<- function(string){
    return(gsub(" ", "", str_squish(string)))
}
## summary 
summary_tbl <-data.frame(summary(airquality))
summary_tbl <- summary_tbl %>%
  select(-Var1) %>%
  rename("Variables" = Var2)%>%
  mutate_if(is.character, remove_all_ws)%>%
  separate(Freq, into=c("indicator","stats"), sep=":") %>%
  pivot_wider(names_from = indicator, values_from = stats)%>%
  select(-"NA")%>%
  mutate_at("NA's",replace_na, 0)
## combine
stat_summary <- merge(summary_tbl, aq_sd, by="Variables")
library(kableExtra)
```

    ## Warning: package 'kableExtra' was built under R version 4.0.4

    ## 
    ## Attaching package: 'kableExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     group_rows

``` r
## pretty table
stat_summary %>%
  kbl() %>%
  kable_styling()
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Variables
</th>
<th style="text-align:left;">
Min.
</th>
<th style="text-align:left;">
1stQu.
</th>
<th style="text-align:left;">
Median
</th>
<th style="text-align:left;">
Mean
</th>
<th style="text-align:left;">
3rdQu.
</th>
<th style="text-align:left;">
Max.
</th>
<th style="text-align:left;">
NA’s
</th>
<th style="text-align:right;">
sd
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Day
</td>
<td style="text-align:left;">
1.0
</td>
<td style="text-align:left;">
8.0
</td>
<td style="text-align:left;">
16.0
</td>
<td style="text-align:left;">
15.8
</td>
<td style="text-align:left;">
23.0
</td>
<td style="text-align:left;">
31.0
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
8.864520
</td>
</tr>
<tr>
<td style="text-align:left;">
Month
</td>
<td style="text-align:left;">
5.000
</td>
<td style="text-align:left;">
6.000
</td>
<td style="text-align:left;">
7.000
</td>
<td style="text-align:left;">
6.993
</td>
<td style="text-align:left;">
8.000
</td>
<td style="text-align:left;">
9.000
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.416522
</td>
</tr>
<tr>
<td style="text-align:left;">
Ozone
</td>
<td style="text-align:left;">
1.00
</td>
<td style="text-align:left;">
18.00
</td>
<td style="text-align:left;">
31.50
</td>
<td style="text-align:left;">
42.13
</td>
<td style="text-align:left;">
63.25
</td>
<td style="text-align:left;">
168.00
</td>
<td style="text-align:left;">
37
</td>
<td style="text-align:right;">
32.987884
</td>
</tr>
<tr>
<td style="text-align:left;">
Solar.R
</td>
<td style="text-align:left;">
7.0
</td>
<td style="text-align:left;">
115.8
</td>
<td style="text-align:left;">
205.0
</td>
<td style="text-align:left;">
185.9
</td>
<td style="text-align:left;">
258.8
</td>
<td style="text-align:left;">
334.0
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:right;">
90.058422
</td>
</tr>
<tr>
<td style="text-align:left;">
Temp
</td>
<td style="text-align:left;">
56.00
</td>
<td style="text-align:left;">
72.00
</td>
<td style="text-align:left;">
79.00
</td>
<td style="text-align:left;">
77.88
</td>
<td style="text-align:left;">
85.00
</td>
<td style="text-align:left;">
97.00
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
9.465270
</td>
</tr>
<tr>
<td style="text-align:left;">
Wind
</td>
<td style="text-align:left;">
1.700
</td>
<td style="text-align:left;">
7.400
</td>
<td style="text-align:left;">
9.700
</td>
<td style="text-align:left;">
9.958
</td>
<td style="text-align:left;">
11.500
</td>
<td style="text-align:left;">
20.700
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
3.523001
</td>
</tr>
</tbody>
</table>

``` r
# relationship graph for MANOVA
library(psych)
```

    ## 
    ## Attaching package: 'psych'

    ## The following objects are masked from 'package:ggplot2':
    ## 
    ##     %+%, alpha

``` r
pairs.panels(airquality, 
             method = "pearson", # correlation coefficient method
             hist.col = "blue", # color of histogram 
             smooth = FALSE, density = FALSE, ellipses = FALSE)
```

![](Project-2_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->

``` r
m <- c("May","June","July","August","September")


# specific univariate and bivariate graphs
aq1 <- aq %>% mutate(Month = factor(Month, 
                    levels = c("May", "Jun", "Jul", "Aug", "Sep"),
                    ordered = TRUE))
## ozone by month
ggplot(aq1, aes(x=Month,y=Ozone, fill=Month))+
  geom_boxplot()+
  labs(title="Ozone concentration by Month", y="Ozone (ppb)")
```

    ## Warning: Removed 37 rows containing non-finite values (stat_boxplot).

![](Project-2_files/figure-gfm/unnamed-chunk-2-3.png)<!-- -->

``` r
## relationship between ozone and solar radiation
ggplot(aq, aes(x=Ozone, y=Solar.R))+
  geom_point()+
  geom_smooth(method=lm,se=F)+
  labs(title="Ozone vs. Solar Radiation", x="Ozone concentration (ppb)", y="Solar Radiation (langley)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 42 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 42 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-2-4.png)<!-- -->

``` r
## relationship between ozone and temperature
ggplot(aq, aes(x=Ozone, y=Temp))+
  geom_point()+
  geom_smooth(method=lm,se=F)+
  labs(title="Ozone vs. Temperature", x= "Ozone concentration (ppb)", y="Temperature (Celsius)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-2-5.png)<!-- -->

``` r
## relationship between ozone and Wind speed
ggplot(aq, aes(x=Ozone, y=Wind))+
  geom_point()+
  geom_smooth(method=lm,se=F)+
  labs(title="Ozone vs. Wind Speed", x= "Ozone concentration (ppb)", y="Wind Speed (mph)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-2-6.png)<!-- -->

The correlation heatmap shows that there is a strong positive
relationship between temperature and ozone concentration. There is a
strong negative correlation between wind speed and ozone concentration.
Ozone and speed have some negative relationship.

Statistical analysis are done for each variable including minimum,
maximum, interquartile, average and standard deviation along with number
of NAs in the data.

Based on the bar graph, July and August have larger variance and range
in ozone concentration in ppb compared to the other months. Based on the
line graph, ozone concentration in ppb and solar radiation in langley
have positive relationship to one another. It would be more fitting if
the line was curved as square root function. Ozone concentration in ppb
and temperature in Celsius have positive relationship to one another in
a linear fashion. Ozone concentration in ppb and wind speed in mph have
negative relationship to one another in a linear manner.

### 3. MANOVA

``` r
#Check for assumption
## 1st assumption - normality
aq1 %>%
  group_by(Month) %>%
  summarize(p.value=shapiro.test(Ozone)$p.value)
```

    ## # A tibble: 5 x 2
    ##   Month    p.value
    ## * <ord>      <dbl>
    ## 1 May   0.00000829
    ## 2 Jun   0.0628    
    ## 3 Jul   0.867     
    ## 4 Aug   0.0903    
    ## 5 Sep   0.0000433

``` r
## data transformation 
aq1 <- aq1 %>%
  mutate (lnozone = log(Ozone))
ggplot(aq1, aes(x=Month,y=lnozone, fill=Month))+
  geom_boxplot()+
  labs(title="Ozone concentration by Month", y="log Ozone (logppb)")
```

    ## Warning: Removed 37 rows containing non-finite values (stat_boxplot).

![](Project-2_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
aq1 %>%
  group_by(Month) %>%
  summarize(p.value=shapiro.test(lnozone)$p.value)
```

    ## # A tibble: 5 x 2
    ##   Month p.value
    ## * <ord>   <dbl>
    ## 1 May    0.163 
    ## 2 Jun    0.823 
    ## 3 Jul    0.0156
    ## 4 Aug    0.320 
    ## 5 Sep    0.310

``` r
## 2nd assumption - equal variance
aq1 %>%
  group_by(Month) %>%
  summarize(variance = var(lnozone,na.rm=T))
```

    ## # A tibble: 5 x 2
    ##   Month variance
    ## * <ord>    <dbl>
    ## 1 May      0.861
    ## 2 Jun      0.314
    ## 3 Jul      0.527
    ## 4 Aug      0.603
    ## 5 Sep      0.445

``` r
# anova
summary(aov(lnozone ~ Month, data = aq1))
```

    ##              Df Sum Sq Mean Sq F value   Pr(>F)    
    ## Month         4  21.38   5.346   9.163 1.96e-06 ***
    ## Residuals   111  64.76   0.583                     
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 37 observations deleted due to missingness

``` r
pairwise.t.test(aq1$lnozone, aq1$Month, p.adj = "none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$lnozone and aq1$Month 
    ## 
    ##     May     Jun    Jul    Aug   
    ## Jun 0.1534  -      -      -     
    ## Jul 1.7e-06 0.0306 -      -     
    ## Aug 3.6e-06 0.0417 0.8562 -     
    ## Sep 0.0511  0.9512 0.0017 0.0030
    ## 
    ## P value adjustment method: none

``` r
pairwise.t.test(aq1$lnozone, aq1$Month, p.adj = "bonferroni")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$lnozone and aq1$Month 
    ## 
    ##     May     Jun   Jul   Aug  
    ## Jun 1.000   -     -     -    
    ## Jul 1.7e-05 0.306 -     -    
    ## Aug 3.6e-05 0.417 1.000 -    
    ## Sep 0.511   1.000 0.017 0.030
    ## 
    ## P value adjustment method: bonferroni

``` r
# manova
manova_aq <- manova(cbind(lnozone,Temp,Solar.R, Wind) ~ Month, data = aq1)
summary(manova_aq) ## significant p < 0.001
```

    ##            Df  Pillai approx F num Df den Df    Pr(>F)    
    ## Month       4 0.62528   4.9101     16    424 2.681e-09 ***
    ## Residuals 106                                             
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
 ## one-way ANOVA for each
 summary.aov(manova_aq) # lnozone, temp, wind are significant
```

    ##  Response lnozone :
    ##              Df Sum Sq Mean Sq F value    Pr(>F)    
    ## Month         4 19.216  4.8040  8.0506 1.046e-05 ***
    ## Residuals   106 63.254  0.5967                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ##  Response Temp :
    ##              Df Sum Sq Mean Sq F value    Pr(>F)    
    ## Month         4 1504.5  376.12   25.25 1.056e-14 ***
    ## Residuals   106 1578.9   14.90                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ##  Response Solar.R :
    ##              Df Sum Sq Mean Sq F value Pr(>F)
    ## Month         4  37326  9331.5  1.1283 0.3472
    ## Residuals   106 876635  8270.1               
    ## 
    ##  Response Wind :
    ##              Df  Sum Sq Mean Sq F value   Pr(>F)   
    ## Month         4  183.31  45.827  4.0179 0.004493 **
    ## Residuals   106 1209.00  11.406                    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## 42 observations deleted due to missingness

``` r
  ### post-hoc analysis - for lnozone
  pairwise.t.test(aq1$lnozone, aq1$Month, p.adj="none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$lnozone and aq1$Month 
    ## 
    ##     May     Jun    Jul    Aug   
    ## Jun 0.1534  -      -      -     
    ## Jul 1.7e-06 0.0306 -      -     
    ## Aug 3.6e-06 0.0417 0.8562 -     
    ## Sep 0.0511  0.9512 0.0017 0.0030
    ## 
    ## P value adjustment method: none

``` r
  ### post-hoc analysis - for temp
  pairwise.t.test(aq1$Temp, aq1$Month, p.adj="none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Temp and aq1$Month 
    ## 
    ##     May     Jun    Jul     Aug    
    ## Jun 4.4e-13 -      -       -      
    ## Jul < 2e-16 0.0055 -       -      
    ## Aug < 2e-16 0.0049 0.9696  -      
    ## Sep 5.0e-10 0.2025 6.6e-05 5.7e-05
    ## 
    ## P value adjustment method: none

``` r
  ### post-hoc analysis - for wind
  pairwise.t.test(aq1$Wind, aq1$Month, p.adj="none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Wind and aq1$Month 
    ## 
    ##     May    Jun    Jul    Aug   
    ## Jun 0.1228 -      -      -     
    ## Jul 0.0024 0.1316 -      -     
    ## Aug 0.0014 0.0939 0.8643 -     
    ## Sep 0.1008 0.9218 0.1586 0.1147
    ## 
    ## P value adjustment method: none

``` r
  ### post-hoc analysis - for lnozone with correction
  pairwise.t.test(aq1$lnozone, aq1$Month, p.adj="bonferroni")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$lnozone and aq1$Month 
    ## 
    ##     May     Jun   Jul   Aug  
    ## Jun 1.000   -     -     -    
    ## Jul 1.7e-05 0.306 -     -    
    ## Aug 3.6e-05 0.417 1.000 -    
    ## Sep 0.511   1.000 0.017 0.030
    ## 
    ## P value adjustment method: bonferroni

``` r
  ### post-hoc analysis - for temp with correction
  pairwise.t.test(aq1$Temp, aq1$Month, p.adj="bonferroni")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Temp and aq1$Month 
    ## 
    ##     May     Jun     Jul     Aug    
    ## Jun 4.4e-12 -       -       -      
    ## Jul < 2e-16 0.05498 -       -      
    ## Aug < 2e-16 0.04914 1.00000 -      
    ## Sep 5.0e-09 1.00000 0.00066 0.00057
    ## 
    ## P value adjustment method: bonferroni

``` r
  ### post-hoc analysis - for wind with correction
  pairwise.t.test(aq1$Wind, aq1$Month, p.adj="bonferroni")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Wind and aq1$Month 
    ## 
    ##     May   Jun   Jul   Aug  
    ## Jun 1.000 -     -     -    
    ## Jul 0.024 1.000 -     -    
    ## Aug 0.014 0.939 1.000 -    
    ## Sep 1.000 1.000 1.000 1.000
    ## 
    ## P value adjustment method: bonferroni

``` r
# permanova
  library(vegan)
```

    ## Warning: package 'vegan' was built under R version 4.0.4

    ## Loading required package: permute

    ## Warning: package 'permute' was built under R version 4.0.4

    ## Loading required package: lattice

    ## This is vegan 2.5-7

``` r
 ## Compute Euclidean distances between observations
 dists <- aq1 %>%
  select(lnozone, Temp, Wind) %>%
  dist
 ## Perform PERMANOVA on the distance matrix
 adonis(dists ~ Month, data = aq1)
```

    ## 
    ## Call:
    ## adonis(formula = dists ~ Month, data = aq1) 
    ## 
    ## Permutation: free
    ## Number of permutations: 999
    ## 
    ## Terms added sequentially (first to last)
    ## 
    ##            Df SumsOfSqs MeanSqs F.Model      R2 Pr(>F)    
    ## Month       4    2948.2  737.05  24.329 0.39669  0.001 ***
    ## Residuals 148    4483.8   30.30         0.60331           
    ## Total     152    7432.0                 1.00000           
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

After the data transformation on ozone concentration, the normality and
homodescedasity assumptions are met.

The null hypothesis is that there is no significant difference in means
of natural log of ozone concentration between months. The alternative
hypothesis is that there is significant difference in means of natural
log of ozone concentration between at least one month and the rest.
*p-value of anova test is small enough to reject the null (p&lt;0.001).
There is a significant difference in ln ozone between months. With
Bonferroni correction, there is a significant difference in ln ozone
between May and July, May and August, July and September, and August and
September.*

The null hypothesis is that there is no significant difference in means
of each variable between months. The alternative hypothesis is that
there is significant difference in means of each variable between at
least one month and the rest. *p-value of manova test is small enough to
reject the null. There is a significant difference in each variable for
each month. All months are significantly different in natural log of
ozone concentration (p&lt;0.001), temperature (p&lt;0.001) and wind
(p=0.004).*

Bonferonni alpha = 0.05/(5+5\*3)= 0.05/20 = 0.0025

With Bonferonni correction, May and July, May and August, July and
September, and August and September pairs in natural log of ozone
concentration appear to be significantly different at alpha = 0.05. With
Bonferonni correction, May and June, May and July, May and August, May
and September, June and August, July and September, August and September
pairs in temperature appear to be significantly different at alpha =
0.05. With Bonferonni correction, May and July, May and August pairs in
wind speed appear to be significantly different at alpha = 0.05

From permanova, it is clear that lnozone, temperature and wind speed are
differ across at least Month.

### 4. Randomization Test

``` r
set.seed(348)
aq4 <- aq1 %>%
  filter(!is.na(lnozone))

# LNOZONE
summary(aov(lnozone ~ Month, data = aq4))
```

    ##              Df Sum Sq Mean Sq F value   Pr(>F)    
    ## Month         4  21.38   5.346   9.163 1.96e-06 ***
    ## Residuals   111  64.76   0.583                     
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
pairwise.t.test(aq1$lnozone, aq1$Month, p.adj = "none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$lnozone and aq1$Month 
    ## 
    ##     May     Jun    Jul    Aug   
    ## Jun 0.1534  -      -      -     
    ## Jul 1.7e-06 0.0306 -      -     
    ## Aug 3.6e-06 0.0417 0.8562 -     
    ## Sep 0.0511  0.9512 0.0017 0.0030
    ## 
    ## P value adjustment method: none

``` r
obs_F <- 9.163
## randomization test
Fs <- replicate(1000,{
  # Randomly permute the response variable across doses
  new <- aq4 %>%
    mutate(lnozone = sample(lnozone))
  # Compute variation within groups
  SSW <- new %>%
    group_by(Month) %>%
    summarize(SSW = sum((lnozone - mean(lnozone,na.rm=T))^2)) %>%
    summarize(sum(SSW)) %>% 
    pull
  # Compute variation between groups
  SSB <- new %>% 
    mutate(mean = mean(lnozone, na.rm=T)) %>%
    group_by(Month) %>% 
    mutate(groupmean = mean(lnozone,na.rm=T)) %>%
    summarize(SSB = sum((mean - groupmean)^2)) %>%
    summarize(sum(SSB)) %>%
    pull
  # Compute the F-statistic (ratio of MSB and MSW)
  # df for SSB is 5 groups - 1 = 4
  # df for SSW is 153 observations - 5 groups = 148
  (SSB/4)/(SSW/148)
  })
 ## Represent the distribution of the F-statistics for each randomized sample
 hist(Fs, prob=T); abline(v = obs_F, col="red",add=TRUE)
```

    ## Warning in int_abline(a = a, b = b, h = h, v = v, untf = untf, ...): "add" is
    ## not a graphical parameter

![](Project-2_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
 ## Calculate the proportion of F statistic that are greater than the observed F-statistic - reject the null hypothesis
 mean(Fs > obs_F)
```

    ## [1] 0.001

``` r
 # TEMPERATURE
summary(aov(Temp ~ Month, data = aq1))
```

    ##              Df Sum Sq Mean Sq F value Pr(>F)    
    ## Month         4   2179   544.8   39.85 <2e-16 ***
    ## Residuals   148   2024    13.7                   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
pairwise.t.test(aq1$Temp, aq1$Month, p.adj = "none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Temp and aq1$Month 
    ## 
    ##     May     Jun    Jul     Aug    
    ## Jun 4.4e-13 -      -       -      
    ## Jul < 2e-16 0.0055 -       -      
    ## Aug < 2e-16 0.0049 0.9696  -      
    ## Sep 5.0e-10 0.2025 6.6e-05 5.7e-05
    ## 
    ## P value adjustment method: none

``` r
obs_F <- 39.85
## randomization test
Fs <- replicate(1000,{
  # Randomly permute the response variable across doses
  new <- aq1 %>%
    mutate(Temp = sample(Temp))
  # Compute variation within groups
  SSW <- new %>%
    group_by(Month) %>%
    summarize(SSW = sum((Temp - mean(Temp,na.rm=T))^2)) %>%
    summarize(sum(SSW)) %>% 
    pull
  # Compute variation between groups
  SSB <- new %>% 
    mutate(mean = mean(Temp, na.rm=T)) %>%
    group_by(Month) %>% 
    mutate(groupmean = mean(Temp,na.rm=T)) %>%
    summarize(SSB = sum((mean - groupmean)^2)) %>%
    summarize(sum(SSB)) %>%
    pull
  # Compute the F-statistic (ratio of MSB and MSW)
  # df for SSB is 5 groups - 1 = 4
  # df for SSW is 153 observations - 5 groups = 148
  (SSB/4)/(SSW/148)
  })
 ## Represent the distribution of the F-statistics for each randomized sample
 hist(Fs, prob=T); abline(v = obs_F, col="red",add=T)
```

    ## Warning in int_abline(a = a, b = b, h = h, v = v, untf = untf, ...): "add" is
    ## not a graphical parameter

![](Project-2_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

``` r
 ## Calculate the proportion of F statistic that are greater than the observed F-statistic - reject the null hypothesis
 mean(Fs > obs_F)
```

    ## [1] 0

``` r
 # WIND
summary(aov(Wind ~ Month, data = aq1))
```

    ##              Df Sum Sq Mean Sq F value  Pr(>F)   
    ## Month         4  164.3   41.07   3.529 0.00879 **
    ## Residuals   148 1722.3   11.64                   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
pairwise.t.test(aq1$Wind, aq1$Month, p.adj = "none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  aq1$Wind and aq1$Month 
    ## 
    ##     May    Jun    Jul    Aug   
    ## Jun 0.1228 -      -      -     
    ## Jul 0.0024 0.1316 -      -     
    ## Aug 0.0014 0.0939 0.8643 -     
    ## Sep 0.1008 0.9218 0.1586 0.1147
    ## 
    ## P value adjustment method: none

``` r
obs_F <- 3.529
## randomization test
Fs <- replicate(1000,{
  # Randomly permute the response variable across doses
  new <- aq1 %>%
    mutate(Wind = sample(Wind))
  # Compute variation within groups
  SSW <- new %>%
    group_by(Month) %>%
    summarize(SSW = sum((Wind - mean(Wind,na.rm=T))^2)) %>%
    summarize(sum(SSW)) %>% 
    pull
  # Compute variation between groups
  SSB <- new %>% 
    mutate(mean = mean(Wind, na.rm=T)) %>%
    group_by(Month) %>% 
    mutate(groupmean = mean(Wind,na.rm=T)) %>%
    summarize(SSB = sum((mean - groupmean)^2)) %>%
    summarize(sum(SSB)) %>%
    pull
  # Compute the F-statistic (ratio of MSB and MSW)
  # df for SSB is 5 groups - 1 = 4
  # df for SSW is 153 observations - 5 groups = 148
  (SSB/4)/(SSW/148)
  })
 ## Represent the distribution of the F-statistics for each randomized sample
 hist(Fs, prob=T); abline(v = obs_F, col="red",add=T)
```

    ## Warning in int_abline(a = a, b = b, h = h, v = v, untf = untf, ...): "add" is
    ## not a graphical parameter

![](Project-2_files/figure-gfm/unnamed-chunk-4-3.png)<!-- -->

``` r
 ## Calculate the proportion of F statistic that are greater than the observed F-statistic - reject the null hypothesis
 mean(Fs > obs_F)
```

    ## [1] 0.013

1.  The null hypothesis is that the mean of natural log of ozone
    concentration is same across Month. The alternative hypothesis is
    that mean of natural log of ozone concentration is different across
    Month at least one. There is a significant difference in mean of
    natural log of ozone concentration across Month (F=9.163, df=4, p
    &lt; 0.001). This concurs with the result from the randomization
    test.(p=0.001)

2.  The null hypothesis is that the mean of temperature is same across
    Month. The alternative hypothesis is that mean of temperature is
    different across Month. There is a significant difference in mean of
    temperature across Month at least one (F=39.85, df=4, p &lt; 0.001).
    This concurs with the result from the randomization test.(p=0)

3.  The null hypothesis is that the mean of wind speed is same across
    Month. The alternative hypothesis is that mean of wind speed is
    different across months at least one. There is a significant
    difference in mean of wind speed across months (F=3.529, df=4, p
    &lt; 0.01). This does not concur but still holds the significance
    with the result from the randomization test.(p=0.013)

### 5. Linear Regression model

``` r
library(lmtest)
```

    ## Warning: package 'lmtest' was built under R version 4.0.4

    ## Loading required package: zoo

    ## Warning: package 'zoo' was built under R version 4.0.4

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

``` r
library(sandwich)
```

    ## Warning: package 'sandwich' was built under R version 4.0.4

``` r
set.seed(348)

aq2 <- aq1 %>%
  mutate (lnozone_c = lnozone - mean(lnozone, na.rm=T),
          Temp_c = Temp - mean(Temp, na.rm=T),
          Wind_c = Wind - mean(Wind, na.rm=T))%>%
  mutate (Month = ntile(Month, 5)) %>%
  mutate (Month = factor(Month, labels=c("May","Jun","Jul","Aug", "Sep")))

# linear regression model to predict lnozone based on temperature only
fit <- lm(lnozone_c ~ Temp_c, data = aq2)
summary(fit)
```

    ## 
    ## Call:
    ## lm(formula = lnozone_c ~ Temp_c, data = aq2)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -2.14469 -0.33095  0.02961  0.36507  1.49421 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 0.0007873  0.0543013   0.014    0.988    
    ## Temp_c      0.1215049  0.0103491  11.741   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5848 on 114 degrees of freedom
    ##   (37 observations deleted due to missingness)
    ## Multiple R-squared:  0.5473, Adjusted R-squared:  0.5434 
    ## F-statistic: 137.8 on 1 and 114 DF,  p-value: < 2.2e-16

``` r
 ## graph
 ggplot(aq2, aes(x=Temp_c, y=lnozone_c))+ geom_point() + geom_smooth(method=lm, se=F) +
   labs(title="scaled temperature vs. scaled ln(ozone)", x="Temperature(C)", y="ln(ozone) (lnppb)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
 ## proportion of variance in lnozone explained by temp_c
 summary(fit)$r.sq
```

    ## [1] 0.5473353

``` r
 ## 1st assumption - normality
 shapiro.test(fit$residuals)
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  fit$residuals
    ## W = 0.97846, p-value = 0.05865

``` r
 ## 2nd assumption - homoscedasticity
 plot(fit, which = 1)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

``` r
 bptest(fit)
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  fit
    ## BP = 7.3298, df = 1, p-value = 0.006782

``` r
 ## robust SEs
 coeftest(fit, vcov = vcovHC(fit))
```

    ## 
    ## t test of coefficients:
    ## 
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 0.0007873  0.0548466  0.0144   0.9886    
    ## Temp_c      0.1215050  0.0115719 10.5000   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
 ## bootstrap SEs
 samp_SEs <- replicate(1000, {
  # Bootstrap your data (resample observations)
  boot_data <- sample_frac(aq2, replace = TRUE)
  # Fit regression model
  fitboot <- lm(lnozone_c ~ Temp_c, data = boot_data)
  # Save the coefficients
  coef(fitboot)
  })
 samp_SEs %>%
  # Transpose the obtained matrices
  t %>%
  # Consider the matrix as a data frame
  as.data.frame %>%
  # Compute the standard error (standard deviation of the sampling distribution)
  summarize_all(sd) #int 0.3098 temp 0.011
```

    ##   (Intercept)     Temp_c
    ## 1   0.0537089 0.01161122

``` r
# linear regression model to predict lnozone based on wind speed only
fit<- lm(lnozone_c ~ Wind_c, data = aq2)
summary(fit)
```

    ## 
    ## Call:
    ## lm(formula = lnozone_c ~ Wind_c, data = aq2)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.4396 -0.4998  0.0605  0.5375  1.6051 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -0.01244    0.06804  -0.183    0.855    
    ## Wind_c      -0.13035    0.01911  -6.822 4.55e-10 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.7325 on 114 degrees of freedom
    ##   (37 observations deleted due to missingness)
    ## Multiple R-squared:  0.2899, Adjusted R-squared:  0.2837 
    ## F-statistic: 46.54 on 1 and 114 DF,  p-value: 4.551e-10

``` r
 ## graph
 ggplot(aq2, aes(x=Wind_c, y=lnozone_c))+ geom_point() + geom_smooth(method=lm, se=F) + 
   labs(title="scaled wind speed vs. scaled ln(ozone)", x="wind speed(mph)", y="ln(ozone) (lnppb)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-5-3.png)<!-- -->

``` r
 ## proportion of variance in lnozone explained by wind_c
 summary(fit)$r.sq
```

    ## [1] 0.289894

``` r
 ## 1st assumption - normality
 shapiro.test(fit$residuals)
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  fit$residuals
    ## W = 0.94295, p-value = 9.047e-05

``` r
 plot(fit, which = 2)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-4.png)<!-- -->

``` r
 ## 2nd assumption - homoscedasticity
 bptest(fit) 
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  fit
    ## BP = 0.15517, df = 1, p-value = 0.6936

``` r
 plot(fit, which = 1)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-5.png)<!-- -->

``` r
 ## robust SEs
 coeftest(fit, vcov = vcovHC(fit))
```

    ## 
    ## t test of coefficients:
    ## 
    ##              Estimate Std. Error t value  Pr(>|t|)    
    ## (Intercept) -0.012442   0.068809 -0.1808    0.8568    
    ## Wind_c      -0.130351   0.019142 -6.8096 4.837e-10 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
 ## bootstrap SEs
 samp_SEs <- replicate(1000, {
  # Bootstrap your data (resample observations)
  boot_data <- sample_frac(aq2, replace = TRUE)
  # Fit regression model
  fitboot <- lm(lnozone_c ~ Wind_c, data = boot_data)
  # Save the coefficients
  coef(fitboot)
  })
 samp_SEs %>%
  # Transpose the obtained matrices
  t %>%
  # Consider the matrix as a data frame
  as.data.frame %>%
  # Compute the standard error (standard deviation of the sampling distribution)
  summarize_all(sd)
```

    ##   (Intercept)     Wind_c
    ## 1  0.07009713 0.01856089

``` r
# linear regression model to predict lnozone based on temperature and Month with interaction
fit <- lm(lnozone_c ~ Temp_c * Month, data=aq2)
summary(fit)
```

    ## 
    ## Call:
    ## lm(formula = lnozone_c ~ Temp_c * Month, data = aq2)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -2.24439 -0.27442  0.03424  0.36108  1.51185 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)      0.212441   0.229266   0.927   0.3562    
    ## Temp_c           0.132177   0.032088   4.119 7.56e-05 ***
    ## MonthJun        -0.282189   0.294995  -0.957   0.3410    
    ## MonthJul        -0.531891   0.298465  -1.782   0.0776 .  
    ## MonthAug        -0.262293   0.279194  -0.939   0.3496    
    ## MonthSep        -0.349997   0.253810  -1.379   0.1708    
    ## Temp_c:MonthJun -0.024751   0.056001  -0.442   0.6594    
    ## Temp_c:MonthJul  0.093175   0.056784   1.641   0.1038    
    ## Temp_c:MonthAug  0.008379   0.045020   0.186   0.8527    
    ## Temp_c:MonthSep -0.018670   0.039652  -0.471   0.6387    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5823 on 106 degrees of freedom
    ##   (37 observations deleted due to missingness)
    ## Multiple R-squared:  0.5827, Adjusted R-squared:  0.5473 
    ## F-statistic: 16.45 on 9 and 106 DF,  p-value: < 2.2e-16

``` r
 ## graph
 ggplot(aq2, aes(x=Temp_c, y=lnozone_c, color=Month))+ geom_point() + geom_smooth(method=lm, se=F) +
   labs(title="scaled temperature vs. scaled ln(ozone) by month", x="Temperature(C)", y="ln(ozone) (lnppb)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-5-6.png)<!-- -->

``` r
 ## proportion of variance in lnozone explained by temp_c and month interaction
 summary(fit)$r.sq
```

    ## [1] 0.5826962

``` r
 ## 1st assumption - normality
 shapiro.test(fit$residuals)
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  fit$residuals
    ## W = 0.96659, p-value = 0.005425

``` r
 plot(fit, which = 2)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-7.png)<!-- -->

``` r
 ## 2nd assumption - homoscedasticity
 bptest(fit) 
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  fit
    ## BP = 12.09, df = 9, p-value = 0.2083

``` r
 plot(fit, which = 1)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-8.png)<!-- -->

``` r
 ## robust SEs
 coeftest(fit, vcov = vcovHC(fit))
```

    ## 
    ## t test of coefficients:
    ## 
    ##                   Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)      0.2124409  0.3429176  0.6195  0.53691  
    ## Temp_c           0.1321771  0.0535785  2.4670  0.01523 *
    ## MonthJun        -0.2821889  0.4092157 -0.6896  0.49196  
    ## MonthJul        -0.5318907  0.3781190 -1.4067  0.16245  
    ## MonthAug        -0.2622926  0.3901905 -0.6722  0.50291  
    ## MonthSep        -0.3499972  0.3511728 -0.9967  0.32120  
    ## Temp_c:MonthJun -0.0247508  0.0753192 -0.3286  0.74310  
    ## Temp_c:MonthJul  0.0931749  0.0614000  1.5175  0.13212  
    ## Temp_c:MonthAug  0.0083787  0.0609550  0.1375  0.89093  
    ## Temp_c:MonthSep -0.0186700  0.0556055 -0.3358  0.73772  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
 ## bootstrap SEs
 samp_SEs <- replicate(1000, {
  # Bootstrap your data (resample observations)
  boot_data <- sample_frac(aq2, replace = TRUE)
  # Fit regression model
  fitboot <- lm(lnozone_c ~ Temp_c * Month, data = boot_data)
  # Save the coefficients
  coef(fitboot)
  })
 samp_SEs %>%
  # Transpose the obtained matrices
  t %>%
  # Consider the matrix as a data frame
  as.data.frame %>%
  # Compute the standard error (standard deviation of the sampling distribution)
  summarize_all(sd)
```

    ##   (Intercept)     Temp_c MonthJun  MonthJul  MonthAug  MonthSep Temp_c:MonthJun
    ## 1   0.3323643 0.05256744 0.407719 0.3676572 0.3739444 0.3406448       0.0803585
    ##   Temp_c:MonthJul Temp_c:MonthAug Temp_c:MonthSep
    ## 1      0.06219634      0.05879779      0.05493873

``` r
 # linear regression model to predict lnozone based on wind and Month 
fit <- lm(lnozone_c ~ Wind_c * Month, data=aq2)
summary(fit)
```

    ## 
    ## Call:
    ## lm(formula = lnozone_c ~ Wind_c * Month, data = aq2)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -2.91301 -0.31527 -0.01519  0.39468  1.60223 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)     -0.52029    0.14410  -3.611 0.000468 ***
    ## Wind_c          -0.05742    0.03835  -1.497 0.137318    
    ## MonthJun         0.54890    0.26687   2.057 0.042164 *  
    ## MonthJul         0.73223    0.20507   3.571 0.000537 ***
    ## MonthAug         0.72678    0.20464   3.551 0.000573 ***
    ## MonthSep         0.33336    0.19087   1.747 0.083614 .  
    ## Wind_c:MonthJun  0.02657    0.06337   0.419 0.675921    
    ## Wind_c:MonthJul -0.09756    0.06042  -1.615 0.109365    
    ## Wind_c:MonthAug -0.11430    0.05618  -2.034 0.044418 *  
    ## Wind_c:MonthSep -0.05064    0.05304  -0.955 0.341923    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6736 on 106 degrees of freedom
    ##   (37 observations deleted due to missingness)
    ## Multiple R-squared:  0.4416, Adjusted R-squared:  0.3942 
    ## F-statistic: 9.313 on 9 and 106 DF,  p-value: 2.6e-10

``` r
 ## graph
 ggplot(aq2, aes(x=Wind_c, y=lnozone_c, color=Month))+ geom_point() + geom_smooth(method=lm, se=F) +
   labs(title="scaled wind speed vs. scaled ln(ozone)", x="wind speed (mph)", y="ln(ozone) (lnppb)")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 37 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 37 rows containing missing values (geom_point).

![](Project-2_files/figure-gfm/unnamed-chunk-5-9.png)<!-- -->

``` r
 ## proportion of variance in lnozone explained by wind_c and month
 summary(fit)$r.sq
```

    ## [1] 0.4415797

``` r
## 1st assumption - normality
 shapiro.test(fit$residuals)
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  fit$residuals
    ## W = 0.96188, p-value = 0.002237

``` r
 plot(fit, which = 2)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-10.png)<!-- -->

``` r
 ## 2nd assumption - homoscedasticity
 bptest(fit) 
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  fit
    ## BP = 12.022, df = 9, p-value = 0.2121

``` r
 plot(fit, which = 1)
```

![](Project-2_files/figure-gfm/unnamed-chunk-5-11.png)<!-- -->

``` r
 ## robust SEs
 coeftest(fit, vcov = vcovHC(fit))
```

    ## 
    ## t test of coefficients:
    ## 
    ##                  Estimate Std. Error t value Pr(>|t|)   
    ## (Intercept)     -0.520294   0.239279 -2.1744 0.031897 * 
    ## Wind_c          -0.057423   0.053725 -1.0688 0.287567   
    ## MonthJun         0.548898   0.455015  1.2063 0.230375   
    ## MonthJul         0.732227   0.283809  2.5800 0.011249 * 
    ## MonthAug         0.726779   0.273451  2.6578 0.009083 **
    ## MonthSep         0.333362   0.262608  1.2694 0.207068   
    ## Wind_c:MonthJun  0.026566   0.121225  0.2191 0.826959   
    ## Wind_c:MonthJul -0.097563   0.073110 -1.3345 0.184907   
    ## Wind_c:MonthAug -0.114296   0.062603 -1.8257 0.070705 . 
    ## Wind_c:MonthSep -0.050639   0.063192 -0.8013 0.424723   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
 ## bootstrap SEs
 samp_SEs <- replicate(1000, {
  # Bootstrap your data (resample observations)
  boot_data <- sample_frac(aq2, replace = TRUE)
  # Fit regression model
  fitboot <- lm(lnozone_c ~ Wind_c*Month, data = boot_data)
  # Save the coefficients
  coef(fitboot)
  })
 samp_SEs %>%
  # Transpose the obtained matrices
  t %>%
  # Consider the matrix as a data frame
  as.data.frame %>%
  # Compute the standard error (standard deviation of the sampling distribution)
  summarize_all(sd)
```

    ##   (Intercept)     Wind_c  MonthJun  MonthJul  MonthAug  MonthSep
    ## 1   0.2373173 0.05591058 0.3781613 0.2715964 0.2753569 0.2605323
    ##   Wind_c:MonthJun Wind_c:MonthJul Wind_c:MonthAug Wind_c:MonthSep
    ## 1        0.116191       0.0720718      0.06315859      0.06458393

1.  Linear regression model that predicts lnozone from temperature met
    the normality assumption but not the homoscedasticity assumption.
    Based on the plot, equal variance does not look too off the straight
    line. Temperature is significantly associated with lnozone; for
    every 1 unit increase in temperature, there is 0.122 increase in
    lnozone (t = 11.7, df = 114, p &lt; 0.001). The proportion of
    variance in lnozone explained by temperature is 0.547 (54.7%).
    *lnozone(hat) = 0.000787 + 0.122(temp\_c) with standard error of
    0.055 on intercept and 0.012 on temp\_c. The robust standard error
    concurs with bootstrapped standard errors (0.054 on intercept, 0.012
    on temp\_c).*

2.  Linear regression model that predicts lnozone from wind speed did
    not met the normality assumption but not the homoscedasticity
    assumption. Wind speed is significantly associated with lnozone; for
    every 1 unit increase in wind speed, there is 0.130 decrease in
    lnozone (t = -6.8, df = 114, p &lt; 0.001). The proportion of
    variance in lnozone explained by wind speed is 0.290 (29.0%).
    *lnozone(hat) = -0.012-0.13(Wind\_c) with standard error of 0.069 on
    intercept and 0.019 on Wind\_c. The robust standard error concurs
    with bootstrapped standard errors (0.070 on intercept, 0.019 on
    wind\_c).*

3.  Linear regression model that predicts lnozone from temperature and
    month with interaction did not met the normality assumption but not
    the homoscedasticity assumption. Temperature is significantly
    associated with lnozone; for every 1 unit increase in temperature,
    there is 0.132 increase in lnozone (t = 4.12, df = 106, p &lt;
    0.001). Month is not a significant predictor of lnozone. There is no
    significant interaction between month and temperature. The
    proportion of variance in lnozone explained by wind speed is 0.583
    (58.3%). *lnozone(hat) = 0.212 + 0.132(Temp\_c) with standard error
    of 0.343 on intercept and 0.054 on Temp\_c. The robust standard
    error is simliar to bootstrapped standard errors (0.33 on intercept,
    and 0.053 on temp\_c).*

4.  Linear regression model that predicts lnozone from wind and month
    with interaction did not met the normality assumption but not the
    homoscedasticity assumption. Wind speed is no longer significantly
    associated with lnozone; for every 1 unit increase in wind speed,
    there is 0.057 decrease in lnozone. Month is significantly
    associated with lnozone controlling wind. For average wind, ln ozone
    for June is 0.549 lnppb higher than May (t=2.06, df=106,
    p&lt;0.001). For average wind, ln ozone for July is 0.732 lnppb
    higher than May (t=3.57, df=106, p&lt;0.001). For average wind, ln
    ozone for August is 0.727 lnppb higher than May (t=3.551, df=106,
    p&lt;0.001). The proportion of variance in lnozone explained by wind
    speed is 0.442 (44.2%). *The standard errors are 0.239 on intercept,
    0.054 on Wind\_c, 0.46 on June, 0.28 on July, 0.27 on August, and
    0.26 on September. The robust standard error is similar to
    bootstrapped standard errors.(0.24 on intercept, 0.056 on wind\_c,
    0.38 on June, 0.27 on July, 0.28 on August, 0.26 on September)*

### 6. Logistic Regression

``` r
# create a binary variable
aq3 <- aq1 %>%
  mutate(y = ifelse(Ozone < 100, 1, 0))%>%
  mutate (Month = ntile(Month, 5)) %>%
  mutate (Month = factor(Month, labels=c("May","Jun","Jul","Aug", "Sep"))) %>%
  filter(!is.na(Ozone))
aq3
```

    ##     Ozone Solar.R Wind     Temp Day Month  lnozone y
    ## 1      41     190  7.4 19.44444   1   May 3.713572 1
    ## 2      36     118  8.0 22.22222   2   May 3.583519 1
    ## 3      12     149 12.6 23.33333   3   May 2.484907 1
    ## 4      18     313 11.5 16.66667   4   May 2.890372 1
    ## 5      28      NA 14.9 18.88889   6   May 3.332205 1
    ## 6      23     299  8.6 18.33333   7   May 3.135494 1
    ## 7      19      99 13.8 15.00000   8   May 2.944439 1
    ## 8       8      19 20.1 16.11111   9   May 2.079442 1
    ## 9       7      NA  6.9 23.33333  11   May 1.945910 1
    ## 10     16     256  9.7 20.55556  12   May 2.772589 1
    ## 11     11     290  9.2 18.88889  13   May 2.397895 1
    ## 12     14     274 10.9 20.00000  14   May 2.639057 1
    ## 13     18      65 13.2 14.44444  15   May 2.890372 1
    ## 14     14     334 11.5 17.77778  16   May 2.639057 1
    ## 15     34     307 12.0 18.88889  17   May 3.526361 1
    ## 16      6      78 18.4 13.88889  18   May 1.791759 1
    ## 17     30     322 11.5 20.00000  19   May 3.401197 1
    ## 18     11      44  9.7 16.66667  20   May 2.397895 1
    ## 19      1       8  9.7 15.00000  21   May 0.000000 1
    ## 20     11     320 16.6 22.77778  22   May 2.397895 1
    ## 21      4      25  9.7 16.11111  23   May 1.386294 1
    ## 22     32      92 12.0 16.11111  24   May 3.465736 1
    ## 23     23      13 12.0 19.44444  28   May 3.135494 1
    ## 24     45     252 14.9 27.22222  29   May 3.806662 1
    ## 25    115     223  5.7 26.11111  30   May 4.744932 0
    ## 26     37     279  7.4 24.44444  31   May 3.610918 1
    ## 27     29     127  9.7 27.77778   7   Jun 3.367296 1
    ## 28     71     291 13.8 32.22222   9   Jun 4.262680 1
    ## 29     39     323 11.5 30.55556  10   Jun 3.663562 1
    ## 30     23     148  8.0 27.77778  13   Jun 3.135494 1
    ## 31     21     191 14.9 25.00000  16   Jun 3.044522 1
    ## 32     37     284 20.7 22.22222  17   Jun 3.610918 1
    ## 33     20      37  9.2 18.33333  18   Jun 2.995732 1
    ## 34     12     120 11.5 22.77778  19   Jun 2.484907 1
    ## 35     13     137 10.3 24.44444  20   Jun 2.564949 1
    ## 36    135     269  4.1 28.88889   1   Jun 4.905275 0
    ## 37     49     248  9.2 29.44444   2   Jul 3.891820 1
    ## 38     32     236  9.2 27.22222   3   Jul 3.465736 1
    ## 39     64     175  4.6 28.33333   5   Jul 4.158883 1
    ## 40     40     314 10.9 28.33333   6   Jul 3.688879 1
    ## 41     77     276  5.1 31.11111   7   Jul 4.343805 1
    ## 42     97     267  6.3 33.33333   8   Jul 4.574711 1
    ## 43     97     272  5.7 33.33333   9   Jul 4.574711 1
    ## 44     85     175  7.4 31.66667  10   Jul 4.442651 1
    ## 45     10     264 14.3 22.77778  12   Jul 2.302585 1
    ## 46     27     175 14.9 27.22222  13   Jul 3.295837 1
    ## 47      7      48 14.3 26.66667  15   Jul 1.945910 1
    ## 48     48     260  6.9 27.22222  16   Jul 3.871201 1
    ## 49     35     274 10.3 27.77778  17   Jul 3.555348 1
    ## 50     61     285  6.3 28.88889  18   Jul 4.110874 1
    ## 51     79     187  5.1 30.55556  19   Jul 4.369448 1
    ## 52     63     220 11.5 29.44444  20   Jul 4.143135 1
    ## 53     16       7  6.9 23.33333  21   Jul 2.772589 1
    ## 54     80     294  8.6 30.00000  24   Jul 4.382027 1
    ## 55    108     223  8.0 29.44444  25   Jul 4.682131 0
    ## 56     20      81  8.6 27.77778  26   Jul 2.995732 1
    ## 57     52      82 12.0 30.00000  27   Jul 3.951244 1
    ## 58     82     213  7.4 31.11111  28   Jul 4.406719 1
    ## 59     50     275  7.4 30.00000  29   Jul 3.912023 1
    ## 60     64     253  7.4 28.33333  30   Jul 4.158883 1
    ## 61     59     254  9.2 27.22222  31   Jul 4.077537 1
    ## 62     39      83  6.9 27.22222   1   Jul 3.663562 1
    ## 63      9      24 13.8 27.22222   2   Aug 2.197225 1
    ## 64     16      77  7.4 27.77778   3   Aug 2.772589 1
    ## 65     78      NA  6.9 30.00000   4   Aug 4.356709 1
    ## 66     35      NA  7.4 29.44444   5   Aug 3.555348 1
    ## 67     66      NA  4.6 30.55556   6   Aug 4.189655 1
    ## 68    122     255  4.0 31.66667   7   Aug 4.804021 0
    ## 69     89     229 10.3 32.22222   8   Aug 4.488636 1
    ## 70    110     207  8.0 32.22222   9   Aug 4.700480 0
    ## 71     44     192 11.5 30.00000  12   Aug 3.784190 1
    ## 72     28     273 11.5 27.77778  13   Aug 3.332205 1
    ## 73     65     157  9.7 26.66667  14   Aug 4.174387 1
    ## 74     22      71 10.3 25.00000  16   Aug 3.091042 1
    ## 75     59      51  6.3 26.11111  17   Aug 4.077537 1
    ## 76     23     115  7.4 24.44444  18   Aug 3.135494 1
    ## 77     31     244 10.9 25.55556  19   Aug 3.433987 1
    ## 78     44     190 10.3 25.55556  20   Aug 3.784190 1
    ## 79     21     259 15.5 25.00000  21   Aug 3.044522 1
    ## 80      9      36 14.3 22.22222  22   Aug 2.197225 1
    ## 81     45     212  9.7 26.11111  24   Aug 3.806662 1
    ## 82    168     238  3.4 27.22222  25   Aug 5.123964 0
    ## 83     73     215  8.0 30.00000  26   Aug 4.290459 1
    ## 84     76     203  9.7 36.11111  28   Aug 4.330733 1
    ## 85    118     225  2.3 34.44444  29   Aug 4.770685 0
    ## 86     84     237  6.3 35.55556  30   Aug 4.430817 1
    ## 87     85     188  6.3 34.44444  31   Aug 4.442651 1
    ## 88     96     167  6.9 32.77778   1   Sep 4.564348 1
    ## 89     78     197  5.1 33.33333   2   Sep 4.356709 1
    ## 90     73     183  2.8 33.88889   3   Sep 4.290459 1
    ## 91     91     189  4.6 33.88889   4   Sep 4.510860 1
    ## 92     47      95  7.4 30.55556   5   Sep 3.850148 1
    ## 93     32      92 15.5 28.88889   6   Sep 3.465736 1
    ## 94     20     252 10.9 26.66667   7   Sep 2.995732 1
    ## 95     23     220 10.3 25.55556   8   Sep 3.135494 1
    ## 96     21     230 10.9 23.88889   9   Sep 3.044522 1
    ## 97     24     259  9.7 22.77778  10   Sep 3.178054 1
    ## 98     44     236 14.9 27.22222  11   Sep 3.784190 1
    ## 99     21     259 15.5 24.44444  12   Sep 3.044522 1
    ## 100    28     238  6.3 25.00000  13   Sep 3.332205 1
    ## 101     9      24 10.9 21.66667  14   Sep 2.197225 1
    ## 102    13     112 11.5 21.66667  15   Sep 2.564949 1
    ## 103    46     237  6.9 25.55556  16   Sep 3.828641 1
    ## 104    18     224 13.8 19.44444  17   Sep 2.890372 1
    ## 105    13      27 10.3 24.44444  18   Sep 2.564949 1
    ## 106    24     238 10.3 20.00000  19   Sep 3.178054 1
    ## 107    16     201  8.0 27.77778  20   Sep 2.772589 1
    ## 108    13     238 12.6 17.77778  21   Sep 2.564949 1
    ## 109    23      14  9.2 21.66667  22   Sep 3.135494 1
    ## 110    36     139 10.3 27.22222  23   Sep 3.583519 1
    ## 111     7      49 10.3 20.55556  24   Sep 1.945910 1
    ## 112    14      20 16.6 17.22222  25   Sep 2.639057 1
    ## 113    30     193  6.9 21.11111  26   Sep 3.401197 1
    ## 114    14     191 14.3 23.88889  28   Sep 2.639057 1
    ## 115    18     131  8.0 24.44444  29   Sep 2.890372 1
    ## 116    20     223 11.5 20.00000  30   Sep 2.995732 1

``` r
# regression model to predict if ozone concentration is permissible by Month and wind 
fit <- glm(y ~ Month + Wind, data= aq3, family="binomial") 
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = y ~ Month + Wind, family = "binomial", data = aq3)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.94032   0.00004   0.06316   0.21403   1.23644  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept)   -4.6722     2.5052  -1.865  0.06218 . 
    ## MonthJun      -0.4619     2.0600  -0.224  0.82260   
    ## MonthJul       1.7226     1.6109   1.069  0.28493   
    ## MonthAug       0.3605     1.4471   0.249  0.80325   
    ## MonthSep      19.1653  2491.5790   0.008  0.99386   
    ## Wind           0.9074     0.3077   2.949  0.00319 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 52.876  on 115  degrees of freedom
    ## Residual deviance: 26.255  on 110  degrees of freedom
    ## AIC: 38.255
    ## 
    ## Number of Fisher Scoring iterations: 19

``` r
 ## interpret
 exp(coef(fit))
```

    ##  (Intercept)     MonthJun     MonthJul     MonthAug     MonthSep         Wind 
    ## 9.351235e-03 6.301046e-01 5.598984e+00 1.434107e+00 2.105536e+08 2.477825e+00

``` r
 ## Confusion matrix: compare true to predicted condition
 aq3$prob1 <- predict(fit, type = "response")
 aq3$predicted <- ifelse(aq3$prob1 > .5, "permissible", "not permissible")
 table(true_condition = aq3$y, predicted_condition = aq3$predicted) %>% 
  addmargins
```

    ##               predicted_condition
    ## true_condition not permissible permissible Sum
    ##            0                 4           3   7
    ##            1                 1         108 109
    ##            Sum               5         111 116

``` r
  ## accuracy
  (4+108)/116
```

    ## [1] 0.9655172

``` r
  ## sensitivity TPR
  108/109
```

    ## [1] 0.9908257

``` r
  ## specificity TNR
  4/7
```

    ## [1] 0.5714286

``` r
  ## recall precision PPV
  108/111
```

    ## [1] 0.972973

``` r
 ## density 
 aq3$logit <- predict(fit)
 ggplot(aq3, aes(logit, fill = as.factor(y))) +
  geom_density(alpha = .3) +
  geom_vline(xintercept = 0, lty = 2) +
  labs(title = "Density graph of permissible ozone concetration", fill = "Permissible status, 1 permissible")
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
 ## Save predicted probabilities
 df <- data.frame(prob=predict(fit, type = "response"),y=aq3$y)
 ## Plot ROC curve
 ROCplot <- ggplot(df) + geom_roc(aes(d = y, m = prob), n.cuts = 0)+labs(title="ROC curve of y~ Month+Wind")
 ROCplot
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
 ## Calculate AUC
 calc_auc(ROCplot)$AUC
```

    ## [1] 0.9259502

``` r
# regression model to predict if ozone concentration is permissible by Month and temperature 
fit <- glm(y ~ Month + Temp, data= aq3, family="binomial") 
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = y ~ Month + Temp, family = "binomial", data = aq3)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.55487   0.00008   0.20948   0.33432   1.17659  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept)    9.0611     3.1409   2.885  0.00392 **
    ## MonthJun       0.8002     1.7179   0.466  0.64136   
    ## MonthJul       2.3516     1.7604   1.336  0.18162   
    ## MonthAug       0.9827     1.6414   0.599  0.54935   
    ## MonthSep      18.1121  1805.2252   0.010  0.99199   
    ## Temp          -0.2781     0.1307  -2.128  0.03333 * 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 52.876  on 115  degrees of freedom
    ## Residual deviance: 40.088  on 110  degrees of freedom
    ## AIC: 52.088
    ## 
    ## Number of Fisher Scoring iterations: 18

``` r
 ## interpret
 exp(coef(fit))
```

    ##  (Intercept)     MonthJun     MonthJul     MonthAug     MonthSep         Temp 
    ## 8.613763e+03 2.225932e+00 1.050218e+01 2.671772e+00 7.345153e+07 7.572332e-01

``` r
  ## Confusion matrix: compare true to predicted condition
 aq3$prob1 <- predict(fit, type = "response")
 aq3$predicted <- ifelse(aq3$prob1 > .5, "permissible", "not permissible")
 table(true_condition = aq3$y, predicted_condition = aq3$predicted) %>% 
  addmargins
```

    ##               predicted_condition
    ## true_condition permissible Sum
    ##            0             7   7
    ##            1           109 109
    ##            Sum         116 116

``` r
  ## accuracy
  (109)/116
```

    ## [1] 0.9396552

``` r
  ## sensitivity TPR
  109/109
```

    ## [1] 1

``` r
  ## specificity TNR
  0/7
```

    ## [1] 0

``` r
  ## recall precision PPV
  0/111
```

    ## [1] 0

``` r
 ## density 
 aq3$logit <- predict(fit)
 ggplot(aq3, aes(logit, fill = as.factor(y))) +
  geom_density(alpha = .3) +
  geom_vline(xintercept = 0, lty = 2) +
  labs(title = "Density graph of permissible ozone concetration",fill = "Permissible status, 1 permissible")
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

``` r
 ## Save predicted probabilities
 df <- data.frame(prob=predict(fit, type = "response"),y=aq3$y)
 ## Plot ROC curve
 ROCplot <- ggplot(df) + geom_roc(aes(d = y, m = prob), n.cuts = 0)+labs(title="ROC curve of y~Month+Temp")
 ROCplot
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-4.png)<!-- -->

``` r
 ## Calculate AUC
 calc_auc(ROCplot)$AUC
```

    ## [1] 0.8761468

``` r
# regression model to predict if ozone concentration is permissible by temperature and wind 
fit <- glm(y ~ Temp + Wind, data= aq3, family="binomial") 
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = y ~ Temp + Wind, family = "binomial", data = aq3)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.64599   0.04315   0.10854   0.31588   1.41843  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept) -3.29351    5.03102  -0.655  0.51270   
    ## Temp         0.01661    0.13443   0.124  0.90168   
    ## Wind         0.77855    0.28378   2.744  0.00608 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 52.876  on 115  degrees of freedom
    ## Residual deviance: 33.720  on 113  degrees of freedom
    ## AIC: 39.72
    ## 
    ## Number of Fisher Scoring iterations: 7

``` r
 ## interpret
 exp(coef(fit))
```

    ## (Intercept)        Temp        Wind 
    ##  0.03712315  1.01674640  2.17830449

``` r
  ## Confusion matrix: compare true to predicted condition
 aq3$prob1 <- predict(fit, type = "response")
 aq3$predicted <- ifelse(aq3$prob1 > .5, "permissible", "not permissible")
 table(true_condition = aq3$y, predicted_condition = aq3$predicted) %>% 
  addmargins
```

    ##               predicted_condition
    ## true_condition not permissible permissible Sum
    ##            0                 2           5   7
    ##            1                 1         108 109
    ##            Sum               3         113 116

``` r
  ## accuracy
  (2+108)/116
```

    ## [1] 0.9482759

``` r
  ## sensitivity TPR
  108/109
```

    ## [1] 0.9908257

``` r
  ## specificity TNR
  2/7
```

    ## [1] 0.2857143

``` r
  ## recall precision PPV
  108/111
```

    ## [1] 0.972973

``` r
 ## density 
 aq3$logit <- predict(fit)
 ggplot(aq3, aes(logit, fill = as.factor(y))) +
  geom_density(alpha = .3) +
  geom_vline(xintercept = 0, lty = 2) +
  labs(title = "Density graph of permissible ozone concetration",fill = "Permissible status, 1 permissible")
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-5.png)<!-- -->

``` r
 ## Save predicted probabilities
 df <- data.frame(prob=predict(fit, type = "response"),y=aq3$y)
 ## Plot ROC curve
 ROCplot <- ggplot(df) + geom_roc(aes(d = y, m = prob), n.cuts = 0)+labs(title="ROC curve of y~ Temp+Wind")
 ROCplot
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-6.png)<!-- -->

``` r
 ## Calculate AUC
 calc_auc(ROCplot)$AUC
```

    ## [1] 0.8912189

``` r
# regression model to predict if ozone concentration is permissible by Month, temperature and wind 
fit <- glm(y ~ Month + Temp + Wind, data= aq3, family="binomial") 
```

    ## Warning: glm.fit: fitted probabilities numerically 0 or 1 occurred

``` r
summary(fit)
```

    ## 
    ## Call:
    ## glm(formula = y ~ Month + Temp + Wind, family = "binomial", data = aq3)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.93743   0.00003   0.05434   0.17455   1.19108  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept)   -0.3880     5.2748  -0.074  0.94136   
    ## MonthJun       0.2431     2.2774   0.107  0.91500   
    ## MonthJul       2.8137     2.0818   1.352  0.17651   
    ## MonthAug       1.5336     2.0226   0.758  0.44831   
    ## MonthSep      20.5497  2393.3771   0.009  0.99315   
    ## Temp          -0.1656     0.1887  -0.877  0.38028   
    ## Wind           0.8438     0.3154   2.675  0.00748 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 52.876  on 115  degrees of freedom
    ## Residual deviance: 25.453  on 109  degrees of freedom
    ## AIC: 39.453
    ## 
    ## Number of Fisher Scoring iterations: 19

``` r
 ## interpret
 exp(coef(fit))
```

    ##  (Intercept)     MonthJun     MonthJul     MonthAug     MonthSep         Temp 
    ## 6.784011e-01 1.275157e+00 1.667218e+01 4.634795e+00 8.406936e+08 8.474136e-01 
    ##         Wind 
    ## 2.325087e+00

``` r
  ## Confusion matrix: compare true to predicted condition
 aq3$prob1 <- predict(fit, type = "response")
 aq3$predicted <- ifelse(aq3$prob1 > .5, "permissible", "not permissible")
 table(true_condition = aq3$y, predicted_condition = aq3$predicted) %>% 
  addmargins
```

    ##               predicted_condition
    ## true_condition not permissible permissible Sum
    ##            0                 4           3   7
    ##            1                 1         108 109
    ##            Sum               5         111 116

``` r
  ## accuracy
  (4+108)/116
```

    ## [1] 0.9655172

``` r
  ## sensitivity TPR
  108/109
```

    ## [1] 0.9908257

``` r
  ## specificity TNR
  4/7
```

    ## [1] 0.5714286

``` r
  ## recall precision PPV
  108/111
```

    ## [1] 0.972973

``` r
 ## density 
 aq3$logit <- predict(fit)
 ggplot(aq3, aes(logit, fill = as.factor(y))) +
  geom_density(alpha = .3) +
  geom_vline(xintercept = 0, lty = 2) +
  labs(title = "Density graph of permissible ozone concetration",fill = "Permissible status, 1 permissible")
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-7.png)<!-- -->

``` r
 ## Save predicted probabilities
 df <- data.frame(prob=predict(fit, type = "response"),y=aq3$y)
 ## Plot ROC curve
 ROCplot <- ggplot(df) + geom_roc(aes(d = y, m = prob), n.cuts = 0)+labs(title="ROC curve of y~ Month+Temp+Wind")
 ROCplot
```

![](Project-2_files/figure-gfm/unnamed-chunk-6-8.png)<!-- -->

``` r
 ## Calculate AUC
 calc_auc(ROCplot)$AUC
```

    ## [1] 0.9410223

Build a regression model to predict a binary response. Interpret the
coefficients and generate a ROC curve, calculate AUC.

1.  Controlling Wind, month is not a significant predictor of ozone
    permissible status. Wind is a significant predictor. Controlling
    month, for every 1 unit increase in wind speed, the odds of
    permissible ozone level changes by a factor of 2.48 (increase by
    148%). Accuracy is 96.6%, sensitivity is 99.1%, specificity is 57.1%
    and recall is 97.3%. AIC = 38.255. AUC = 0.926

2.  Controlling temperature, month is not a significant predictor of
    ozone permissible status. Temperature is a significant predictor.
    Controlling month, for every 1 unit increase in temperature, the
    odds of permissible ozone level changes by a factor of 0.757.
    Accuracy is 94.0%, sensitivity is 100%, specificity is 0% and recall
    is 0%. AIC = 52.088. AUC = 0.876

3.  Controlling temperature, wind is a significant predictor of ozone
    permissible status (p&lt;0.01). However, controlling wind,
    temperature is not a significant predictor. Controlling temperature,
    for every 1 unit increase in wind the odds of permissible ozone
    level changes by a factor of 2.18 (increase by 118%). Accuracy is
    94.8%, sensitivity is 99.1% , specificty is 28.6% and recall is
    89.1%. AIC = 39.72. AUC = 0.891

4.  Controlling temperature and month, wind is a significant predictor
    of ozone permissible status (p &lt; 0.01). Controlling temperature
    and month, for every 1 unit increase in wind, the odds of
    permissible ozone level changes by a factor of 2.33 (increase by
    133%). Accuracy is 96.6%, Sensitivity = 99.1%, specificity = 0.571,
    and recall is 97.3%. AIC = 39.453. AUC = 0.941

By AUC, a model with month, wind and temperature does a better job of
predicting if the ozone level is permissible or not. By AIC, a model
with month and wind fits better than the other models.

    ##        sysname        release        version       nodename        machine 
    ##      "Windows"       "10 x64"  "build 19042" "<U+C774><U+D61C><U+C815>"       "x86-64" 
    ##          login           user effective_user 
    ##        "hjlee"        "hjlee"        "hjlee"
