###### Reporting
----------------------------------------------------------------------------------------------------------------



pattern and trend analysis &animation 
========================================================================================
- Add the Play Axis (Dynamic Slicer) visual from AppSource
- Add a Scatter chart & set the Play Axis option 

Q: 
    - Pattern & trend analysis. 
    - use ***animation*** to show changes over time

    A: 
        - Add the Play Axis (Dynamic Slicer) visual from AppSource
        - Add a Scatter chart & set the Play Axis option 

    Explain:
        - scatter chart has a built-in play axis,  
            you can step through a time series using the Play Axis (Dynamic Slicer) visual from App Source.

        - (Play Axis - slicer to achieve the animation) Adding the date to the X-axis will work (continuous or not) 
            but you'll also need the Play Axis to step through the slicer to achieve the animation.

        - Adding ***relative date slicer*** does ***not*** do automatic ***animations***

        - Adding a series of bookmarks will be impractical for a large date range. 
            Also, the bookmarks do not automatically animate in view mode, you have to advance them manually.

High cardinality
========================================================================================

Q:
    Which column in the exhibit has the highest cardinality?
    - ***Add distinct and unique counts together***. ***High answer = high cardinality*** and vice versa.
    - Lower cardinality increases performance.
        https://docs.microsoft.com/en-za/learn/modules/optimize-model-power-bi/4-reduce-cardinality

    e.g. 
        1 Distinct 0 unique| 4 Distinct 4 unique| 2 Distinct 0 unique
        Col 1              | Col 2              |  Col 3
        1                   a                    a
        1                   b                    a
        1                   c                    b
        1                   d                    b

###### drillthrough 
========================================================================================
Put a Category to the drillthrough

###### KPI  
========================================================================================

Values Field
    - Margin (Target)(Percentage changes)
    - Status
    - Trend


To create a ***status*** Column

    VAR MarginPercentage = [Margin %]
    VAR MarginTolerance = 0.02
    VAR MarginGoal = [_Margin % Goal]
    RETURN
        IF(
            NOT ISBlank(MarginPercentage),
            Switch(
                TRUE,
                MarginTolerance < MarginGoal - MarginTolerance, -1
                MarginTolerance < MarginGoal + MarginTolerance, 1,
                0
            )
        )

To create a ***Trend*** Column

    VAR MarginPerc = [Margin %]
    VAR PrevMarginPerc =
        Calculate(
            [Margin %],
            PreviousYear('Date'[Date])
        )
    RETURN
        IF(
            NOT ISBlank(MarginPerc) && NOT IsBlank(PrevMarginPerc),
            Switch(
                True,
                MarginPerc > PervMarginPerc, 1, --Negative
                MarginPerc < PervMarginPerc, -1,
                0
            )
        )


###### Pin Visual
========================================================================================
    Pin > hover chart > ... > pin 
    Slicer can not be pined 

###### File types
========================================================================================
    .pbix -> default file format as Power BI Desktop report
        - contains the connection strings, data model, visualisations and any imported data.
        - save a Power BI report -> template file 
            - include the connection strings, 
            - data model 
            - visualisations
            - NOT the actual source data.
    .pbiviz
        - save a custom visual you created in a development environment.
    .pbids
        - the connection strings
        - NOT the data models
        - visualisations or source data.


###### Power BI Dashboards (Power BI Service feature)
========================================================================================
    - is a ***Power BI Service feature***
    - is limited to a single page(although you could scroll down nearly infinity)
    - not designed in Power BI Desktop    
    - pin visuals as tiles to dashboards from reports published to the Power BI Service.  
    - set a dashboard or a report as a favourite in the Power BI Service.  
    - mash several data sources together in ***Power Query***

###### Power BI model
========================================================================================
        Once loaded, it considered a ***single data set***

###### Power BI Embedding - Share External vs Internal
========================================================================================
Power BI Embedding
    - sharing your reports on web sites (internally or externally) or
    - ***SharePoint*** they are referring to ***embedding Power BI reports***.  
     
Power BU Embedded(Power BI Premium)
    - no license is required to view reports
    - possible to allow anonymous access under these conditions


Setting in report
Q:
    - created and published a reportfor your organisation's data analytics team. 
    - team members (including you) are only permitted to publish updated reports.
    - request the change through ***your organisation's change control system***
    - Your team -> ***Viewer role*** on the workspace in question.
    - allow your team the flexibility to make changes to visuals 
        (without going through the change control process)
        a. swap out a measures 
        b. dimensions
    How can you allow this without republishing the report?

    (contributor access)
    A: Change the report settings to allow Personalize visuals

    Explain:

        - Allowing Personalize visuals allows users to make changes to report visuals 
            without needing edit permissions or republishing the report.

        - contributor access to the workspace to change this setting.

        - Pinning visuals to a dashboard and allowing Q&A will achieve the goal in concept,
             but ***does not allow changing the visuals*** as is requested by the question. 

        (viewer role not allow Q&A to create new visuals)
        - Q&A to create new visuals (and then pin them to the dashboard), 
        but since the team has only viewer role

        (Distributing the .pbix file allow change the visuals, but require republishing report)
        Adding a Q&A visual to the report will not allow changing existing visuals and would require the report to be republished.
        Distributing the .pbix file to the users will allow them to change the visuals, 
        but again would require republishing the report for others to use. 
        
        https://docs.microsoft.com/en-us/power-bi/consumer/end-user-personalize-visuals


###### Alert / Notification
========================================================================================

Q:
    How do you configure a push notification on data in a ***Power BI Dashboard***? 

    A:
        - Available only for card, gauge or the KPI tiles
        - Click the elipses (...) button on the tile, then click manage alerts

    Explan:
    Push notifications are known in the Power BI Service as alerts.  
    They are available only for 
    KPI 
    and 
    card tiles 
    and is configured using the manage alerts menu item on the tile's ellipses (...) menu.

(Alerts) - Power BI Service feature
    available only for
        - Power BI Service
        - KPI
        - card tiles 
        - Open menu item on the tile's ellipses (...) menu


Q:
    You have pinned a card visual from one of your reports to a dashboard 
        in the Power BI Service as in the exhibit.
    Your dashboard users want an alert to be sent 
        when fewer than 50% of apps are games.
    Select the actions you must perform from the list. Each action represents part of the solution. (Choose 6)

    A:
        - Choose Manage alerts from move options on the card
        - Click + add alert rule
        - Choose below in the condition field
        - Set the threshold value to 0.5
        - check Send me email too checkbox
        - click Save and close 

    Explain:
        -configure alerts on the card in a dashboard, not on the dashboard itself
        Values formatted as percentage must be specified as absolute value on the alert (0.5 instead of 50%)

        The Send me email too checkbox must be 
            selected - this is the only way an email will be sent.
             Users must configure their own alerts - you can't configure this on their behalf.
        https://docs.microsoft.com/en-us/power-bi/create-reports/service-set-data-alerts


Power BI Service - pinned a card visual - one of your reports to a dashboard 
    (configure alerts on the card Only, not on the dashboard, when fewer than 50% of apps)
    - Users must ***configure their own alerts*** - ***you can't configure this on their behalf***.

(Legend field)(color the bar chart by fiscal year group)
Q: (How to display ***Fiscal year*** without changing ***calendar year***)
    Scenario
    - analysing your organisation's financial records
    - created a calendar table & related to the other tables ((Connected to Fact table)contains financial transaction data)
    - created several report pages and visuals
    - Some visuals shows data by ***calendar year***
    - financial department requires 
        a. option to view the data by fiscal year
    -How would you change your Power BI report to accommodate this new request?
    -How would you show ***what fiscal year the charted quantities*** belong to?
        ***Bar charts***

    A:
        Add Fiscal Year to the Legend field well of the visual  (Legend and become colored)

    Explan: 
    The best way visualise without replacing the calendar year
        - display the fiscal year in a different colour

(Config Alert)
Q:
    You have pinned a card visual from one of your reports to a dashboard 
        in the Power BI Service as in the exhibit.
    Your dashboard users want an alert to be sent 
        when fewer than 50% of apps are games.
    
    A:
        - Choose Manage alerts from move options on the card
        - Click + add alert rule
        - Choose below in the condition field
        - Set the threshold value to 0.5
        - check Send me email too checkbox
        - click Save and close 

    Explain:
        - configure alerts on the card in a dashboard, 
        - not on the dashboard itself
        - Values formatted as percentage must be specified as absolute value on the alert (0.5 instead of 50%)

        The Send me email too checkbox must be 
            selected - this is the only way an email will be sent.
             Users must configure their own alerts - you can't configure this on their behalf.
        https://docs.microsoft.com/en-us/power-bi/create-reports/service-set-data-alerts


Power BI Service - pinned a card visual - one of your reports to a dashboard 
    (configure alerts on the card Only, not on the dashboard, when fewer than 50% of apps)
    - Users must ***configure their own alerts*** - ***you can't configure this on their behalf***.



Q:
    - using a scatter chart visual to 
    compare 
        1. total revenue and 
        2. total returns for products as shown in the exhibit.
    Your plan is to use the 
        Automatically find clusters feature to 
            - identify groups of products with similar price/returns correlation. 
            - Where would you add the Products[Product Name] field?
        
        A:
            Detail
        
        Explain:
            https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-scatter
            https://docs.microsoft.com/en-us/learn/modules/perform-analytics-power-bi/6-time-series-analysis


Column chart & avaergae line 
Q:  
    - create a column chart showing sales per category 
    - another showing sales by manufacturer.  
    add an average line to 
        the category chart 
            from the analytics menu resulting in the visualisations.

    A:
        Edit interactions, select manufacturer chart, select filter on the category chart

    Explain:
        average line on the category chart 
            to change based on selections on the manufacturer chart

        1. set the interaction mode on the ***target chart (the category chart)*** to filter. 
        2. Setting the interaction mode to none or highlight will not change the average calculation. 

Relevant documentation is here: https://docs.microsoft.com/en-us/power-bi/service-reports-visual-interactions

<!-- ============================================================================== -->
***Report Navigation***
Q: a)
    Scenario
        - work for a educational institution. 
        - create a Power BI report for your organisation that analyses 
            --> different aspects of student enrolments into your various educational programmes 
                -> on several pages.
        >> publish the report, 
        >> ensure that ***users*** can see 
            >> an overview of the report on ***a single page*** 
            >> ***navigate to the different pages*** of the report easily.
    Solution
    -add bookmarks for each of the report pages
    -add an additional page to the report
    -add buttons with descriptions to the report contents to the new page
    -set the action for each button to bookmark and specify the bookmarks previously created

    A: 
        NO

    https://docs.microsoft.com/en-za/learn/modules/data-driven-story-power-bi/4-report-navigation

Q:  b)
    Solution
    -add an additional page to the report
    -add buttons with descriptions to the report contents to the new page
    -set the action for each button to page navigation and specify the pages previously created

    A: 
        YES

    https://docs.microsoft.com/en-za/learn/modules/data-driven-story-power-bi/4-report-navigation

Q: c)
    Solution
    -add an additional page to the report
    -add images that represents the different aspects of your report to the new page
    -set the action for each image to page navigation and specify the pages previously created

    A: 
        YES

    https://docs.microsoft.com/en-za/learn/modules/data-driven-story-power-bi/4-report-navigation

Q: d)
    Solution
    - You publish the report
    - You pin visuals from each page to a new dashboard

    A: 
        YES
    
    https://docs.microsoft.com/en-za/learn/modules/data-driven-story-power-bi/4-report-navigation

###### Q&A fields History Days
----------------------------------------------------------------------------------------------------------------

Q:
    How many days of question history is stored for questions typed into the ***Q&A fields***?

    A:
        28 days

###### Slicer / Sync Slicer 
###### Sync Slicer 
----------------------------------------------------------------------------------------------------------------
View > Sync Slicer 
    Sync Slicers can be selected for specific pages,
    ***Right Pane*** has checkbox for what 



###### Slicers
--------------------------------------------------
To change the visual in Slicer (Change way to Filter)(Change the slicer to checkbox)
    1. hover over Slicer
    2. Click drop down box
    3. Select the visual format

Mutiple Selection on Slicer
    Ctrl + Press or, 
    Format your visuals -> Visual -> Selection -> Single Select -> off (And) Mutiselect with Ctrl -> off
    

Viusal not ignore page filters. 


Q: 
    What is the ***difference*** between creating a 
        - page-level filter and 
        - adding a slicer visual?

    A:
        - A slicer by default filters content on the entire page
        - page filter by default filters content on the entire page

        - Visuals can be configured to ignore slicers
        
        - Slicer are manipulated at run-time 
        - Page filters are manipulated at run-time 

    Explain:

        Slicers and page filters filter the entire page by default, 
            but visuals can be set to ignore slicers with interaction mode.

        - Visuals can not ignore page filters. 
        - Slicers and page filters can manipulated at run-time.

        https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-slicers
        https://docs.microsoft.com/en-us/power-bi/power-bi-report-add-filter



    Also the check box select 
          Category
        [] A
        [] B
        [] C

    O------O
    --> Slicer is the Horitzontal Bar
        Hortzontal -> Categories Bottom

    - provide an interactive way for users
        - sort and filter a report 

         with 2 Big Dot


    -Filter charts using the date slicer, then bookmarks

    You can get back to an exact state when you select your saved bookmark. 
    This makes bookmarks ideal for creating a presentation in Power BI.

Question : Vertical Slicer to "horizontal list"

Q: get the same slicer into a "horizontal list" of buttons that automatically adapts to size changes

        A: 
            Change the orientation to Horizontal and Responsive on
     
        "Orientation change" -> setting to Horizontal -> ensure the visual will adapt to size changes, toggle the Responsive switch on.

###### Power Bi desktop Right side pane - Field / Visualizations / Filters / Analytics
====================================================================================================================================
###### Filters
------------------------------------------------------------------------------------------------------------
1. Filters on the Visual
    Filter only for selected chart, filter by selected value 
2. Filters on this page
    Selected value Filter apply to entire page
3. Filters on all pages
    Selected value Filter apply to all pages


###### Analytics Pane / display trend line (Scatter plots & line chart) / Pattern & trend analysis / Time Series chart
------------------------------------------------------------------------------------------------------------

    the Analytics pane, 
            you can create the following types of dynamic reference lines:

    Trend Line
        Color 
        Transparency
        Line Style
            Combine Series
            Use Highlight Values

    X-Axis constant line
    Y-Axis constant line
    Min line
    Max line
    Average line
        - Series -> Pick which data to write Line
        - Data Label 
            -> add figure on top of Average line
            -> Horizontal Posisiton -> Right / Left
            -> Vertical Position -> under / above line
            -> Style -> Name of the average line / Figure
            
    Median line
    Percentile line

Error Bars -> similiar bollinger band
    Upper bound of bollinger band 
    Lower bound

    -> Relationship to measure
        Relative -> it means +/- bound field, if field is 5000, means [Sales amount] + 5000 
        Absolute -> it means it is absolute value if sales amount is 1M , Set up the corresponding field as 2M

    (What-if parameter) Add Parameter allow user to put upper & lower bound them self

Forcast 
    If there is item in Legend, Forcast will disable

    - Ignore last (Compare the actual result to power bi forecast)
        What if we wanted to compare how the forecast compares to actual data? We can do this with the “Ignore last” setting.

        ignore the last 3 months of the data
        Power Bi will then forecast 3 months worth of data using the dataset but ignoring the last 3 months
        
        This way, we can compare the Power BI’s forecasting result with the actual data in the last 3 months of the dataset.

    - Seasonality
            the Seasonality setting lets you override the automatically detected season value. 
            For example, if you know your data comes from monthly observation, 
            you can set Seasonality to 12. 
            If the data comes from quarterly observation, you can set Seasonality to 4.

    Symmetry shading
    https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-analytics-pane

###### Analytics Pane -> Considerations and limitations
    The ability to use dynamic reference lines is based on the type of visual being used. The following lists describe these limitations more specifically.

x-axis -> constant line
y-axis -> constant line
symmetry shading on the following visual:

Scatter chart
    Use of constant line, min line, max line, average line, median line, and percentile line is available on these visuals:

Area chart
    Clustered bar chart
    Clustered column chart
    Line chart
    Scatter chart
    The following visuals can use only a constant line from the Analytics pane:

Stacked area chart
    Stacked bar chart
    Stacked column chart
    Waterfall chart
    100% Stacked bar chart
    100% Stacked column chart
    The following visuals can use a trend line if there's time data:

Area chart
    Clustered column chart
    Line chart
    Line and clustered column chart
    Scatter chart
    Lastly, you can't currently apply any dynamic lines to many visuals, including (but not limited to):

Funnel
    Line and clustered column chart
    Line and stacked column chart
    Ribbon chart
    Non-Cartesian visuals, such as Donut chart, Gauge, Matrix, Pie chart, and Table
    The percentile line is only available when using imported data in Power BI Desktop or when connected live to a model on a server that's running Analysis Service 2016 or later, Azure Analysis Services, or a dataset on the Power BI service.



###### Drill through / Page viusalization / Drill Down / Hierarchy 

Power BI automatic page
-----------------------------------------------------------------

Q: 
    In which of the following areas will you ***configure Power BI automatic page refresh***?

    A:
        Power BI Report page

    Explain:

    Power BI Desktop
    Power BI service


Usage :
When you monitor critical events, 
    you want data to be refreshed as soon as the source data is updated. 
    For example, in the manufacturing industry, 
    you need to know when a machine is malfunctioning or is close to malfunctioning. 
    If you're monitoring signals like social media sentiment, 
    you want to know about sudden changes as soon as they happen.        



     fixed interval  
     change detection
     
     

     When selecting Change detection as your refresh type,
     you are presented with a link to Add change detection.
     You can also access the change detection window from the Modeling tab in the ribbon.
     Then click on the Change detection icon on the Page refresh section.
     Finally, you can right-click or select the dropdown arrow next to any value in the Values well, 
     and select Change detection from the menu.

Drill Down
-----------------------------------------------------------------
>> Turn on Drill Down
    When Drill Down mode is turn on in the chart,
    click on the data (the particular bar in bar chart, etc),
    it will go down to the next level of data hierachy


Click-on Single arrow
grey background -> active

Double down - takes you to the next level in the hierarchy
Split down arrow - Expand all fields at once
Split down arrow - Expand adds an additional hierarchy level to the current view. 
Up Arrow - drill-up until you get back to "Total units this year by territory".


Show as a table to get a look behind the scenes. Each time you drill or expand, 
Show as a table displays the data being used to build the visual.
This may help you understand how hierarchies, 
drill, and expand work together to build visuals.


Considerations and limitations
-------------------------------------
By default, drilling ***won't filter other visuals*** in a report. 
However, the ***report designer*** can change this default behavior. 
As you drill, look to see if the other visuals on the page are 
    cross-filtering or 
    cross-highlighting.

Q: 
    ***False*** regarding Drill Down
    
From left to right in the exhibit:
    - Up arrow
    - Down arrow
    - Double down arrow
    - Split down arrow

    A: (False)

        -Double down arrow : Turn on Drill-down toggle
        -Double down arrow : Go to the last level down the hierarchy 
        -Down arrow : Add one level down hierarchy to the visual
        -Split down arrow : Go to the last level down the hierarchy

    
    Explain
    - Drill-down buttons are used for navigating up and down a hierarchy in a visual.
    - A good analyst knows 
        what happens when each of the drill-down buttons are used.
    Similarly, one that wants to pass the official exam will know these.

    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-drill



Page viusalization
    Q: 
    - report and have created the visualisation on Page 1 of your report as in the exhibit.
    - enhance this visualisation to show a different chart (chart 2) when you ***hover over*** the visual.
        (Chart 1 title - Total Revenue - has tool tips )
    - are ***not*** required to accomplish your goal

Steps Not require to achieve

    Ans: 
        1. On Page 2:
            - Select View
            - Select Page View
            - Select Tooltip

        2. On Page 1, on the Total Revenue chart:
            -Select Fields
            -in the Tooltip field
            -remove the quantity field

        3. On Page 1, on the Total Revenue chart:
            -Select Fields 
            -on the tooltip filed 
            -add Page 2

    Explain:
    To achieve Create chart
        The steps required are as follows:
            1. Create Page 2
            2. On Page 2, select Format > Tooltip > On
            3. On Page 2, select Format > Page Size > Tooltip
            4. Create chart 2   
            5. Back on Page 1, select the chart, from format choose tooltip, then page then specify Page 2
            https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-tooltips

Perform Drill through

    report page &  a detailed chart in a separate page using the drill through feature
    
    a detailed chart in a separate page using the drill through feature.

    The Sales page shows a visual of total sales by month.
    When you click on drill through on the sales by month chart, 

    redirect to a detail page -> Sales Detail -> selected month by category

    What FOUR actions should you perform?

        -On the Sales Detail page, under drill through option add month as the drill through field
        -Create a new page called Sales Detail
        -On the Sales Details page under Drill through, toggle Keep all filter on
        -Create a table visual to show total sales by month and Category


###### AI Sight / decomposition tree / key influencer
---------------------------------------------------------------------------------------
##### Apply AI Insights

1. Path to use ML (Home > Transform Data > Query editor > Add Column tab > Text Analytics / Vision / Azure Machine Learning)

2. No ML tools in Power Query -> Enable AI sight features
         - Power BI Desktop setting --> File > Options and settings > Options 
         - Global options -> Preview features -> (check box) AI Insight function browser option -> ok


AI Insights feature 
    - allows you to connect to a collection of pretrained machine learning models 
    - apply to your data to enhance your data preparation efforts.

Example 
    1. add text analytics to the content of the Comments field in the ticketing data. 
    2. determine the sentiment of the customers that are featured in the Help tickets. 

Text Analytics
    - includes Azure Cognitive Services models
        Sentiment Analysis
        Key Phrase Extraction
        Language Detection
    >> derive meaning or specific pieces of language from text data

Sentiment Analysis or Key Phrase Extraction option
    --> determine the customer sentiments in the Help tickets and visually show the results in Power BI
    https://learn.microsoft.com/en-za/training/modules/perform-analytics-power-bi/10-ai-insights


