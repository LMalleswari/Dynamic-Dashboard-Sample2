# Dynamic-Dashboard-Sample2
This dynamic Power BI dashboard features metrics that update dynamically, providing real-time sales insights, trend analysis, and key performance indicators to support data-driven decision-making

### Dashboard Link :

## Problem Statement

This dashboard presents sales data across different regions, enabling users to analyze quarterly sales and profits dynamically. It provides insights into various regions, categories, and subcategories for the years 2021–2025.

### Steps followed

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : It was observed that in none of the columns errors & empty values were present.

- step 4: Under report view , drag Donut chart and add category column to Legend and total sales in values . In visuaization under format turn off the legend ,under slice set spacing to 75% ,under detail labels set label contents to Category column  and under values make all the format changes.Under general turn off title, under Effects set transparency to 100%.

    image 1

- step 4: Now create a measure for dynamic selection of Total sales for each category.

           selection donut = var selectedvalue=SELECTEDVALUE('Sales Data'[Category])
                  return 
                  if(ISBLANK(selectedvalue), "",
                                sum('Sales Data'[Sales])
                                )
