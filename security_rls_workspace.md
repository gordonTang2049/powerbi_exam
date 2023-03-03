###### Create report / dataset improvement / report alert
###### Workspace security - User level -  Admin, Member, Contributor, Viewer / Workspace admin / Woekspace setting / Power BI Premium / Organizational Custom Visual / permission

Workspace Roles Capability 
--------------------------------------------

    Capability	                                                                Admin	Member	Contributor	Viewer
    Update and delete the workspace.	                                        ✔️			
    Add or remove people, including other admins.	                            ✔️			
    Allow Contributors to update the app for the workspace.	                    ✔️			
    Add members or others with lower permissions.	                            ✔️	✔️		
    Publish, unpublish, and change permissions for an app.	                    ✔️	✔️		
    Update an app.	                                                            ✔️	✔️	If allowed 1	
    Share an item or share an app.2	                                            ✔️	✔️		
    Allow others to reshare items.2	                                            ✔️	✔️		
    Feature apps on colleagues' home.	                                        ✔️	✔️		
    Manage dataset permissions.3	                                            ✔️	✔️		
    Feature dashboards and reports on colleagues' home.	                        ✔️	✔️	✔️	
    Create, edit, and delete content, such as reports, in the workspace.	    ✔️	✔️	✔️	
    Publish reports to the workspace, and delete content.	                    ✔️	✔️	✔️	
    Create a report in another workspace based on a dataset in this workspace.3	✔️	✔️	✔️	
    Copy a report.3	                                                            ✔️	✔️	✔️	
    Create metrics that's based on a dataset in the workspace.3	                ✔️	✔️	✔️	
    Schedule data refreshes via the on-premises gateway.4	                    ✔️	✔️	✔️	
    Modify gateway connection settings.4	                                    ✔️	✔️	✔️	
    View and interact with an item.5	                                        ✔️	✔️	✔️	✔️
    Read data that's stored in workspace dataflows.	                            ✔️	✔️	✔️	✔️


    1 Contributors can update the app that's associated with the workspace, 
        if the workspace Admin delegates this permission to them. However, 
        they can't publish a new app or change who has permission to edit it.

    2 Contributors and Viewers can also share items in a workspace, 
        if they have Reshare permissions.

    3 To copy a report to another workspace, and to create a report in another workspace based on a dataset in the current workspace, 
        you need Build permission for the dataset. 
        For datasets in the original workspace, 
        if you have at least the Contributor role, 
        you automatically have Build permission through your workspace role. For details, see Copy reports from other workspaces.

    4 Keep in mind that you also need permissions on the gateway. 
        Those permissions are managed elsewhere, 
        independent of workspace roles and permissions. 
        For details, see Manage an on-premises gateway.

    5 If the items are in a workspace in a Premium capacity, 
        you can view and interact with items in the Power BI service 
        even if you don't have a Power BI Pro license.

######  WorkSpace Setting 
============================================================================================================
###### WorkSpace in Power Bi services

    Workspaces are places to 
    1. collaborate with colleagues 
        to create collections of 
            - dashboards
            - reports
            - datasets 
            - paginated reports
    

Use granular workspace roles for flexible permissions management in the workspaces: 
    Admin, Member, Contributor, and Viewer

Contact list:  -> Create a contact list 
    Specify who receives notification about workspace activity.

1. (Create Contact list)Create a workspace > 
        More options (...) > Workspace settings
            -> Advanced 
                - check Specific users and groups
                - Save

2. (Create Workspace Onedrive) (configure a Microsoft 365 Group whose SharePoint)
    Workspace OneDrive feature
        - configure a Microsoft 365 Group --->> SharePoint document library is available to ***workspace users***
        1. Create Group -> outside of Power BI
        2. available method OneDrive
    (may be disabled) creation of Microsoft 365 Groups may be restricted in your environment, and/or the ability to create them from your OneDrive site may be disabled. 
    speak with your IT department.
        workspace > 
        More options (...) > Workspace settings
            -> Advanced 
                - Workspace OneDrive
                - Save


###### Allow contributors to update the app
-> Admins 
-> Members
- By default, only workspace Admins and Members can create, publish and update the app for the workspace
    https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces#create-a-contact-list

    Under Advanced, expand Security settings. 
    -> Select Allow contributors to update the app for this workspace.
        


    Access the Allow contributors to update the app setting in one of two ways:
    

    nav pane, select the arrow next to Workspaces, select More options (...) next to the workspace name > Workspace settings. The Settings pane opens.

    When enabled
    contributors
    Can 
    - Update app metadata like name, icon, description, support site, and color.
    - Add or remove items included in the app, like adding reports or datasets.
    - Change the visibility of the items for all the audience groups in the audience tab.
    
    Can Not
    - Create or publish the app for the first time.
    - Add users to the app or change who has permission to the app.
    - Enable or disable automatic installation of app for app users.
    - Enable or disable advance settings under Manage audience access pane. These settings include share and build permissions for the datasets in the audience groups.
    - Allow or prevent app consumers saving a copy of reports included in the app.    


###### Premium capacity settings
###### License mode - Premium Per User (PPU) / Premium per capacity (PPC) / Embedded

 Settings  -> Premium capacity to On.

Premium Per User (PPU) gives organizations a way to license premium features on a per-user basis. 
PPU includes all Power BI Pro license capabilities, 
including features like paginated reports, AI, 
and other capabilities that were only available with a Premium capacity. 
With a PPU license, you don't need a separate Power BI Pro license because all Pro license capabilities are included.

###### Premium Per User (PPU)

    Feature description	                                            Per User	Per Capacity
    Model size limit	                                               100 GB	25-400 GB1
    Refresh rate	                                                    48/day	48/day
    Paginated reports	                                                    ✔	✔
    AI capabilities (AutoML, Impact Analysis, Cognitive Services)	        ✔	✔
    Advanced dataflows features, such as DirectQuery	                    ✔	✔
    Usage-based aggregate optimization	                                    ✔	✔
    Deployment Pipelines	                                                ✔	✔
    XMLA endpoint connectivity	                                            ✔	✔
    Enhanced automatic page refresh	                                        ✔	✔
    Incremental refresh	                                                    ✔	✔
    Multi-Geo support	                                                    X	✔
    Unlimited distribution                                              	X	✔
    Power BI reports on-premises	                                        X	✔
    Bring Your Own Key (BYOK)	                                            ✔ *	✔

    1 Depending on the type of SKU you have. For more details, see Capacities and SKUs.

Administration of Premium Per User (PPU) 
    (Unlike Premium capacity settings, PPU licenses don't require memory management or CPU management)
    (You can move workspaces between Premium Per User (PPU) and Premium capacities as needed.)

Administrators manage PPU licenses, users, and settings in the Power BI Admin portal. 
Admins can determine which per-user settings are exposed, which users can create PPU workspaces, which workspaces are Premium or Premium Per User, and other settings.

Once a Premium Per User (PPU) license is provisioned in a tenant, its features are available in any workspace where you turn them on.

Unlike Premium capacity settings, PPU licenses don't require memory management or CPU management, similar to how Pro licenses don't require such management. Tenant administrators can select feature settings for PPU licenses, but can't disable specific workloads.

You can move workspaces between Premium Per User (PPU) and Premium capacities as needed. Any such move requires a full refresh of datasets or dataflows in the workspace after you move it back to a Premium capacity. A limited set of APIs enable movement of workspaces, but they don't include actions such as turning off a workload.

Datasets in the Large Dataset format in Premium Per User (PPU) won't appear in the user interface.

Considerations and limitations

    - Premium Per User is the lowest entry-point for Power BI Premium features. It's built upon the Premium platform with built-in mechanisms ensuring that PPU users can use the platform’s ability to scale. PPU is designed to support enterprise workloads including Power BI items with size limits equivalent to that of a P3. For datasets, the 100-GB limit is documented in the Capacities and SKUs table.

    - Your entire PPU tenant has the same 100-TB storage limit that is applied to a Premium capacity.

    - PPU model refresh parallelism limits depend on the number of licenses your organization owns. The lowest PPU model refresh parallelism limit is 40, and the highest is 160.

    - If your PPU trial expires, you and your users can still access the workspace, but content that requires the license is unavailable. You must then either move the workspace to a Premium capacity, or turn off the requirement.

    - The export API for PPU is available for paginated reports, with a limit of one call every 5 minutes, per user. Power BI reports aren't supported.

    - The Export Power BI report to file REST API isn't supported for PPU.

    - The number of refreshes isn't restricted.

    - The Power BI Premium metrics app isn't currently supported for PPU.

    - You can't have a dataflow run in a PPU workspace, import it to a Power BI dataset in another workspace, and then allow users without a PPU license to access the content.

    - Any workspace migrated from a PPU environment to a non-PPU environment (such as Premium, Premium Gen2, or shared environments) must have its datasets refreshed before use. Reports opened after such migrations without being refreshed will fail with an error like: This operation isn't allowed, as the database 'database name' is in a blocked state.

