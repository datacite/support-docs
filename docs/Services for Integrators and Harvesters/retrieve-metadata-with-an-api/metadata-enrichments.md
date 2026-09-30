---
title: Metadata enrichments
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
DataCite is developing community-driven DOI metadata enrichment processes as part of an ongoing, multi-faceted effort to improve the quality and utility of the DataCite metadata store and enhance discovery, reuse, and reporting across the research ecosystem.

Below, we use the terms "enriched DOI record" to refer to a DataCite DOI metadata record that has been enriched using one or more metadata enrichments and "enrichment record" to refer to a record that describes a change to DataCite DOI metadata.

Enrichment services are currently in development and are subject to change. Feedback on enrichment services is welcome via open [Requests for Comment](https://github.com/datacite/datacite-suggestions/discussions/categories/requests-for-comment?discussions_q=is%3Aopen+category%3A%22Requests+for+Comment%22+enrichments) and at [support@datacite.org](mailto:support@datacite.org).

## Where are metadata enrichments sourced from?

DataCite works with [COMET](https://cometadata.org) (Collaborative Metadata) on [enrichment projects](https://www.cometadata.org/enrichment-projects). These projects produce metadata enrichments for DataCite DOIs, which complement the metadata submissions of original depositors. 

Enrichments are then ingested into DataCite systems as a series of individual enrichment records. An [enrichment record](doc:metadata-enrichments#enrichment-records) describes a change to DOI metadata and contains additional provenance information about how that change was produced. Enrichment records can be requested using the [enrichments endpoint](doc:metadata-enrichments#retrieve-enrichment-records) of the DataCite REST API.

Before being ingested by DataCite, each enrichment record is also checked against several indicators of validity. These include:

- Whether the enrichment record is structured as expected  
- Whether the enrichment record contains key provenance metadata  
- If the enrichment record is still relevant to the original DOI record in DataCite; i.e., if the original metadata targeted by the enrichment has changed since the enrichment record was created  
- If the enrichment record, when applied to the original DOI record, produces a DataCite DOI record valid under the DataCite Metadata Schema

## Enriched DOI records

When retrieving an enriched DOI record, the enrichment records associated with a given DOI are applied to the original DOI record, generating a separate, enriched DOI record. The original DOI record is not modified by this process in any way. 

Enrichment records are not applied if targeted metadata fields are changed by the original depositor. The original DOI record is displayed in place of the enriched record if the enriched record is in any way invalid according to the DataCite Metadata Schema.

### How are enriched DOI records generated?

The image below visualizes the process that produces an enriched DOI record. The **original DOI record**, which is stored separately and is not modified by the following process, exists at the left. It contains a title that reads “Dataset”. The **enrichment record** in the center targets the “Dataset” title and updates it to a more descriptive and discoverable title. When the enrichment record is applied to the original DOI record, the outcome is an **enriched DOI metadata record**—stored and displayed separately from the original DOI record—with the enriched title.

![](https://files.readme.io/efa77838dc3af792908a87a29b4c0107a4d557972506aa5e0a2432dd0548e2b1-Screen_Shot_2026-06-01_at_2.02.39_PM.png)

### Retrieve a list of DOI records with enrichments applied

When [retrieving a list of DOIs](https://support.datacite.org/docs/api-get-lists) with the REST API, set the parameter `enriched=true` to retrieve a list of DOI records with enrichments applied. DOI records with enrichments will appear with enriched values. DOI records without applicable enrichments will appear the same way they do when the `enriched=true` parameter is not set. 

For example, the following request can be used to retrieve a list of all DOI metadata records with enrichments applied using [cursor pagination](https://support.datacite.org/docs/pagination#method-2-cursor): 

```shell
curl “https://api.datacite.org/dois?enriched=true&affiliation=true&publisher=true&page[cursor]=1”
```

#### Queries and filtering
 
All [REST API query and filter parameters](https://support.datacite.org/docs/api-queries) for list requests are supported when `enriched=true`. Querying and filtering with these parameters will query and filter by enriched metadata values if available and original values if not. 

For example, the following request retrieves journal articles using the `resource-type-id=JournalArticle` parameter. Because `enriched=true`, the request filters by enriched resourceTypeGeneral values in the DOI metadata if available and original resourceTypeGeneral values if not: 

```shell
curl “https://api.datacite.org/dois?resource-type-id=JournalArticle&enriched=true&affiliation=true&publisher=true”
```

The following request retrieves DOIs by British Library-affiliated researchers using the `affiliation-id=https://ror.org/05dhe8b71` parameter, which contains the [British Library’s ROR ID](https://ror.org/05dhe8b71). Because `enriched=true`, the request filters by enriched affiliationIdentifier values in the DOI metadata if available and original affiliationIdentifier values if not: 

```shell
curl “https://api.datacite.org/dois?affiliation-id=https://ror.org/05dhe8b71&enriched=true&affiliation=true&publisher=true”
```

#### What’s in the API response?

The response includes a list of enriched DOI metadata records in JSON format. The fields returned in [a list response](https://support.datacite.org/docs/api-get-lists#whats-in-the-api-response) by default are also included.

### Retrieve a single enriched DOI record

When [retrieving a single DOI](https://support.datacite.org/docs/api-get-doi) with the REST API, set the parameter `enriched=true` to retrieve an enriched DOI record. For example:

```shell
curl "https://api.datacite.org/dois/10.60692/44wdx-8kd18?affiliation=true&publisher=true&enriched=true"
```

#### What’s in the API response?

The response includes the enriched DOI metadata record in JSON format. The fields returned in [a singleton response](https://support.datacite.org/docs/api-get-doi#whats-in-the-response) by default are also included.

### Relationships to enrichment records

The enrichment records associated with a DOI are listed in the `relationships` attribute of the DOI record when retrieving lists of DOI records and single enriched DOI records. If no enrichments are listed, then either no enrichment records are available for that DOI or the available enrichment records could not be used to generate an enriched DOI record, leaving the original record in its place. 

The list below provides a description of the additional relationships fields that appear when `enriched=true`:

#### relationships.enrichments

An array of enrichments as dictionaries.

#### relationships.enrichments.data.id

The identifier of the enrichment.

#### relationships.enrichments.data.type

Always "enrichments".

> 📘 Notice a metadata issue?
> 
> Contact [support@datacite.org](mailto:support@datacite.org) to report any issues with the metadata in enriched DOI records. Metadata feedback helps DataCite improve COMET enrichment processes and supports DOI metadata precision across the research ecosystem.

## Enrichment records

Enrichment records describe changes to DataCite DOI metadata, but they do not alter the original DOI metadata maintained by DataCite members. When combined with original DOI records, enrichment records can be used to generate separate, enriched DOI records.

### Structure of enrichment records

Enrichment records have three core pieces of information: 

- The DOI on which the enrichment is asserting a change  
- The provenance of the enrichment, i.e., the resource that produced the enrichment record  
- The enrichment action, i.e., the change the enrichment asserts to the DOI’s original metadata

#### Enrichment record fields

Each field of an enrichment record is described below:

| Field         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| doi           | The target DOI of the enrichment record.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| sourceId  | A DOI for a resource containing provenance information about the enrichment source, including project documentation and related datasets.                                                                                                                                                                                                                                                                                                                                                  |
| field         | The top-level metadata field to enrich, e.g., creators, relatedIdentifiers, types, etc.                                                                                                                                                                                                                                                                                                                                                                           |
| action        | The action that the enrichment performs. The available actions are:  update (change the entire top-level "field" from the "originalValue" to the "enrichedValue")  updateChild (change a child object within the top-level "field" from the "originalValue" to the "enrichedValue")  insert (insert the object in "enrichedValue" into the top-level "field")  deleteChild (remove the object in "originalValue" within the top-level field specified in "field") |
| originalValue | When the action is update, updateChild, or deleteChild: the original value of the field or the child value to be replaced with the enrichedValue. Otherwise, this field is empty.                                                                                                                                                                                                                                                                                 |
| enrichedValue | When the action is update, updateChild, or insert: the enriched value of the field or child value. Otherwise, this field is empty.                                                                                                                                                                                                                                                                                                                                |
### Retrieve a list of enrichment records

Retrieve a list of enrichments via a GET request to <https://api.datacite.org/enrichments> with optional parameters:

```shell
curl https://api.datacite.org/enrichments
```

#### Parameters

The enrichments endpoint supports filter parameters that refine the list of results. This includes the following filter:

| Filter      | Example values            | Description                                                            |
| :---------- | :------------------------ | :--------------------------------------------------------------------- |
| `doi`       | 10.48550/arxiv.2408.15127 | Retrieve enrichments for a specific DOI                                |

#### What's in the API response?

The REST API response includes enrichment records in JSON format. If another page is available for the request, the URL of the new page will be available in `links.next` portion of the response.

### Retrieve a single enrichment record

If you know the ID of an enrichment record, you can retrieve a single enrichment record via a GET request to <https://api.datacite.org/enrichments/{id}>. For example:

```shell
curl https://api.datacite.org/enrichments/dae3ff7e-6c18-4391-b5fd-c5ad29988d95
```
