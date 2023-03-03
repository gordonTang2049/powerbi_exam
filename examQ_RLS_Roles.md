Q:   
    - implementing row-level security for a Power BI report 
    - need to configure the Table filter DAX expression for one of the roles.
    - The role must only be able to see data for the "Europe" continent 
    - only for the "Bikes" product store - both fields from the Territories table. 
    Which of the following DAX expressions is correct for the requirement?
    
    A:
      1.  [Continent] = "Europe" && 
          [Store] = "Bikes"
      
      2.  AND (
        [Continent] = "Europe",
        [Store] = "Bikes"
      )


    Explan:
    The table filter DAX expression used with RLS must return a true/false value.
    If 
        more than one field must be evaluated the logic comparison or 
        operator must be used - in our case this is AND.  
        We can use the AND() function or the double-& operator for this purpose.  
        If the fields are in different tables, a single DAX expression is added to the tables individually. 
        
    https://docs.microsoft.com/en-us/power-bi/service-admin-rls


Q:
    Which of the following ***admin roles*** allow you to use ***the Power BI Service admin portal***?
        -admin roles
        -the Power BI Service -> admin portal

    A:
        - Power BI Service Administrator role
        - Office 365 Global Administrator role

    Explanation
        - PBI Service Admin
        - O365 Global Admin roles 
            have access to tools in the ***Power BI Service Admin portal*** 
            
        The other roles provide 
            access to different aspects of administering the Power BI Service,
        but only 
            the two roles specified 
            can use the Power BI Service admin portal features.
        https://docs.microsoft.com/en-us/power-bi/service-admin-administering-power-bi-in-your-organization#administrator-roles-related-to-power-bi


Q:
    You have created a report in Power BI and published it.  You ***intend sharing this report internally*** by ***embedding it in a web site***.  Which statement below is ***false***?

    A:
        Emdedding allows permitting anonymous access to the report (False)

    Explan:
        Embed is used internally, is secure, 
        requires a PBI Pro license to consume and a URL is created to the report.
        Anonymous access is not allowed.
        https://powerbi.microsoft.com/en-us/blog/easily-embed-secure-power-bi-reports-in-your-internal-portals-or-websites/

        Power BI Embedding should not be confused with Power BU Embedded, 

        although the terminology is often used interchangeably.  

        Consider the context of the question.  

        If the question has to do with sharing your reports on web sites (internally or externally) 
        or SharePoint they are referring to embedding Power BI reports.  

        If the question refers to embedding Power BI reports in custom applications, 
        they are referring to Power BI Embedded.

        The latter is similar of Power BI Premium where 
            no license is required to view reports, and theoretically, 
                
    (Share External vs Internal)

    Power BI Embedding
        - sharing your reports on web sites (internally or externally) or
        - ***SharePoint*** they are referring to ***embedding Power BI reports***.  
        - 

    Power BU Embedded(Power BI Premium)
        - no license is required to view reports
        - possible to allow anonymous access under these conditions


Q:
    While following the principal of least privilege, 
    select the appropriate workspace permission level that 
        allows a user 
        - add new members
        - assign the contributor role
    
    A:
        Member

    Explan
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-new-workspaces#roles-in-the-new-workspaces


PDF option
-------------------------------------
no PDF options in the tenant settings.


Q:
Config static Row-Level Security in Power BI, define associated with roles Configure option?

    A: Dataset Security

    Explaination : 
        https://docs.microsoft.com/en-za/power-bi/guidance/rls-guidance


Q: (Workspace - Add members to the group and add the group to the workspace)
    - already created a workspace in Power BI service
    - want to to store temporary source data files (OneDrive) for analysis. 
    - not yet added the members of your team to the workspace & want to ensure that all members of your team can collaborate in the workspace (and OneDrive)
    - must minimise ongoing access control administrative effort
    -->***NOT*** do to accomplish your goals

        A:
            - Add the members of your team to the workspace (want to manage access for both the workspace and Office 365 group separately)
            - Add the workspace to the office 365 group (Must add an Office 365 group to the work space)

    Explain:
        1. In the past when you created 
        a workspace in Power BI Service, 
        an Office 365 group was automatically created. 

        --> With modern workspaces, this is no longer the case. 
        If you want to take advantage of a shared OneDrive for the workspace,
        you must add an Office 365 group to the workspace. 
        This can be an existing or a newly created Office 365 group.

        To minimise ongoing access control administrative effort you would 
        not 
        want to manage access for both the workspace and Office 365 group separately. 

        So you want to add members to the group and add the group to the workspace. 
        Access control to your workspace is then managed through O365 group membership 
        and 
        not 
        directly on the workspace as you would normally do.

        ***You cannot add a workspace to the O365 group configuration.***
        https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces#set-a-workspace-onedrive
        https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-connect-to-files-in-app-workspace-onedrive-for-business

Q: Q14
data handling policy -> must be classified according to the level of sensitivity of the content
The classification levels  
    a. non-business 
    b. business general 
    c. confidential
Enable for data exported from the organisation's Power BI reports Action to perform?

    A:
        -Create and Publish labels in MS365 Security & Compliance Centre
        -Allow users to apply sensitiy labels for PowerBI content in the PowerBI admin center
        -Select the Sensitivity & Compliance Centre

    Explain: Sensitivity labels must be applied to Power BI content manually for this scenario
            https://docs.microsoft.com/en-za/power-bi/admin/service-security-sensitivity-label-overview
