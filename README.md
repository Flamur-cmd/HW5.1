> library(dplyr)
> library(nycflights13)
> # Exercise 1: Which carrier has the worst average delays?
> flights |> 
+   group_by(carrier) |> 
+   summarize(avg_arr_delay = mean(arr_delay, na.rm = TRUE)) |> 
+   arrange(desc(avg_arr_delay))
# A tibble: 16 × 2
   carrier avg_arr_delay
   <chr>           <dbl>
 1 F9             21.9  
 2 FL             20.1  
 3 EV             15.8  
 4 YV             15.6  
 5 OO             11.9  
 6 MQ             10.8  
 7 WN              9.65 
 8 B6              9.46 
 9 9E              7.38 
10 UA              3.56 
11 US              2.13 
12 VX              1.76 
13 DL              1.64 
14 AA              0.364
15 HA             -6.92 
16 AS             -9.93 
>  Answer:
+ 
+ # The worst delays are with F9, averaging nearly 22 minutes late.
+ # AS and HA perform exceptionally well, because they are negative average delays
+ # which mean they often arrive early.
+ 
+ 
+ # Challenge: can you disentangle the effects of bad airports vs. bad carriers? Why/why not? 
+ # (Hint: think about flights |> group_by(carrier, dest) |> summarize(n()))
+  Answer:
+ 
+ # The worst delays are with F9, averaging nearly 22 minutes late.
+ # AS and HA perform exceptionally well, because they are negative average delays
+ # which mean they often arrive early.
+ 
+ 
+ # Challenge: can you disentangle the effects of bad airports vs. bad carriers? Why/why not? 
+ # (Hint: think about flights |> group_by(carrier, dest) |> summarize(n()))
+ 
+ flights |>
+   group_by(carrier, dest) |>
+   summarize(
+     avg_arr_delay = mean(arr_delay, na.rm = TRUE),
+     n = n()
+   ) |>
+   arrange(desc(avg_arr_delay))
Error: object 'Answer' not found
>  Answer:
+ 
+ # The worst delays are with F9, averaging nearly 22 minutes late.
+ # AS and HA perform exceptionally well, because they are negative average delays
+ # which mean they often arrive early.
+ 
+ 
+ # Challenge: can you disentangle the effects of bad airports vs. bad carriers? Why/why not? 
+ # (Hint: think about flights |> group_by(carrier, dest) |> summarize(n()))
+ 
+ flights |>
+   group_by(carrier, dest) |>
+   summarize(
+     avg_arr_delay = mean(arr_delay, na.rm = TRUE),
+     n = n()
+   ) |>
+   arrange(desc(avg_arr_delay))
Error: object 'Answer' not found
> flights |>
+   group_by(carrier, dest) |>
+   summarize(
+     avg_arr_delay = mean(arr_delay, na.rm = TRUE),
+     n = n()
+   ) |>
+   arrange(desc(avg_arr_delay))
`summarise()` has grouped output by 'carrier'. You can override using the `.groups`
argument.
# A tibble: 314 × 4
# Groups:   carrier [16]
   carrier dest  avg_arr_delay     n
   <chr>   <chr>         <dbl> <int>
 1 UA      STL           110       2
 2 OO      ORD           107       1
 3 OO      DTW            68.5     2
 4 UA      RDU            56       1
 5 EV      CAE            42.8   113
 6 EV      TYS            41.2   323
 7 EV      PBI            40.7     6
 8 EV      TUL            33.7   315
 9 EV      OKC            30.6   346
10 UA      JAC            29.9    23
# ℹ 304 more rows
# ℹ Use `print(n = ...)` to see more rows
> summary(model1)
Error: object 'model1' not found
> model1 <- lm(arr_delay ~ carrier + dest + origin + hour, data = flights)
> summary(model1)

Call:
lm(formula = arr_delay ~ carrier + dest + origin + hour, data = flights)

Residuals:
    Min      1Q  Median      3Q     Max 
 -98.58  -23.34   -9.59    8.40 1280.14 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept) -32.96601    2.80610 -11.748  < 2e-16 ***
carrierAA    -2.86023    0.52334  -5.465 4.62e-08 ***
carrierAS   -11.02584    1.87956  -5.866 4.46e-09 ***
carrierB6     5.10373    0.45057  11.327  < 2e-16 ***
carrierDL    -4.33183    0.46555  -9.305  < 2e-16 ***
carrierEV     9.46921    0.46575  20.331  < 2e-16 ***
carrierF9    13.40000    1.81825   7.370 1.71e-13 ***
carrierFL     9.29262    1.06536   8.723  < 2e-16 ***
carrierHA    -6.20824    3.32492  -1.867 0.061877 .  
carrierMQ     4.46882    0.48706   9.175  < 2e-16 ***
carrierOO     0.37235    8.11140   0.046 0.963386    
carrierUA    -1.52525    0.51485  -2.963 0.003052 ** 
carrierUS    -1.80008    0.58085  -3.099 0.001942 ** 
carrierVX     0.36240    0.79992   0.453 0.650521    
carrierWN     3.58824    0.71894   4.991 6.01e-07 ***
carrierYV     4.94612    1.95058   2.536 0.011222 *  
destACK      17.15233    3.83138   4.477 7.58e-06 ***
destALB      11.03898    3.48670   3.166 0.001546 ** 
destANC       4.82352   15.64165   0.308 0.757796    
destATL      24.24381    2.77710   8.730  < 2e-16 ***
destAUS      14.36640    2.88082   4.987 6.14e-07 ***
destAVL      12.88547    3.85978   3.338 0.000843 ***
destBDL       6.01659    3.49605   1.721 0.085258 .  
destBGR       6.02910    3.60074   1.674 0.094052 .  
destBHM      10.58520    3.83616   2.759 0.005793 ** 
destBNA      17.52626    2.81321   6.230 4.67e-10 ***
destBOS      13.51245    2.76570   4.886 1.03e-06 ***
destBQN      11.92323    3.10134   3.845 0.000121 ***
destBTV      12.44614    2.87476   4.329 1.50e-05 ***
destBUF      15.15688    2.81318   5.388 7.14e-08 ***
destBUR       8.54973    3.54905   2.409 0.015996 *  
destBWI      15.66788    2.95267   5.306 1.12e-07 ***
destBZN      28.50739    7.86123   3.626 0.000288 ***
destCAE      35.67707    5.05053   7.064 1.62e-12 ***
destCAK      20.04195    3.28078   6.109 1.00e-09 ***
destCHO       1.47987    6.99274   0.212 0.832397    
destCHS      15.90838    2.87232   5.539 3.05e-08 ***
destCLE      16.53510    2.82792   5.847 5.01e-09 ***
destCLT      19.69203    2.78609   7.068 1.58e-12 ***
destCMH      16.15323    2.86387   5.640 1.70e-08 ***
destCRW      14.78947    4.67271   3.165 0.001551 ** 
destCVG      19.54038    2.84869   6.859 6.93e-12 ***
destDAY      16.27023    2.99563   5.431 5.60e-08 ***
destDCA      18.43174    2.79507   6.594 4.28e-11 ***
destDEN      20.26831    2.80262   7.232 4.77e-13 ***
destDFW      15.83812    2.80273   5.651 1.60e-08 ***
destDSM      14.48594    3.35199   4.322 1.55e-05 ***
destDTW      17.37119    2.79098   6.224 4.85e-10 ***
destEGE      20.14312    4.09120   4.924 8.50e-07 ***
destEYW      28.85530   10.91788   2.643 0.008219 ** 
destFLL      18.93811    2.76870   6.840 7.93e-12 ***
destGRR      20.77498    3.19836   6.496 8.29e-11 ***
destGSO      15.57614    2.98302   5.222 1.77e-07 ***
destGSP      16.65871    3.16494   5.264 1.41e-07 ***
destHDN      23.05025   11.96186   1.927 0.053983 .  
destHNL      17.41786    3.58720   4.856 1.20e-06 ***
destHOU      17.18799    2.92788   5.870 4.35e-09 ***
destIAD      19.27114    2.81902   6.836 8.15e-12 ***
destIAH      18.96844    2.80190   6.770 1.29e-11 ***
destILM      -2.51631    5.03902  -0.499 0.617523    
destIND      16.04976    2.92532   5.486 4.10e-08 ***
destJAC      49.02393    9.89524   4.954 7.26e-07 ***
destJAX      15.91230    2.87229   5.540 3.03e-08 ***
destLAS      13.51461    2.80095   4.825 1.40e-06 ***
destLAX      13.19993    2.76905   4.767 1.87e-06 ***
destLEX     -20.80931   43.63994  -0.477 0.633476    
destLGB       3.68426    3.21610   1.146 0.251975    
destMCI      17.55684    2.93440   5.983 2.19e-09 ***
destMCO      16.79852    2.76494   6.076 1.24e-09 ***
destMDW      20.95719    2.89160   7.248 4.25e-13 ***
destMEM      17.67645    2.95357   5.985 2.17e-09 ***
destMHT      13.92358    3.10738   4.481 7.44e-06 ***
destMIA      17.32075    2.78442   6.221 4.96e-10 ***
destMKE      20.89352    2.88951   7.231 4.81e-13 ***
destMSN      19.89669    3.32226   5.989 2.11e-09 ***
destMSP      19.66840    2.80261   7.018 2.26e-12 ***
destMSY      15.47924    2.83380   5.462 4.70e-08 ***
destMTJ      20.99512   11.96160   1.755 0.079224 .  
destMVY      10.26463    4.06657   2.524 0.011598 *  
destMYR      14.01458    6.35215   2.206 0.027366 *  
destOAK       3.16476    3.68883   0.858 0.390931    
destOKC      21.39597    3.69298   5.794 6.89e-09 ***
destOMA      15.77929    3.15368   5.003 5.63e-07 ***
destORD      19.33195    2.77090   6.977 3.03e-12 ***
destORF      13.91588    2.98506   4.662 3.14e-06 ***
destPBI      19.79680    2.79367   7.086 1.38e-12 ***
destPDX      12.13079    2.98794   4.060 4.91e-05 ***
destPHL      23.71560    2.97600   7.969 1.61e-15 ***
destPHX      14.86205    2.82687   5.257 1.46e-07 ***
destPIT      15.82796    2.87670   5.502 3.76e-08 ***
destPSE      -1.65307    3.57323  -0.463 0.643633    
destPSP       4.56358   10.64762   0.429 0.668214    
destPVD      13.89647    3.59427   3.866 0.000111 ***
destPWM      14.45968    2.88522   5.012 5.40e-07 ***
destRDU      17.06673    2.79904   6.097 1.08e-09 ***
destRIC      19.72476    2.90136   6.798 1.06e-11 ***
destROC      15.39584    2.88122   5.344 9.12e-08 ***
destRSW      15.48575    2.83718   5.458 4.81e-08 ***
destSAN      14.31600    2.86717   4.993 5.95e-07 ***
destSAT      13.48178    3.22795   4.177 2.96e-05 ***
destSAV      17.66670    3.18753   5.542 2.99e-08 ***
destSBN       6.17725   14.04655   0.440 0.660104    
destSDF      17.37749    3.05549   5.687 1.29e-08 ***
destSEA      12.58590    2.85050   4.415 1.01e-05 ***
destSFO      16.31870    2.77490   5.881 4.09e-09 ***
destSJC       2.44911    3.64020   0.673 0.501078    
destSJU      15.24687    2.79912   5.447 5.13e-08 ***
destSLC      13.43825    2.88597   4.656 3.22e-06 ***
destSMF       9.85424    3.76744   2.616 0.008907 ** 
destSNA       4.57434    3.14932   1.452 0.146368    
destSRQ      17.61214    3.01640   5.839 5.26e-09 ***
destSTL      18.36024    2.84011   6.465 1.02e-10 ***
destSTT      18.91238    3.35651   5.635 1.76e-08 ***
destSYR      12.98437    2.93194   4.429 9.49e-06 ***
destTPA      19.14187    2.78742   6.867 6.56e-12 ***
destTUL      24.01711    3.75077   6.403 1.52e-10 ***
destTVC      16.34128    5.25209   3.111 0.001862 ** 
destTYS      19.96567    3.30215   6.046 1.48e-09 ***
destXNA      16.68384    3.09139   5.397 6.79e-08 ***
originJFK    -1.66203    0.28172  -5.900 3.65e-09 ***
originLGA    -2.18435    0.24795  -8.809  < 2e-16 ***
hour          1.69798    0.01693 100.285  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 43.55 on 327224 degrees of freedom
  (9430 observations deleted due to missingness)
Multiple R-squared:  0.04826,	Adjusted R-squared:  0.04791 
F-statistic: 137.1 on 121 and 327224 DF,  p-value: < 2.2e-16

> most_delayed <- flights |>
+   group_by(origin) |>
+   slice_max(dep_delay, n = 1, with_ties = FALSE) |>
+   select(
+     origin, year, month, day, carrier, flight, dep_delay, arr_delay,
+     dest, tailnum, sched_dep_time, dep_time, arr_time
+   )
> # Exercise 2: Find the flights most delayed on departure from each destination
> most_delayed <- flights |>
+   group_by(origin) |>
+   slice_max(dep_delay, n = 1, with_ties = FALSE) |>
+   select(
+     origin, year, month, day, carrier, flight, dep_delay, arr_delay,
+     dest, tailnum, sched_dep_time, dep_time, arr_time
+   )
> View(most_delayed)
> ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) +
+   geom_col(width = 0.6) +
+   geom_text(aes(label = paste0(dep_delay, " min")), vjust = -0.5, size = 5) +
+   labs(
+     title = "Most Extreme Departure Delay by NYC Airport (2013)",
+     x = "Origin Airport",
+     y = "Departure Delay (minutes)"
+   ) +
+   theme_minimal() +
+   theme(legend.position = "none")
Error in ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) : 
  could not find function "ggplot"
> ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) +
+   geom_col(width = 0.6) +
+   geom_text(aes(label = paste0(dep_delay, " min")), vjust = -0.5, size = 5) +
+   labs(
+     title = "Most Extreme Departure Delay by NYC Airport (2013)",
+     x = "Origin Airport",
+     y = "Departure Delay (minutes)"
+   ) +
+   theme_minimal() +
+   theme(legend.position = "none")
Error in ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) : 
  could not find function "ggplot"
> ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) +
+   geom_col(width = 0.6) +
+   geom_text(aes(label = paste0(dep_delay, " min")), vjust = -0.5, size = 5) +
+   labs(
+     title = "Most Extreme Departure Delay by NYC Airport (2013)",
+     x = "Origin Airport",
+     y = "Departure Delay (minutes)"
+   ) +
+   theme_minimal() +
+   theme(legend.position = "none")
Error in ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) : 
  could not find function "ggplot"
> library(ggplot)
Error in library(ggplot) : there is no package called ‘ggplot’
> install.packages(ggplot)
Error in install.packages : object 'ggplot' not found
> install.packages("ggplot")
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
Installing package into ‘C:/Users/KUKAJ/AppData/Local/R/win-library/4.4’
(as ‘lib’ is unspecified)
Warning in install.packages :
  package ‘ggplot’ is not available for this version of R

A version of this package for your version of R might be available elsewhere,
see the ideas at
https://cran.r-project.org/doc/manuals/r-patched/R-admin.html#Installing-packages
> library(ggplot)
Error in library(ggplot) : there is no package called ‘ggplot’
> install.packages("ggplot2")
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
Installing package into ‘C:/Users/KUKAJ/AppData/Local/R/win-library/4.4’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/ggplot2_3.5.1.zip'
Content type 'application/zip' length 5023219 bytes (4.8 MB)
downloaded 4.8 MB

package ‘ggplot2’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\KUKAJ\AppData\Local\Temp\Rtmp8mbMnB\downloaded_packages
> library(ggplot)
Error in library(ggplot) : there is no package called ‘ggplot’
> ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) +
+   geom_col(width = 0.6) +
+   geom_text(aes(label = paste0(dep_delay, " min")), vjust = -0.5, size = 5) +
+   labs(
+     title = "Most Extreme Departure Delay by NYC Airport (2013)",
+     x = "Origin Airport",
+     y = "Departure Delay (minutes)"
+   ) +
+   theme_minimal() +
+   theme(legend.position = "none")
Error in ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) : 
  could not find function "ggplot"
> ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) +
+   geom_col(width = 0.6) +
+   geom_text(aes(label = paste0(dep_delay, " min")), vjust = -0.5, size = 5) +
+   labs(
+     title = "Most Extreme Departure Delay by NYC Airport (2013)",
+     x = "Origin Airport",
+     y = "Departure Delay (minutes)"
+   ) +
+   theme_minimal() +
+   theme(legend.position = "none")
Error in ggplot(most_delayed, aes(x = origin, y = dep_delay, fill = origin)) : 
  could not find function "ggplot"
> Exercise 5: Explain what count() does in terms of dplyr verbs
Error: unexpected numeric constant in "Exercise 5"
> #Exercise 5: Explain what count() does in terms of dplyr verbs
> flights |> 
+   group_by(carrier) |> 
+   summarize(n = n())
# A tibble: 16 × 2
   carrier     n
   <chr>   <int>
 1 9E      18460
 2 AA      32729
 3 AS        714
 4 B6      54635
 5 DL      48110
 6 EV      54173
 7 F9        685
 8 FL       3260
 9 HA        342
10 MQ      26397
11 OO         32
12 UA      58665
13 US      20536
14 VX       5162
15 WN      12275
16 YV        601
> #  What does sort = TRUE do?
> flights |> count(carrier, sort = TRUE)
# A tibble: 16 × 2
   carrier     n
   <chr>   <int>
 1 UA      58665
 2 B6      54635
 3 EV      54173
 4 DL      48110
 5 AA      32729
 6 MQ      26397
 7 US      20536
 8 9E      18460
 9 WN      12275
10 VX       5162
11 FL       3260
12 AS        714
13 F9        685
14 YV        601
15 HA        342
16 OO         32
> # Answer:
> # It sorts the result in descending order of n — most frequent groups appear first.
>
 
