---
title: AWS Cloud Practitioner Chronicles - The Infrastructure
date: 2023-04-28 22:55:00 +0800
categories: [aws, cloud computing]
tags: [aws, cloud computing, aws cloud practitioner]
---

![AWS](https://allcode.com/wp-content/uploads/2021/02/Group-169-3.png "AWS")

To help me stay on track and document my progress during my preparation for AWS Cloud Practitioner certification, I've decided to start a blog post series where I will share my experiences. By doing so, I hope to inspire and motivate others who are also interested in cloud computing and create a record of my own growth and development in this field. I'll be using materials like AWS Skill Builder, Digital Cloud and so on during the preparation.


## The AWS Global Infrastructure

As of April 2023, AWS has 31 launched regions and 99 availability zones in total. A region normally consists of 3 or more availability zones. Each region is completely independent but the availability zones in a region are connected through low-latency links. We can also replicate data within a region and between regions using private or public internet connections.

On the other hand, an availability zone is basically a data center facility that is located within a region and each with redundant power, networking, and connectivity, housed in separate facilities. AZs span one or more data centers and have direct, low-latency, high throughput, and redundant network connections between each other.
An availability zone is represented by a region code followed by a letter identifier; for example, us-east-1a

![Zones](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2022/03/23/infografi%CC%81a-aws-local-zones-english-map-1080.png "Zones")

### Local Zones

Local zones are extension of an AWS region where they are closer to the end-users. They can place compute, storage and other selected AWS services with high bandwith, secure connection and so on and so forth.

With local zones, we can easily run highly demanding applications that require single-digit millisecond latencies to our end-users.

### Wavelength Zones

These kind of zones are similar to local zones except they're for 5G connectivity. They are essentially extensions of existing AWS Regions that are deployed in close proximity to 5G network operators’ data centers.

By placing compute and storage resources in Wavelength Zones, developers can deliver their applications with single-digit millisecond latencies to end-users. This enables new applications that were not previously possible due to latency issues, such as gaming, augmented and virtual reality, industrial automation, and autonomous vehicles, to name a few.


### Outposts

AWS outposts is basically a hardware from AWS where we can deploy in our own data center which brings some native AWS services, infrastructure and operating models to virtually any data center. They can also connected to a region for other AWS services as well. 


### Cloudfront

AWS cloudfront is a CDN and its mission is naturally to deliver the static and dynamic content, including websites, APIs, video streams, and other web applications to users. It works by caching content(regional edge cache) at edge locations around the world, which are AWS-managed data centers that are located closer to end-users. 


![Cloudfront](https://digitalcloud.training/wp-content/uploads/2022/02/aws-cloudfront-edge-cache.png "Cloudfront")

To give an example, if we're in Turkey, then when we try to access a video that's being shared through cloudfront, we're going to get that video from an edge location that is close to us. This results in better performance.

## The AWS Shared Responsibility Model
![Shared Responsibility](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg "Shared Responsibility")

The shared responsibility model is a concept in cloud computing that outlines the responsibilities of both the cloud provider and the customer for securing and managing the cloud environment. This image is from AWS' website and it clearly specifies the responsibilites.

The AWS is responsible for the security and maintenance of the underlying cloud infrastructure, while the customer is responsible for securing and managing their own applications, data, and access to the cloud resources they use.










