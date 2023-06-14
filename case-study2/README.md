Design a compute solution
Requirements
Tailwind Traders would like to migrate their product catalog application to the cloud. This application has a traditional 3-tier configuration using SQL Server as the data store. The IT team hopes you can help modernize the application. They have provided this diagram and several areas that could be improved.

compute architecture
![image](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/8794a4dc-75ac-4d25-9267-e72b90776bf0)


The frontend application is a .NET core-based web app. During peak periods 1750 customers visit the website each hour.

The application runs on IIS web servers in a front-end tier. This tier handles all customer requests for purchasing products. During the latest holiday sale, the front-end servers reached their performance limits and page loads were lengthy. The IT team has considered adding more servers, but during off hours the servers are often idle.

The middle tier hosts the business logic that processes customer requests. These requests are often for help desk support. Support requests are queued and lately the wait times have been very long. Customers are offered email rather than wait for a representative. But many customers seem frustrated and are disconnecting rather than wait. Customer requests are 75-125 per hour.

The back-end tier uses SQL Server database to store customer orders. Currently, the back-end database servers are performing well.

While high availability is a concern, due to legal requirements the company must keep all the resources in a single region.

Tasks
Front-end tier. Which Azure compute service would you recommend for the front-end tier? Explain why you decided on your solution.

Middle tier. Which Azure compute service would you recommend for the middle tier? Explain why you decided on your solution.

How are you incorporating the Well Architected Framework pillars to produce a high quality, stable, and efficient cloud architecture?


My Answer:

![MicrosoftTeams-image (23)](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/5ccdfabf-fbb6-4b83-8cba-fd1e60c82c5d)


MS answer:


![MicrosoftTeams-image (24)](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/b4562a6e-4772-4fec-8a8c-3183476646f3)


![MicrosoftTeams-image (25)](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/2b638802-7637-4ded-bf62-0b93e2b4920e)


Here are some more thoughts
 
Front-end tier
Which Azure compute service would you recommend for the front-end tier? Discuss both the workload hosting and the web application. Explain why you decided on your solution.
You could use an Azure VM scale set (VMSS) to satisfy the autoscaling requirement. When customer requests increase or decrease, VMSS will automatically scale. It is also recommended to create availability sets or zones.The best choice would be an Azure App Service web app. This web app supports autoscaling and can host a .NET Core-based web app. It would be recommended to use availability zones.To ensure you are solving the problem, Application Monitoring and Application Insights are recommended. These products supply detailed IIS web server/client performance metrics. This will help detect SLA issues and notify those users who have exceeded a threshold while holding for support representative.Would you need both VMSS and App Services scaling?
 
Middle
Which Azure compute service would you recommend for the middle tier application? Justify your recommendation with proper illustration.
Azure functions provide the ability to manage message queues, like the customer help desk requests. Functions allow you to write less code, maintain less infrastructure, and save on costs. Instead of worrying about deploying and supporting servers, the cloud infrastructure provides all the up-to-date resources needed • As requests increase, Azure functions meet the demand with as many resources and function instances as necessary - but only while needed. As requests fall, any extra resources and application instances drop off automatically.Azure functions can be triggered by an event. For example, the customer selecting they would like to send email. Also, monitoring and logging are available with Azure functions.API Management should also be considered. APIM would allow for policies such as throttling, caching and authentication. If the middle tier were to expand or move to a microservice model later, APIM would allow for a single frontend access point with flexibility to connect or redirect to many backend API locations. In addition, APIM allows for more logging and visualizations of traffic.

