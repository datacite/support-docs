---
title: Updating from Schema 3 to Schema 4
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
> ❗️ Schema 3 has been deprecated
> 
> As of January 2025, Schema 3 is no longer supported for DOI registrations and updates. 
> 
> DataCite Members and Consortium Organizations must use [Schema 4](https://schema.datacite.org/meta/kernel-4/)  to register DOIs and update DOI metadata.

## Frequently Asked Questions

### What changed from Schema 3 to Schema 4?

Schema 4 introduced two breaking changes:

- The  `resourceType` property was changed from optional to mandatory. This property has `resourceTypeGeneral` as a mandatory attribute.
- The `contributorType` "Funder" was deprecated. This concept was replaced with the `FundingReference` property.

There are also many new properties, sub-properties, and controlled list values. For more information, see the latest version documentation at <https://schema.datacite.org/>.

### Can repositories still register Schema 3 DOIs?

No, new DOIs can only be registered using Schema 4.

### Can repositories update existing Schema 3 DOIs?

Yes, Schema 3 DOIs can still be updated. These updates must be sent as Schema 4 metadata.

### What happens to Schema 3 DOIs that aren’t updated to Schema 4?

Schema 3 DOIs are searchable in DataCite’s APIs and services and continue to resolve.

### I received a 422 error response saying Schema 3 is no longer supported. What can I do?

Because Schema 3 metadata is no longer accepted, DataCite’s APIs return a 422 error response with a message like this:

#### MDS API

```
DOI 10.14454/10703: Schema http://datacite.org/schema/kernel-3 is no longer supported
```

#### REST API

```json
{
  "errors": [
    {
      "source": "xml",
      "title": "DOI 10.14454/10703: Schema http://datacite.org/schema/kernel-3 is no longer supported",
      "uid": "10.14454/10703"
    }
  ]
}

```

To continue registering or updating DOIs, repositories should switch to Schema 4.

***

## How to switch to Schema 4

### Method 1: Submit Schema 4 XML

The DataCite MDS API accepts XML metadata. XML is also accepted via the REST API (“xml” attribute) and the Fabrica File Upload.

To change from Schema 3 to Schema 4 in XML, make the following changes:

#### Specify Kernel 4

The XML record should indicate kernel-4 in the `resource` element:

```xml
<resource xmlns="http://datacite.org/schema/kernel-4" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://datacite.org/schema/kernel-4 http://schema.datacite.org/meta/kernel-4/metadata.xsd">
```

kernel-4 will always represent the latest minor version of Schema 4. Note that it is also possible to specify a minor version, e.g., kernel-4.4. However, because all minor versions are backward compatible, we recommend specifying kernel-4 to stay up-to-date with the latest changes.

> 👍 
> 
> When submitting XML metadata, we recommend specifying the major version (kernel-4). This enables you to always take advantage of the latest minor version changes. All minor versions are backward compatible.

#### Include resourceType / resourceTypeGeneral

The record must include—or be updated to include—the `resourceType` property with the `resourceTypeGeneral` attribute. For example:

```xml
<resourceType resourceTypeGeneral="Dataset">Census Data</resourceType>
```

It is possible to include `resourceTypeGeneral` only without specifying a free text `resourceType`. For example:

```xml
<resourceType resourceTypeGeneral="JournalArticle"/>
```

#### Move Contributors with contributorType "Funder" to FundingReference

The record must not use the `contributorType` "Funder". This information can be moved to the `FundingReference` property, which was introduced in Schema 4.0. This property has sub-properties for the `funderName`, `funderIdentifier`, `awardNumber`, and `awardTitle`.

```xml
<fundingReferences>
  <fundingReference>
    <funderName>European Commission</funderName>
    <funderIdentifier funderIdentifierType="Crossref Funder ID">https://doi.org/10.13039/501100000780</funderIdentifier>
    <awardNumber awardURI="https://cordis.europa.eu/project/rcn/100603_en.html">284382</awardNumber>
    <awardTitle>Institutionalizing global genetic-resource commons. Global Strategies for accessing and using essential public knowledge assets in the life sciences</awardTitle>
  </fundingReference>
<fundingReferences>
```

### Method 2: Submit JSON with the REST API

When updating a Schema 3 DOI to Schema 4, you can [make a PUT request to update the DOI](https://support.datacite.org/reference/put_dois-id) with the REST API. This request should include the following attributes.

#### Include schemaVersion to trigger the update to Schema 4

Include the `schemaVersion` attribute, set to "<http://datacite.org/schema/kernel-4">. While this is not required for new DOI registrations or to update DOIs that already use Schema 4, this is necessary to trigger the update from Schema 3 to Schema 4.

#### Add a resourceTypeGeneral if not already present

If not already present in the record, include the required metadata property `resourceTypeGeneral` (part of `types` in JSON).

```json
{  
  "data": {  
    "id": "10.21384/1f84-ta02",  
    "type": "dois",  
    "attributes": {  
      "doi": "10.21384/1f84-ta02",  
      "types": {  
        "resourceTypeGeneral": "JournalArticle"  
      },  
      "schemaVersion": "http://datacite.org/schema/kernel-4"  
    }  
  }  
}
```

#### Move Contributors with contributorType "Funder" to fundingReferences

If any existing Contributors use `contributorType` “Funder”, they should be migrated to `fundingReferences`. To avoid data loss, provide both the `contributors` property (with all non-Funder contributors) and the `fundingReferences` property.

```json
{  
  "data": {  
    "id": "10.21384/1f84-ta02",  
    "type": "dois",  
    "attributes": {  
      "doi": "10.21384/1f84-ta02",  
      "types": {  
        "resourceTypeGeneral": "JournalArticle"  
      },  
      "contributors": [  
        {  
          "name": "Garcia, Sofia",  
          "contributorType": "ProjectLeader",  
        }  
      ],
      "fundingReferences": [  
        {  
          "funderName": "National Science Foundation",  
          "funderIdentifier": "https://ror.org/021nxhr62",  
          "funderIdentifierType": "ROR"  
        }  
      ],
      "schemaVersion": "http://datacite.org/schema/kernel-4"
    } 
}
```

### Method 3: Use the Fabrica Form

Updating a Schema 3 DOI using the [Fabrica form](doc:fabrica-doi-form) will update the DOI to Schema 4. A warning will appear at the top of the page for Schema 3 DOIs:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9c3ba63-Screen_Shot_2023-12-08_at_08.57.44.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


If the metadata is not compatible with Schema 4, an error message will appear at the bottom of the page: 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8714d5b-Screen_Shot_2023-12-08_at_08.57.39.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


To save the DOI using Schema 4, add  `resourceTypeGeneral` and remove any Contributors with `contributorType` "Funder".

## How to find Schema 3 DOIs

To identify Schema 3 DOIs in your repository, you can use the REST API and filter DOI results by `client-id` and `schema-version` using the request below. Replace the `client-id` "abcd.efgh" with your Repository account ID:

`https://api.datacite.org/dois?client-id=abcd.efgh&schema-version=3`

You can also filter by a Direct Member or Consortium Organization (`provider-id` parameter) or by a Consortium ( `consortium-id`) parameter. See [Queries and filtering: Filtering List Responses](doc:api-queries#filtering-list-responses) for additional filter parameters.