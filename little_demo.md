
``` r
knitr::opts_chunk$set(warning = FALSE, message = FALSE)
```

``` r
library(tidyverse)
```

# y axis by scales

``` r
p1 <-
  data.frame(pctg = runif(10, 0, 1)) %>%
  mutate(id = row_number() %>% as.factor()) %>%
  ggplot(aes(x = id, y = pctg)) +
  geom_col() +
  coord_flip() +
  scale_y_continuous(labels = scales::percent)
p1
```

![](little_demo_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

# label by scales

``` r
p2 <-
  p1 +
  geom_text(aes(label = scales::percent(pctg)), nudge_y = 0.1)
p2
```

![](little_demo_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

# tidy up

比如显而易见的 axis title 就可以删除，标注了数据就可以删除网格线。

``` r
p2 + 
  theme(
    axis.title = element_blank(),
    panel.grid = element_blank(), # 失去网格
    axis.text.x = element_blank() # 都有百分比了，x轴去掉
  ) +
  labs(
    title = "各id的占比"
  )
```

![](little_demo_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
# tidy up 的原则是删除 axis title 但是在 title 里面表示
```
