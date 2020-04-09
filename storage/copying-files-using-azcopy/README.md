# Copying Files from On-Premises to Azure Storage Accounts and vice versa using AzCopy

![image](https://res.cloudinary.com/practicaldev/image/fetch/s--A7pGlOl9--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://res.cloudinary.com/practicaldev/image/fetch/s--IZtHKWc0--/c_imagga_scale%2Cf_auto%2Cfl_progressive%2Ch_420%2Cq_auto%2Cw_1000/https://thepracticaldev.s3.amazonaws.com/i/pdg1ks10al0hcbvo9rh9.png)

- From an on-premise to the Azure Storage Account
- From Azure Storage Account to another Azure Storage Account
- From the Azure Storage Account to an on-premise

# What is AzCopy
AzCopy is a command-line utility that you can use to copy blobs or files to or from a storage account.

# Disable Security Configuration
If you are using Virtual Machine, you need to change the security configuration in order to download AzCopy. 

Login to your Virtual Machine and Open Server Manager

![image](https://user-images.githubusercontent.com/35857179/71639874-63e96200-2cba-11ea-8c63-0e78bce6c424.png)

On the left navigation, click Local Server

![image](https://user-images.githubusercontent.com/35857179/71639876-6ba90680-2cba-11ea-81ac-e026f1f33995.png)

Click On next to IE Enhanced Security Configuration

![image](https://user-images.githubusercontent.com/35857179/71639879-87141180-2cba-11ea-91a6-9f4f48d9461d.png)

For Administrators, select Off and click OK

![image](https://user-images.githubusercontent.com/35857179/71639858-06edac00-2cba-11ea-80c2-b6d9a5468dea.png)

# Download AzCopy
Now we can download AzCopy. 

Open the browser and browse https://aka.ms/downloadazcopy

Click Run

![image](https://user-images.githubusercontent.com/35857179/71639887-cb071680-2cba-11ea-8625-4016d35dd32b.png)

Click Next

![image](https://user-images.githubusercontent.com/35857179/71639892-e5d98b00-2cba-11ea-84e4-9628ae47bd43.png)

Tick I accept the terms in the License Agreement and click Next

![image](https://user-images.githubusercontent.com/35857179/71639899-043f8680-2cbb-11ea-9bef-5bb2a8d7541e.png)

Select a destination folder and click Next

![image](https://user-images.githubusercontent.com/35857179/71639900-0d305800-2cbb-11ea-9c5d-28a9f9c83c5e.png)

Click Install

![image](https://user-images.githubusercontent.com/35857179/71639901-15889300-2cbb-11ea-94ee-c5e2d420e916.png)

# Create Storage Account

> A storage account provides a unique namespace in Azure for your data. Every object that you store in Azure Storage has an address that includes your unique account name. The combination of the account name and the Azure Storage blob endpoint forms the base address for the objects in your storage account.

Go to Azure Portal and select Storage Accounts

Click Add

![image](https://user-images.githubusercontent.com/35857179/71639925-a495ab00-2cbb-11ea-928d-dc1644f88c4c.png)

Select a Resource group if it is not populated. Enter the storage account name you want to use and leave other options as default. Click Review and Create.

![image](https://user-images.githubusercontent.com/35857179/71640037-c55f0000-2cbd-11ea-86b0-d06d4ac6a491.png)

Click Create

![image](https://user-images.githubusercontent.com/35857179/71640051-e4f62880-2cbd-11ea-9f4a-7980c7609ebc.png)

Wait for the deployment. It may takes around 30 seconds or longer.

Once it's complete, click Go to Resource

# Create Blob Service Container 

We will use Azure Blob storage for storing our data for this demonstration.

> Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimised for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

Under Blob service, click Containers. 

> A container organises a set of blobs, similar to a directory in a file system. A storage account can include an unlimited number of containers, and a container can store an unlimited number of blobs.

![image](https://user-images.githubusercontent.com/35857179/71640004-44a00400-2cbd-11ea-9b10-f073b624a984.png)

Create a new Container. Enter the name and click ok

![image](https://user-images.githubusercontent.com/35857179/71640011-57b2d400-2cbd-11ea-9b82-558b581cce6e.png)

Now let's do the above steps again to create our second Storage Account.

![image](https://user-images.githubusercontent.com/35857179/71640073-4d450a00-2cbe-11ea-839d-13d0a2faed20.png)

Now we got two Storage Accounts.

# Copy data from an on-premise to Storage Account 1

Go to Storage Account 1, Navigate back to Blob service - Containers. Click the three dot button and click Container properties

![image](https://user-images.githubusercontent.com/35857179/71640798-fe05d600-2ccb-11ea-8459-2c51d4b35043.png)

Copy the URL and paste it to a text editor first. We'll use it later.

Since the container is private, we need to access it with the container access key. 

Under Settings, you can see ``Access keys``. Copy ``Key`` from key1.

![image](https://user-images.githubusercontent.com/35857179/71640825-9d2acd80-2ccc-11ea-957e-109b9ea0885e.png)

You may wonder why there are two access keys. It is designed for avoiding downtime and for temporary sharing of access keys. For more, please check out [Why does an Azure storage account have two access keys?](https://blogs.msdn.microsoft.com/mast/2013/11/06/why-does-an-azure-storage-account-have-two-access-keys/)

Go back to Virtual Machine, launch Command Prompt and type the below command and click Enter. Remember to replace <YOUR_URL> and <YOUR_ACCESS_KEY> with the values you just copied.

For this demonstration, we're going to upload files under ``C:\Windows\System32\drivers``

```
azcopy 
/Source:C:\Windows\System32\drivers 
/Dest:<YOUR_URL> 
/DestKey:<YOUR_ACCESS_KEY>
```

You should see similar output

![image](https://user-images.githubusercontent.com/35857179/71640847-0d395380-2ccd-11ea-9619-fdfc1c4aa805.png)

Back to the console, click Storage Explorer(preview). Under BLOB CONTAINERS, click ``data``. You should see the files that you just uploaded using AzCopy.

![image](https://user-images.githubusercontent.com/35857179/71640867-4bcf0e00-2ccd-11ea-9624-bd1a296c4a8b.png)

# Copy data from Storage Account 1 to Storage Account 2
What if you want to copy files from one blob container in a Storage Account to that in another Storage Account?

Similarly, copy the source URL in the second Storage Account.

Go back to Command Prompt, 

```
azcopy 
/source:<YOUR_SOURCE_URL> 
/Dest:<YOUR_DEST_URL> 
/sourcekey:<YOUR_ACCESS_KEY_IN_STORAGE_ACCOUNT_1> 
/DestKey <YOUR_ACCESS_KEY_IN_STORAGE_ACCOUNT_2> 
/s
```

![image](https://user-images.githubusercontent.com/35857179/71640931-7cfc0e00-2cce-11ea-9888-f29287ec348d.png)

Go back to the console, check Storage Explorer in Storage Account 2. 

![image](https://user-images.githubusercontent.com/35857179/71640940-d6643d00-2cce-11ea-8c4e-75be5d2fa371.png)

We've successfully copied the files from Storage Account 1 to Storage Account 2. 

# Copy data from Storage Account to an on-premise
What if we want to copy the files from Storage Account to our local system? You may already know the answer.

```
azcopy 
/source:<YOUR_SOURCE_URL> 
/Dest <YOUR_DESTINATION_PATH_IN_LOCAL_SYSTEM> 
/SourceKey:<YOUR_ACCESS_KEY> 
/s
```