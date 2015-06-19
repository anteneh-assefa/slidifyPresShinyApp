---
title       : Degree fahrenheit to celcius convertor
subtitle    : A simple application using shiny
author      : Anteneh
job         : aa
logo        : logo.png
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : mathjax            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Background
### Mathimatical relationship between celcius and fahrenheit

- The general equation is:

$$
^{0}C = (^{0}F - 32)/1.8
$$

r code:

```r
oF = 32
oC = round((oF - 32)/1.8, 0)
```

- 32 degree fahrenheit equal to 0 degree celcius



- 98 degree fahrenheit equal to 37 degree celcius

--- 

## Exploring ui.R


```r
library(shiny)
shinyUI(pageWithSidebar(
    headerPanel("Fahrenheit to Celsius convertor"),
    sidebarPanel(
        paste("This program convertes a temprature in degree Farenheit to degree Celcius. Please enter a temprature, select unit and press 'convert'. The result will be displayed in the right side panel."),
        numericInput(
            "obs", h3("Enter temprature to convert:"), 0),
        selectInput(
            "unit", h3("Unit"),
            choices = c(paste('oF'))),
        submitButton("convert")),
    mainPanel(
        img(src="logo.png"),
        h4("You entered:"),
        verbatimTextOutput("obs"),
        h4("which is equivalent to:"),
        verbatimTextOutput("evaluated"))
))
```

---

## Exploring server.R


```r
library(shiny)

oC <- function(obs) (obs-32) / 1.8
    
shinyServer(function(input, output) {
    
    output$obs <- renderText({paste(round(input$obs,0),"degree fahrenheit")})
    output$evaluated <- renderText({paste(round(oC(input$obs),0),"degree celsius")})
})
```

--- 

## How to use the application

### Steps:
1. Provide a temprature (in degree fahranheit)
2. Choose a unit (this application resitricted to farenheit to celcius conversion)
3. Press the 'convert' button
4. A summary of the temprature you entered and the temprature in degree celcius will be displayed in the right side panel

### Thank you!

### Questions?
