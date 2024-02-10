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

3. General Configuration
a. AWS Region: Amazon S3 creates buckets in a Region that we specify. **AWS** recommends that to reduce latency, minimize costs, or address regulatory requirements, should choose any AWS Region that is geographically close to users. The region is usually preselected to the region in which you created the account. Nonetheless, this can be changed to meet business requirements.<p>
b. Bucket type: Select **general purpose** since we need to store and access objects accross multiple Availability Zones. 
c. For **Bucket Name**, enter **website-123**. 
**N/B:** Once an S3 bucket name is established, it becomes globally unique, with all AWS accounts sharing the namespace. Hence, if the bucket name we entered exist, we will be prompted to enter a unique bucket name. Following the creation of a bucket, the designated name is reserved exclusively for the account that created it across all AWS Regions. Only upon deletion of the bucket can the name become available for use by other AWS accounts.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/f4261c0d-2c8a-434b-b377-0f4b56766b5c)<p>
**Optionally**, we can copy existing bucket settings and apply it to our new bucket we are creating.  

4. For Object Ownership, choose **ACLs enabled**.
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
- Value: Marketing
We can use tags to manage and our bucket(s), and also optimise cost.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/d0a65f11-3f3e-4cc7-827f-a76fec31e67b)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/9110b046-a684-46a1-aa01-7af145f2b3cc)<p>
10. Click on **Create bucket**. 
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/bf6fbfe0-d01b-4ce2-8746-58f6df3cddc2)<p>
**Our bucket has been created successfully:<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/9a4f009b-8f19-4bbd-95a6-d8cdd0b6497c)<p>
11. In the **Bucket** section, click the name of the bucket toopen it.
12. Next, select the **Properties** tab.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/875aeb28-22cf-4f9a-8d48-bff0be7ae9fa)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/4957e721-8c73-4826-ab7c-37048ff76945)<p>
## Configuring the Static Website on Amazon S3
We will confidure the bucket to host the static website.
1. Having chosen the **Property** tab above, scroll to the *Static website **hosting** panel and select **Edit**.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/8eabcccf-8c3d-4543-9aa8-adcabc12bc09)
2. Next, **Enable** static website hosting.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/98b1898d-dd38-4c17-92f8-854e6f4cc534)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/a100e458-03ca-4760-a5cf-019b5e46ad47)<p>
3. Next, we will specify the home or default page of the website.
4. Save your changes.
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/acbd4887-df0c-404f-ae6c-44265c3a2fb3)
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/ac521204-e343-49a8-8004-fa65aaa87240)































