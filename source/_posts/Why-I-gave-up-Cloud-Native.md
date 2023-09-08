---
title: Why I gave up Cloud Native
lang: en
date: 2023-09-08 22:04:21
tags:
  - Cloud Native
categories:
  - Cloud Native
---

> I chose not to follow Cloud Native for several reasons, and I found that Cloud Native is not as powerful as I used to believe. It's not a "silver bullet", and I don't need to stick to it.

# How did I know Cloud Native

I was passionate about Spring Cloud Alibaba-based microservices before April 2020 because it's really easy to use it to develop faultless microservices. I developed a Spring Cloud Alibaba-based project to participate in a software development competition. However, after I transferred the microservices into Docker containers and used Kubernetes (K8S) to manage them, I found Kubernetes and Spring Cloud could not work together: some functionalities (like Nacos and ApiServer, Spring Cloud Gateway and Ingress) overlapped and caused incompatibility between them. There were so many conflicts that the entire project couldn't work properly.

That failure reminded me that I didn't know enough about Spring Cloud and Kubernetes. After searching for a lot of information, I realized that Spring Cloud is a framework for building "traditional" microservices, which are not so suitable for Kubernetes unless using Spring Cloud Kubernetes. I also learned about a new technology called "Service Mesh" and a new theory related to Service Mesh called "Cloud Native" when collecting information related to K8S.

It was a little hard for me to understand service mesh and Cloud Native then, but after I read some articles and books related to them, I finally knew what they were and what their advantages were. Suddenly, I felt that "traditional" microservices were outdated because they depended a lot on SDKs. Many basic functionalities, like service discovery and resource management, are provided by SDKs, which are coupled with service codes. What's worse, the service codes need to be changed every time the SDKs make destructive updates. Service mesh provides a better solution: refactor those basic functionalities into a separate process or container that runs with (in the same Pod) the microservice container. Service mesh amazed me and solved my problems with microservices completely.

# Cloud Native is my favorite theory ever

Service mesh piqued my interest in Cloud Native. I found that it's an attractive theory that everyone holds their own opinion on it. Though it's so abstract that I still can't fully understand it, I kept studying and following Cloud Native from 2020 to 2022. I decided I needed to get a job related to Cloud Native (such as Cloud Native Engineer, Site Reliability Engineer, and Basic Software Developer). So I chose Golang as the programming language I mainly used and studied a lot about Docker, Kubernetes, and Istio. I never missed every conference about Cloud Native and service mesh that I was able to attend then. I don't think it's a successful choice, but in addition to learning how to use Cloud Native tools and their inner workings, I also learned a lot about software design and software architecture.

Looking back to that time now, I can confidently say that "Cloud Native is my favorite theory ever".

# Why I gave up Cloud Native

Finally, I chose not to follow Cloud Native in late 2022 due to three main reasons:

1. Cloud Native is just an immature and abstract theory in software engineering; it's impossible to use it to solve every kind of problem, such as designing a simple and low-cost web service.
2. Startups and small businesses don't have to use Cloud Native and service meshes in practice. They're only suitable for large-scale web services.
3. Cloud Native is a broad theory; I don't have to stick to it. For example, developing and maintaining UNIX-like operating systems and high-performance proxies can also make contributions to Cloud Native and service mesh.

That doesn't mean that Cloud Native is bad and we shouldn't pay any attention to it. To be precise, I have changed my way of making contributions to it by focusing on developing UNIX-like operating systems, proxies, virtual machines, and other basic software related to the cloud.
