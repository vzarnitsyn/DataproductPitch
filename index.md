---
title       : Data products project pitch
subtitle    : Demonstration of elegant interactive graphic with GoogleVis+Shiny+Shinyapps.io
author      : V. Zarnitsyn
job         : July 25,2015
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Project description

* The proposed shiny presentation for developing data products class is based on several brilliant simple development tools presented in the course.

* In my line of work interactive geographic maps are valuable demonstration tools

* Combination of slidify+googleVis or shiny+shinyApps+GoogleVis makes them easy to develop and present

* The following presentation is based on the following small subset of world stat data


```
##     Country Population_M GDP_per_capita
## 1     China         1371          11907
## 2     India         1275           5418
## 3       USA          321          53042
## 4 Indonesia          256           9561
## 5    Brazil          205          15038
```

--- 

## Shiny details

* In developing shiny application in addtion to tools described in Coursera lectures I used the following widgets found through shinyapps tutorials

* helpText() to place a Note with simple explanations on main page

* Tabs to present more detailed documentation and table view of the data with the following code
 
 ```r
 tabsetPanel(type = "tabs",  tabPanel("Plot",htmlOutput("gvis")), 
                            tabPanel("Documentation",verbatimTextOutput("summary")), 
                            tabPanel("Table view", tableOutput("table"))
                )
 ```

* htmlOutput() function was used to pass googleVis html code to main presentation apge as you can see in the piece of code above

* selectInput() widget to select one option out of multiple availabe
                

--- 

## GoogleVis use details

* To create colored maps the googleVis based code was used. 
* Field to present and color choice are being read from ui.R inputs and passed to gvisGeoChart() in server .R. GoogleGeoChart function generates the map with selected variable and selected color scheme

* The fragment of this code is shown below:

 
 ```r
 field=input$Field
 choice=input$Color_choice
 if (choice == 1)
 { g<-gvisGeoChart(... colorvar=field,...options=list( ...colorAxis="{colors:['yellow', 'green']}")) } 
 if (choice == 2)
 { g<-gvisGeoChart(... options=list( ...colorAxis="{colors:['green', 'red']}")) } 
 if (choice == 3)
 { g<-gvisGeoChart(... options=list( ...colorAxis="{colors:['grey', 'black']}")) } 
 g
 ```

On the next slide I will show you the results of the code adapted for slidify execution with fixed Field='Population_M' and choice = 1 (Yellow to green color map ).


--- 

## Sample interactive plot


```r
library(googleVis)
op <- options(gvis.plot.tag='chart') # very critical to use in slidify or knitr 
field='Population_M'
g<-gvisGeoChart(myData,locationvar="Country", colorvar=field,
options=list( width=400, height=300,colorAxis="{colors:['yellow', 'green']}"))  
plot(g)
```

<!-- GeoChart generated in R 3.2.1 by googleVis 0.5.9 package -->
<!-- Sat Jul 25 22:50:18 2015 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID103c3256614f () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "China",
1371 
],
[
 "India",
1275 
],
[
 "USA",
321 
],
[
 "Indonesia",
256 
],
[
 "Brazil",
205 
] 
];
data.addColumn('string','Country');
data.addColumn('number','Population_M');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartGeoChartID103c3256614f() {
var data = gvisDataGeoChartID103c3256614f();
var options = {};
options["width"] =    400;
options["height"] =    300;
options["colorAxis"] = {colors:['yellow', 'green']};

    var chart = new google.visualization.GeoChart(
    document.getElementById('GeoChartID103c3256614f')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "geochart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartGeoChartID103c3256614f);
})();
function displayChartGeoChartID103c3256614f() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID103c3256614f"></script>
 
<!-- divChart -->
  
<div id="GeoChartID103c3256614f" 
  style="width: 400; height: 300;">
</div>






