###### DirectQuery vs m Code vs Power Query vs Dax vs advance query
    
    -Import Data -> cache Data -> fast & less space use
    -DirectQuery -> Pull Schema not data itself
    
        DirectQuery limitation
            from power query and DAX

    -Live Connection
        Analysis Services -> powerBI -> powerBI Dataset
            No change with model

    -Composite Model
        Mix and Match


     Azure SQL database -> connect with  -> By setting the data connectivity mode to DirectQuery
            While connecting to a data source in Power BI Desktop, it is always possible to import a copy of the data in Power BI Desktop.
             Some data sources have the option of connecting directly to the data source using DirectQuery. 
             With the DirectQuery option, no data is imported or copied to Power BI Desktop. 
             For relational sources, the chosen columns and tables appear in the Fields list.
              In multi-dimensional sources such as SAP Business Warehouse, 
              the dimensions and measures for the chosen cube appear in the Fields list. 
              As you interact with the visualization, Power BI queries the underlying data source and you always view the current data.


###### Power Query Editor-> Column quality vs profile vs distribution

    -Column Quality
    -Column distribution
    -Column profile 
        are data profiling functionalities under the View tab in Data Preview Section. 
        These functionalities help in understanding the data anomalies and statistics. 
        Out of these three functionalities, Column quality is the one that can be used to show the percentages of data that is in error, empty and valid.

    Column profile ->
        provides a deeper look into the statistics within the column. 
        This column can be used to provide many different values like the count of rows 
        but it does not help in identifying the percentage of empty cells in the column.

    Column Quality ->
        Column quality is the data preview option that is used to show the percentages of data that is in error, empty and valid.        

    Column distribution ->
        displays the data distribution within the column and the counts of unique and distinct values. It is not the right choice for the target goal.

###### the dataset settings
    it has user Q&A comment session enable

    no -> Check the cardinality for the columns in the dataset

###### RLS 

    RLS roles that use the DAX functions USERNAME and USERPRINCIPALNAME are examples of dynamic RLS roles

    B. 1-2-3-5-4-6
    1. Create a report in Microsoft Power BI Desktop that involves import the data, confirm the data model between both tables, and create the report visuals.
    2. Create RLS roles in Power BI Desktop by using DAX.
    3. Test the roles in Power BI Desktop.
    4. Add members to the role in the Power BI service.
    5. Deploy the report to Microsoft Power BI service.
    6. Test the roles in the Power BI service.


###### decomposition tree & Key influencer


###### Admin Feature only
    Creating a report in another workspace depending upon the dataset of this workspace


###### query editor -> where the query at the beignning of importing the ds

    There are steps of queries, if I want to split your query into two parts,
    I right click "Extract previous"

    resharpe transform and then load data into data model

###### Active vs Inactive relationship and relationship

type of cardinality describes the ideal type of table relationship


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



Salary_Cost having Q&A enabled on it.
 When a user tries to get the count of Employees, 
 the query gets failed. 
 On the other hand, when the user asks for the count of workers

C. Editing synonyms from the Power BI Desktop

When you are interested in improving the Q&A experience, it is always a good practice to add synonyms from the Power BI Desktop Model view.

###### resources
    https://www.whizlabs.com/blog/da-100-exam-questions/

    **Scrope**
    https://www.mssqltips.com/sqlservertip/7285/microsoft-exam-pl-300-microsoft-power-bi-data-analyst-prep-guide/



    