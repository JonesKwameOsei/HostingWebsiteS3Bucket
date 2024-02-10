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
b. For **Bucket Name**, enter **website-123**. 
**N/B:** Once an S3 bucket name is established, it becomes globally unique, with all AWS accounts sharing the namespace. Hence, if the bucket name we entered exist, we will be prompted to enter a unique bucket name. Following the creation of a bucket, the designated name is reserved exclusively for the account that created it across all AWS Regions. Only upon deletion of the bucket can the name become available for use by other AWS accounts.<p>
![image](https://github.com/JonesKwameOsei/HostingWebsiteS3Bucket/assets/81886509/f4261c0d-2c8a-434b-b377-0f4b56766b5c)<p>
**Optional**, we can copy an existing bucket settings and apply it to our new bucket we are creating.  


























