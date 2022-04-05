---
title: 'Weekly Exercises #5'
author: "Ellery Island"
output:
  html_document:
    keep_md: yes
    toc: yes
    toc_float: yes
    df_print: paged
    code_download: yes
---





```r
library(tidyverse)     # for data cleaning and plotting
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(gifski)        # need the library for creating gifs but don't need to load each time
#library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels and alt text.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
breed_traits <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2022/2022-02-01/breed_traits.csv')
```



```r
dog_graph<- ggplot(breed_traits,
       aes(x= `Shedding Level`, 
           y = `Coat Grooming Frequency`, 
           color = `Coat Length`))+
  geom_jitter(width = 0.3)+
  labs(title = "The Shedding and Maintenance of Different Coat Lengths")+
  theme_light() +
  scale_color_manual(values = c("Long" = "darkslategray3",
                                "Short" ="salmon",
                                "Medium" = "magenta1",
                                "Plot Hounds" = "gray"))+
  theme(text = element_text(family = "Times New Roman"))

ggplotly(dog_graph)
```

```{=html}
<div id="htmlwidget-ce7e199b5336c33af97a" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-ce7e199b5336c33af97a">{"x":{"data":[{"x":[0.830946535570547,1.19025350422598,1.07023558192886,2.27437830804847,1.95715769343078,2.95927472636104,2.83426648657769,1.1544004177209,0.988299696333706,2.03544074045494,2.89941088026389,2.73255534432828,0.932358727324754,2.23079530303366,3.18923332127742,2.91125129736029,4.12959198215976,2.74070198549889,1.70110063804314,0.783116588555276,2.93559986497276,1.16244496004656,1.0849262860138,2.2285780465696,1.88825890352018,0.785179202258587,1.75742846359499,0.988357975846156,2.88757700272836],"y":[4.11846539415419,5.33508336395025,4.34503695443273,2.86550053711981,2.82067142464221,3.14283033013344,4.37480949517339,4.03768852576613,4.61796455532312,4.03984137102962,2.81484554000199,4.00681849941611,2.82192902266979,4.15485374461859,3.28646139074117,3.21796222496778,3.61449476201087,3.09651116486639,3.12853794861585,3.91503673642874,3.76543385051191,4.6205666154623,3.7539789846167,1.67866349481046,2.04424265306443,0.720674218609929,3.83014912344515,3.8795758575201,2.6620704356581],"text":["Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 5<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 5<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 4<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 5<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 1<br />Coat Length: Long","Shedding Level: 2<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Long","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Long"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(121,205,205,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(121,205,205,1)"}},"hoveron":"points","name":"Long","legendgroup":"Long","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[3.74583180411719,3.98169606602751,3.05128218652681,4.13172103823163,2.03083132472821,2.8458147293888,5.04764696713537,2.78246899126098,2.87072139400989,3.11547066257335,3.02612646454945,3.28716689273715,3.29348545507528,2.89511888022535,3.13563319835812,3.24095087125897,2.08543531605974,0.943397880578414,2.26851979834028,3.12905336678959,3.27621586541645,3.20898704943247,3.23229663879611,2.95104774255306,1.97774332100526,3.20998154170811,3.29128389498219,2.73535533193499,2.97309615206905,1.08560468903743,2.86715062307194,2.82737775435671,0.704529161797836,3.1926724950783,3.20478781275451,3.10439751218073,2.79931128420867,2.24222893994302,3.15951142343692,2.94705441067927,2.92261597565375,2.82887468584813,1.98088413425721,3.01146733467467,2.85553919607773,3.1145634457469,2.06229222021066,2.74986557364464,2.85420599151403,1.00774624226615,2.91838231366128,2.92708728122525,3.95253416565247,1.19335255520418,1.07286854251288,3.27835134258494,1.07960301418789,2.91606239131652,2.92772059771232,0.920734743680805,3.03910401617177,1.02958428892307,2.78969219508581,3.13104789610952,4.05439472147264,2.77444485425949,3.2871825219132,1.75714116045274,2.06841573119164,3.25398234589957,0.970300700888038,1.9882749398239,2.96429956513457,2.03874503672123,2.92037101644091,3.10210990724154,3.19262026799843,2.89111413457431,1.77176219415851],"y":[1.7148963181302,1.71074005514383,2.27073668856174,2.36126874703914,1.69487496390939,3.60529916491359,3.39156202729791,1.83982054833323,3.22228767480701,2.60793137811124,2.09658022299409,3.15108557585627,2.84351011868566,2.93366716373712,3.14266686700284,2.27709571216255,2.99024623334408,4.30089080668986,1.84918806385249,1.61444901507348,2.75591258909553,2.08827733602375,4.25918402802199,1.72618066463619,1.67644679974765,1.81423222180456,3.2451069559902,3.16377339661121,2.66714768260717,1.92064069304615,1.68890135027468,2.14682507123798,2.96230354961008,4.08793221171945,2.74243885315955,1.83083814512938,2.0346561819315,2.92377955913544,1.99091059677303,1.64191850982606,1.96811341010034,2.2068973261863,3.01612093411386,2.23483745679259,1.60748317074031,2.65175020415336,1.12147816866636,3.75833687577397,1.76292035095394,2.83734999895096,1.92411114536226,2.85428766719997,2.70218176264316,3.00019242223352,2.61080177016556,2.85626886542887,3.72408021166921,0.901211385428905,2.18722694404423,2.38350723050535,1.69818460624665,2.70488297548145,2.30825256388634,2.30605567563325,1.63166461717337,1.10176602862775,2.07378737721592,3.06246034409851,1.93795053381473,2.61061536110938,3.20876867771149,1.81753227226436,2.23535495884717,2.72621335294098,2.10985255427659,3.04671781919897,2.0261938277632,1.71199415400624,1.64311308264732],"text":["Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 5<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 4<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 4<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Medium","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Medium"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(255,0,255,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(255,0,255,1)"}},"hoveron":"points","name":"Medium","legendgroup":"Medium","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[0.00449297893792389],"y":[0.114639317058027],"text":"Shedding Level: 0<br />Coat Grooming Frequency: 0<br />Coat Length: Plott Hounds","type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(127,127,127,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(127,127,127,1)"}},"hoveron":"points","name":"Plott Hounds","legendgroup":"Plott Hounds","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[3.83053331179544,2.92111331359483,3.23294852413237,2.93689184971154,2.74698572242632,3.01748431683518,1.96728433892131,4.07911013802513,2.03350468804128,2.78541201227345,4.02708166735247,1.73750985432416,1.96161111635156,3.07509004818276,3.89302210034803,3.22189643452875,2.01907307417132,3.02971142772585,2.1585144024808,2.89099537055008,3.03457730356604,3.00629909592681,2.86754243778996,2.70841365186498,2.96767607093789,4.22710064533167,2.79042371967807,3.05859969095327,2.78351887674071,1.7621242204681,3.06857454716228,1.11426646653563,3.29686109307222,2.8645388119854,4.29930182183161,2.80898450254463,2.7702404001262,3.16635773973539,1.1870365510229,2.26922278436832,2.02595146647654,2.97332562818192,3.08387136007659,1.99042406957597,2.91554392771795,3.72913669920526,2.26256799902767,3.18618448083289,2.28613787875511,2.87119394950569,3.18983422955498,3.28780065332539,1.81379198543727,3.19717509252951,3.77539006192237,2.94898979128338,2.99436990218237,3.19095944250002,0.807133536506444,3.03816879400983,1.15394455422647,1.83852468044497,1.16377787166275,1.80045888633467,3.12500958507881,3.06310868756846,1.7349813115783,2.01015042299405,2.96622890881263,3.93694303785451,2.98744880394079,2.73364166705869,3.20825353804976,1.94696494881064,3.14667702340521,2.27888203132898,0.991738087963313,2.70722676012665,4.02661565127783,2.1975790197961,3.12770210620947,2.96113348994404,2.71483015562408,1.96709060240537,3.21208213604987,3.15317780566402],"y":[1.88561727609485,0.869423059187829,2.64657655544579,1.75291617419571,0.721915111504495,2.21616571005434,1.88057697042823,1.7115722598508,1.83798486087471,0.779048293828964,0.665765244141221,2.12269398551434,1.32124446257949,3.18871671054512,1.71527324598283,0.896724480576813,0.760197146423161,2.14115883558989,2.72723260186613,1.68777698166668,2.01092748325318,2.65237528737634,2.38542333766818,1.7778739720583,1.79757284410298,2.14720842204988,2.14030343480408,1.07389278430492,0.87945115417242,1.24266396723688,0.607812298648059,3.3059868728742,1.84082044456154,1.34652094226331,1.06177504640073,1.74870890174061,2.03654479961842,0.662862402386963,2.12333932593465,2.3155733294785,1.13917261827737,2.17179294768721,1.86238277032971,0.666633486934006,2.83473695050925,1.00418676808476,2.14289877023548,1.7051892047748,0.875733496621251,1.85515431668609,1.87977452296764,2.25173050705344,2.08811431750655,1.78992322161794,2.92747089862823,1.85668066181242,1.94587549697608,2.35797082446516,0.623327715322375,2.19589769039303,1.18424013946205,1.77366608865559,1.87666011564434,2.22156532779336,2.13716136440635,0.998657514154911,1.01220706608146,0.847992171905935,1.72295192088932,1.7436748707667,1.35107290539891,1.25224699769169,0.764112672023475,1.26586714535952,3.15179544594139,1.03081776723266,1.11301353611052,1.75408360939473,1.91146211065352,0.631135506182909,1.13400562610477,1.21412528939545,1.07001518569887,1.8367947191,1.31322895679623,2.01620091143996],"text":["Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 3<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 1<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 4<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 2<br />Coat Grooming Frequency: 2<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 1<br />Coat Length: Short","Shedding Level: 3<br />Coat Grooming Frequency: 2<br />Coat Length: Short"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(250,128,114,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(250,128,114,1)"}},"hoveron":"points","name":"Short","legendgroup":"Short","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":31.4155251141553},"plot_bgcolor":"rgba(255,255,255,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":14.6118721461187},"title":{"text":"The Shedding and Maintenance of Different Coat Lengths","font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.247664720471948,5.29980466654524],"tickmode":"array","ticktext":["0","1","2","3","4","5"],"tickvals":[0,1,2,3,4,5],"categoryorder":"array","categoryarray":["0","1","2","3","4","5"],"nticks":null,"ticks":"outside","tickcolor":"rgba(179,179,179,1)","ticklen":3.65296803652968,"tickwidth":0.33208800332088,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"Times New Roman","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(222,222,222,1)","gridwidth":0.33208800332088,"zeroline":false,"anchor":"y","title":{"text":"Shedding Level","font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.146382885286585,5.59610556629486],"tickmode":"array","ticktext":["0","2","4"],"tickvals":[0,2,4],"categoryorder":"array","categoryarray":["0","2","4"],"nticks":null,"ticks":"outside","tickcolor":"rgba(179,179,179,1)","ticklen":3.65296803652968,"tickwidth":0.33208800332088,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"Times New Roman","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(222,222,222,1)","gridwidth":0.33208800332088,"zeroline":false,"anchor":"x","title":{"text":"Coat Grooming Frequency","font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":"transparent","line":{"color":"rgba(179,179,179,1)","width":0.66417600664176,"linetype":"solid"},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":11.689497716895},"title":{"text":"Coat Length","font":{"color":"rgba(0,0,0,1)","family":"Times New Roman","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"7f084caef42":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"7f084caef42","visdat":{"7f084caef42":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

```r
library(gardenR)
library(geomtextpath)
data(garden_harvest)

garden_harvest_new <- garden_harvest%>%
  mutate(Vegetable = str_to_title(vegetable))%>%
  select(Vegetable, weight, date)%>%
  group_by(date, Vegetable)%>%
  summarize(total = sum(weight))%>%
  group_by(Vegetable) %>%
  mutate(cum_weight = cumsum(total))%>%
  filter(Vegetable %in% c("Lettuce", "Kale", "Spinach", "Swiss Chard")) 
  
garden_graph <- ggplot(garden_harvest_new, aes(x = date, y = cum_weight, color = Vegetable, label = Vegetable))+
    geom_line(size = .6, se = FALSE) +
    geom_textline(size = 4, fontface = "bold", vjust = 0, hjust = "xmax", text_smoothing = 35) +
    scale_color_manual(values = c("Kale" = "deepskyblue4",
                                "Lettuce" ="orangered1",
                                "Spinach" = "cadetblue3",
                                "Swiss Chard" = "goldenrod2"))+
    theme(text = element_text(family = "Avenir"))+
    theme(legend.position = "none")+
    labs(title = "Cumulative Harvest of Leafy Greens", 
         x = NULL, 
         y = NULL) +
    theme(panel.grid.major.x = element_blank(), 
        panel.grid.minor.x = element_blank(),
        panel.background = element_blank(),
        panel.grid.major.y = element_line(size = .1, color = "gray85" ))
 
ggplotly(garden_graph)
```

```{=html}
<div id="htmlwidget-5c8a4469e0e7c66cb332" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-5c8a4469e0e7c66cb332">{"x":{"data":[{"x":[18426,18434,18457,18461,18462,18463,18468,18472,18477,18482,18489,18491,18498,18517,18525,18530,18536,18537,18539,18547],"y":[10,70,198,259,372,500,621,901,1284,1589,1660,1833,1950,2058,2221,2249,2376,2521,2560,2697],"text":["date: 2020-06-13<br />cum_weight:   10<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-06-21<br />cum_weight:   70<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-14<br />cum_weight:  198<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-18<br />cum_weight:  259<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-19<br />cum_weight:  372<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-20<br />cum_weight:  500<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-25<br />cum_weight:  621<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-07-29<br />cum_weight:  901<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-08-03<br />cum_weight: 1284<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-08-08<br />cum_weight: 1589<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-08-15<br />cum_weight: 1660<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-08-17<br />cum_weight: 1833<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-08-24<br />cum_weight: 1950<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-09-12<br />cum_weight: 2058<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-09-20<br />cum_weight: 2221<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-09-25<br />cum_weight: 2249<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-10-01<br />cum_weight: 2376<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-10-02<br />cum_weight: 2521<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-10-04<br />cum_weight: 2560<br />Vegetable: Kale<br />Vegetable: Kale","date: 2020-10-12<br />cum_weight: 2697<br />Vegetable: Kale<br />Vegetable: Kale"],"type":"scatter","mode":"lines","line":{"width":2.26771653543307,"color":"rgba(0,104,139,1)","dash":"solid"},"hoveron":"points","name":"Kale","legendgroup":"Kale","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18419,18421,18422,18424,18426,18430,18431,18432,18433,18434,18435,18437,18438,18440,18441,18442,18444,18445,18446,18447,18449,18450,18451,18452,18454,18455,18456,18459,18463,18465,18466,18467,18469,18470,18471,18472,18473,18474,18477,18478,18480,18481,18485,18486,18488,18489,18490,18491,18492,18494,18497,18498,18501,18502,18521,18531,18532,18542],"y":[20,35,45,57,76,124,171,248,288,383,453,575,605,746,857,1020,1080,1224,1657,1804,1993,2073,2187,2248,2327,2410,2600,2661,2784,2807,2937,2953,3034,3133,3224,3297,3391,3498,3563,3619,3717,3736,3828,3901,3981,4037,4082,4149,4236,4657,4768,4902,4916,5001,5009,5104,5243,5260],"text":["date: 2020-06-06<br />cum_weight:   20<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-08<br />cum_weight:   35<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-09<br />cum_weight:   45<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-11<br />cum_weight:   57<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-13<br />cum_weight:   76<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-17<br />cum_weight:  124<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-18<br />cum_weight:  171<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-19<br />cum_weight:  248<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-20<br />cum_weight:  288<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-21<br />cum_weight:  383<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-22<br />cum_weight:  453<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-24<br />cum_weight:  575<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-25<br />cum_weight:  605<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-27<br />cum_weight:  746<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-28<br />cum_weight:  857<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-06-29<br />cum_weight: 1020<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-01<br />cum_weight: 1080<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-02<br />cum_weight: 1224<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-03<br />cum_weight: 1657<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-04<br />cum_weight: 1804<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-06<br />cum_weight: 1993<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-07<br />cum_weight: 2073<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-08<br />cum_weight: 2187<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-09<br />cum_weight: 2248<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-11<br />cum_weight: 2327<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-12<br />cum_weight: 2410<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-13<br />cum_weight: 2600<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-16<br />cum_weight: 2661<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-20<br />cum_weight: 2784<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-22<br />cum_weight: 2807<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-23<br />cum_weight: 2937<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-24<br />cum_weight: 2953<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-26<br />cum_weight: 3034<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-27<br />cum_weight: 3133<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-28<br />cum_weight: 3224<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-29<br />cum_weight: 3297<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-30<br />cum_weight: 3391<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-07-31<br />cum_weight: 3498<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-03<br />cum_weight: 3563<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-04<br />cum_weight: 3619<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-06<br />cum_weight: 3717<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-07<br />cum_weight: 3736<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-11<br />cum_weight: 3828<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-12<br />cum_weight: 3901<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-14<br />cum_weight: 3981<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-15<br />cum_weight: 4037<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-16<br />cum_weight: 4082<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-17<br />cum_weight: 4149<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-18<br />cum_weight: 4236<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-20<br />cum_weight: 4657<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-23<br />cum_weight: 4768<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-24<br />cum_weight: 4902<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-27<br />cum_weight: 4916<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-08-28<br />cum_weight: 5001<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-09-16<br />cum_weight: 5009<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-09-26<br />cum_weight: 5104<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-09-27<br />cum_weight: 5243<br />Vegetable: Lettuce<br />Vegetable: Lettuce","date: 2020-10-07<br />cum_weight: 5260<br />Vegetable: Lettuce<br />Vegetable: Lettuce"],"type":"scatter","mode":"lines","line":{"width":2.26771653543307,"color":"rgba(255,69,0,1)","dash":"solid"},"hoveron":"points","name":"Lettuce","legendgroup":"Lettuce","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18424,18426,18430,18431,18432,18433,18434,18435,18436,18438,18440,18441,18443,18445,18454,18458,18464,18474,18478,18491,18492],"y":[9,23,81,140,198,223,345,382,423,445,505,604,684,700,719,758,779,810,854,884,923],"text":["date: 2020-06-11<br />cum_weight:    9<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-13<br />cum_weight:   23<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-17<br />cum_weight:   81<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-18<br />cum_weight:  140<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-19<br />cum_weight:  198<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-20<br />cum_weight:  223<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-21<br />cum_weight:  345<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-22<br />cum_weight:  382<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-23<br />cum_weight:  423<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-25<br />cum_weight:  445<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-27<br />cum_weight:  505<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-28<br />cum_weight:  604<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-06-30<br />cum_weight:  684<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-07-02<br />cum_weight:  700<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-07-11<br />cum_weight:  719<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-07-15<br />cum_weight:  758<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-07-21<br />cum_weight:  779<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-07-31<br />cum_weight:  810<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-08-04<br />cum_weight:  854<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-08-17<br />cum_weight:  884<br />Vegetable: Spinach<br />Vegetable: Spinach","date: 2020-08-18<br />cum_weight:  923<br />Vegetable: Spinach<br />Vegetable: Spinach"],"type":"scatter","mode":"lines","line":{"width":2.26771653543307,"color":"rgba(122,197,205,1)","dash":"solid"},"hoveron":"points","name":"Spinach","legendgroup":"Spinach","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18434,18443,18451,18459,18463,18466,18483,18484,18487,18509,18514,18530,18532,18535,18545,18552],"y":[32,64,160,189,367,833,1135,1444,1961,2217,2445,2469,2701,2789,2812,3122],"text":["date: 2020-06-21<br />cum_weight:   32<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-06-30<br />cum_weight:   64<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-07-08<br />cum_weight:  160<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-07-16<br />cum_weight:  189<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-07-20<br />cum_weight:  367<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-07-23<br />cum_weight:  833<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-08-09<br />cum_weight: 1135<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-08-10<br />cum_weight: 1444<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-08-13<br />cum_weight: 1961<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-09-04<br />cum_weight: 2217<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-09-09<br />cum_weight: 2445<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-09-25<br />cum_weight: 2469<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-09-27<br />cum_weight: 2701<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-09-30<br />cum_weight: 2789<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-10-10<br />cum_weight: 2812<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard","date: 2020-10-17<br />cum_weight: 3122<br />Vegetable: Swiss Chard<br />Vegetable: Swiss Chard"],"type":"scatter","mode":"lines","line":{"width":2.26771653543307,"color":"rgba(238,180,34,1)","dash":"solid"},"hoveron":"points","name":"Swiss Chard","legendgroup":"Swiss Chard","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"Kale","legendgroup":"Kale","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"Lettuce","legendgroup":"Lettuce","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"Spinach","legendgroup":"Spinach","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"Swiss Chard","legendgroup":"Swiss Chard","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":34.337899543379},"font":{"color":"rgba(0,0,0,1)","family":"Avenir","size":14.6118721461187},"title":{"text":"Cumulative Harvest of Leafy Greens","font":{"color":"rgba(0,0,0,1)","family":"Avenir","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18412.35,18558.65],"tickmode":"array","ticktext":["Jun","Jul","Aug","Sep","Oct"],"tickvals":[18414,18444,18475,18506,18536],"categoryorder":"array","categoryarray":["Jun","Jul","Aug","Sep","Oct"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"Avenir","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"Avenir","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-253.55,5522.55],"tickmode":"array","ticktext":["0","1000","2000","3000","4000","5000"],"tickvals":[0,1000,2000,3000,4000,5000],"categoryorder":"array","categoryarray":["0","1000","2000","3000","4000","5000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"Avenir","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(217,217,217,1)","gridwidth":0.132835201328352,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"Avenir","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"Avenir","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"7f085645592d":{"x":{},"y":{},"colour":{},"label":{},"type":"scatter"},"7f0862e1c59a":{"x":{},"y":{},"colour":{},"label":{}}},"cur_data":"7f085645592d","visdat":{"7f085645592d":["function (y) ","x"],"7f0862e1c59a":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
trains_anim<-small_trains%>%
  filter(departure_station == c("PARIS LYON", "PARIS EST", "PARIS MONTPARNASSE", "PARIS NORD"))%>%
  group_by(departure_station, year)%>%
  summarize(total_num_departures = sum(total_num_trips), total_late_departures = sum(num_late_at_departure))%>%
  mutate(percent_late_departures = total_late_departures/total_num_departures*100)%>%
  ggplot(aes(y= percent_late_departures, x = departure_station))+
  geom_bar(stat = "identity", fill = "darkseagreen")+
  transition_states(year)+
  labs(title = "Percent of Late Departures at Paris Train Stations from 2015-2018",
       subtitle = "Year: {closest_state}",
       y = NULL,
       x = NULL)+
  theme_classic()
```



<img src="trains_anim.gif" title="This plot shows the percentage of late depatures in 4 Paris train stations over a 4 year time period." alt="This plot shows the percentage of late depatures in 4 Paris train stations over a 4 year time period."  />

## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. I have filtered the data to the tomatoes and find the *daily* harvest in pounds for each variety. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0. 
  You should do the following:
  * For each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each variety and arranged (HINT: `fct_reorder()`) from most to least harvested weights (most on the bottom).  
  * Add animation to reveal the plot over date. Instead of having a legend, place the variety names directly on the graph (refer back to the tutorial for how to do this).


```r
garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, 
           date, 
           fill = list(daily_harvest_lb = 0))%>%
  group_by(variety)%>%
  mutate(cum_harvest = cumsum(daily_harvest_lb))%>%
  ggplot(aes(x = date, y= cum_harvest, fill = fct_reorder(variety, cum_harvest, max)))+
    geom_area() +
  transition_reveal(date)+
  geom_text(aes(label = variety), position = "stack")+
  theme(legend.position = "note")+
  labs(title = "Cumulative Harvest (lbs) of Tomato Varieties",
       y = NULL,
       x= NULL)
```



<img src="tomatoes1.gif" title="This plot shows the cumulative growth of the harvest of different tomato varieties over time." alt="This plot shows the cumulative growth of the harvest of different tomato varieties over time."  />


## Maps, animation, and movement!

  4. Map Lisa's `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  

```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.28, bottom = 39.4, right = 2.8, top = 39.8), 
    maptype = "toner-lite",
    zoom = 11)

mallorca_map_anim <-ggmap(mallorca_map) +
  geom_path(data = mallorca_bike_day7, 
             aes(x = lon, 
                 y = lat , 
                 color = ele),
             size = 3) +
  geom_point(data = mallorca_bike_day7, 
             aes(x = lon, 
                 y = lat), 
             color = "red", size = 5)+
  scale_color_viridis_c(option = "magma") +
  theme_map() +
  theme(legend.background = element_blank())+
  transition_reveal(time)+
  labs(title = "Mallorca Bike Trip Day 7", 
       subtitle = "Date: {frame_along}",
       x = "",
       y = "",
       color = "elevation")
```



<img src="mallorca_map_anim.gif" title="This map shows a bike trip on Mallorca over the course of a day." alt="This map shows a bike trip on Mallorca over the course of a day."  />
  
  5. In this exercise, you get to meet Lisa's sister, Heather! She is a proud Mac grad, currently works as a Data Scientist where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 
  1. combine the files putting them in swim, bike, run order (HINT: `bind_rows()`), 
  2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 
  3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
panama_total<-panama_swim%>%
  bind_rows(panama_bike)%>%
  bind_rows(panama_run)

panama_map <- get_stamenmap(
    bbox = c(left = -79.5867, bottom = 8.8849 , right = -79.45, top = 9.0017), 
    maptype = "toner-lite",
    zoom = 13)

panama_map_anim <- ggmap(panama_map)+
    geom_path(data = panama_total, 
            aes(x = lon, y = lat, color = event),
            size = 1) +
    geom_point(data = panama_total, 
            aes(x = lon, y = lat, color = event),
            size = 2)+
  theme_map()+
  transition_reveal(hrminsec)+
  labs(title = "Panama Triathlon", 
       subtitle = "hrminsec: {frame_along}",
       x = "",
       y = "")
```
  


<img src="panamamap.gif" title="This map shows the path of a triathelete during a triatholon on each stage of the race." alt="This map shows the path of a triathelete during a triatholon on each stage of the race."  />

## COVID-19 data

  6. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for the the 15th of each month. So, filter only to those dates - there are some lubridate functions that can help you do this.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))

states_map <- map_data("state")

covid_cases <- covid19 %>% 
  mutate(state = str_to_lower(state))

covid_map_anim<- 
  covid_cases %>% 
  left_join(census_pop_est_2018,
            by = c("state")) %>% 
  group_by(state)%>%
  mutate(cases_per_10000 = (cases/est_pop_2018)*10000)
  group_by(state)%>%
  mutate(day_of_month = day(date))%>%
  filter(day_of_month == 15)%>%
  ggplot() +
  geom_map(map = states_map,
           aes(map_id = state, 
               fill = cases_per_10000, group = date)) +
  expand_limits(x =  states_map$long , y =  states_map$lat) + 
  theme_map()+
  scale_fill_viridis_c(option = "mako") +
  labs(title = "Current Cumulative COVID Cases") +
  transition_states(date)+
  labs(title = "Cumulative Covid Cases Over Time", 
       subtitle = "date: {closest_state}",
       x = "",
       y = "")

covid_map_anim2<-animate(covid_map_anim, nframes = 200, end_pause = 10)
```




```
## Error in knitr::include_graphics("covid_map_anim.gif"): Cannot find the file(s): "covid_map_anim.gif"
```

## Your first `shiny` app 

  7. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. You should create a new project for the app, separate from the homework project. Below, you will post a link to the app that you publish on shinyapps.io. **You will create an app to compare states' daily number of COVID cases per 100,000 over time.** The x-axis will be date. You will have an input box where the user can choose which states to compare (`selectInput()`), a slider where the user can choose the date range, and a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
Put the link to your app here: https://eisland.shinyapps.io/exerise5shinyapp/ 


## GitHub link

  8. Below, provide a link to your GitHub repo with this set of Weekly Exercises. 

https://github.com/elleryisland/Exercise-5 



