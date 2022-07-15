###### Active vs Inactive relationship



###### M code vs Dax Function 
    M code is for Data processing Manuplation 
    Dax Function is for Viusalize data


##### Dax Function

###### Corss Filter
    -----------------------------------------------------------------------
        CorssFilter(col1, col2, direction)
        
        - Col1 Many Side of the relationship
        - Col2 One side or lookup side of the relationship
        - Direction -> None , Both, Oneway, OneWay_LeftFiltersRight, OneWay_RightFiltersLeft

    Data Model

        DimProduct attribute                    Fact_Sales              DimSalesCountry
            - Arabic Description                -ProductKey             -SalesCountry
            - Chinese Desc                      -Product Number         -SalesGroup
            - Color
            - etc.....

        DimSalesCountry -> filtering FactSales  but FactSales does not filter DimProduct attribute
        therefore -> cross filter


        Business Question:
            ***Each country -> how many colors the product are selling
            
color Distn Count = Distinctcount(DimProduct[Color])  ==>it will all same numebr, because fact table does not filter color 
    
    |country    | Color||
    Australia    10
    Canada       10
    
Should Write code


        Country -> Fact -> Product

        To Link the filter From Fact to Product

    MEASURE Cross filter color Count = Calculate(Distinctcount(DimProduct[Color]), 
        CrossFilter(FactInternetSales[ProductKey]), DimProduct[ProductKey], Both) 

###### TREATAS -> treatAs
    -----------------------------------------------------------------------
    One Table has not been related

    Business question : want to see Expense Vs Sales?

    issues 
        Expense is at month Level 
        Sales is at day level

    Data Model
                                                            This is daily 
        Product_Master          Sales                      DimDate
            -Category Name      -Cost Amount                -Date
            -Cost Price         -Cost Per Unit              -DayName
                                -Customer Name              -Etc...

                                                                No Relationship with the Fact sales table
                                                            MonthlyExpense
                                                                -Expense
                                                                - Month
                                                                -Year
**I can also apply filter**

    MEASURE Expense Total = Calculate(Sum(MonthlyExpense[Expense]), 
        TreatAs(Summarize(DimDate, DimDate[Year], DimDate[Month]), 
        MonthlyExpense[Year], MonthlyExpense[Month]),
        DimDate[month] = "December"
        )



-----------------------------------------------------------------------
###### SelectedValue

    Data table 
        Location       Year     Month

    When user select One Month, It is only shows that one month 

    e.g. When User Select June User wants to show from January to June 
    
    Default From Jan to Dec

    // Create Table for all Months name\
    // Filter the measures
1. Table Tools -> New Table 

    MonthList = Summarize(DimDate, DimDate[Month], DimDate[MonthNum])


    // Param1 -> From what ds
    // Param2 -> Default Value select till
// This will return what Month Value you Selected  
    Sales Till Selmonth = Var sm = SELECTEDVALUE(MonthList[MonthNum],12)
    return sm

// Actual Calculation
    Sales Till Selmonth = Var sm = SELECTEDVALUE(MonthList[MonthNum],12)
    return Calculate(Sum(Sales[Sales Amount]), FILTER(DimDate, DimDate[MonthNum] <= sm) )

        

**Tips**
    Use Column Tools -> Sort by Column -> To Sort with right order


USERELATIONSHIP 

RELATEDTETABLE 

RELATED 


###### query editor -> where the query at the beignning of importing the ds

    There are steps of queries, if I want to split your query into two parts,
    I right click "Extract previous"



###### Look up table & data table
    - Look up table -> Dimension Table
    - Data Table -> Fact Table


###### Slicers
    O------O
    --> Slicer is the Horitzontal Bar
        Hortzontal -> Categories Bottom

    - provide an interactive way for users
        - sort and filter a report 

         with 2 Big Dot

###### Key Influencer

    
Q 1. You are interested in creating a measure that will always calculate the total sales for 2020, 
irrespective of the year selected in any other visual in Power BI. Which of the following is the right way to create such a measure?

A. Total Sales for 2020= CALCULATE(SUM(‘Sales OrderDetails'[Total Price]), YEAR(‘Sales OrderDetails'[orderdate]) = 2020)

B. FORMAT([Date],”MMMM DD, YYYY”)



data model has an impact on the time consumed in the refreshing of a model but once the model is loaded in the memory,
no impact on the performance of the reports

measures still affect performance

    False
the measures need to iterate over more data and therefore the evaluation is likely to consume more time that will certainly affect the performance of the reports. Therefore, reducing the size of the data model by removing the unnecessary rows or columns will help in improving the performance of the reports.


2019 Salary_Cost = CALCULATE([Total Salary_cost], Filter (Date, Date[Year]=2019))
    C. Blank. It will return no records.


C. CROSSFILTER -> DAX function that takes the two columns and set the cross filter relationship between these columns.
    DAX function to modify a single directional relationship to a bi-directional relationship on the fly (within the measure)


###### resources
    https://www.whizlabs.com/blog/da-100-exam-questions/

    **Scrope**
    https://www.mssqltips.com/sqlservertip/7285/microsoft-exam-pl-300-microsoft-power-bi-data-analyst-prep-guide/