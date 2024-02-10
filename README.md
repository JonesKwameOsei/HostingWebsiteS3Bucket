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






> Written with [StackEdit](https://stackedit.io/).
