---
title: Harvesting DataCite DOI Metadata
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The DataCite Metadata Store is the collaborative effort of hundreds of organisations across the world. Metadata is created by DataCite Members using [DataCite's Metadata Schema](https://schema.datacite.org/). This guide is intended to provide information for anyone wishing to harvest DataCite metadata from the DataCite Metadata Store.

### What do we mean by “harvesting”?

Harvesting metadata refers to the automated process of collecting and aggregating metadata records from the DataCite Metadata Store. This can be done using protocols such as OAI-PMH (Open Archives Initiative Protocol for Metadata Harvesting) or APIs. 

This process allows external services, research institutions, and data discovery platforms to access structured information about research outputs, including datasets, software, and many more. By harvesting metadata, organizations integrate DataCite metadata into global research infrastructures.

### Who can harvest DataCite metadata?

All DataCite metadata is openly available with a CC0 license, meaning it is available to everyone. The DataCite Metadata Store includes all DOIs and deposited metadata in our database and to the extent possible under law, DataCite e.V. has waived all copyright and related or neighboring rights. However, harvesters should be familiar with [DataCite's DataCite Data File Use Policy](doc:datacite-data-file-use-policy).

### How can I harvest DataCite Metadata?

Below are the main DataCite services for harvesting DataCite DOI metadata:

[REST API](doc:api-queries): The DataCite REST API is DataCite's primary API and enables retrieval, creation, and update of DataCite DOI metadata records and account information. The REST API requests can include various filters and parameters to allow for limiting the results based on specific criteria.

[OAI-PMH](doc:datacite-oai-pmh): This DataCite service exposes metadata stored in the DataCite Metadata  
Store (MDS) using the Open Archives Initiative Protocol for Metadata Harvesting (OAI-PMH).

[Public Data File](doc:datacite-public-data-file): The Public Data File contains metadata for all publicly available DataCite DOIs. An updated version of the public data file is released annually. Each annual public data file contains all DOIs that were registered up to the end of the year.

[Monthly Data File](doc:datacite-monthly-data-file) : The DataCite Monthly Data File contains metadata for all publicly available DataCite DOIs registered up to the end of the last month. The data file is distributed via AWS S3 and is currently available to all DataCite Members and Consortium Organizations.

Each service supports metadata harvesting workflows and use cases in different ways. The chart below outlines the primary differences:

| Service               | Availability                                                                                                     | Update Frequency | Filters                                                | Access pattern | Formats    |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------- | :--------------- | :----------------------------------------------------- | :------------- | :--------- |
| **REST API**          | All users, including unidentified users. Higher rate limits are available to identified and authenticated users. | Real-time        | Yes                                                    | Request-based  | JSON       |
| **OAI-PMH**           | All users, including unidentified users.                                                                         | Real-time        | Yes                                                    | Request-based  | XML        |
| **Public Data File**  | Identified users (must provide email address to access).                                                         | Annual           | No                                                     | Bulk download  | JSON Lines |
| **Monthly Data File** | Authenticated users.                                                                                             | Monthly          | Records can be downloaded selectively by month updated | Bulk download  | JSON Lines |

### Related resources

- [How can I detect removed or retracted records with the REST API?](doc:how-do-i-detect-removed-records-or-retractions-with-the-rest-api) 
- [How can I harvest metadata in XML format?](doc:how-can-i-harvest-xml-metadata-with-datacite-apis)
- [How can I make my DOI list query more efficient when using the REST API?](doc:how-can-i-make-my-doi-list-query-more-efficient-when-using-the-rest-api)
- [What can I do if I receive "read timeout reached" errors while paging through DataCite DOI metadata using the REST API?](doc:what-can-i-do-if-i-receive-read-timeout-reached-errors-while-paging-through-datacite-doi-metadata-using-the-rest-api)

Keep up to date with the latest information about harvesting metadata by joining the [Harvesters Interest Group](https://groups.google.com/a/datacite.org/g/harvesters-interest-group/about?pli=1).

Please get in touch if you have any questions at [support@datacite.org](mailto:support@datacite.org).