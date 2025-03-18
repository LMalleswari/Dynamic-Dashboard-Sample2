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

    ![Image](https://github.com/user-attachments/assets/f65d6d0c-0495-45dc-9b9a-382b6a6c9bb4)

- step 5: Now create measures for dynamic selection of Total sales and catogry name for each category.

      1.For dynamic catogery name tile 

            Selected Category = 
                               var selectedCategory = SELECTEDVALUE(
                                                                  'Sales Data'[Category])
                               return 
                               IF(ISBLANK(selectedCategory),"",selectedCategory)


      2.For dynamic value of sales 

           selection value = 
                            var selectedvalue=SELECTEDVALUE(
                                                           'Sales Data'[Category])
                            return 
                            if(
                               ISBLANK(selectedvalue), "",
                                sum('Sales Data'[Sales])
                                )


- step 6: Now Drag card and add Selected Category to data , Also add an other card and add selection value to data and do all the format required .
   And place the bot cards in centet of donut chart .
     select all 3 charts and right click and group them. 

   ![Image](https://github.com/user-attachments/assets/b7a816ea-bdbe-4d7b-bea6-7537078d04f9) 

- step 7: Drag a new slicer and add year column to the field and do all required formatting.
  
- step 8: Create a new measure to display the current data 

           today = "Latest Date" & format(today(),"DD-MM-YYYY")

- step 9: Create a column for year ,month name, month number and measure to calculate the following.
    

              Month Name = FORMAT('Sales Data'[Order Date],"MMM")
              Month Number = MONTH('Sales Data'[Order Date])
              Year = YEAR('Sales Data'[Order Date])

      ## Measures 
        1.Current year Profit

           Current Year Profit = 
                              var selectedyear = SELECTEDVALUE('Sales Data'[Year])
                              var yeartouse = IF(
                                                 ISBLANK(selectedyear),
                                                 YEAR(TODAY()),
                                                 selectedyear
                                                 )
                              var profitvalue = CALCULATE(
                                                         [Total Profits],
                                                         'Sales Data'[Year]=yeartouse
                                                         )
                              return
                                   IF(
                                   ISBLANK(profitvalue),
                                   "No data",
                                   profitvalue
                                   )

          2.Profits dynamic title 

               Year Profit dynamic title = 
                                         var selectedYear = SELECTEDVALUE('Sales Data'[Year])
                                         var yearToUse = IF(
                                                         ISBLANK(selectedYear),
                                                         YEAR(TODAY()),
                                                         selectedYear)
                                         return "Profits for Year " & yearToUse 
    
           3.Current year sales

                Current year sales = 
                          var selectedYear=SELECTEDVALUE('Sales Data'[Year])
                          var yearToUse =IF(
                                        ISBLANK(selectedYear),
                                        YEAR(TODAY()),
                                        selectedYear
                                           )
                          var salesValue= CALCULATE(
                                         [Total Sales],
                                         'Sales Data'[Year]=yearToUse
                                                   )
                         return 
                             IF(
                               ISBLANK(salesValue),
                               "No data",
                               salesValue
                              )

           4.Sales dynamic title 
             
                   Year Sales dynamic title = 
                              var selectedYear = SELECTEDVALUE('Sales Data'[Year])
                              var yearToUse = IF(
                                                 ISBLANK(selectedYear),
                                                 YEAR(TODAY()),
                                                 selectedYear
                                                 )
                               return "Sales for Year " & yearToUse
    
            5.Previous Year Profit

                    Previous Year Profit = 
                                     var selectedYear = SELECTEDVALUE('Sales Data'[Year])
                                     var yearToUse = IF(
                                                      ISBLANK(selectedYear),
                                                      YEAR(TODAY()),
                                                      selectedYear
                                                      )
                                     var prevProfit = CALCULATE(
                                        [Total Profits],
                                        'Sales Data'[Year]=yearToUse-1
                                        )
                                     return
                                         IF(
                                            ISBLANK(prevProfit),
                                            "No data",
                                            prevProfit
                                            )

            6.Previous Year Sles

                    Previous year sales = 
                                  var selectedyear=SELECTEDVALUE('Sales Data'[Year])
                                  var yearToUse= IF(
                                                   ISBLANK(selectedyear),
                                                   YEAR(TODAY()),
                                                   selectedyear
                                                   )
                                  var prevSales = CALCULATE(
                                                   [Total Profits],
                                                   'Sales Data'[Year]=yearToUse-1
                                                   )
                                  return 
                                      IF(
                                         ISBLANK(prevSales),
                                         "No data",prevSales
                                         )

            7.Current Quarter Profit 

                      Current Quarter Profit =
                                        var selectedyear= SELECTEDVALUE('Sales Data'[Year],YEAR(TODAY()))
                                        var selectedquarter = QUARTER(TODAY())
                                        var quarterprofit = CALCULATE(
                                                               [Total Profit],
                                                               'Sales Data'[Year]=selectedyear,
                                                               'Sales Data'[QTR] = "Q" & selectedquarter
                                                               )
                        return 
                        IF(ISBLANK(quarterprofit),"No data",quarterprofit)

            8.Current Quarter Sales

                       Current Quarter Sales = 
                                        var selectedyear = SELECTEDVALUE('Sales Data'[Year],YEAR(TODAY()))
                                        var selectedquarter = QUARTER(TODAY())
                                        var quarterSales = CALCULATE(
                                                                [Total Sales],
                                                                'Sales Data'[Year]=selectedyear,
                                                                'Sales Data'[QTR]= "Q" & selectedquarter
                                                                     )
                                        RETURN
                                             IF(
                                                ISBLANK(quarterSales),
                                                "No data",
                                                quarterSales
                                                )

             9.Quarter Profit Dynamic Title

                        Quarter Profit Dynamic Title = 
                                              var selectedquarter =  SELECTEDVALUE('Sales Data'[QTR])
                                              var quarterToUse = IF(
                                                                ISBLANK(selectedquarter),
                                                                "Q" & QUARTER(TODAY()),
                                                                 selectedquarter
                                                                 )
                                              return "Profit for Quarter " & quarterToUse

             10.Quarter Sales Dynamic Title

                          Quarter Sales Dynamic Title = 
                                                   var selectedquarter = SELECTEDVALUE('Sales Data'[QTR])
                                                   var quartertouse = IF(
                                                                  ISBLANK(selectedquarter),
                                                                  "Q" & QUARTER(TODAY()),
                                                                  selectedquarter
                                                                  )
                            return "Sales for Quarter " & quartertouse


        
             11.Current Monthly Sales

                     Current Monthly Sales = 
                                         var selectedYear = SELECTEDVALUE('Sales Data'[Year],YEAR(TODAY()))
                                         var selectedMonth = SELECTEDVALUE('Sales Data'[Month Name],MONTH(TODAY()))
                                         var monthlysales = CALCULATE(
                                                               [Total Sales],
                                                               'Sales Data'[Month Number]=selectedMonth,
                                                               'Sales Data'[Year]=selectedYear
                                                               )
                                         return 
                                              if(
                                                 ISBLANK(monthlysales),
                                                 "No data",
                                                 monthlysales
                                                 )

            12.Current Monthly Profits

                      Current Monthly Profits = 
                                           var selectedYear = SELECTEDVALUE('Sales Data'[Year],YEAR(TODAY()))
                                           var selectedMonth = SELECTEDVALUE('Sales Data'[Month Name],MONTH(TODAY()))
                                           var monthlyprofit = CALCULATE(
                                                                   [Total Profits],
                                                                   'Sales Data'[Month Number]=selectedMonth,
                                                                   'Sales Data'[Year]=selectedYear
                                                                   )
                                           return 
                                               if(
                                                  ISBLANK(monthlyprofit),
                                                  "No data",
                                                  monthlyprofit
                                                  )


         13.Month Profit Dynamic Title

                         Month Profit Dynamic Title = 
                                             var selectedmonth = SELECTEDVALUE('Sales Data'[Month Name])
                                             var monthToUse =IF(
                                                      ISBLANK(selectedmonth)
                                                      FORMAT(TODAY(),"MMM"),
                                                      selectedmonth
                                                         )
                                             return 
                                             "Profit for Month " & monthToUse

          14.Monthly Sales Dynamic Title
                 
                         Monthly Sales Dynamic Title = 
                                              var selectedmonth= SELECTEDVALUE('Sales Data'[Month Name])
                                              var monthToUse = IF(
                                                 ISBLANK(selectedmonth),
                                                 FORMAT(TODAY(),
                                                 "MMM"),selectedmonth
                                                 )
                                             return 
                                                 "Sales for Month " & monthToUse


- step 10: Add Slicer for all the measures created.

![Image](https://github.com/user-attachments/assets/0e15450d-df96-4f1c-bcab-7e0161912986)



                        
