---
title: 'Weekly Exercises #5'
author: "Maya Hajny Fernandez"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
## ✓ tibble  3.0.5     ✓ dplyr   1.0.3
## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.8.1, GDAL 3.1.4, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(ggthemes)
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   year = col_double(),
##   month = col_double(),
##   service = col_character(),
##   departure_station = col_character(),
##   arrival_station = col_character(),
##   journey_time_avg = col_double(),
##   total_num_trips = col_double(),
##   avg_delay_all_departing = col_double(),
##   avg_delay_all_arriving = col_double(),
##   num_late_at_departure = col_double(),
##   num_arriving_late = col_double(),
##   delay_cause = col_character(),
##   delayed_number = col_double()
## )
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele.num = col_double(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = ""),
##   time_hr = col_double(),
##   dist_km = col_double(),
##   speed = col_double()
## )
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele = col_logical(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

```r
hbcu_all <- read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-02-02/hbcu_all.csv') %>% 
  clean_names()
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   Year = col_double(),
##   `Total enrollment` = col_double(),
##   Males = col_double(),
##   Females = col_double(),
##   `4-year` = col_double(),
##   `2-year` = col_double(),
##   `Total - Public` = col_double(),
##   `4-year - Public` = col_double(),
##   `2-year - Public` = col_double(),
##   `Total - Private` = col_double(),
##   `4-year - Private` = col_double(),
##   `2-year - Private` = col_double()
## )
```

```r
data_site <- 
  "https://www.macalester.edu/~dshuman1/data/112/2014-Q4-Trips-History-Data.rds" 
Trips <- readRDS(gzcon(url(data_site)))
Stations<-read_csv("http://www.macalester.edu/~dshuman1/data/112/DC-Stations.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   name = col_character(),
##   lat = col_double(),
##   long = col_double(),
##   nbBikes = col_double(),
##   nbEmptyDocks = col_double()
## )
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  


```r
enrollment_school_type <- hbcu_all %>% 
  select(year, total_public, total_private, males, females) %>% 
  pivot_longer(total_public:total_private,
               names_to = "school_type",
               values_to = "total_enrollment") %>% 
  mutate(school_type = str_remove(school_type, "s$")) %>% 
  ggplot(aes(x = year, 
             y = total_enrollment, color = school_type,)) + 
             geom_line() +
  labs(title="Total enrollment at HBCU's from 1980-2010 by school type", x = "", y="")

enrollment_school_type
```

![](05_exercises_files/figure-html/unnamed-chunk-1-1.png)<!-- -->


```r
ggplotly(enrollment_school_type)
```

```{=html}
<div id="htmlwidget-19d655a90a1c424490db" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-19d655a90a1c424490db">{"x":{"data":[{"x":[1976,1980,1982,1984,1986,1988,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015],"y":[65777,65340,62500,63403,61227,66083,70106,71488,74575,74659,73551,73999,72449,74493,74869,74495,75955,79902,80608,78631,77760,75893,74269,72708,77667,76265,77468,76963,74656,72866,71440,72028],"text":["year: 1976<br />total_enrollment:  65777<br />school_type: total_private","year: 1980<br />total_enrollment:  65340<br />school_type: total_private","year: 1982<br />total_enrollment:  62500<br />school_type: total_private","year: 1984<br />total_enrollment:  63403<br />school_type: total_private","year: 1986<br />total_enrollment:  61227<br />school_type: total_private","year: 1988<br />total_enrollment:  66083<br />school_type: total_private","year: 1990<br />total_enrollment:  70106<br />school_type: total_private","year: 1991<br />total_enrollment:  71488<br />school_type: total_private","year: 1992<br />total_enrollment:  74575<br />school_type: total_private","year: 1993<br />total_enrollment:  74659<br />school_type: total_private","year: 1994<br />total_enrollment:  73551<br />school_type: total_private","year: 1995<br />total_enrollment:  73999<br />school_type: total_private","year: 1996<br />total_enrollment:  72449<br />school_type: total_private","year: 1997<br />total_enrollment:  74493<br />school_type: total_private","year: 1998<br />total_enrollment:  74869<br />school_type: total_private","year: 1999<br />total_enrollment:  74495<br />school_type: total_private","year: 2000<br />total_enrollment:  75955<br />school_type: total_private","year: 2001<br />total_enrollment:  79902<br />school_type: total_private","year: 2002<br />total_enrollment:  80608<br />school_type: total_private","year: 2003<br />total_enrollment:  78631<br />school_type: total_private","year: 2004<br />total_enrollment:  77760<br />school_type: total_private","year: 2005<br />total_enrollment:  75893<br />school_type: total_private","year: 2006<br />total_enrollment:  74269<br />school_type: total_private","year: 2007<br />total_enrollment:  72708<br />school_type: total_private","year: 2008<br />total_enrollment:  77667<br />school_type: total_private","year: 2009<br />total_enrollment:  76265<br />school_type: total_private","year: 2010<br />total_enrollment:  77468<br />school_type: total_private","year: 2011<br />total_enrollment:  76963<br />school_type: total_private","year: 2012<br />total_enrollment:  74656<br />school_type: total_private","year: 2013<br />total_enrollment:  72866<br />school_type: total_private","year: 2014<br />total_enrollment:  71440<br />school_type: total_private","year: 2015<br />total_enrollment:  72028<br />school_type: total_private"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)","dash":"solid"},"hoveron":"points","name":"total_private","legendgroup":"total_private","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1976,1980,1982,1984,1986,1988,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015],"y":[156836,168217,165871,164116,162048,173672,187046,197847,204966,208197,206520,204726,200569,194674,198603,199826,199725,210083,218433,228096,231179,235875,234505,233807,235824,246595,249146,246685,237782,230325,222876,221360],"text":["year: 1976<br />total_enrollment: 156836<br />school_type: total_public","year: 1980<br />total_enrollment: 168217<br />school_type: total_public","year: 1982<br />total_enrollment: 165871<br />school_type: total_public","year: 1984<br />total_enrollment: 164116<br />school_type: total_public","year: 1986<br />total_enrollment: 162048<br />school_type: total_public","year: 1988<br />total_enrollment: 173672<br />school_type: total_public","year: 1990<br />total_enrollment: 187046<br />school_type: total_public","year: 1991<br />total_enrollment: 197847<br />school_type: total_public","year: 1992<br />total_enrollment: 204966<br />school_type: total_public","year: 1993<br />total_enrollment: 208197<br />school_type: total_public","year: 1994<br />total_enrollment: 206520<br />school_type: total_public","year: 1995<br />total_enrollment: 204726<br />school_type: total_public","year: 1996<br />total_enrollment: 200569<br />school_type: total_public","year: 1997<br />total_enrollment: 194674<br />school_type: total_public","year: 1998<br />total_enrollment: 198603<br />school_type: total_public","year: 1999<br />total_enrollment: 199826<br />school_type: total_public","year: 2000<br />total_enrollment: 199725<br />school_type: total_public","year: 2001<br />total_enrollment: 210083<br />school_type: total_public","year: 2002<br />total_enrollment: 218433<br />school_type: total_public","year: 2003<br />total_enrollment: 228096<br />school_type: total_public","year: 2004<br />total_enrollment: 231179<br />school_type: total_public","year: 2005<br />total_enrollment: 235875<br />school_type: total_public","year: 2006<br />total_enrollment: 234505<br />school_type: total_public","year: 2007<br />total_enrollment: 233807<br />school_type: total_public","year: 2008<br />total_enrollment: 235824<br />school_type: total_public","year: 2009<br />total_enrollment: 246595<br />school_type: total_public","year: 2010<br />total_enrollment: 249146<br />school_type: total_public","year: 2011<br />total_enrollment: 246685<br />school_type: total_public","year: 2012<br />total_enrollment: 237782<br />school_type: total_public","year: 2013<br />total_enrollment: 230325<br />school_type: total_public","year: 2014<br />total_enrollment: 222876<br />school_type: total_public","year: 2015<br />total_enrollment: 221360<br />school_type: total_public"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)","dash":"solid"},"hoveron":"points","name":"total_public","legendgroup":"total_public","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":46.027397260274},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Total enrollment at HBCU's from 1980-2010 by school type","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1974.05,2016.95],"tickmode":"array","ticktext":["1980","1990","2000","2010"],"tickvals":[1980,1990,2000,2010],"categoryorder":"array","categoryarray":["1980","1990","2000","2010"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[51831.05,258541.95],"tickmode":"array","ticktext":["100000","150000","200000","250000"],"tickvals":[100000,150000,200000,250000],"categoryorder":"array","categoryarray":["100000","150000","200000","250000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"school_type","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"10f31ad044a6":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"10f31ad044a6","visdat":{"10f31ad044a6":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```



```r
rent_event <- Trips %>% 
  mutate(week_day = wday(sdate, 
            label = TRUE)) %>% 
  ggplot(aes(y=week_day)) +
  geom_bar()+
   labs(x = "Events", 
       y = "", 
       title = "Rental Events by Day of the Week")

rent_event
```

![](05_exercises_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


```r
ggplotly(rent_event)
```

```{=html}
<div id="htmlwidget-963df5db53c1c34c52e6" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-963df5db53c1c34c52e6">{"x":{"data":[{"orientation":"v","width":[84095,97432,95568,95091,98918,98244,84415],"base":[0.55,1.55,2.55,3.55,4.55,5.55,6.55],"x":[42047.5,48716,47784,47545.5,49459,49122,42207.5],"y":[0.9,0.9,0.9,0.9,0.9,0.9,0.9],"text":["count: 84095<br />week_day: 0.9","count: 97432<br />week_day: 0.9","count: 95568<br />week_day: 0.9","count: 95091<br />week_day: 0.9","count: 98918<br />week_day: 0.9","count: 98244<br />week_day: 0.9","count: 84415<br />week_day: 0.9"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":28.4931506849315},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Rental Events by Day of the Week","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-4945.9,103863.9],"tickmode":"array","ticktext":["0","25000","50000","75000","100000"],"tickvals":[0,25000,50000,75000,100000],"categoryorder":"array","categoryarray":["0","25000","50000","75000","100000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Events","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,7.6],"tickmode":"array","ticktext":["Sun","Mon","Tue","Wed","Thu","Fri","Sat"],"tickvals":[1,2,3,4,5,6,7],"categoryorder":"array","categoryarray":["Sun","Mon","Tue","Wed","Thu","Fri","Sat"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"10f348e494ef":{"y":{},"type":"bar"}},"cur_data":"10f348e494ef","visdat":{"10f348e494ef":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```


2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
cum_depart <- small_trains %>% 
  filter(service %in% c("International")) %>% 
  group_by(departure_station, year) %>% 
  summarize(yearly_depart = sum(total_num_trips)) %>% 
  mutate(cumsum_depart = cumsum(yearly_depart))
```

```
## `summarise()` has grouped output by 'departure_station'. You can override using the `.groups` argument.
```

```r
cum_depart
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["departure_station"],"name":[1],"type":["chr"],"align":["left"]},{"label":["year"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["yearly_depart"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["cumsum_depart"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"FRANCFORT","2":"2015","3":"8220","4":"8220"},{"1":"FRANCFORT","2":"2016","3":"4104","4":"12324"},{"1":"FRANCFORT","2":"2017","3":"12222","4":"24546"},{"1":"GENEVE","2":"2015","3":"16572","4":"16572"},{"1":"GENEVE","2":"2016","3":"15486","4":"32058"},{"1":"GENEVE","2":"2017","3":"15642","4":"47700"},{"1":"ITALIE","2":"2015","3":"6702","4":"6702"},{"1":"ITALIE","2":"2016","3":"5346","4":"12048"},{"1":"ITALIE","2":"2017","3":"6498","4":"18546"},{"1":"LAUSANNE","2":"2015","3":"7866","4":"7866"},{"1":"LAUSANNE","2":"2016","3":"7752","4":"15618"},{"1":"LAUSANNE","2":"2017","3":"9618","4":"25236"},{"1":"PARIS EST","2":"2015","3":"17508","4":"17508"},{"1":"PARIS EST","2":"2016","3":"18594","4":"36102"},{"1":"PARIS EST","2":"2017","3":"22794","4":"58896"},{"1":"PARIS LYON","2":"2015","3":"40956","4":"40956"},{"1":"PARIS LYON","2":"2016","3":"35526","4":"76482"},{"1":"PARIS LYON","2":"2017","3":"40362","4":"116844"},{"1":"STUTTGART","2":"2015","3":"7770","4":"7770"},{"1":"STUTTGART","2":"2016","3":"10080","4":"17850"},{"1":"STUTTGART","2":"2017","3":"10242","4":"28092"},{"1":"ZURICH","2":"2015","3":"12342","4":"12342"},{"1":"ZURICH","2":"2016","3":"11286","4":"23628"},{"1":"ZURICH","2":"2017","3":"9372","4":"33000"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


```r
depart_animate <- cum_depart %>% 
  ggplot(aes(x = year, 
             y = cumsum_depart,
             color = departure_station)) +
  geom_line() +
  geom_text(aes(label = departure_station)) +
  labs(title = "", 
       x = "",
       y = "",
       color = "departure_station") +
  theme(legend.position = "top",
        legend.title = element_blank()) +
  transition_reveal(year)


animate(depart_animate, duration = 20)

anim_save("depart.gif")
```

```r
knitr::include_graphics("depart.gif")
```

![](depart.gif)<!-- -->


## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
harvest_anim <- garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0, cum_har_lbs = 0)) %>% 
  group_by(variety) %>% 
  mutate(cum_har_lbs = cumsum(daily_harvest_lb)) %>% 
  ggplot(aes(x = date, 
             y = cum_har_lbs, 
             fill = fct_reorder(variety, daily_harvest_lb, sum))) +
  geom_area() +
  transition_reveal(date)

animate(harvest_anim, duration = 20)

anim_save("harvest.gif")
```


```r
knitr::include_graphics("harvest.gif")
```

![](harvest.gif)<!-- -->


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  

```r
mallorca_map_7 <- get_stamenmap(
    bbox = c(left = 2.2891, bottom = 39.5006, right = 2.6228, top = 39.6820), 
    maptype = "terrain",
    zoom = 12
)

mallorca_map_7_anim <- ggmap(mallorca_map_7) +
  geom_path(data = mallorca_bike_day7, 
             aes(x = lon, y = lat, color = ele),
             size = .5) +
  geom_point(data = mallorca_bike_day7,
             aes(x = lon, y = lat),
             size = .5, color = "red") +
  scale_color_viridis_c() +
  theme_map() +
  theme(legend.background = element_blank()) +
  labs(title = "", 
       subtitle = "time: {frame_along}",
       x = "",
       y = "") +
  transition_reveal(time) 

animate(mallorca_map_7_anim, duration = 20)

anim_save("mallorca_7.gif")
```



```r
knitr::include_graphics("mallorca_7.gif")
```

![](mallorca_7.gif)<!-- -->
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
panama <- 
  bind_rows(panama_bike, panama_run, panama_swim)

panama_map <- get_stamenmap(
    bbox = c(left = -79.5747, bottom = 8.9052, right = -79.5050, top = 8.9923), 
    maptype = "terrain",
    zoom = 13
)

panama_map_anim <- ggmap(panama_map) +
  geom_path(data = panama, 
             aes(x = lon, y = lat),
             size = .5) +
  geom_point(data = panama,
             aes(x = lon, y = lat, color = event),
             size = 2) +
  theme_map() +
  theme(legend.background = element_blank()) +
  labs(title = "", 
      subtitle = "time: {frame_along}",
      x = "",
      y = "") +
  transition_reveal(time) 

animate(panama_map_anim,  duration = 20)

anim_save("panama.gif")
```



```r
knitr::include_graphics("panama.gif")
```

![](panama.gif)<!-- -->
  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  

```r
cum_covid <- covid19 %>% 
  group_by(state) %>% 
  mutate(seven_day_lag = lag(cases, n = 7, order_by = date)) %>% 
  replace_na(list(seven_day_lag = 0)) %>% 
  mutate(newcases = cases - seven_day_lag) %>% 
  filter(cases>=20)

covid_anim <- cum_covid %>% 
  ggplot(aes(x = cases, y = newcases, group = state)) +
  scale_y_log10(labels = scales::comma) +
  scale_x_log10(labels = scales::comma) +
  geom_path() +
  geom_point(color = "red") +
  geom_text(aes(label = state), check_overlap = TRUE, color = "blue") +
  theme(legend.position = 0) +
  labs(title = "Cumulative and new cases over time", 
      subtitle = "date: {frame_along}",
       y = "New Cases", 
       x = "Cumulative cases ") +
  transition_reveal(date)

animate(covid_anim, nframes = 200, duration = 30)

anim_save("covidcases.gif")
```
  

  

```r
knitr::include_graphics("covidcases.gif")
```

![](covidcases.gif)<!-- -->

  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
states_map <- map_data("state")
```



```r
 covid_with_10000 <-
  covid19 %>% 
  group_by(state, date) %>% 
  summarize(sum_covid = max(cases)) %>% 
  mutate(new_state = str_to_lower(state)) %>% 
  left_join(census_pop_est_2018, by = c("new_state" = "state")) %>% 
  mutate(cases_per_ten = (sum_covid/est_pop_2018)*10000) %>% 
  mutate(day_of_week = wday(date, 
            label = TRUE,
            abbr = TRUE,
            week_start = getOption("lubridate.week.start", 7))) %>% 
  filter(day_of_week == "Fri")
```

```
## `summarise()` has grouped output by 'state'. You can override using the `.groups` argument.
```

```r
states_map <- map_data("state")

covid_10 <- covid_with_10000 %>% 
  ggplot(aes(fill = cases_per_ten)) +
  geom_map(map = states_map,
           aes(group = date, map_id = new_state)) +
  scale_fill_distiller(palette = "YlGnBu", 
                       direction = 1,
                       labels = scales::comma_format()) +
  expand_limits(x = states_map$long, y = states_map$lat) + 
  theme_map()  +
  labs(title = "Most Recent Cumulative Cases per 10,000 people", 
       subtitle = "date: {frame_time}") +
  transition_time(date)

animate(covid_10, nframes = 200, duration = 30)
```

![](05_exercises_files/figure-html/unnamed-chunk-17-1.gif)<!-- -->

```r
anim_save("covid10.gif")
```


  

```r
knitr::include_graphics("covid10.gif")
```

![](covid10.gif)<!-- -->

## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
