# Adding the Event Calendar Application to Power Canvas Apps 

## SharePoint Calendar Setup

When creating a SharePoint site, such as a communication site, an Events calendar is automatically created. However, if one does not already exist, or you have an existing calendar you would like to use, just make note of the name and location.

![image-20250520083634259](/DocumentationImages/Screenshot%202025-05-20%20083556.png)

>  It is not required to use a SharePoint calendar. This application will also work if connected to a generic list or other data source so long as it contains the necessary columns. Note that when using a generic list, there may be  additional configuration required beyond the scope of this document.

Currently, this app uses the 'Category', 'Start Time',  'End Time', and 'Title' fields. However, more can be added to customize the calendar form.

![image-20250520085453273](/DocumentationImages/Screenshot%202025-05-20%20085448.png)

## Import & Configure the App

Once the calendar or list is setup, it is time to add the application to your Power Apps environment. If more than one calendar is required within the tenant, make sure that the name is changed during the import process in order to configure each calendar app as needed and to keep a separate reference when adding to the respective SharePoint page. 

### Import the app

In Power Apps Studio, click on the 'Apps' link found in the left-hand menu, then click on the 'Import app' link found in the ribbon. You can choose to select from either .msapp or .zip. For this walkthrough, we will be using a downloaded unmanaged .zip file.

![image-20250520090517777](/DocumentationImages/Screenshot%202025-05-20%20090515.png)

![image-20250520091320847](/DocumentationImages/Screenshot%202025-05-20%20091317.png)

After the .zip file has been uploaded, you should be routed to a new screen to review and complete import.

![image-20250520091431301](/DocumentationImages/Screenshot%202025-05-20%20091343.png)

In order to change the name of the application, click on the "Create as new" link, and you should be presented with an option to change the Resource Name and save. Once completed, click on the 'Import' button.

![image-20250520091650361](/DocumentationImages/Screenshot%202025-05-20%20091633.png)

![image-20250520091736009](/DocumentationImages/Screenshot%202025-05-20%20091733.png)

Click on the "Open app" link after it has been imported to begin the next configuration steps.

### Configure the app

Upon opening of the app, you will see many errors. This is because no data source is currently associated with the app. BUT before we connect the data source, we will first configure the UI.

![image-20250520092144803](/DocumentationImages/Screenshot%202025-05-20%20092016.png)

Navigate to the App.OnStart of the newly imported app and add/change the values in the 'ClearCollect' to mimic the choices in the "Category" SharePoint column. Each value will be the location. The 'Color' and 'TextColor' are for assigning the look up the display.

![image-20250520093619447](/DocumentationImages/Screenshot%202025-05-20%20093220.png)

Next, change "Events" to whatever your calendar is named. Since I am using the default collaboration site's calendar, I will keep "Events" for this demo.

Next, for the gallery representing the legend, ensure that the same data source is used. This is to retrieve the choices that are in SharePoint.

![image-20250520094056401](/DocumentationImages/Screenshot%202025-05-20%20093942.png)

Now, we need to add the data connection using a SharePoint connector. Select the site that contains your calendar or list.

![image-20250520094535579](/DocumentationImages/Screenshot%202025-05-20%20094518.png)

When dealing with calendars, you will need to manually add the name of the calendar list by clicking on the checkbox marked, "Enter a custom name" and type the name of your calendar (in this case, Events).

![image-20250520094754183](/DocumentationImages/Screenshot%202025-05-20%20094557.png)

Once you connect to it, the errors should be removed from the screen. In order to see everything properly however, you need to run the App.OnStart or save and refresh the application. 

![image-20250520094945058](/DocumentationImages/Screenshot%202025-05-20%20094942.png)

![image-20250520095035666](/DocumentationImages/Screenshot%202025-05-20%20095033.png)

Now when adding something to the calendar with the specific category, it will show up and can be filtered by category by clicking on an item in the legend. and you may reset all by clicking the reset button next to the legend's title.

![image-20250520095405377](/DocumentationImages/Screenshot%202025-05-20%20095355.png)

![image-20250520095427768](/DocumentationImages/Screenshot%202025-05-20%20095424.png)

Lastly, clicking in the calendar item brings up the details using an overlay. You need to pass the information you want to see on the detailed overlay by using when the item is clicked by using the OnSelect of the child gallery ('Gallery2')

```typescript
UpdateContext(
    {
        ShowDetails: true,
        Title: ThisItem.Title,
        Category:ThisItem.Category,
        Description:ThisItem.Description
    }
)
```

Then in the dialog, you need to simply reference the context variable to display the information.

![image-20250520100123489](/DocumentationImages/Screenshot%202025-05-20 100116.png)

## Running the Completed App

Final step is to save and publish the app to use as a stand-alone or embedded in SharePoint as an example.

## Other Thoughts

If the SharePoint calendar or list is set up with a flow that runs when an item is created, it could copy the information to a Master Calendar/List displaying multiple site calendars. 
