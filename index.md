---
title       : App to predict MPG of a car
subtitle    : Linear model to predict MPG of a car to help car buyers
author      : YVH
job         : Presenter
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, shiny, interactive, bootstrap, quiz]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Problem introduction 

- People want to buy a car that has high Miles Per Gallon (MPG)
- But ... 
- What is affecting MPG the most?
- Transmission? Weight? 
- Different standards of measurements give different MPG, they cannot be compared easily
- This app give you a general idea of what to look for 


--- .class #id 

## Data and linear model

- This app uses the mtcars dataset that comes with R 
- A study has been performed to find the parameters that influence MPG the most
- A linear fit was performed in following way:

```r
  fit <- lm(mpg ~ factor(am) + factor(cyl) + wt, data = mtcars)
```
- Out of studying a lot of fits the number of cylinders and the weight of the car are the most determining factors for MPG 
- This fit is the core of the developped shiny app.


--- .class #id 

## Shiny app 
- https://yvestools.shinyapps.io/Shiny_app_yv/
- Preview of app:
<div class="row-fluid">
  <div class="col-sm-4">
    <form class="well">
      <div class="form-group shiny-input-container">
        <label class="control-label" for="am">Transmission</label>
        <div>
          <select id="am"><option value="0" selected>Automatic</option>
<option value="1">Manual</option></select>
          <script type="application/json" data-for="am" data-nonempty="">{}</script>
        </div>
      </div>
      <div class="form-group shiny-input-container">
        <label class="control-label" for="cyl">Number of cylinders</label>
        <input class="js-range-slider" id="cyl" data-min="4" data-max="8" data-from="2" data-step="2" data-grid="true" data-grid-num="2" data-grid-snap="false" data-prettify-separator="," data-keyboard="true" data-keyboard-step="50" data-drag-interval="true" data-data-type="number"/>
      </div>
      <div class="form-group shiny-input-container">
        <label class="control-label" for="wt">Weight of the car [10^3 lb]</label>
        <input class="js-range-slider" id="wt" data-min="0.1" data-max="5.5" data-from="0.1" data-step="0.01" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-keyboard="true" data-keyboard-step="0.185185185185185" data-drag-interval="true" data-data-type="number"/>
      </div>
      <div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </div>
    </form>
  </div>
  <div class="col-sm-8"></div>
</div>
- Fill in values and press submit and the app will predict the MPG. 



--- .class #id 

## Example of usefulness
- Suppose you want to buy a car with high MPG and you have the choice between car #1: 2000 lb, 6 cylinders and automatic transmission and car #2: manual transmission, 8 cylinders and 2100 lb.

```r
MPGcar1 <- fit$coefficients[1] + fit$coefficients[2] * 0 + fit$coefficients[3] * 
    1 + fit$coefficients[4] * 0 + fit$coefficients[5] * 2
MPGcar2 <- fit$coefficients[1] + fit$coefficients[2] * 1 + fit$coefficients[3] * 
    0 + fit$coefficients[4] * 1 + fit$coefficients[5] * 2.1
as.numeric(c(MPGcar1, MPGcar2))
```

```
## [1] 23.19708 21.21042
```
- MPG car #1 has MPG of 23.1970779 and MPG car #2 is 21.2104209
- You drive 310 miles per week or 16120 miles per year and 1 gallon fuel is about USD 2
- Cost of fuel car 1: USD 1390 and car 2: USD 1520 per year
- Car 1 saves you $130/year in fuel! 
 






