> # This loads the dataset
> flights
# A tibble: 336,776 × 19
    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
 1  2013     1     1      517            515         2      830            819
 2  2013     1     1      533            529         4      850            830
 3  2013     1     1      542            540         2      923            850
 4  2013     1     1      544            545        -1     1004           1022
 5  2013     1     1      554            600        -6      812            837
 6  2013     1     1      554            558        -4      740            728
 7  2013     1     1      555            600        -5      913            854
 8  2013     1     1      557            600        -3      709            723
 9  2013     1     1      557            600        -3      838            846
10  2013     1     1      558            600        -2      753            745
# ℹ 336,766 more rows
# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
#   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
#   minute <dbl>, time_hour <dttm>
# ℹ Use `print(n = ...)` to see more rows
> flights |> 
+   group_by(carrier) |> 
+   summarize(avg_delay = mean(arr_delay, na.rm = TRUE)) |> 
+   arrange(desc(avg_delay))
# A tibble: 16 × 2
   carrier avg_delay
   <chr>       <dbl>
 1 F9         21.9  
 2 FL         20.1  
 3 EV         15.8  
 4 YV         15.6  
 5 OO         11.9  
 6 MQ         10.8  
 7 WN          9.65 
 8 B6          9.46 
 9 9E          7.38 
10 UA          3.56 
11 US          2.13 
12 VX          1.76 
13 DL          1.64 
14 AA          0.364
15 HA         -6.92 
16 AS         -9.93 
> flights |> 
+   group_by(carrier, dest) |> 
+   summarize(n(), avg_delay = mean(dep_delay, na.rm = TRUE)) |> 
+   arrange(desc(avg_delay))
`summarise()` has grouped output by 'carrier'. You can override using the `.groups`
argument.
# A tibble: 314 × 4
# Groups:   carrier [16]
   carrier dest  `n()` avg_delay
   <chr>   <chr> <int>     <dbl>
 1 UA      STL       2      77.5
 2 OO      ORD       1      67  
 3 OO      DTW       2      61  
 4 UA      RDU       1      60  
 5 EV      PBI       6      48.7
 6 EV      TYS     323      41.8
 7 EV      CAE     113      36.7
 8 EV      TUL     315      34.9
 9 9E      BGR       1      34  
10 WN      MSY     298      33.4
# ℹ 304 more rows
# ℹ Use `print(n = ...)` to see more rows
> flights |> 
+   group_by(dest) |> 
+   filter(dep_delay == max(dep_delay, na.rm = TRUE))
# A tibble: 104 × 19
# Groups:   dest [104]
    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
 1  2013     1     1      848           1835       853     1001           1950
 2  2013     1     1     2343           1724       379      314           1938
 3  2013     1     2     1244            900       224     1431           1104
 4  2013     1     9      641            900      1301     1242           1530
 5  2013     1    10     1121           1635      1126     1239           1810
 6  2013     1    20     2347           1936       251      230           2208
 7  2013     1    24     2051           1522       329     2307           1727
 8  2013     1    25      123           2000       323      229           2101
 9  2013    11    22     2013           1905        68     2224           2131
10  2013    11    24     2026           2035        -9     2227           2249
# ℹ 94 more rows
# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
#   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
#   minute <dbl>, time_hour <dttm>
# ℹ Use `print(n = ...)` to see more rows
Warning message:
There was 1 warning in `filter()`.
ℹ In argument: `dep_delay == max(dep_delay, na.rm = TRUE)`.
ℹ In group 52: `dest = "LGA"`.
Caused by warning in `max()`:
! no non-missing arguments to max; returning -Inf 
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
> df <- tibble(
+   x = 1:5,
+   y = c("a", "b", "a", "a", "b"),
+   z = c("K", "K", "L", "L", "K")
+ )
> # A tibble: 2 × 2
> y     mean_x
Error: unexpected symbol in "y     mean_x"
> 2 b       3.5
Error: unexpected symbol in "2 b"
> # A tibble: 2 × 2
> y     mean_x
Error: unexpected symbol in "y     mean_x"
> <chr>  <dbl>
Error: unexpected '<' in "<"
> <chr>  <dbl>
Error: unexpected '<' in "<"
> df |>
+   group_by(y) |>
+   summarize(mean_x = mean(x))
# A tibble: 2 × 2
  y     mean_x
  <chr>  <dbl>
1 a       2.67
2 b       3.5 
> 2 b        3.5 
Error: unexpected symbol in "2 b"
> df |>
+   group_by(y, z) |>
+   summarize(mean_x = mean(x))
`summarise()` has grouped output by 'y'. You can override using the `.groups`
argument.
# A tibble: 3 × 3
# Groups:   y [2]
  y     z     mean_x
  <chr> <chr>  <dbl>
1 a     K        1  
2 a     L        3.5
3 b     K        3.5
> 3 b     K          3.5
Error: unexpected symbol in "3 b"
> # A tibble: 4 × 3
> # Groups:   y [2]
> y     z     mean_x
Error: unexpected symbol in "y     z"
> df |>
+   group_by(y, z) |>
+   summarize(mean_x = mean(x), .groups = "drop")
# A tibble: 3 × 3
  y     z     mean_x
  <chr> <chr>  <dbl>
1 a     K        1  
2 a     L        3.5
3 b     K        3.5
> df |>
+   group_by(y, z) |>
+   summarize(mean_x = mean(x))
`summarise()` has grouped output by 'y'. You can override using the `.groups`
argument.
# A tibble: 3 × 3
# Groups:   y [2]
  y     z     mean_x
  <chr> <chr>  <dbl>
1 a     K        1  
2 a     L        3.5
3 b     K        3.5
> df |>
+   group_by(y, z) |>
+   mutate(mean_x = mean(x))
# A tibble: 5 × 4
# Groups:   y, z [3]
      x y     z     mean_x
  <int> <chr> <chr>  <dbl>
1     1 a     K        1  
2     2 b     K        3.5
3     3 a     L        3.5
4     4 a     L        3.5
5     5 b     K        3.5
