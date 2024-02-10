 # Creating a Static Website with Amazon Simple Storage Service (Amazon S3)

## Overview 
In this project, we will utilise some Amazon Simple Storage Service (Amazon S3) features to build a static website. 
Static websites consist of HTML pages, images, style sheets, and other essential files required for rendering a website. Unlike dynamic websites, static websites do not rely on server-side scripting or database interactions. However, they may incorporate client-side scripts that execute within the user's web browser.

Hosting a static website on Amazon S3 entails uploading the website's content and configuring permissions to allow users to access it. This approach eliminates the need for dedicated servers, as Amazon S3 provides a reliable storage solution capable of storing and retrieving vast amounts of data from anywhere on the web, at any time. Leveraging Amazon S3 for static website hosting offers scalability, durability, and cost-effectiveness, making it an ideal choice for various web projects.
## Setting Goal
This project seeks to achieve the following:

- Create an Amazon S3 bucket, configure the bucket to host the static website and upload contents to the bucket.
- Perform security operations to securely share an object from the bucket using **presigned URL**.
- Add another layer of security to secure the bucket using policy.

Our website will look like this at the end of this project:<p>

![S3Static Website](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3334a1b4-87ee-4893-84cf-3afbc7efdbfb)

## Creating a bucket in Amazon S3
Store virtually any amount of data with industry-leading reliability, security, and affordability thanks to s3's object storage solution. Its scalable design ensures flexible data access and management, making it ideal for website and mobile app content and diverse use cases like:
- Data lakes and analytics
- Cloud-native applications
- Backups and archiving

1. In the **AWS Management Console, on the Service menu, select or search for **S3**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/1f62dcb5-4625-4673-8bb2-d01f01bf17e6)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/f267bd74-eb3c-4090-b539-38a50d7b9654)

2. Select **Create bucket**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/48681f07-93b7-4e6d-930e-0904b6a2f11b)

3. General Configuration<p>
a. AWS Region: Amazon S3 creates buckets in a Region that we specify although being a global service. **AWS** recommends that to reduce latency, minimize costs, or address regulatory requirements, should choose any AWS Region that is geographically close to users. The region is usually preselected to the region in which you created the account. Nonetheless, this can be changed to meet business requirements.<p>
b. Bucket type: Select **general purpose** since we need to store and access objects accross multiple Availability Zones. <p>
c. For **Bucket Name**, enter **website-123**. <p>
**N/B:** Once an S3 bucket name is established, it becomes globally unique, with all AWS accounts sharing the namespace. Hence, if the bucket name we entered exist, we will be prompted to enter a unique bucket name. Following the creation of a bucket, the designated name is reserved exclusively for the account that created it across all AWS Regions. Only upon deletion of the bucket can the name become available for use by other AWS accounts.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/f4261c0d-2c8a-434b-b377-0f4b56766b5c)<p>
**Optionally**, we can copy existing bucket settings and apply it to our new bucket we are creating.  <p>

4. For Object Ownership, choose **ACLs enabled**.<p>
5. Next, select **Bucket ownwer preferred**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/a99b5ffd-13c4-472e-abd4-60a35e7b3482)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/aa050075-035b-4090-a813-4ba882b3ce3d)<p>
7. **Block Public Access** settings for this bucket: This means the bucket and its objects will be private denying pucblic access. or our project, we will make it public. We will later secure it.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3309cf96-2fbc-48ee-85bf-df25d709cb75)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/e926743d-d69a-47c8-970b-8a3ab9b32a57)<p>
8. For **Bucket Versioning**, we will select **Enable**.
**Note:** After enabling this feature, we cannot turn it off once the bucket is created.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/5ab5c0aa-078d-45dd-9e11-3db226297eda)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/b87d32cc-542e-4180-8ff1-1366afcc5a99)<p>
9. We will utilise Tags in provisioing a our bucket, choose **Add tag**, and enter the following:
- Key: Department
- Value: Marketing<p>
We can use tags to manage and our bucket(s), and also optimise cost.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/d0a65f11-3f3e-4cc7-827f-a76fec31e67b)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/9110b046-a684-46a1-aa01-7af145f2b3cc)<p>
10. Click on **Create bucket**. 
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/bf6fbfe0-d01b-4ce2-8746-58f6df3cddc2)<p>
**Our bucket has been created successfully**:<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/9a4f009b-8f19-4bbd-95a6-d8cdd0b6497c)<p>
11. In the **Bucket** section, click the name of the bucket toopen it.
12. Next, select the **Properties** tab.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/875aeb28-22cf-4f9a-8d48-bff0be7ae9fa)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/4957e721-8c73-4826-ab7c-37048ff76945)<p>
## Configuring the Static Website on Amazon S3
We will confidure the bucket to host the static website.
1. Having chosen the **Property** tab above, scroll to the *Static website **hosting** panel and select **Edit**.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/8eabcccf-8c3d-4543-9aa8-adcabc12bc09)
2. Next, **Enable** static website hosting. Then, choose **Host a static website**.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/98b1898d-dd38-4c17-92f8-854e6f4cc534)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/a100e458-03ca-4760-a5cf-019b5e46ad47)<p>
3. Next, we will specify the home or default page of the website..
- **Index document**: Enter index.html
- **Error document**: Enter error.html
4. Save your changes.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/acbd4887-df0c-404f-ae6c-44265c3a2fb3)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/ac521204-e343-49a8-8004-fa65aaa87240)<p>
5. In the Static website hosting panel under Bucket website endpoint, choose the link.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3622e0ae-9cce-4fb8-bab6-8b91c3aeb8f6)<p>
**Note:** This will return a **403 Forbidden** error message. This is because the bucket's permissions have not been configured.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/34ef3dae-9f0e-408e-9592-b632af08a250)<p>

## Uploading content to the bucket
Here, we will upload the static files to our bucket. 
1. Let's go back to the Amazon S3 console, and choose the **Objects** tab.
2. Choose **Upload**.
3. Choose **Add files**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3596bfa5-b216-4471-bd6f-dee180acb9e5)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/ed9e49f0-92f6-4fbb-8b2d-5d9f0a2ac2f6)<p>
5. Select files to be uploaded.<p> 
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3f559ea8-5b07-4791-b98a-6f8bef5f0faf)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/2f7ba7d3-9c43-4ad6-a2b1-b7415d973d89)<p>
Choose **Upload**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/8d4e854f-1ab8-4196-8707-c640dac177ff)<p>

The files are uploaded to the bucket.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/2595115c-8054-4389-923d-946789c00780)<p>

6. Select **Close**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/e29996e3-296d-4f44-9a19-12a3d9725694)<p>

## Grant public access to the objects
In this task, we will make the uploaded objects publicly accessible so users can view the website.
First, confirm that the objects are currently private. 
- Return to the browser tab that showed the 403 Forbidden message.
- Refresh the webpage.
The expected results should be the **403 Forbidden** message we had earlier. This message demonstrates that your static website is being hosted by Amazon S3 but that the content is private. Hence, we need to make the content public. 

1. To make Amazon S3 objects public, you have two options:
   - To make an entire bucket or a specific directory within a bucket public, utilize a bucket policy.
   - To make individual objects in a bucket public, use an access control list (ACL).<p>
**Best Practice:** It is **generally safer to make individual objects public to avoid unintentionally making other objects public**. However, if it is certain that the entire bucket does not contain sensitive information, we can can opt for a bucket policy.

3. Now we will proceed to configure the individual objects for public access:
   i. Keep the website tab open and go back to the web browser tab with the Amazon S3 console.
   ii. Select all three objects.
   iii. From the Actions menu, choose "Make public using ACL."<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/669f791b-5fd0-4b20-a678-7fc74b6a01a7)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/4804dc0a-fd0f-43a0-909b-689a3efb016b)<p>
Our static website is now publicly accessible.
5. Choose Close

7. Return to the web browser tab that has the 403 Forbidden message.
8. Refresh the webpage.<p>
Now we can see the static website that is being hosted by Amazon S3.

## Securely sharing an object using a presigned URL
To securely share an object temporarily, generate a presigned URL indicating how long it will remain valid before sharing it with specific users. While the presigned URL is active, anyone possessing it can access the object. It's important to limit the URL's validity and only share it with trusted individuals.

1. We will add a new file
2. Navigate back to the Amazon S3 console and access the **Objects tab**.
3. Click on **Upload**.
4. Select **Add files**.
5. Choose the file to be added.
6. Proceed with the **upload process**.
7. Once uploaded, **close the upload window**.<p>

To maintain privacy, the file added, **new-report.png** file is initially private. Instead of making it public, a presigned URL has been created for access.

8. In the Objects tab, select **new-report.png**.
9. From the Actions menu, opt for **Share with a presigned URL**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/c32785fb-dcfe-477c-aa95-aeda69b79418)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/75778169-0378-4c81-9715-0ef0744fc7c6)<p>
11. Configure the expiration time for the **presigned URL**:
   - Choose Minutes.
   - Set the Number of minutes to **2**.
11. **Generate** the presigned URL.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/7175e1f2-2bb3-48f2-b673-90b90381362a)<p>
12. Upon creation, **copy the presigned URL from the banner at the top of the page**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/2365d96e-fb17-4841-a25c-6e122cb2f65e)<p>
13. **Open a new browser tab** and **paste the copied URL into the address bar to view the report** in the web browser<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/44b6c3b7-cc02-4929-87e8-3b6ba3ec5b69)

## Using a bucket policy to secure the bucket
You want to protect your website files and make sure that no one can delete them. To do this, you apply a
bucket policy that denies delete privileges on your website files.
1. We will return to the Amazon S3 console, and choose the **Permissions tab**.
2. Under **Bucket policy**, choose **Edit**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/4146d7c9-77d3-434b-9a83-0e4b594d9fd6)<p>
3. Enter the **Bucket policy**
```
{
"Version": "2012-10-17",
"Id": "MyBucketPolicy",
"Statement": [
{
   "Sid": "BucketPutDelete",
   "Effect": "Deny",
   "Principal": "*",
   "Action": "s3:DeleteObject",
   "Resource": [
      "arn:aws:s3:::web-548/index.html",
      "arn:aws:s3:::web-548/script.js",
      "arn:aws:s3:::web-548/style.css"
      ]
   }
 ]
}
```
This policy denys everyone from deleting the three files that make the website function.<p>
4. Save Changes<p><p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/90ef57c5-d28a-4ccb-869c-70b5fa1cfdcc)<p>
5. Return to the **Object tab**.<p>
6. Select index.html.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/854276fa-6509-41aa-b4d5-59a859a94783)<p>
7. Choose **Delete**.<p>
8. In the Delete objects panel, enter delete to confirm that we want to remove this file.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/0d067e0d-c5a4-4d4e-a8ce-ce7048ec9275)<p>
9. Choose Delete objects.<p>
10. Notice that the index.html file is listed in the **Failed to delete pane**.<p>
This confirms that our **policy is working and preventing the website's files from being deleted**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/89d41308-2c0f-42ff-bc91-28343db8165e)<p>
11. Choose Close to return to the Objects tab.<p>
## Updating the website
Although we have configured a policy to prevent deletion of website files, we can still update the website by editing the HTML file and uploading it to the S3 bucket. Amazon S3 is an object storage service, so we must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object; instead, you must replace the whole object.<p>
12. We will edit the HTML file, **index.html**.<p>
13. Save the file.<p>
14. Return to the Amazon S3 console, and upload the **index.html** file that you just edited.<p>
15. Choose index.html, and in the **Actions** menu, choose the **Make public using ACL** option.<p>
16. Choose **Make public**.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/18617d2a-46fa-4f9a-b4b0-feb350880b33)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/0cd67c1d-cab8-477f-b0cb-0fd3f78fb5d4)<p>

17. Return to the web browser tab with the static website, and refresh the page.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/7bcf4e48-8b78-4316-8de5-358b9d245dc6)<p>

Our static website is now accessible on the internet. Because it is hosted on Amazon S3, the website has high
availability and can serve high volumes of traffic without using any servers.
## Exploring file versions
**Bucket versioning** is **disabled** as the **default setting**. With versioning turned off, modifications made to objects are **irreversible**. For instance, when we upload a new version of a file, the old one is replaced, leading to the loss of the original file. Deleting a file results in permanent removal with no option for retrieval.<p>

On the other hand, **enabling versioning ensures that altered and deleted file versions are retained**. While previous versions of objects are not displayed automatically, we can access them through the console or programmatically. By preserving earlier versions of objects, we have the ability to recover them when necessary.<p>
1. When created the bucket, we **turned on versioning**. In this task, we will view the object versions
available in the bucket.
2. Go to the Amazon S3 console, and choose the **Objects tab**.
3. Choose **Show versions** to turn on bucket versioning.
4. Review the list of objects in the bucket.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/3c6d1c88-b1fb-44bb-84b2-a866b35f77b6)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/7f471660-4a84-45a9-b172-f63daba4fa23)<p>

- Notice that each file has a **Version ID**. These IDs are **automatically generated** by Amazon S3 when
versioning is turned on.
- We should also find two versions of the index.html file because you uploaded a new version of the
file. The current version is the file that you uploaded when you updated your website.
## Summary
In this practical lab, we established a **custom static website** that is **publicly accessible**. We gained insights into **utilising a presigned URL** to share objects temporarily within your bucket. Additionally, we safeguarded the contents in the bucket by **implementing a bucket policy** to inhibit file deletion and **enabled bucket versioning** for potential retrieval of earlier file versions. This hands-on project has exposed us to the **best practices** in sharing objects from S3 bucket. 








