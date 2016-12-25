Reprocible Pitch Presentation
========================================================
author: Jesin Fahad
date: 25-December-2016
autosize: true

First Slide
========================================================

Coursera Reproducible Pitch Presentation

Please check out the Course Project
<https://jesyfax.shinyapps.io/Myshinyapp/>.

The code is share  in the github repository
<https://github.com/jesyfax/Peer-graded-Assignment-Course-Project-Shiny-Application-and-Reproducible-Pitch>

Overview
========================================================

This data table set of Rock, Pressure and Cars are displyed in the screen for viewing

Presentation is being created as part of the peer assessment for the Coursera Developing Data Products. The assignment is geared toward ensuring the following concepts were well understood by the students:

shiny to build data product application
R-Presentation or slidify to create data product related presentations

-A selection of three tables are displyed in the page
-The table name can be dynamically selected by the user.
-The number of observations to viewed can also be inputted.
-OPtion to show/hide the table or summary and be selected by the user. 

Slide With UICode
========================================================


```r
library(shiny)
fluidPage(
  titlePanel("Shiny Text"),
  sidebarLayout(
    sidebarPanel(
      selectInput("dataset", "Choose a dataset:", 
                  choices = c("rock", "pressure", "cars")),
      
      numericInput("obs", "Number of observations to view:", 10),
      checkboxInput("Summary","Show Summary"),
      checkboxInput("Table","Show Table")
    ),
    mainPanel(
      verbatimTextOutput("summary"),
      
      tableOutput("view")
    )
  )
)
```

<!--html_preserve--><div class="container-fluid">
<h2>Shiny Text</h2>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label class="control-label" for="dataset">Choose a dataset:</label>
<div>
<select id="dataset"><option value="rock" selected>rock</option>
<option value="pressure">pressure</option>
<option value="cars">cars</option></select>
<script type="application/json" data-for="dataset" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<label for="obs">Number of observations to view:</label>
<input id="obs" type="number" class="form-control" value="10"/>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="Summary" type="checkbox"/>
<span>Show Summary</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="Table" type="checkbox"/>
<span>Show Table</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<pre id="summary" class="shiny-text-output"></pre>
<div id="view" class="shiny-html-output"></div>
</div>
</div>
</div><!--/html_preserve-->

Slide With ServerCode
========================================================

```r
library(shiny)
library(datasets)
function(input, output) {
  # Return the requested dataset
  datasetInput <- reactive({
    switch(input$dataset,
           "rock" = rock,
           "pressure" = pressure,
           "cars" = cars)
  })
  output$summary <- renderPrint({
    dataset <- datasetInput()
    summary(dataset)
  })
  output$view <- renderTable({
    head(datasetInput(), n = input$obs)
  })
}
```

```
function(input, output) {
  # Return the requested dataset
  datasetInput <- reactive({
    switch(input$dataset,
           "rock" = rock,
           "pressure" = pressure,
           "cars" = cars)
  })
  output$summary <- renderPrint({
    dataset <- datasetInput()
    summary(dataset)
  })
  output$view <- renderTable({
    head(datasetInput(), n = input$obs)
  })
}
```



