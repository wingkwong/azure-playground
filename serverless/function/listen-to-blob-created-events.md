# Create an Azure Function to Listen to Blob Created Events

## Scenario
Your need to process images uploaded to a blob container. You decide to create an Azure Function that is triggered by an Event Grid wired to blob-created events in the storage account. To test the concept, you create the function, configure the Event Grid subscription, and write the event data to the functions log.

## Prerequisites

- Existing Resource Group
- Existing App Service plan
- Existing App Service
- Existing Storage Account

## Log In to the Azure Portal

Log in to the Azure Portal using your credentials

## Create the Event Grid-Triggered Function

Open the menu in the top-left corner and select All resources.

![image](https://user-images.githubusercontent.com/35857179/78986096-04bea780-7b5d-11ea-9af7-c43a187ac32b.png)

Click on the app service.

![image](https://user-images.githubusercontent.com/35857179/78986152-2fa8fb80-7b5d-11ea-9938-b2bb79507463.png)

In the left-hand pane, select the Functions row.

![image](https://user-images.githubusercontent.com/35857179/78986213-55ce9b80-7b5d-11ea-9aef-d688ff2c2ec8.png)

Click + New function.

![image](https://user-images.githubusercontent.com/35857179/78986272-7b5ba500-7b5d-11ea-9b93-37a432e849ee.png)

Select the Azure Event Grid trigger box from the list.

![image](https://user-images.githubusercontent.com/35857179/78986304-929a9280-7b5d-11ea-9311-39efb2b456df.png)

Enter "MyEventGridTrigger" without quotes in the Name box.

![image](https://user-images.githubusercontent.com/35857179/78986350-afcf6100-7b5d-11ea-8895-23bc7e34bdfe.png)

Click Create.

You should see the sample C# script (.csx).

```csharp
#r "Microsoft.Azure.EventGrid"
using Microsoft.Azure.EventGrid.Models;

public static void Run(EventGridEvent eventGridEvent, ILogger log)
{
    log.LogInformation(eventGridEvent.Data.ToString());
}

```

## Create the Event Grid Subscription

Click Add Event Grid subscription.

![image](https://user-images.githubusercontent.com/35857179/78986393-c07fd700-7b5d-11ea-97b1-75efb46f1fad.png)

In the Name box, enter "blobevent" without quotes.

Use the Topic Types combo box to select Storage Accounts.

Click the Subscription combo box and select the only available option.

Click the Resource Group combo box and select the only available option.

Click the Resource combo box and select the only available option.

Click Create.

![image](https://user-images.githubusercontent.com/35857179/78986503-ff159180-7b5d-11ea-9441-5a12cd6e9533.png)



## Create a Blob in the Storage Account

At the top of the window, right-click on All resources and open it in a new tab.

![image](https://user-images.githubusercontent.com/35857179/78986587-29ffe580-7b5e-11ea-8512-f32573a038d0.png)

Navigate to the new tab.

Click on the storage account.

![image](https://user-images.githubusercontent.com/35857179/78986639-4b60d180-7b5e-11ea-87d4-3c799b28f844.png)

In the main pane, click Containers.

![image](https://user-images.githubusercontent.com/35857179/78986674-63385580-7b5e-11ea-8a00-f7cec2f1d066.png)

Click + Container.

Enter a Name of "images" without quotes in the box provided.

![image](https://user-images.githubusercontent.com/35857179/78986714-79deac80-7b5e-11ea-8b96-44cd6ce4294c.png)

Click OK.

Click the images row.

Click Upload.

![image](https://user-images.githubusercontent.com/35857179/78986770-a72b5a80-7b5e-11ea-8dec-f89945f61cd8.png)

Click the folder button to open the file browser.

Select a local file and then click Open. It is recommended to use a small file.

Click Upload.

![image](https://user-images.githubusercontent.com/35857179/78986836-c924dd00-7b5e-11ea-9c28-72b215ce3eee.png)

Examine the Function Logs to verify it ran

Return to the Event Grid trigger tab and verify the logs.

![image](https://user-images.githubusercontent.com/35857179/78986889-ef4a7d00-7b5e-11ea-9578-2242329ace4e.png)