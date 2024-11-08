library(shiny)
library(quantmod)
library(ggplot2)

# Define UI for application that draws a histogram
ui <- fluidPage(
  titlePanel("Stock Price Viewer"),
  sidebarLayout(
    sidebarPanel(
      textInput('ticker', 'Enter Stock Ticker Symbol:', value = 'AAPL'),
      dateRangeInput('dateRange', 'Select Date Range:',
                     start = Sys.Date() - 30, end = Sys.Date()),
      actionButton('goButton', 'GO')
      
    ),
    mainPanel(
      plotOutput("distPlot")
    )
  )
)

# Define server logic required to draw a histogram
server <- function(input, output) {
  # Reactive expression to subset the mtcars data based on selected cylinders
  stockData <- eventReactive(input$goButton, {
    getSymbols(input$ticker, src = 'yahoo',
               from = input$dateRange[1], to = input$dateRange[2],
               auto.assign = FALSE)
  })
  output$distPlot <- renderPlot({
    data <- stockData()
    chartSeries(data, name = paste(input$ticker, "stock price"), subset = "2023::")
  })
}

# Run the application 
shinyApp(ui = ui, server = server)