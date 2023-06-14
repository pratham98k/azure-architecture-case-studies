Design Non-relational Storage Case Study
Requirements
Tailwind Traders wants to reduce storage costs by reducing duplicate content and, whenever applicable, migrating it to the cloud. They would like a solution that centralizes maintenance while still providing world-wide access for customers who browse media files and marketing literature. Additionally, they would like to address the storage of company data files.


![image](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/fe14ec02-87f2-4f55-a74a-608927ebb3ce)

Non-relational storage architecture

Media files. Media files include product photos and feature videos that are displayed on the company’s public website, which is developed and maintained in house. When a customer browses to an item, the corresponding media files are displayed. The media files are in different formats, but JPEG and MP4 are the most common.

Marketing literature. The marketing literature includes customer stories, sales flyers, sizing charts, and eco-friendly manufacturing information. Internal marketing users access the literature via a mapped drive on their Windows workstations. Customers access the literature directly from the company’s public website.

Corporate documents. These are internal documents for departments such as human resources and finance. These documents are accessed and managed via an internally developed web application. Legal requires that various documents be retained for a specific period of time. Occasionally documents will need to be maintained longer when legal or HR issues are being investigated. Most corporate documents older than one year are only kept for compliance reasons and are seldom accessed.

File location. All the files are stored locally in the main office data center. There are numerous file shares organized by department or product line. The data servers are struggling to provide files for the website. During peak hours website pages are slow to render.

File access frequency. Some products are more popular, and that data is accessed more frequently. However, some products, like ski gear, are only accessed during that season. Sales events generate a lot of interest in certain on sale items.

Tasks
Design a storage solution for Tailwind Traders.

What type of data is represented?

What factors will you consider in your design?

Will you use blob access tiers?

Will you use immutable storage?

How will the content be securely accessed?

Your solution should consider the media, marketing literature, and corporate documents. Your recommendations may be different depending on the data. Be prepared to discuss your decisions.

How are you incorporating the Well Architected Framework pillars to produce a high quality, stable, and efficient cloud architecture?


MS answer:


![MicrosoftTeams-image (26)](https://github.com/pratham98k/azure-architecture-case-studies/assets/7745943/0cee590a-6b54-413d-a375-960a728acda4)



• All the content is classified as non-relational.
• The design should consider file location, compliance and regulatory requirements, performance, and storage replication. Also, the solution should be cost effective and easy to centrally manage.
• Blob storage is recommended for the media and corporate files. Blob storage is less expensive, offers the immutable storage requirements for legal, and supports API access for internal applications.
• Azure Files is recommended for the marketing literature. Azure Files is needed for marketing since the files will be accessed via SMB internally.
• Marketing literature access latency for internal users could be reduced by using a local Windows Server and File Sync
• Zone redundant storage is recommended. An argument could be made for Geo-redundant zone storage if the files are mission critical. Read access geo-redundant storage could be used if the front end could make use of a secondary region. This decision would depend on the customer’s locations and traffic.
• The hot tier should be used for all media, marketing literature and corporate documents less than one year old. The archive tier or cold tier should be used for corporate documents older than one year. This decision is based on retrieval latency, storage duration and a desire to reduce costs. Discuss that there is not enough information to decide between Cold and Archive and ask what other questions they may want to ask Tailwind Traders. Lifecycle management should be used to convert corporate documents to a cheaper storage tier after one year.
• Private endpoints and firewall policies should be applied. If private endpoints haven’t been discussed yet, do not go in depth at this point. They are covered in the Networking module.
