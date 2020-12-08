---
title: Interactive Visualization With ggplot2 and Plotly
author: Diwash Shrestha
date: '2020-11-29'
slug: interactive-visualization-with-ggplot2-and-plotly
categories:
  - R
  - Data Visualization
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2020-11-29T15:48:32+05:45'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
diagram: true
---
<link href="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/pagedtable-1.1/css/pagedtable.css" rel="stylesheet" />
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/pagedtable-1.1/js/pagedtable.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/htmlwidgets-1.5.2/htmlwidgets.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-binding-4.9.2.1/plotly.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/typedarray-0.1/typedarray.min.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/jquery-1.11.3/jquery.min.js"></script>
<link href="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/crosstalk-1.1.0.1/css/crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/crosstalk-1.1.0.1/js/crosstalk.min.js"></script>
<link href="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-htmlwidgets-css-1.52.2/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-main-1.52.2/plotly-latest.min.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/htmlwidgets-1.5.2/htmlwidgets.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-binding-4.9.2.1/plotly.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/typedarray-0.1/typedarray.min.js"></script>
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/jquery-1.11.3/jquery.min.js"></script>
<link href="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/crosstalk-1.1.0.1/css/crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/crosstalk-1.1.0.1/js/crosstalk.min.js"></script>
<link href="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-htmlwidgets-css-1.52.2/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/plotly-main-1.52.2/plotly-latest.min.js"></script>



I love to work with data while analysing the data, I like to explore it and for that best thing is to visualize the data. I create a visualization to show the information or finding from the analysis. For this task, I use the ggplot2 package from the Tidyverse Universe. 

![](plot.png)


[GGplot2](https://ggplot2.tidyverse.org/) is powerful visualization package based on   [The grammar of graphics](https://www.springer.com/gp/book/9780387245447) and part of [tidyverse](https://www.tidyverse.org/). It is easy to use and powerful to create any type of visualization. The problem is it can only make beautiful static visualization.

I write blogs, create dashboard and reports. The interactive graph allows users to interact with a graph which is more meaningful than a static graph. It is not possible to create an interactive graph with ggplot2.


[Plotly](https://plot.ly/r/) can convert the high-quality ggplot graphs to interactive using the ggploty function in plotly package.  plotly is a free opensource library for interactive visualization. In this blog, I will create a static visualization with ggplot2 and then make the ggplot graph interactive with plotly package. I will use data about Nobel prize winner to create the visualization. Let's get visualizing


### Load Packages

lets load the required packages in our R environment.


```r
library(readr) # read csv file
library(ggplot2) # for visualization
library(dplyr) # data manipulation
library(plotly) # interactive data visualization
```


### Load Data

I am using the Nobel prize winner data which is sourced from [tidytuesday github](https://github.com/rfordatascience/tidytuesday) which release every week new data project. 


```r
data <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-05-14/nobel_winners.csv")
```

Here is the data that i will use to create visualization.

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["prize_year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["category"],"name":[2],"type":["chr"],"align":["left"]},{"label":["prize"],"name":[3],"type":["chr"],"align":["left"]},{"label":["motivation"],"name":[4],"type":["chr"],"align":["left"]},{"label":["prize_share"],"name":[5],"type":["chr"],"align":["left"]},{"label":["laureate_id"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["laureate_type"],"name":[7],"type":["chr"],"align":["left"]},{"label":["full_name"],"name":[8],"type":["chr"],"align":["left"]},{"label":["birth_date"],"name":[9],"type":["date"],"align":["right"]},{"label":["birth_city"],"name":[10],"type":["chr"],"align":["left"]},{"label":["birth_country"],"name":[11],"type":["chr"],"align":["left"]},{"label":["gender"],"name":[12],"type":["chr"],"align":["left"]},{"label":["organization_name"],"name":[13],"type":["chr"],"align":["left"]},{"label":["organization_city"],"name":[14],"type":["chr"],"align":["left"]},{"label":["organization_country"],"name":[15],"type":["chr"],"align":["left"]},{"label":["death_date"],"name":[16],"type":["date"],"align":["right"]},{"label":["death_city"],"name":[17],"type":["chr"],"align":["left"]},{"label":["death_country"],"name":[18],"type":["chr"],"align":["left"]}],"data":[{"1":"1901","2":"Chemistry","3":"The Nobel Prize in Chemistry 1901","4":"\"in recognition of the extraordinary services he has rendered by the discovery of the laws of chemical dynamics and osmotic pressure in solutions\"","5":"1/1","6":"160","7":"Individual","8":"Jacobus Henricus van 't Hoff","9":"1852-08-30","10":"Rotterdam","11":"Netherlands","12":"Male","13":"Berlin University","14":"Berlin","15":"Germany","16":"1911-03-01","17":"Berlin","18":"Germany"},{"1":"1901","2":"Literature","3":"The Nobel Prize in Literature 1901","4":"\"in special recognition of his poetic composition, which gives evidence of lofty idealism, artistic perfection and a rare combination of the qualities of both heart and intellect\"","5":"1/1","6":"569","7":"Individual","8":"Sully Prudhomme","9":"1839-03-16","10":"Paris","11":"France","12":"Male","13":"NA","14":"NA","15":"NA","16":"1907-09-07","17":"Châtenay","18":"France"},{"1":"1901","2":"Medicine","3":"The Nobel Prize in Physiology or Medicine 1901","4":"\"for his work on serum therapy, especially its application against diphtheria, by which he has opened a new road in the domain of medical science and thereby placed in the hands of the physician a victorious weapon against illness and deaths\"","5":"1/1","6":"293","7":"Individual","8":"Emil Adolf von Behring","9":"1854-03-15","10":"Hansdorf (Lawice)","11":"Prussia (Poland)","12":"Male","13":"Marburg University","14":"Marburg","15":"Germany","16":"1917-03-31","17":"Marburg","18":"Germany"},{"1":"1901","2":"Peace","3":"The Nobel Peace Prize 1901","4":"NA","5":"1/2","6":"462","7":"Individual","8":"Jean Henry Dunant","9":"1828-05-08","10":"Geneva","11":"Switzerland","12":"Male","13":"NA","14":"NA","15":"NA","16":"1910-10-30","17":"Heiden","18":"Switzerland"},{"1":"1901","2":"Peace","3":"The Nobel Peace Prize 1901","4":"NA","5":"1/2","6":"463","7":"Individual","8":"Frédéric Passy","9":"1822-05-20","10":"Paris","11":"France","12":"Male","13":"NA","14":"NA","15":"NA","16":"1912-06-12","17":"Paris","18":"France"},{"1":"1901","2":"Physics","3":"The Nobel Prize in Physics 1901","4":"\"in recognition of the extraordinary services he has rendered by the discovery of the remarkable rays subsequently named after him\"","5":"1/1","6":"1","7":"Individual","8":"Wilhelm Conrad Röntgen","9":"1845-03-27","10":"Lennep (Remscheid)","11":"Prussia (Germany)","12":"Male","13":"Munich University","14":"Munich","15":"Germany","16":"1923-02-10","17":"Munich","18":"Germany"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

### Create a barplot

I created a barplot showing the number of the Nobel prize winner and the prize category. At first, I create a static plot with ggplot2.


```r
nobelbar <- ggplot(data) + geom_bar(aes(category, fill = category)) +
  theme_minimal() +
  theme(legend.position = "none", axis.title.x = element_blank()) + 
  labs(title = "Number of Nobel prize winner by category") +
  scale_fill_brewer(palette = "Set2")

nobelbar
```

<img src="{{< relref "post/2020-11-29-interactive-visualization-with-ggplot2-and-plotly/index.en.markdown" >}}index.en_files/figure-html/unnamed-chunk-4-1.png" width="672" />


### Make ggplot interactive 

I will pass the ggplot to the ggplotly function from plotly package, which creates an interactive graph.


```r
ggplotly(nobelbar, tooltip = c("fill", "count"))
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"orientation":"v","width":0.9,"base":0,"x":[1],"y":[194],"text":"count: 194<br />category: Chemistry","type":"bar","marker":{"autocolorscale":false,"color":"rgba(102,194,165,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Chemistry","legendgroup":"Chemistry","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[2],"y":[83],"text":"count:  83<br />category: Economics","type":"bar","marker":{"autocolorscale":false,"color":"rgba(252,141,98,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Economics","legendgroup":"Economics","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[3],"y":[113],"text":"count: 113<br />category: Literature","type":"bar","marker":{"autocolorscale":false,"color":"rgba(141,160,203,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Literature","legendgroup":"Literature","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[4],"y":[227],"text":"count: 227<br />category: Medicine","type":"bar","marker":{"autocolorscale":false,"color":"rgba(231,138,195,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Medicine","legendgroup":"Medicine","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[5],"y":[130],"text":"count: 130<br />category: Peace","type":"bar","marker":{"autocolorscale":false,"color":"rgba(166,216,84,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Peace","legendgroup":"Peace","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[6],"y":[222],"text":"count: 222<br />category: Physics","type":"bar","marker":{"autocolorscale":false,"color":"rgba(255,217,47,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Physics","legendgroup":"Physics","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":43.1050228310502},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Number of Nobel prize winner by category","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,6.6],"tickmode":"array","ticktext":["Chemistry","Economics","Literature","Medicine","Peace","Physics"],"tickvals":[1,2,3,4,5,6],"categoryorder":"array","categoryarray":["Chemistry","Economics","Literature","Medicine","Peace","Physics"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-11.35,238.35],"tickmode":"array","ticktext":["0","50","100","150","200"],"tickvals":[0,50,100,150,200],"categoryorder":"array","categoryarray":["0","50","100","150","200"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"count","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"1c444aa27ea8":{"x":{},"fill":{},"type":"bar"}},"cur_data":"1c444aa27ea8","visdat":{"1c444aa27ea8":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>


I like to keep the plot clean, So I hide the Modebar of the plotly.


```r
nobel_plot <- ggplotly(nobelbar, tooltip = c("fill", "count")) %>%
  config(displayModeBar = F)
nobel_plot
```

<div id="htmlwidget-2" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"data":[{"orientation":"v","width":0.9,"base":0,"x":[1],"y":[194],"text":"count: 194<br />category: Chemistry","type":"bar","marker":{"autocolorscale":false,"color":"rgba(102,194,165,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Chemistry","legendgroup":"Chemistry","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[2],"y":[83],"text":"count:  83<br />category: Economics","type":"bar","marker":{"autocolorscale":false,"color":"rgba(252,141,98,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Economics","legendgroup":"Economics","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[3],"y":[113],"text":"count: 113<br />category: Literature","type":"bar","marker":{"autocolorscale":false,"color":"rgba(141,160,203,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Literature","legendgroup":"Literature","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[4],"y":[227],"text":"count: 227<br />category: Medicine","type":"bar","marker":{"autocolorscale":false,"color":"rgba(231,138,195,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Medicine","legendgroup":"Medicine","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[5],"y":[130],"text":"count: 130<br />category: Peace","type":"bar","marker":{"autocolorscale":false,"color":"rgba(166,216,84,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Peace","legendgroup":"Peace","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.9,"base":0,"x":[6],"y":[222],"text":"count: 222<br />category: Physics","type":"bar","marker":{"autocolorscale":false,"color":"rgba(255,217,47,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Physics","legendgroup":"Physics","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":43.1050228310502},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Number of Nobel prize winner by category","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,6.6],"tickmode":"array","ticktext":["Chemistry","Economics","Literature","Medicine","Peace","Physics"],"tickvals":[1,2,3,4,5,6],"categoryorder":"array","categoryarray":["Chemistry","Economics","Literature","Medicine","Peace","Physics"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-11.35,238.35],"tickmode":"array","ticktext":["0","50","100","150","200"],"tickvals":[0,50,100,150,200],"categoryorder":"array","categoryarray":["0","50","100","150","200"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"count","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false,"displayModeBar":false},"source":"A","attrs":{"1c441cca18ff":{"x":{},"fill":{},"type":"bar"}},"cur_data":"1c441cca18ff","visdat":{"1c441cca18ff":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Save the plot

I can use this interactive plot in website, reports and also share with others. Let's save it locally and we can share the HTML file.




### Wrapping up

At least we made the ggplot2 charts interactive using a single ggplotly() function. You can find lots of data in [Tidytuesday repo](https://github.com/rfordatascience/tidytuesday) and create great visualization to show the insights.
