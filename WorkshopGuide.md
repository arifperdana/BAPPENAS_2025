# Day 4 Workshop Guide: From Analysis to Interactive Insight
## Building Interactive Dashboards with R Shiny and AI-Assisted Coding

**BAPPENAS-Monash Masterclass 2025**  
**Facilitator:** Dr. Arif Perdana  
**Duration:** 2 hours 30 minutes (Sessions 3 & 4)  
**Date:** Day 4 of Masterclass

---

## Table of Contents
1. [Workshop Overview](#workshop-overview)
2. [Learning Objectives](#learning-objectives)
3. [Prerequisites](#prerequisites)
4. [Technical Setup](#technical-setup)
5. [Session 3: Introduction to R Shiny](#session-3-introduction-to-r-shiny)
6. [Session 4: Applied Dashboard Development](#session-4-applied-dashboard-development)
7. [Datasets Reference](#datasets-reference)
8. [AI Prompt Library](#ai-prompt-library)
9. [Troubleshooting Guide](#troubleshooting-guide)
10. [Resources for Further Learning](#resources-for-further-learning)

---

## Workshop Overview

### The Journey So Far
Over the past three days with Professor Di Cook, you have mastered:
- **Day 1-2:** Tidy data principles, data wrangling with dplyr and tidyr
- **Day 2:** Creating powerful visualizations with ggplot2
- **Day 3:** Building statistical models and machine learning workflows with tidymodels

### Today's Goal
Transform your static R analysis into **interactive web applications** that policymakers can explore themselves, using AI-assisted coding to accelerate development.

### Why This Matters for BAPPENAS
- Enable stakeholders to explore data without running R code
- Create transparent, reproducible policy tools
- Allow "what-if" scenario planning
- Turn analysts into tool builders, not just report writers

---

## Learning Objectives

By the end of this workshop, you will be able to:

1. ✓ Understand the architecture of Shiny applications (UI, Server, Reactivity)
2. ✓ Build interactive dashboards from static ggplot2 visualizations
3. ✓ Integrate tidymodels predictions into Shiny outputs
4. ✓ Use AI coding assistants effectively (prompt engineering for Shiny)
5. ✓ Debug and customize AI-generated code
6. ✓ Deploy and share your applications

---

## Prerequisites

### Knowledge Requirements
- Completion of Di Cook's Sessions 1-3
- Basic familiarity with:
  - R syntax and RStudio
  - dplyr data manipulation
  - ggplot2 visualization
  - Linear regression concepts

### Technical Requirements
- R version 4.0+ and RStudio
- Stable internet connection (for AI tools and package installation)
- Access to at least one AI coding assistant (see setup below)

---

## Technical Setup

### Step 1: Install Required R Packages

Run this code in your R console **before the workshop**:

```r
# Core Shiny packages
install.packages(c(
  "shiny",           # Interactive web apps
  "shinydashboard",  # Dashboard layouts
  "shinyWidgets",    # Enhanced input widgets
  "DT",              # Interactive tables
  "plotly",          # Interactive plots
  "fresh"            # Custom themes
), dependencies = TRUE)

# Data and modeling (review from Di Cook's sessions)
install.packages(c(
  "tidyverse",       # Data wrangling and visualization
  "broom",           # Tidy model outputs
  "tidymodels"       # Modeling framework
), dependencies = TRUE)

# Optional but useful
install.packages(c(
  "leaflet",         # Interactive maps (Day 5 preview)
  "lubridate",       # Date handling
  "scales"           # Formatting helpers
))
```

**Verify installation:**
```r
library(shiny)
library(tidyverse)
library(DT)

# If no errors appear, you're ready!
```

### Step 2: Set Up AI Coding Assistant

Choose **at least one** of these options:

#### Option A: ChatGPT (Recommended for Beginners)
1. Go to [https://chat.openai.com](https://chat.openai.com)  
2. Create free account or log in  
3. Test with: `Write a simple R Shiny app that displays 'Hello World'`

#### Option B: Claude (Alternative)
1. Visit [https://claude.ai](https://claude.ai)  
2. Create free account  
3. Good for explaining code and debugging

#### Option C: Qwen (Lightweight Alternative)
1. Go to [https://chat.qwen.ai](https://chat.qwen.ai)  
2. Log in with Alibaba account or create a new one  
3. Supports multiple languages and handles large code snippets efficiently


**Workshop Tip:** Have both ChatGPT (for generating code) and Claude (for explaining concepts) open.

### Step 3: Download Workshop Materials

**GitHub Repository:** https://github.com/dicook/BAPPENAS_2025

Download these files to your working directory:

```r
# Set your working directory
setwd("~/BAPPENAS_Workshop_Day4")

# Files you should have:
# - bappenas_regional_clean.csv
# - bappenas_irio_summary.csv
# - template_app.R
# - example_dashboard_simple.R
# - example_dashboard_advanced.R
```

---

## Session 3: Introduction to R Shiny
**Duration:** 75 minutes

### Part 1: The Bridge (0-15 minutes)

#### From Static to Interactive: The Policy Challenge

**Reflection Exercise:**
Think about your last data analysis project. How did you share results?
- [ ] Static PDF report
- [ ] PowerPoint presentation
- [ ] Excel spreadsheet
- [ ] Email with tables

**The Problem:**
Static outputs can't answer follow-up questions like:
- "What if we look at only Java provinces?"
- "How does this change over different time periods?"
- "Can you show me the outliers?"

**The Solution: Shiny**
Shiny turns your R analysis into interactive web applications—no web development experience needed.

#### Live Demo: The "Wow" Moment

Your instructor will demonstrate a completed dashboard showing:
- Regional GRDP trends (2015-2023)
- Interactive province selection
- Dynamic visualizations that update automatically
- Model predictions based on user inputs
- Downloadable filtered datasets

**Key Insight:** This was built entirely in R using the same tools you've been learning.

#### Understanding AI-Assisted Development

**Traditional Coding:**
```
Write code line by line → Test → Debug syntax → Repeat
Time: Hours to days
```

**AI-Assisted "Vibe Coding":**
```
Describe what you want → AI generates boilerplate → You refine → Test
Time: Minutes to hours
```

**Important Mindset:**
- AI is a **coding accelerator**, not a replacement for understanding
- You are the architect, AI is the construction worker
- Always review and understand generated code

---

### Part 2: Understanding Shiny Structure (15-45 minutes)

#### Core Concepts: Anatomy of a Shiny App

Every Shiny app has TWO parts:

**1. UI (User Interface)** - What users SEE and INTERACT with
```r
ui <- fluidPage(
  titlePanel("My Dashboard Title"),
  
  sidebarLayout(
    sidebarPanel(
      # INPUT CONTROLS go here
      selectInput("province", "Choose Province:",
                  choices = c("DKI Jakarta", "West Java", "East Java"))
    ),
    
    mainPanel(
      # OUTPUT DISPLAYS go here
      plotOutput("myPlot"),
      tableOutput("myTable")
    )
  )
)
```

**2. Server** - The R BRAIN that does the work
```r
server <- function(input, output) {
  
  # REACTIVE LOGIC: When input changes, this reruns automatically
  output$myPlot <- renderPlot({
    # Use input$province here to filter data
    # Then create ggplot
  })
  
  output$myTable <- renderTable({
    # Create table based on input$province
  })
}
```

**3. Reactivity** - The "Magic" Connection
- User changes input → Server detects change → Outputs update automatically
- You don't manually refresh or click "Update"
- Shiny handles all the communication

#### The Pattern to Remember

| UI Side | Server Side | Purpose |
|---------|-------------|---------|
| `sliderInput()` | `input$name` | User adjusts slider |
| `selectInput()` | `input$name` | User selects from dropdown |
| `plotOutput()` | `renderPlot()` | Display ggplot |
| `tableOutput()` | `renderTable()` | Display data frame |
| `textOutput()` | `renderText()` | Display text/numbers |

---

#### Hands-On Activity 1: "Hello, Shiny!"

**Step 1: Create Template App (5 minutes)**

In RStudio:
1. File → New File → Shiny Web App
2. Name it "MyFirstApp"
3. Choose "Single File (app.R)"
4. Click Create

You'll see the "Old Faithful" template app.

**Step 2: Identify Components (5 minutes)**

Find these in the template:
- [ ] `sliderInput` - Where is it? What does it control?
- [ ] `plotOutput` - Where is it defined?
- [ ] `renderPlot` - What R code is inside?
- [ ] `input$bins` - Where is this used?

**Step 3: Run the App (2 minutes)**
- Click "Run App" button (top right)
- Move the slider → Watch histogram update
- **This is reactivity in action!**

**Step 4: Make a Simple Change (3 minutes)**
Change the title from "Old Faithful Geyser Data" to "My First Shiny App"
- Where did you make the change? (UI or Server?)
- Re-run the app to see your edit

---

#### Hands-On Activity 2: AI-Generated App (15 minutes)

**Goal:** Build a simple app from scratch using AI assistance.

**The Challenge:**
Create an app that lets users explore the `mtcars` dataset by choosing which variable to visualize.

**Step 1: Write Your AI Prompt**

Open ChatGPT or your AI tool and paste this prompt:

```
Create a simple R Shiny app with the following features:

1. Use the built-in mtcars dataset
2. Add a selectInput that lets users choose a variable to visualize:
   - Options: 'mpg', 'hp', 'wt', 'disp', 'qsec'
3. Display a histogram of the selected variable
4. Include proper axis labels and a title
5. Use a clean layout with sidebarLayout
6. Add a brief text description above the plot explaining what the user is seeing

Please provide complete, runnable code in a single file.
```

**Step 2: Generate and Test**
1. Copy the AI-generated code
2. Create new R script: File → New File → R Script
3. Paste the code
4. Click "Run App"

**Step 3: Understand What Was Generated**

Review the code with a partner and identify:
- Where is `selectInput` defined? What parameter names do you see?
- How does the server access the user's selection?
- Where is the histogram created?
- What happens if you change `bins = 30` to `bins = 10`?

**Step 4: Customize (5 minutes)**

Ask the AI to modify your app:
```
Modify the app to:
1. Change the color of the histogram to blue
2. Add a second output showing summary statistics of the selected variable
3. Change the title to "Exploring Motor Trends Data"
```

**Key Takeaway:** You just built a working web app in <10 minutes. This would take hours without AI assistance.

---

### Part 3: Connecting to Di Cook's Work (45-75 minutes)

#### Setup: Loading BAPPENAS Data

**Step 1: Load Your Data**

```r
library(tidyverse)
library(shiny)

# Load the cleaned regional data from previous sessions
bappenas_data <- read_csv("bappenas_regional_clean.csv")

# Verify data structure
glimpse(bappenas_data)
```

**Expected columns:**
- `province` - Province name (character)
- `year` - Year (numeric, 2015-2023)
- `grdp` - Gross Regional Domestic Product (numeric)
- `employment` - Employment rate (numeric)
- `sector` - Economic sector (character)
- `population` - Population (numeric)

---

#### Hands-On Activity 3: From ggplot to Shiny (25 minutes)

**The Challenge:**
Remember the scatter plots you created with Professor Cook? Let's make them interactive!

**Step 1: Review Your Static Code (5 minutes)**

Here's a typical ggplot from Day 2:

```r
# Static visualization from Di Cook's session
ggplot(bappenas_data, aes(x = grdp, y = employment)) +
  geom_point(aes(color = sector), size = 3) +
  geom_smooth(method = "lm", se = TRUE) +
  facet_wrap(~province) +
  theme_minimal() +
  labs(title = "GRDP vs Employment by Province",
       x = "GRDP (Trillion IDR)",
       y = "Employment Rate (%)")
```

**Problem:** This shows ALL provinces at once. Hard to focus on one region.

**Step 2: AI Prompt to Convert to Shiny**

Use this prompt with your AI assistant:

```
Convert this ggplot code into an R Shiny app:

[Paste your ggplot code here]

Requirements:
1. Add a selectInput in the UI that allows users to choose ONE province
2. Filter the data in the server to show only the selected province
3. Keep all the ggplot styling (colors, theme, labels)
4. Add a title showing which province is selected
5. Display the plot in the main panel

Provide complete code in a single app.R file.
```

**Step 3: Generate and Debug (10 minutes)**

1. Copy the AI-generated code into a new script
2. Run the app
3. **Expected Issues and Fixes:**

**Issue 1: Plot is empty**
```
Error message might say: "object not found" or plot shows nothing

Fix prompt:
"The plot isn't showing. The data filtering isn't working. 
Here's my server code: [paste code]
How do I correctly filter the data based on input$province?"
```

**Issue 2: Province list is wrong**
```
Fix prompt:
"My selectInput should show province names from the data, 
but it's showing [what you see]. How do I populate choices 
dynamically from the dataframe?"
```

**Step 4: Enhance with AI (10 minutes)**

Now ask AI to add features:

**Enhancement Prompt 1: Add Summary Stats**
```
Add a second output below the plot that shows:
- Total GRDP for the selected province
- Average employment rate
- Number of data points

Display these as formatted text.
```

**Enhancement Prompt 2: Add Download Button**
```
Add a downloadButton that allows users to download 
the filtered data for the selected province as a CSV file.
```

**Step 5: Experiment and Share (5 minutes)**
- Try selecting different provinces
- Show your app to a neighbor
- Discuss: How would this be useful in a policy briefing?

---

#### Understanding Reactivity: A Deeper Look

**Key Concept: The Reactive Graph**

```
User Input → Reactive Expression → Output
   ↓              ↓                  ↓
input$province → filtered_data() → renderPlot()
```

**Example Code Pattern:**
```r
server <- function(input, output) {
  
  # REACTIVE EXPRESSION: Automatically updates when input changes
  filtered_data <- reactive({
    bappenas_data %>%
      filter(province == input$province)
  })
  
  # Use filtered_data() with parentheses - it's a function!
  output$plot <- renderPlot({
    ggplot(filtered_data(), aes(x = year, y = grdp)) +
      geom_line()
  })
  
  output$table <- renderTable({
    filtered_data() %>%
      summarise(avg_grdp = mean(grdp))
  })
}
```

**Why reactive()? Efficiency!**
- Without `reactive()`: Data filters twice (once for plot, once for table)
- With `reactive()`: Data filters once, both outputs use the result
- Critical for large datasets and complex calculations

---

### Session 3 Summary

**What You've Learned:**
- ✓ Shiny app structure (UI, Server, Reactivity)
- ✓ How to use AI to generate Shiny boilerplate code
- ✓ Converting static ggplot visualizations to interactive apps
- ✓ Basic debugging with AI assistance
- ✓ The power of reactive expressions

**Next Up:** Build a complete policy dashboard integrating visualization AND modeling!

---

## Session 4: Applied Dashboard Development
**Duration:** 75 minutes

### Part 4: The Project Brief (0-15 minutes)

#### "My First Policy Dashboard"

**Objective:** In the next 60 minutes, build a dashboard that integrates:
1. Data wrangling (Di Cook Session 1)
2. Visualization (Di Cook Session 2)
3. Modeling (Di Cook Session 3)
4. Interactivity (Today's Session 3)

#### Project Requirements Checklist

Your dashboard MUST include:

**Data Layer:**
- [ ] Load BAPPENAS regional economic dataset
- [ ] Clean and prepare data using tidyverse

**Interactivity:**
- [ ] At least ONE user input control
  - Examples: Province selector, year range slider, sector filter

**Visualization Output:**
- [ ] At least ONE interactive ggplot
  - Must update based on user input
  - Should include proper labels and theme

**Modeling Output:**
- [ ] At least ONE statistical model result
  - Examples: Linear regression summary, predictions, R-squared
  - Must update based on user input

**Layout:**
- [ ] Organized using `sidebarLayout` or `fluidRow/column`
- [ ] Clear title and instructions for users

**Bonus Features (Optional):**
- [ ] Download button for filtered data
- [ ] Multiple tabs using `tabsetPanel`
- [ ] Summary statistics with `valueBox` or `infoBox`
- [ ] Interactive table with DT package

---

#### Understanding the Dashboard Template

**Starter Code: template_app.R**

```r
# BAPPENAS Policy Dashboard Template
# Day 4 Workshop - Dr. Arif Perdana

library(shiny)
library(tidyverse)
library(broom)
library(DT)

# ===== DATA LOADING =====
# Load your cleaned data
data <- read_csv("bappenas_regional_clean.csv")

# Quick data check
glimpse(data)

# ===== USER INTERFACE =====
ui <- fluidPage(
  
  # Application title
  titlePanel("BAPPENAS Regional Economic Dashboard"),
  
  # Sidebar with input controls
  sidebarLayout(
    
    sidebarPanel(
      
      # TODO: Add your input controls here
      
      # Example: Province selector
      selectInput("province", 
                  "Select Province:",
                  choices = unique(data$province),
                  selected = "DKI Jakarta"),
      
      # Example: Year range slider
      sliderInput("year_range",
                  "Select Year Range:",
                  min = min(data$year),
                  max = max(data$year),
                  value = c(2015, 2023),
                  step = 1,
                  sep = ""),
      
      # Horizontal line separator
      hr(),
      
      # Help text
      helpText("Select province and year range to update visualizations and model results.")
      
    ),
    
    # Main panel with outputs
    mainPanel(
      
      # TODO: Add your output displays here
      
      # Tab layout for organized outputs
      tabsetPanel(
        
        tabPanel("Visualization",
                 h3("GRDP Trends"),
                 plotOutput("trendPlot", height = "400px"),
                 hr(),
                 DT::dataTableOutput("dataTable")
        ),
        
        tabPanel("Model Results",
                 h3("Predictive Model"),
                 verbatimTextOutput("modelSummary"),
                 hr(),
                 plotOutput("modelPlot", height = "400px")
        ),
        
        tabPanel("About",
                 h3("About This Dashboard"),
                 p("This dashboard demonstrates integration of:"),
                 tags$ul(
                   tags$li("Tidy data principles (Di Cook Session 1)"),
                   tags$li("Data visualization (Di Cook Session 2)"),
                   tags$li("Statistical modeling (Di Cook Session 3)"),
                   tags$li("Interactive applications (Arif Perdana Session 3-4)")
                 ),
                 p("Data source: BAPPENAS Regional Economic Indicators 2015-2023")
        )
      )
      
    )
  )
)

# ===== SERVER LOGIC =====
server <- function(input, output) {
  
  # REACTIVE DATA FILTERING
  # This automatically updates when user changes inputs
  filtered_data <- reactive({
    data %>%
      filter(
        province == input$province,
        year >= input$year_range[1],
        year <= input$year_range[2]
      )
  })
  
  # TODO: Add your render functions here
  
  # OUTPUT 1: Trend Plot
  output$trendPlot <- renderPlot({
    
    # Use filtered_data() with parentheses!
    ggplot(filtered_data(), aes(x = year, y = grdp)) +
      geom_line(size = 1.5, color = "steelblue") +
      geom_point(size = 3, color = "steelblue") +
      geom_smooth(method = "lm", se = TRUE, color = "darkred") +
      theme_minimal(base_size = 14) +
      labs(
        title = paste("GRDP Trends -", input$province),
        x = "Year",
        y = "GRDP (Trillion IDR)"
      )
    
  })
  
  # OUTPUT 2: Data Table
  output$dataTable <- DT::renderDataTable({
    filtered_data() %>%
      select(year, grdp, employment, population) %>%
      mutate(
        grdp = round(grdp, 2),
        employment = round(employment, 2)
      )
  }, options = list(pageLength = 5))
  
  # OUTPUT 3: Model Summary
  output$modelSummary <- renderPrint({
    
    # Fit linear model on filtered data
    model <- lm(grdp ~ year + employment, data = filtered_data())
    
    # Display tidy summary
    summary(model)
    
  })
  
  # OUTPUT 4: Model Diagnostic Plot
  output$modelPlot <- renderPlot({
    
    # Fit model
    model <- lm(grdp ~ year + employment, data = filtered_data())
    
    # Create predictions
    predictions <- filtered_data() %>%
      mutate(predicted = predict(model))
    
    # Plot actual vs predicted
    ggplot(predictions, aes(x = grdp, y = predicted)) +
      geom_point(size = 3, alpha = 0.6) +
      geom_abline(slope = 1, intercept = 0, color = "red", linetype = "dashed") +
      theme_minimal(base_size = 14) +
      labs(
        title = "Model Fit: Actual vs Predicted GRDP",
        x = "Actual GRDP",
        y = "Predicted GRDP"
      )
    
  })
  
}

# ===== RUN APPLICATION =====
shinyApp(ui = ui, server = server)
```

**Key Components Explained:**

1. **Data Loading Section:**
   - Load once, use throughout the app
   - Validate data structure with `glimpse()`

2. **UI Structure:**
   - `sidebarPanel`: Inputs on the left
   - `mainPanel`: Outputs on the right
   - `tabsetPanel`: Organize multiple outputs

3. **Server Logic:**
   - `reactive()`: Creates smart data filtering
   - `render*()`: Creates outputs that update automatically

4. **The TODO Sections:**
   - These are where YOU customize for your specific analysis

---

### Part 5: AI-Assisted Development Sprint (15-75 minutes)

#### Work Mode: Individual or Pairs (45 minutes)

**Getting Started:**

1. **Copy the template:** Save `template_app.R` as `my_dashboard.R`
2. **Choose your focus:** What economic question do you want to explore?
3. **Start coding:** Use AI to help you build!

---

#### AI Prompt Library for Your Dashboard

Use these prompts with your AI assistant (ChatGPT, Copilot, Claude):

**For Adding Input Controls:**

```
Prompt 1: Multiple Selection
"Add a checkboxGroupInput that allows users to select multiple 
sectors (Agriculture, Manufacturing, Services, Mining) and filter 
the data to show only selected sectors."

Prompt 2: Date Picker
"Replace the year slider with a dateRangeInput for selecting 
start and end dates. Format the dates as YYYY-MM-DD."

Prompt 3: Conditional Inputs
"Add a radioButtons input to choose between 'Province View' 
and 'National View'. Show the province selector only when 
'Province View' is selected."
```

**For Enhanced Visualizations:**

```
Prompt 4: Faceted Plot
"Modify the trend plot to show facets for each economic sector, 
comparing trends across sectors for the selected province."

Prompt 5: Interactive Plotly
"Convert the ggplot trend chart to plotly for interactive 
tooltips showing exact values on hover."

Prompt 6: Comparison Plot
"Create a bar chart comparing the selected province's GRDP 
to the top 5 provinces in the most recent year."
```

**For Modeling Outputs:**

```
Prompt 7: Multiple Models
"Fit three models: (1) linear trend, (2) quadratic trend, 
(3) with employment as predictor. Display all three R-squared 
values in a comparison table."

Prompt 8: Forecast Display
"Using the linear model, create predictions for the next 3 years 
beyond the data range. Display these forecasts in a table and 
add them to the trend plot as a dashed line."

Prompt 9: Model Diagnostics
"Create a 2x2 grid of diagnostic plots: residuals vs fitted, 
Q-Q plot, scale-location, and residuals vs leverage."
```

**For Advanced Features:**

```
Prompt 10: Download Functionality
"Add a downloadButton that exports the filtered data as an Excel 
file with two sheets: (1) raw data, (2) summary statistics."

Prompt 11: Dynamic Text Summary
"Add a textOutput that displays: 'The average GRDP growth rate 
for [province] during [year range] was [X]% per year.' 
Calculate X from the filtered data."

Prompt 12: Value Boxes
"Using the shinydashboard package, add three valueBox outputs 
at the top showing: (1) Total GRDP, (2) Average Employment, 
(3) Population, all formatted with appropriate units."
```

**For Layout Improvements:**

```
Prompt 13: Responsive Layout
"Convert the sidebarLayout to a more modern design using 
fluidRow and column with cards (using shinydashboard::box)."

Prompt 14: Custom Styling
"Add custom CSS to change the theme colors to match BAPPENAS 
branding: primary color #1e3a8a (blue), secondary color #10b981 (green)."

Prompt 15: Loading Indicators
"Add loading spinners to all plots and tables using the 
shinycssloaders package."
```

**For Debugging:**

```
Prompt 16: Error Diagnosis
"My app crashes with this error: [paste error message]
Here is my code: [paste code]
What's wrong and how do I fix it?"

Prompt 17: Performance Issues
"My app is slow when I change inputs. Here's my server code: 
[paste code]
How can I optimize performance?"

Prompt 18: Reactive Logic
"My plot isn't updating when I change the province selector. 
Here's my reactive code: [paste code]
What am I doing wrong?"
```

---

#### Development Milestones

**20 Minutes In - Basic Checkpoint:**
You should have:
- ✓ App running without errors
- ✓ At least one input control working
- ✓ At least one output displaying (even if simple)
- ✓ Basic filtering logic functional

**35 Minutes In - Feature Complete:**
You should have:
- ✓ Multiple input controls working together
- ✓ Reactive data filtering correct
- ✓ Visualization updating based on inputs
- ✓ Model results displaying
- ✓ Basic layout organized

**45 Minutes In - Polish Phase:**
You should be:
- ✓ Adding labels and titles
- ✓ Improving visual styling
- ✓ Testing edge cases (empty data, single year, etc.)
- ✓ Adding bonus features if time permits

---

#### Common Issues and Solutions

**Problem 1: "Object not found" Error**
```
Symptom: App crashes on load or when changing inputs

Common Causes:
- Typo in variable name
- Using input$ before it exists
- Forgetting parentheses on reactive: filtered_data vs filtered_data()

AI Fix Prompt:
"I'm getting 'object not found' error. Here's my code: [paste]
The error points to line X. What's the issue?"
```

**Problem 2: Plot Not Updating**
```
Symptom: Plot shows once but doesn't change when input changes

Common Causes:
- Not using reactive data inside renderPlot
- Using <- instead of reactive()
- Data filtering logic incorrect

AI Fix Prompt:
"My plot displays initially but doesn't update when I change [input name].
Here's my renderPlot code: [paste]
Why isn't it reactive?"
```

**Problem 3: Empty Plot/Table**
```
Symptom: Output area shows but is blank

Common Causes:
- Filter too restrictive (no matching data)
- Wrong column names in filter
- Data not loaded correctly

Quick Debug:
Add this inside your server:
observe({
  print(nrow(filtered_data()))
  print(names(filtered_data()))
})

Then check the R console for output when you change inputs.
```

**Problem 4: App is Slow**
```
Symptom: Long delay when changing inputs

Common Causes:
- Re-reading data file in server (should load once at top)
- Complex calculations not using reactive()
- Plotting entire large dataset

AI Fix Prompt:
"My app takes 5+ seconds to update. Here's my server function: [paste]
How can I improve performance?"
```

---

#### Advanced Challenges (For Fast Finishers)

If you complete the basic requirements early, try these:

**Challenge 1: Spatial Integration (Preview for Day 5)**
```
Prompt:
"Add a third tab with a leaflet map showing all provinces.
Color provinces by their GRDP value in the selected year.
When user clicks a province on the map, update the province 
selector to match."
```

**Challenge 2: Time Series Animation**
```
Prompt:
"Using the gganimate package, create an animated scatter plot 
showing how GRDP vs Employment evolves over years for the 
selected province. Add a play/pause button."
```

**Challenge 3: Comparative Analysis**
```
Prompt:
"Add a 'Comparison Mode' checkbox. When checked, allow users 
to select 2-3 provinces and display side-by-side comparison 
plots and statistics."
```

**Challenge 4: Report Generation**
```
Prompt:
"Add a 'Generate Report' button that creates a downloadable 
PDF report using R Markdown, including:
- Selected parameters
- All current plots
- Model summary
- Data table
Include BAPPENAS logo in header."
```

---

### Part 6: Showcase & Reflection (75-90 minutes)

#### Presentation Protocol

**Each group/individual will present for 3-4 minutes:**

**Structure Your Presentation:**

1. **Introduction (30 seconds):**
   - "My dashboard explores [economic question]"
   - "I focused on [specific provinces/sectors/time period]"

2. **Live Demo (2 minutes):**
   - Run your app
   - Show 2-3 key interactions
   - Highlight one feature you're proud of

3. **AI Assistance Story (1 minute):**
   - "I used AI to help with [specific task]"
   - "The most useful prompt was: [example]"
   - "I had to modify AI output because [reason]"

4. **Challenge & Solution (30 seconds):**
   - "One problem I faced was [issue]"
   - "I solved it by [approach]"

**Audience Participation:**
- Each presenter can receive 1-2 questions from peers
- Instructor will highlight interesting approaches

---

#### Reflection Discussion

**Group Discussion Questions:**

1. **AI as a Tool:**
   - When did AI help most? When did it struggle?
   - How did you verify AI-generated code was correct?
   - What's one thing you learned about prompting?

2. **Integration:**
   - How does Shiny connect to Di Cook's tidy data principles?
   - Where did your data wrangling skills help today?
   - How could you use this in your current BAPPENAS projects?

3. **Learning Process:**
   - What was easier/harder than expected?
   - What would you do differently next time?
   - What feature do you want to learn next?

---

#### Key Takeaways

**Technical Skills Acquired:**
- ✓ Understanding of reactive programming
- ✓ Ability to convert static analysis to interactive apps
- ✓ Effective AI prompt engineering for Shiny
- ✓ Debugging skills for Shiny applications

**Conceptual Understanding:**
- ✓ AI as coding accelerator, not replacement for understanding
- ✓ Importance of iterative development (prompt → test → refine)
- ✓ Integration of tidy data workflows with interactive outputs
- ✓ User-centered design for policy applications

**Practical Capabilities:**
- ✓ Can build functional dashboard in <2 hours
- ✓ Can customize templates for specific needs
- ✓ Can deploy and share apps with colleagues
- ✓ Can debug common Shiny issues independently

---

### Part 7: Next Steps & Resources (90+ minutes)

#### Deployment Options for Your Dashboard

**Option 1: shinyapps.io (Recommended for Beginners)**

**Pros:**
- Free tier available (5 apps, 25 active hours/month)
- Easiest deployment process
- No server management needed

**Setup Steps:**
```r
# Install deployment package
install.packages("rsconnect")

# Create account at shinyapps.io
# Copy your token from account settings

# Configure your account
library(rsconnect)
rsconnect::setAccountInfo(
  name="your-username",
  token="your-token",
  secret="your-secret"
)

# Deploy your app
rsconnect::deployApp("path/to/your/app")
```

**Full Tutorial:** https://shiny.rstudio.com/articles/shinyapps.html

---

**Option 2: RStudio Connect (For BAPPENAS Enterprise)**

**Pros:**
- On-premises hosting (data security)
- Authentication and access control
- Scheduled reports and email delivery
- Better for internal organizational use

**Requirements:**
- IT support for server setup
- License purchase (contact Posit)
- Integration with BAPPENAS infrastructure

**Contact:** Your IT department or https://posit.co/products/enterprise/connect/

---

**Option 3: Shinylive (Experimental)**

**Pros:**
- No server needed - runs in browser
- Free hosting via GitHub Pages
- Good for simple apps with small data

**Cons:**
- Limited to smaller datasets
- Still in development
- Not all R packages supported

**Learn More:** https://github.com/posit-dev/shinylive

---

#### Version Control and Collaboration

**Why Use Git/GitHub for Shiny Apps:**
- Track changes to your code over time
- Collaborate with colleagues
- Easy deployment to shinyapps.io
- Backup and version history

**Quick Start Guide:**

```bash
# In your app directory
git init
git add app.R data/
git commit -m "Initial dashboard version"

# Create repository on GitHub
# Follow instructions to push

git remote add origin https://github.com/yourusername/your-repo.git
git push -u origin main
```

**Resources:**
- Happy Git and GitHub for the useR: https://happygitwithr.com/
- GitHub Desktop (GUI option): https://desktop.github.com/

---

#### Continuing Your Learning Journey

**Essential Resources:**

**1. Mastering Shiny (Free Online Book)**
- Author: Hadley Wickham (creator of tidyverse)
- URL: https://mastering-shiny.org/
- Covers: Advanced reactivity, modules, testing, performance

**2. Shiny Gallery**
- URL: https://shiny.rstudio.com/gallery/
- Browse 100+ example apps with source code
- Filter by category: Healthcare, Finance, Science, etc.

**3. RStudio Community**
- URL: https://community.rstudio.com/c/shiny
- Ask questions, share apps, get help
- Very active and welcoming community

**4. Awesome Shiny Extensions**
- URL: https://github.com/nanxstats/awesome-shiny-extensions
- Curated list of packages that extend Shiny
- Themes, widgets, deployment tools

---

**Advanced Topics to Explore:**

**Shiny Modules:**
- Organize complex apps into reusable components
- Essential for large applications
- Tutorial: https://shiny.rstudio.com/articles/modules.html

**Shiny Dashboard:**
- Professional dashboard layouts
- Value boxes, info boxes, navigation
- Package: `shinydashboard`

**Performance Optimization:**
- Caching with `bindCache()`
- Async programming with `future` package
- Profiling with `profvis`

**Testing:**
- `shinytest2` for automated testing
- Ensures app works after code changes

**Authentication:**
- `shinymanager` for login screens
- LDAP integration for enterprise
- OAuth for external authentication

---

#### BAPPENAS-Specific Resources

**Templates and Examples:**

We've prepared templates specifically for BAPPENAS workflows:

1. **Economic Indicator Dashboard**
   - GRDP, employment, poverty visualization
   - Provincial and national views
   - Download: `bappenas_economic_template.R`

2. **IRIO Analysis Dashboard**
   - Input-output table explorer
   - Multiplier calculations
   - Sector linkage visualization
   - Download: `bappenas_irio_template.R`

3. **Spatial Economic Dashboard**
   - Integration with Day 5 material (A/Prof. Raschky)
   - Leaflet maps with economic data
   - Regional clustering analysis
   - Download: `bappenas_spatial_template.R`

**Data Sources:**

- `bappenas_regional_clean.csv` - Regional economic indicators 2015-2023
- `bappenas_irio_summary.csv` - Input-output summary tables
- `bappenas_spatial.geojson` - Province boundaries (for Day 5)

---

#### AI Tools: Best Practices

**Effective Prompting Strategies:**

**Be Specific:**
❌ "Make my app better"
✅ "Add a download button below the plot that exports filtered data as CSV"

**Provide Context:**
❌ "Why is this broken?"
✅ "My renderPlot isn't updating when I change input$year. Here's the relevant code: [paste code]. What's wrong?"

**Iterate:**
❌ Ask for everything at once in one huge prompt
✅ Build incrementally - get basic version working, then enhance

**Verify:**
❌ Trust AI output blindly
✅ Always test, read the code, understand the logic

---

**When to Use Which AI Tool:**

**ChatGPT:**
- Best for: Generating complete app structures
- Good for: Explaining concepts, providing alternatives
- Prompt style: Conversational, can iterate in thread

**GitHub Copilot:**
- Best for: Auto-completing code as you type
- Good for: Suggesting similar patterns, fixing syntax
- Works within: RStudio directly (inline suggestions)

**Claude:**
- Best for: Explaining complex code, debugging
- Good for: Understanding errors, architectural advice
- Prompt style: Can handle longer code snippets

---

#### Ethical Considerations

**Using AI Responsibly:**

**1. Attribution:**
- If AI generated significant portions of code, note it in comments:
```r
# Core reactive structure generated with ChatGPT assistance
# Modified by [Your Name] for BAPPENAS-specific requirements
```

**2. Understanding:**
- Don't deploy code you don't understand
- Use AI as a learning tool, not a black box
- Test thoroughly before sharing with stakeholders

**3. Data Privacy:**
- Don't paste sensitive data into AI tools
- Use dummy data when requesting help
- Be aware of your organization's AI usage policies

**4. Verification:**
- AI can generate plausible-looking but incorrect code
- Always validate outputs, especially statistical calculations
- Cross-reference with official documentation

---

## Datasets Reference

### Dataset 1: bappenas_regional_clean.csv

**Description:**
Cleaned regional economic indicators for Indonesian provinces (2015-2023)

**Columns:**

| Column | Type | Description | Example Values |
|--------|------|-------------|----------------|
| `province` | Character | Province name | "DKI Jakarta", "West Java" |
| `province_code` | Character | Province code | "31", "32" |
| `year` | Numeric | Year | 2015, 2016, ..., 2023 |
| `grdp` | Numeric | Gross Regional Domestic Product (Trillion IDR) | 2.56, 2.78, 3.02 |
| `grdp_growth` | Numeric | Annual GRDP growth rate (%) | 5.2, 5.8, 6.1 |
| `employment` | Numeric | Employment rate (%) | 94.2, 94.8, 95.1 |
| `population` | Numeric | Population (millions) | 10.2, 10.4, 10.6 |
| `sector` | Character | Economic sector | "Agriculture", "Manufacturing", "Services" |
| `sector_contribution` | Numeric | Sector contribution to GRDP (%) | 15.3, 35.2, 49.5 |
| `poverty_rate` | Numeric | Poverty rate (%) | 9.8, 9.2, 8.5 |

**Data Source:** BPS (Statistics Indonesia), cleaned and aggregated for workshop use

**Usage Example:**
```r
library(tidyverse)

# Load data
data <- read_csv("bappenas_regional_clean.csv")

# Quick exploration
glimpse(data)
summary(data)

# Example analysis
data %>%
  filter(year == 2023) %>%
  arrange(desc(grdp)) %>%
  head(10)
```

---

### Dataset 2: bappenas_irio_summary.csv

**Description:**
Simplified Input-Output table summary for Indonesia (2020)

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `sector_code` | Character | Sector classification code |
| `sector_name` | Character | Sector name |
| `output` | Numeric | Total output (Billion IDR) |
| `intermediate_input` | Numeric | Intermediate consumption |
| `value_added` | Numeric | Value added |
| `final_demand` | Numeric | Final demand |
| `export` | Numeric | Export value |
| `import` | Numeric | Import value |
| `output_multiplier` | Numeric | Output multiplier |
| `employment_multiplier` | Numeric | Employment multiplier |
| `backward_linkage` | Numeric | Backward linkage index |
| `forward_linkage` | Numeric | Forward linkage index |

**Usage Example:**
```r
# Identify key sectors
irio <- read_csv("bappenas_irio_summary.csv")

# Find sectors with highest multipliers
irio %>%
  arrange(desc(output_multiplier)) %>%
  select(sector_name, output_multiplier, employment_multiplier) %>%
  head(10)
```

---

### Dataset 3: mtcars (Built-in R Dataset)

**Description:**
1974 Motor Trend car data - useful for learning examples

**Columns:**
- `mpg`: Miles per gallon
- `cyl`: Number of cylinders
- `disp`: Displacement (cu.in.)
- `hp`: Horsepower
- `wt`: Weight (1000 lbs)
- `qsec`: 1/4 mile time
- `vs`: Engine (0 = V-shaped, 1 = straight)
- `am`: Transmission (0 = automatic, 1 = manual)
- `gear`: Number of forward gears
- `carb`: Number of carburetors

**Usage:**
```r
# Already loaded in R
data(mtcars)
head(mtcars)
```

---

### Dataset 4: gapminder (From gapminder Package)

**Description:**
Global development statistics (1952-2007)

**Installation:**
```r
install.packages("gapminder")
library(gapminder)
```

**Columns:**
- `country`: Country name
- `continent`: Continent
- `year`: Year
- `lifeExp`: Life expectancy
- `pop`: Population
- `gdpPercap`: GDP per capita

**Why Useful:**
- Similar structure to regional economic data
- Good for learning time series visualization
- International comparison examples

---

## AI Prompt Library

### Category 1: Getting Started Prompts

**Prompt G1: Create Basic Structure**
```
Create a Shiny app with:
- Title: [Your Title]
- Sidebar with [describe inputs]
- Main panel with [describe outputs]
- Use sidebarLayout
- Include helpful text instructions for users
```

**Prompt G2: Load and Preview Data**
```
Create a Shiny app that:
1. Loads the dataset from "data.csv"
2. Shows the first 10 rows in a table
3. Displays basic summary statistics
4. Includes a selectInput to choose which column to summarize
```

**Prompt G3: Simple Visualization**
```
Build a Shiny app using [dataset name] that:
- Has a selectInput for choosing the x-axis variable
- Has a selectInput for choosing the y-axis variable
- Displays a scatter plot with ggplot2
- Includes a linear regression line
- Uses theme_minimal()
```

---

### Category 2: Visualization Prompts

**Prompt V1: Interactive ggplot**
```
Convert this ggplot code into a Shiny renderPlot:
[paste your ggplot code]

Add controls to:
- Filter by [variable name]
- Adjust point size
- Change color scheme
```

**Prompt V2: Multiple Plot Types**
```
Create a Shiny app with a radioButtons input to choose plot type:
- "Scatter" -> scatter plot
- "Line" -> line plot
- "Box" -> box plot
Display the selected plot type using the same data.
```

**Prompt V3: Faceted Visualization**
```
Modify my renderPlot to:
- Add facet_wrap by [variable]
- Let users choose the number of columns via sliderInput
- Update the facet layout dynamically
```

**Prompt V4: Plotly Integration**
```
Convert my ggplot to plotly for interactive tooltips that show:
- Exact values on hover
- Province/region name
- Additional information from [column name]
Make it responsive and add zoom functionality.
```

---

### Category 3: Data Manipulation Prompts

**Prompt D1: Reactive Filtering**
```
Create a reactive expression that filters my dataset based on:
- input$province (province selector)
- input$year_range (slider with min and max)
- input$sector (checkbox group)
Return the filtered dataframe.
```

**Prompt D2: Dynamic Summary Statistics**
```
Add a renderTable output that shows:
- Mean, median, and sd of [variable]
- For the selected province and year range
- Formatted with 2 decimal places
- With clear column headers
```

**Prompt D3: Aggregation**
```
Create a reactive that:
1. Takes the filtered data
2. Groups by [variable]
3. Calculates sum, mean, and count
4. Returns a summary table
Use this in both a table output and bar chart.
```

---

### Category 4: Modeling Prompts

**Prompt M1: Simple Linear Model**
```
In the server function:
1. Fit a linear model: lm([outcome] ~ [predictor])
2. Use the filtered reactive data
3. Display the model summary in renderPrint
4. Show R-squared and coefficients clearly
```

**Prompt M2: Model Comparison**
```
Fit three models:
- Model 1: Simple linear trend (y ~ year)
- Model 2: With additional predictor (y ~ year + x)
- Model 3: With interaction (y ~ year * x)

Display a comparison table showing:
- Model name
- R-squared
- AIC
- Number of observations
```

**Prompt M3: Predictions**
```
Using the fitted model:
1. Generate predictions for the next 3 years
2. Calculate confidence intervals
3. Create a dataframe with: year, predicted_value, lower_ci, upper_ci
4. Display in a table and add to the trend plot as a dashed line
```

**Prompt M4: Tidymodels Integration**
```
Convert this tidymodels workflow to work in Shiny:
[paste your tidymodels code]

Update the workflow when user changes input$province.
Display:
- Model metrics (RMSE, R-squared)
- Variable importance plot
- Residuals plot
```

---

### Category 5: Layout and Styling Prompts

**Prompt L1: Tab Organization**
```
Reorganize my app to use tabsetPanel with tabs:
- "Overview": Summary statistics and key metrics
- "Visualizations": All plots
- "Model Results": Statistical outputs
- "Data": Interactive data table
- "About": Information about the dashboard
```

**Prompt L2: Sidebar Enhancement**
```
Improve my sidebar by:
- Grouping related inputs under headers
- Adding helpText below each input explaining what it does
- Including action buttons to "Apply Filters" and "Reset"
- Adding horizontal lines (hr()) as separators
```

**Prompt L3: Value Boxes**
```
Using shinydashboard, add a row of 4 valueBox widgets showing:
- Total GRDP (with icon "chart-line")
- Average growth rate (with icon "arrow-up")
- Number of observations (with icon "database")
- Latest year available (with icon "calendar")

Make them dynamically update based on filtered data.
Use color="blue" for positive metrics, color="yellow" for neutral.
```

**Prompt L4: Custom CSS**
```
Add custom CSS styling to my app to:
- Change the background color of the sidebar to #f0f0f0
- Make all headers (h3) blue (#1e3a8a)
- Add a subtle shadow to all plots
- Increase font size for readability
- Add the BAPPENAS logo in the top left
```

---

### Category 6: Advanced Features Prompts

**Prompt A1: Download Handler**
```
Add a downloadButton that exports:
1. The filtered data as an Excel file
2. With two sheets: "Data" and "Summary"
3. "Data" sheet: All filtered rows
4. "Summary" sheet: Basic statistics
Include the current date in the filename.
```

**Prompt A2: Dynamic UI**
```
Make the sector selector appear only when:
- User checks a box labeled "Filter by sector"
Use conditionalPanel or renderUI
Update the reactive filter accordingly.
```

**Prompt A3: Bookmarking**
```
Add bookmark functionality so users can:
- Save the current state (all input values)
- Get a URL they can share
- Return to the exact same view later
Use shiny::enableBookmarking
```

**Prompt A4: File Upload**
```
Add a fileInput that allows users to:
- Upload their own CSV file
- Validate it has required columns: [list columns]
- Replace the default dataset with uploaded data
- Show an error message if format is wrong
```

---

### Category 7: Debugging Prompts

**Prompt Debug1: Error Diagnosis**
```
I'm getting this error: [paste full error message]

Here's my code:
[paste relevant code section]

What's causing this error and how do I fix it?
```

**Prompt Debug2: Reactivity Issues**
```
My [output name] isn't updating when I change [input name].

Here's my reactive expression:
[paste reactive code]

Here's my render function:
[paste render code]

Why isn't it reacting to input changes?
```

**Prompt Debug3: Performance**
```
My app is very slow. It takes [X seconds] to update.

Here's my server function:
[paste server code]

How can I optimize this? Should I use reactive(), observe(), or isolate()?
```

**Prompt Debug4: Empty Output**
```
My plot/table shows up but is completely empty.

Filtering code:
[paste filter code]

Render code:
[paste render code]

Sample data:
[paste head(data, 3)]

What's wrong with my logic?
```

---

## Troubleshooting Guide

### Issue 1: App Won't Run

**Symptom:** Error immediately when clicking "Run App"

**Common Causes and Solutions:**

**Error: "Could not find function shinyApp"**
```r
# Solution: Load shiny library
library(shiny)
```

**Error: "Object 'ui' not found"**
```
Solution: Ensure ui and server are defined BEFORE shinyApp() call.
Check that you have:
ui <- fluidPage(...)
server <- function(input, output) {...}
shinyApp(ui, server)
```

**Error: "Cannot open file 'data.csv'"**
```r
# Solution: Check your working directory
getwd()
# Set to correct location
setwd("path/to/your/app")
# Or use relative path
data <- read_csv("data/data.csv")
```

---

### Issue 2: Inputs Not Working

**Symptom:** Moving slider or selecting option doesn't change output

**Diagnostic Steps:**

**Step 1: Check Input ID Matching**
```r
# In UI - input ID is "year_slider"
sliderInput("year_slider", ...)

# In Server - must use same ID
output$plot <- renderPlot({
  # Correct:
  filtered <- data %>% filter(year == input$year_slider)
  
  # Wrong (typo):
  filtered <- data %>% filter(year == input$yearslider)
})
```

**Step 2: Verify Reactive Context**
```r
# Wrong - reading input outside reactive context:
server <- function(input, output) {
  selected_year <- input$year  # This won't work!
  
  output$plot <- renderPlot({
    ...
  })
}

# Correct - read input inside render function:
server <- function(input, output) {
  output$plot <- renderPlot({
    selected_year <- input$year  # Now it's reactive!
    ...
  })
}
```

**Step 3: Check for Typos in reactive()**
```r
# Wrong - forgot parentheses:
output$plot <- renderPlot({
  ggplot(filtered_data, aes(x, y)) + ...  # filtered_data is a function, not data
})

# Correct:
output$plot <- renderPlot({
  ggplot(filtered_data(), aes(x, y)) + ...  # Call the function with ()
})
```

---

### Issue 3: Plots Not Displaying

**Symptom:** Empty space where plot should be, or gray box

**Solution Checklist:**

**1. Check render function matches output:**
```r
# UI declares plotOutput
plotOutput("myPlot")

# Server must have renderPlot with same ID
output$myPlot <- renderPlot({ ... })  # IDs must match!
```

**2. Ensure ggplot has data:**
```r
output$plot <- renderPlot({
  # Add validation
  req(filtered_data())  # Stops if data is NULL
  
  # Check if data is empty
  validate(
    need(nrow(filtered_data()) > 0, "No data matches your filters")
  )
  
  ggplot(filtered_data(), ...) + ...
})
```

**3. Check for ggplot errors:**
```r
# Common error: wrong aesthetics
ggplot(data, aes(x = wrong_column_name, y = ...))  # Column doesn't exist!

# Fix: Verify column names
names(filtered_data())
```

---

### Issue 4: Error Messages

**Error: "Operation not allowed without an active reactive context"**

**Cause:** Trying to read input$ outside of reactive context

**Fix:**
```r
# Wrong:
server <- function(input, output) {
  x <- input$slider  # Can't do this here!
}

# Right:
server <- function(input, output) {
  x <- reactive({
    input$slider  # Now it's inside reactive()
  })
  
  # Or use directly in render:
  output$text <- renderText({
    input$slider  # This works too
  })
}
```

---

**Error: "Promise already under evaluation"**

**Cause:** Circular reactivity (reactive depends on itself)

**Fix:**
```r
# Wrong - circular:
filtered <- reactive({
  data %>% filter(x == filtered()$y)  # Oops! Uses itself
})

# Right - break the cycle:
filtered <- reactive({
  data %>% filter(x == input$value)
})
```

---

**Error: "Evaluation error: object 'input' not found"**

**Cause:** Using input outside server function

**Fix:**
```r
# Wrong - data loading at top level
data <- read_csv("file.csv") %>%
  filter(year == input$year)  # input doesn't exist here!

# Right - filter inside server
server <- function(input, output) {
  filtered <- reactive({
    read_csv("file.csv") %>%
      filter(year == input$year)  # Now input exists
  })
}
```

---

### Issue 5: Performance Problems

**Symptom:** App is very slow, freezes, or times out

**Optimization Strategies:**

**1. Load data once, not repeatedly:**
```r
# Bad - reloads every time
server <- function(input, output) {
  output$plot <- renderPlot({
    data <- read_csv("large_file.csv")  # Don't do this!
    ...
  })
}

# Good - load once at startup
data <- read_csv("large_file.csv")  # Load once
server <- function(input, output) {
  output$plot <- renderPlot({
    # Use pre-loaded data
    ...
  })
}
```

**2. Use reactive() for shared calculations:**
```r
# Bad - filters data multiple times
server <- function(input, output) {
  output$plot <- renderPlot({
    filtered <- data %>% filter(province == input$prov)
    ggplot(filtered, ...)
  })
  
  output$table <- renderTable({
    filtered <- data %>% filter(province == input$prov)  # Duplicate work!
    summary(filtered)
  })
}

# Good - filter once, use many times
server <- function(input, output) {
  filtered <- reactive({
    data %>% filter(province == input$prov)
  })
  
  output$plot <- renderPlot({
    ggplot(filtered(), ...)  # Use cached result
  })
  
  output$table <- renderTable({
    summary(filtered())  # Use same cached result
  })
}
```

**3. Use isolate() to prevent unnecessary updates:**
```r
# Updates whenever ANY input changes - wasteful if many inputs
output$plot <- renderPlot({
  data %>%
    filter(
      province == input$prov,
      year == input$year,
      sector == input$sector
    ) %>%
    ggplot(...)
})

# Better - only update when action button clicked
output$plot <- renderPlot({
  input$update_button  # Depend on button
  
  data %>%
    filter(
      province == isolate(input$prov),    # Don't react to these
      year == isolate(input$year),
      sector == isolate(input$sector)
    ) %>%
    ggplot(...)
})
```

---

### Issue 6: Deployment Problems

**Symptom:** App works locally but fails on shinyapps.io

**Common Causes:**

**1. Missing packages:**
```r
# Solution: Add library() calls at top of app.R
library(shiny)
library(tidyverse)
library(DT)
# ... all packages you use
```

**2. Wrong file paths:**
```r
# Wrong - absolute path (only works on your computer)
data <- read_csv("C:/Users/YourName/Documents/data.csv")

# Right - relative path
data <- read_csv("data/data.csv")  # Assuming data/ folder uploaded too
```

**3. Large data files:**
```
Solution: shinyapps.io has file size limits
- Free tier: 1 GB total
- Compress data or use database connection instead
- Consider sampling for demo purposes
```

**4. Check deployment logs:**
```r
# View logs after deployment fails
rsconnect::showLogs()
```

---

## Resources for Further Learning

### Online Courses

**1. Datacamp: Building Web Applications with Shiny**
- Duration: 4 hours
- Level: Beginner to Intermediate
- Cost: Requires Datacamp subscription
- Link: https://www.datacamp.com/courses/building-web-applications-with-shiny-in-r

**2. RStudio Education: Shiny Workshops**
- Duration: Various (2-4 hours each)
- Level: All levels
- Cost: Free
- Link: https://education.rstudio.com/

**3. Coursera: Developing Data Products**
- Duration: 4 weeks
- Level: Intermediate
- Cost: Free to audit, certificate optional
- Link: https://www.coursera.org/learn/data-products

---

### Books (Free Online)

**1. Mastering Shiny by Hadley Wickham**
- Best for: Comprehensive learning
- Topics: Reactivity, modules, testing, deployment
- Link: https://mastering-shiny.org/
- Recommended chapters for beginners: 1-7

**2. Outstanding User Interfaces with Shiny**
- Best for: Improving app design
- Topics: UX, advanced layouts, JavaScript integration
- Link: https://unleash-shiny.rinterface.com/
- Recommended: Chapters on shinydashboard

**3. Engineering Production-Grade Shiny Apps**
- Best for: Professional development
- Topics: Project structure, testing, optimization
- Link: https://engineering-shiny.org/
- Recommended: When scaling beyond prototypes

---

### Video Tutorials

**1. Shiny Tutorial Playlist by RStudio**
- Platform: YouTube
- Duration: ~3 hours total
- Link: Search "RStudio Shiny tutorial" on YouTube
- Great for visual learners

**2. Statistical Analysis with R - Shiny Series**
- Platform: YouTube / Coursera
- Focus: Integrating statistics with Shiny
- Good complement to this workshop

---

### Package Documentation

**Essential Packages to Explore:**

**shinydashboard:**
- Professional dashboard layouts
- Docs: https://rstudio.github.io/shinydashboard/
- Example: https://rstudio.github.io/shinydashboard/examples.html

**DT (DataTables):**
- Interactive, searchable tables
- Docs: https://rstudio.github.io/DT/
- Features: Sorting, filtering, pagination

**plotly:**
- Interactive plots from ggplot
- Docs: https://plotly.com/r/
- Use: `ggplotly(your_ggplot)`

**shinyWidgets:**
- Enhanced input controls
- Docs: https://dreamrs.github.io/shinyWidgets/
- Includes: Better selectors, switches, date pickers

**leaflet:**
- Interactive maps (preview for Day 5)
- Docs: https://rstudio.github.io/leaflet/
- Integration: Add maps to your dashboards

---

### Community and Support

**1. RStudio Community Forum**
- URL: https://community.rstudio.com/c/shiny
- Very active, friendly community
- Post questions, share apps
- Search before posting - many questions already answered

**2. Stack Overflow**
- Tag: [r] [shiny]
- Good for specific technical questions
- Search first: https://stackoverflow.com/questions/tagged/shiny

**3. Shiny Contest**
- Annual competition showcasing best Shiny apps
- Gallery: https://www.rstudio.com/blog/winners-of-the-3rd-annual-shiny-contest/
- Great inspiration for features and design

**4. R-Bloggers**
- URL: https://www.r-bloggers.com/
- Search: "Shiny" for tutorials and examples
- Weekly Shiny tips and tricks

---

### BAPPENAS-Specific Resources

**Internal Resources:**

**1. BAPPENAS Data Portal**
- Access to official datasets
- API documentation for live data
- Contact: [Your data team contact]

**2. IT Support for Deployment**
- RStudio Connect setup
- Server access
- Authentication integration
- Contact: [Your IT contact]

**3. Colleague Network**
- Workshop alumni mailing list
- Monthly meetup for R users
- Code review partnerships

---

### Recommended Learning Path

**Week 1-2: Foundations**
- Complete Mastering Shiny chapters 1-3
- Build 3 simple apps using different datasets
- Practice with the mtcars dataset

**Week 3-4: Integration**
- Recreate one of your existing analyses as a Shiny app
- Add reactive filtering and multiple outputs
- Get feedback from colleagues

**Week 5-6: Enhancement**
- Add shinydashboard layout
- Integrate plotly for interactivity
- Deploy to shinyapps.io

**Week 7-8: Production**
- Build app for actual BAPPENAS project
- Add authentication if needed
- Deploy to RStudio Connect
- Train colleagues on usage

---

### Staying Current

**Follow These Accounts for Updates:**

**Twitter/X:**
- @rstudio (official news)
- @hadleywickham (tidyverse creator)
- @dataandme (R community curator)
- Hashtag: #rstats #shiny

**LinkedIn:**
- Posit (formerly RStudio)
- R programming groups

**Newsletters:**
- R Weekly: https://rweekly.org/
- Includes Shiny news and tutorials

---

## Appendix

### Glossary of Terms

**Reactive Expression:** A function that automatically re-executes when its dependencies change.

**Input:** User interface element that captures user interaction (e.g., slider, dropdown).

**Output:** Display element that shows results (e.g., plot, table, text).

**Render Function:** Server function that creates output (e.g., renderPlot, renderTable).

**UI (User Interface):** The visual layout and controls users interact with.

**Server:** The R code that performs computations and creates outputs.

**Observer:** Code that runs in response to reactive changes but doesn't return a value.

**Reactive Dependency:** When one reactive element depends on another, creating automatic updates.

**Isolate:** Function to read reactive values without creating dependencies.

**Session:** The connection between a user's browser and the Shiny server.

---

### Keyboard Shortcuts

**RStudio:**
- `Ctrl+Shift+Enter` (Win) / `Cmd+Shift+Enter` (Mac): Run current chunk
- `Ctrl+Enter` / `Cmd+Enter`: Run current line
- `Ctrl+Shift+K` / `Cmd+Shift+K`: Knit document
- `Ctrl+1` / `Cmd+1`: Focus on source pane
- `Ctrl+2` / `Cmd+2`: Focus on console

**When Running App:**
- `Ctrl+C` in console: Stop app
- `Esc`: Stop app (alternative)
- Browser refresh: Reload app

---

### File Structure Best Practices

**Recommended App Organization:**

```
my_dashboard/
├── app.R                 # Main app file
├── data/
│   ├── raw/             # Original data files
│   │   └── source.csv
│   └── clean/           # Cleaned data
│       └── data_clean.csv
├── R/
│   ├── data_processing.R    # Data cleaning functions
│   ├── plotting_functions.R # Custom plot functions
│   └── modeling.R           # Model functions
├── www/
│   ├── styles.css       # Custom CSS
│   ├── logo.png         # Images
│   └── script.js        # Custom JavaScript (if needed)
├── README.md            # Project documentation
└── .gitignore          # Git ignore file

```

**For Deployment:**
- Only include necessary files
- Compress large data files
- Remove intermediate/temporary files

---

### Complete Example: Minimal App

```r
# minimal_app.R
# A complete, working Shiny app in minimal form

library(shiny)
library(ggplot2)

# UI: What users see
ui <- fluidPage(
  titlePanel("Minimal Shiny App"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("n", "Sample size:", 10, 100, 50)
    ),
    mainPanel(
      plotOutput("histogram")
    )
  )
)

# Server: The R logic
server <- function(input, output) {
  output$histogram <- renderPlot({
    data <- rnorm(input$n)
    hist(data, main = paste("Histogram of", input$n, "random values"),
         xlab = "Value", col = "steelblue")
  })
}

# Run the app
shinyApp(ui, server)
```

**To run:** Save and click "Run App" in RStudio

---

### Acknowledgments

**Workshop Materials:**
- Based on materials by Professor Dianne Cook (Monash University)
- Integration with BAPPENAS datasets and use cases
- AI-assisted coding methodology development

**Data Sources:**
- BPS (Statistics Indonesia)
- BAPPENAS planning documents
- Synthetic data for workshop examples

**Special Thanks:**
- Monash University BAPPENAS Masterclass team
- Workshop participants for feedback
- BAPPENAS staff for data access and context

---

### Contact Information

**Workshop Facilitator:**
Dr. Arif Perdana  
[Contact details]

**For Technical Support:**
[BAPPENAS IT contact]

**For Further Learning:**
RStudio Community: https://community.rstudio.com/

---

### License and Usage

**Workshop Materials:**
These materials are provided for educational purposes for BAPPENAS Masterclass participants.

**Code Examples:**
All code examples in this guide are released under MIT License - free to use, modify, and distribute with attribution.

**Data:**
Workshop datasets are for educational use only. Contact BAPPENAS for permissions regarding actual data use in production applications.

---

## Quick Reference Cards

### Essential Function Reference

**UI Functions:**
```r
fluidPage()           # Main container
titlePanel()          # App title
sidebarLayout()       # Two-panel layout
sidebarPanel()        # Left sidebar
mainPanel()           # Right main area
tabsetPanel()         # Multiple tabs
tabPanel()            # Individual tab

# Inputs
sliderInput(id, label, min, max, value)
selectInput(id, label, choices)
checkboxInput(id, label, value)
radioButtons(id, label, choices)
dateRangeInput(id, label)
fileInput(id, label)
actionButton(id, label)

# Outputs
plotOutput(id)
tableOutput(id)
textOutput(id)
verbatimTextOutput(id)
uiOutput(id)
```

**Server Functions:**
```r
# Rendering
renderPlot({ ... })
renderTable({ ... })
renderText({ ... })
renderPrint({ ... })
renderUI({ ... })

# Reactivity
reactive({ ... })
observe({ ... })
observeEvent(input$x, { ... })
isolate({ ... })

# Validation
req(input$x)
validate(need(condition, message))
```

---

### Common Patterns Cheat Sheet

**Pattern 1: Basic Input → Output**
```r
ui <- fluidPage(
  sliderInput("x", "Value:", 1, 100, 50),
  textOutput("result")
)

server <- function(input, output) {
  output$result <- renderText({
    paste("You selected:", input$x)
  })
}
```

**Pattern 2: Reactive Data Filtering**
```r
server <- function(input, output) {
  filtered <- reactive({
    data %>% filter(category == input$category)
  })
  
  output$plot <- renderPlot({
    ggplot(filtered(), aes(x, y)) + geom_point()
  })
}
```

**Pattern 3: Action Button**
```r
ui <- fluidPage(
  actionButton("go", "Update"),
  plotOutput("plot")
)

server <- function(input, output) {
  data_to_plot <- eventReactive(input$go, {
    # Only runs when button clicked
    expensive_computation()
  })
  
  output$plot <- renderPlot({
    plot(data_to_plot())
  })
}
```

---

## End of Guide

**Congratulations!** You now have a comprehensive reference for building interactive Shiny applications with AI assistance.

**Remember:**
- Start simple, iterate
- Use AI as a tool, not a crutch
- Test thoroughly
- Share your work with the community

**Next Steps:**
1. Review this guide when stuck
2. Build your first real-world app
3. Join the RStudio Community
4. Keep learning and experimenting

**Good luck with your Shiny journey!**

---

*Last Updated: November 2025*  
*Version: 1.0*  
*BAPPENAS-Monash Masterclass 2025*
