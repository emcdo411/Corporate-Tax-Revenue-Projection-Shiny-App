# Corporate Tax Revenue Projection Shiny App

This repository contains a Shiny application designed to estimate the potential tax revenue impact of relocating 30% of operations from 187 companies to the United States. The application calculates the projected tax contributions based on user-defined parameters and visualizes the results interactively.

## Table of Contents

1. [Repository Naming Conventions](#repository-naming-conventions)
2. [Shiny App Overview](#shiny-app-overview)
   - [Functionality](#functionality)
   - [Code Implementation](#code-implementation)
3. [Calculating the 187-Year Payoff Scenario](#calculating-the-187-year-payoff-scenario)
   - [Assumptions](#assumptions)
   - [Code Explanation](#code-explanation)
4. [Why This Matters](#why-this-matters)
5. [Conclusion](#conclusion)
6. [License](#license)

## Repository Naming Conventions

Adhering to consistent naming conventions enhances readability and maintainability. This repository follows the guidelines of using lowercase letters and hyphenated words for clarity and consistency. citeturn0search2

## Shiny App Overview

### Functionality

The Shiny app allows users to:

- Input the number of companies considered.
- Define the average tax revenue increase per company resulting from the relocation.
- Calculate the total projected tax revenue increase.
- Visualize the distribution of tax contributions across the companies.

### Code Implementation

The app consists of two main components:

1. **UI (User Interface):** Defines the layout and elements of the app.
2. **Server:** Contains the logic for calculations and data processing.

```r
# UI
ui <- fluidPage(
  titlePanel("Projected Tax Revenue Increase"),
  sidebarLayout(
    sidebarPanel(
      numericInput("num_companies", "Number of Companies:", 187, min = 1),
      numericInput("tax_increase", "Tax Increase per Company ($):", 200000000, min = 0)
    ),
    mainPanel(
      textOutput("total_tax"),
      plotOutput("tax_plot")
    )
  )
)

# Server
server <- function(input, output) {
  total_tax <- reactive({
    input$num_companies * input$tax_increase
  })
  
  output$total_tax <- renderText({
    paste("Total Projected Tax Revenue Increase: $", format(total_tax(), big.mark = ","))
  })
  
  output$tax_plot <- renderPlot({
    barplot(rep(input$tax_increase, input$num_companies), main = "Tax Revenue Distribution", ylab = "Tax Increase ($)")
  })
}

# Run the application
shinyApp(ui = ui, server = server)
```

## Calculating the 187-Year Payoff Scenario

### Assumptions

- **Number of Companies:** 187
- **Tax Increase per Company:** $200,000,000
- **Total Tax Revenue Increase:** $37,400,000,000

### Code Explanation

The server function calculates the total tax revenue by multiplying the number of companies by the tax increase per company. It also generates a bar plot to visualize the tax distribution.

```r
# Total tax revenue calculation
total_tax <- reactive({
  input$num_companies * input$tax_increase
})

# Render total tax revenue text
output$total_tax <- renderText({
  paste("Total Projected Tax Revenue Increase: $", format(total_tax(), big.mark = ","))
})

# Render tax distribution plot
output$tax_plot <- renderPlot({
  barplot(rep(input$tax_increase, input$num_companies), main = "Tax Revenue Distribution", ylab = "Tax Increase ($)")
})
```

## Why This Matters

Understanding the financial implications of relocating business operations is crucial for policymakers and business leaders. This app provides insights into potential tax revenue increases, aiding in informed decision-making regarding economic development strategies and resource allocation.

## Conclusion

This Shiny application offers a simplified model to estimate the tax revenue impact of relocating a portion of corporate operations. While based on hypothetical scenarios, it serves as a tool for exploring the potential economic benefits of such strategic decisions.

## License

This project is licensed under the MIT License - see the LICENSE file for details. 
