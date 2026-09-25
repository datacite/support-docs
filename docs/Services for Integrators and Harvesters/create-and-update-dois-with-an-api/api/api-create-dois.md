---
title: Create DOIs with the REST API
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
To create DOIs with the REST API, you will need:

- **Repository account credentials** or **a corresponding [API key](doc:api-keys)**. Only Repository accounts have the ability to create and update DOIs. For more information on account types and permissions, see [Accounts in DataCite](doc:datacite-account-types).
- **Prefix**. The prefix associated with your Repository account must be included in the API request. The request will fail with an error message if the prefix used is not associated with your Repository ID.

> 👍 Test and Production Environments
> 
> DataCite's test and production environments are completely separate. Your repository credentials, password and prefix will be different for each environment. The examples in this guide use the test environment. Make sure you are using the correct endpoint:
> 
> Test: <https://api.test.datacite.org/>  
> Production: <https://api.datacite.org/>
> 
> For more information, see our [Testing Guide](doc:testing-guide).

## DOI Creation Basics

To add a new DOI, you will make a POST request to <https://api.test.datacite.org/dois> with a JSON payload. See the [API Reference](ref:post_dois) for more information.

Your Repository account username and password are needed for authentication. [API keys](api-keys#use-an-api-key) corresponding to a Repository account can also be used for authentication instead of a Repository credentials. The JSON payload can be specified in a file. Here is an example curl command using the test endpoint:

```shell
curl -X POST -H "Content-Type: application/vnd.api+json" --user YOUR_REPOSITORY_ID:YOUR_PASSWORD -d @doi.json https://api.test.datacite.org/dois 
```

Replace `YOUR_REPOSITORY_ID:YOUR_PASSWORD` with your DataCite repository credentials and replace `doi.json`with the name of your JSON payload file.

## Constructing the JSON Payload

Repositories have several options when creating DOIs.

### Create a Findable DOI or a Draft record

Repositories can create a Findable DOI by including the attribute `"event"` with value `"publish"` in the payload.

When `"event": "publish"` is not included, a Draft record will be created by default. To change this record to a Findable DOI, a second request to update the DOI state is required.

Learn more about [DOI States](doc:doi-states).

### Auto-generate a suffix or specify a suffix

Repositories can opt to have DataCite auto-generate a random DOI suffix. This is done by including the `"prefix"` attribute and excluding the `"doi"` attribute. Following a successful request, the auto-generated suffix will be returned in the response.

To specify a suffix, include the `"doi"` attribute with the full DOI name (prefix and suffix combined). When the `"doi"` attribute is included, the `"prefix"` attribute is not required. For considerations when specifying a suffix, see [DOI Basics](doc:doi-basics#suffix).

### Include metadata as JSON or provide alternate formats

By default, the REST API allows DataCite metadata properties to be provided directly in the JSON payload.

> 📘 What metadata should I include?
> 
> The [DataCite Metadata Schema documentation](https://schema.datacite.org) contains information on required metadata, optional metadata, and those metadata elements that are recommended for enhancing data discovery. You will also find descriptions of controlled vocabulary for those fields that require it.

As an alternative to providing metadata attributes directly in JSON, you can also provide metadata in other formats.

The following metadata formats can be used to register DOIs:

- DataCite XML
- RIS
- BibTeX
- Schema.org JSON-LD
- Citeproc JSON
- Codemeta
- Crossref XML

You do this by 1.) base64-encoding the metadata and 2.) including them in the `"xml"` attribute of the JSON payload. An example can be found in this [knowledge base article](doc:what-formats-can-i-use-to-submit-my-metadata-and-how-do-i-do-it). 

## Examples

### Create a Findable DOI with basic metadata and auto-generated suffix

In this example, we will create a DOI in Findable state with an auto-generated suffix.

The example payload includes:

- The attribute `"event"` with value `"publish"` to trigger creation of a Findable DOI.
- The attribute `"prefix"`, without the attribute `"doi"`, to trigger suffix auto-generation.
  - Change this prefix to the one associated with your Repository account.
- The minimum required metadata properties from the DataCite Metadata Schema:
  - Creator
  - Title
  - Publisher
  - PublicationYear
  - resourceTypeGeneral
- The `"url"` to which the DOI will resolve.

Although Identifier (the DOI) is also a required property, it does not need to be included here because the suffix is automatically generated.

#### Request Payload

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "event": "publish",
      "prefix": "10.5438",
      "creators": [
        {
          "name": "DataCite Metadata Working Group"
        }
      ],
      "titles": [
        {
          "title": "DataCite Metadata Schema Documentation for the Publication and Citation of Research Data v4.0"
        }
      ],
      "publisher": "DataCite e.V.",
      "publicationYear": 2016,
      "types": {
        "resourceTypeGeneral": "Text"
      },
      "url": "https://example.org"
    }
  }
}
```

#### Response

A successful request will result in a 201 Created response. This will include the full DOI name with the auto-generated suffix, the complete metadata, and other information. Your response will look something like the following, but containing your Repository information:

```json
{
  "data": {
    "id": "10.5438/q5e8-9585",
    "type": "dois",
    "attributes": {
      "doi": "10.5438/q5e8-9585",
      "prefix": "10.5438",
      "suffix": "q5e8-9585",
      "identifiers": [],
      "alternateIdentifiers": [],
      "creators": [
        {
          "name": "DataCite Metadata Working Group",
          "affiliation": [],
          "nameIdentifiers": []
        }
      ],
      "titles": [
        {
          "title": "DataCite Metadata Schema Documentation for the Publication and Citation of Research Data v4.0"
        }
      ],
      "publisher": "DataCite e.V.",
      "container": {},
      "publicationYear": 2016,
      "subjects": [],
      "contributors": [],
      "dates": [],
      "language": null,
      "types": {
        "schemaOrg": "ScholarlyArticle",
        "citeproc": "article-journal",
        "bibtex": "article",
        "ris": "RPRT",
        "resourceTypeGeneral": "Text"
      },
      "relatedIdentifiers": [],
      "relatedItems": [],
      "sizes": [],
      "formats": [],
      "version": null,
      "rightsList": [],
      "descriptions": [],
      "geoLocations": [],
      "fundingReferences": [],
      "xml": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHJlc291cmNlIHhtbG5zOnhzaT0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEtaW5zdGFuY2UiIHhtbG5zPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCIgeHNpOnNjaGVtYUxvY2F0aW9uPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCBodHRwOi8vc2NoZW1hLmRhdGFjaXRlLm9yZy9tZXRhL2tlcm5lbC00L21ldGFkYXRhLnhzZCI+CiAgPGlkZW50aWZpZXIgaWRlbnRpZmllclR5cGU9IkRPSSI+MTAuNTQzOC9RNUU4LTk1ODU8L2lkZW50aWZpZXI+CiAgPGNyZWF0b3JzPgogICAgPGNyZWF0b3I+CiAgICAgIDxjcmVhdG9yTmFtZT5EYXRhQ2l0ZSBNZXRhZGF0YSBXb3JraW5nIEdyb3VwPC9jcmVhdG9yTmFtZT4KICAgIDwvY3JlYXRvcj4KICA8L2NyZWF0b3JzPgogIDx0aXRsZXM+CiAgICA8dGl0bGU+RGF0YUNpdGUgTWV0YWRhdGEgU2NoZW1hIERvY3VtZW50YXRpb24gZm9yIHRoZSBQdWJsaWNhdGlvbiBhbmQgQ2l0YXRpb24gb2YgUmVzZWFyY2ggRGF0YSB2NC4wPC90aXRsZT4KICA8L3RpdGxlcz4KICA8cHVibGlzaGVyPkRhdGFDaXRlIGUuVi48L3B1Ymxpc2hlcj4KICA8cHVibGljYXRpb25ZZWFyPjIwMTY8L3B1YmxpY2F0aW9uWWVhcj4KICA8cmVzb3VyY2VUeXBlIHJlc291cmNlVHlwZUdlbmVyYWw9IlRleHQiLz4KICA8c2l6ZXMvPgogIDxmb3JtYXRzLz4KICA8dmVyc2lvbi8+CjwvcmVzb3VyY2U+",
      "url": "https://example.org",
      "contentUrl": null,
      "metadataVersion": 0,
      "schemaVersion": null,
      "source": "api",
      "isActive": true,
      "state": "findable",
      "reason": null,
      "landingPage": null,
      "viewCount": 0,
      "viewsOverTime": [],
      "downloadCount": 0,
      "downloadsOverTime": [],
      "referenceCount": 0,
      "citationCount": 0,
      "citationsOverTime": [],
      "partCount": 0,
      "partOfCount": 0,
      "versionCount": 0,
      "versionOfCount": 0,
      "created": "2023-08-21T19:02:56.000Z",
      "registered": "2023-08-21T19:02:56.000Z",
      "published": "2016",
      "updated": "2023-08-21T19:02:56.000Z"
    },
    "relationships": {
      "client": {
        "data": {
          "id": "datacite.datacite",
          "type": "clients"
        }
      },
      "provider": {
        "data": {
          "id": "datacite",
          "type": "providers"
        }
      },
      "media": {
        "data": {
          "id": "10.5438/q5e8-9585",
          "type": "media"
        }
      },
      "references": {
        "data": []
      },
      "citations": {
        "data": []
      },
      "parts": {
        "data": []
      },
      "partOf": {
        "data": []
      },
      "versions": {
        "data": []
      },
      "versionOf": {
        "data": []
      }
    }
  }
}
```

### Create a Findable DOI with rich metadata and specify suffix

In this example, we will create a DOI in Findable state with an explicit DOI suffix specified in our payload.

The example payload includes:

- The attribute `"event"` with value `"publish"` to trigger creation of a Findable DOI.
- The attribute `"doi"` with the full DOI name (prefix/suffix).
  - Change the prefix to the one associated with your Repository account.
- All required, recommended, and optional properties from the DataCite Metadata Schema.
- The `"url"` to which the DOI will resolve.

> 📘 How do I structure the metadata in JSON?
> 
> The properties correspond to the DataCite Metadata Schema. Some of the property names are slightly different from the XML schema.
> 
> The following resources are available to help you include rich metadata:
> 
> - The [API Reference](ref:post_dois) provides an interactive tool to construct JSON metadata.
> - You can copy the example Request Payload below as a starting point.
> - Another approach is to look at the response from a DOI request. Here is an example of an API query that will retrieve all the available metadata fields in JSON: <https://api.test.datacite.org/dois/10.17596/qf5s-pc52?affiliation=true>

#### Request Payload

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "doi": "10.17596/qf5s-pc52",
      "event": "publish",
      "creators": [
        {
          "name": "Miller, Elizabeth",
          "nameType": "Personal",
          "givenName": "Elizabeth",
          "familyName": "Miller",
          "affiliation": [
            {
              "affiliationIdentifier": "https://ror.org/04wxnsj81",
              "affiliationIdentifierScheme": "ROR",
              "name": "DataCite",
              "schemeUri": "https://ror.org/"
            },
            {
              "affiliationIdentifier": "https://ror.org/05dxps055",
              "affiliationIdentifierScheme": "ROR",
              "name": "California Institute of Technology",
              "schemeUri": "https://ror.org/"
            }
          ],
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0001-5000-0007",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        }
      ],
      "titles": [
        {
          "lang": "en",
          "title": "Full DataCite XML Example"
        },
        {
          "lang": "en",
          "title": "Demonstration of DataCite Properties.",
          "titleType": "Subtitle"
        }
      ],
      "publisher": {
        "name": "DataCite",
        "publisherIdentifier":"https://ror.org/04wxnsj81",
        "publisherIdentifierScheme":"ROR",
        "schemeUri": "https://ror.org/"
      },
      "publicationYear": 2014,
      "subjects": [
        {
          "subject": "computer science",
          "schemeUri": "http://dewey.info/",
          "subjectScheme": "dewey",
          "classificationCode": "000"
        }
      ],
      "contributors": [
        {
          "name": "Starr, Joan",
          "nameType": "Personal",
          "givenName": "Joan",
          "familyName": "Starr",
          "affiliation": [
            {
              "affiliationIdentifier": "https://ror.org/03yrm5c26",
              "affiliationIdentifierScheme": "ROR",
              "name": "California Digital Library",
              "schemeUri": "https://ror.org/"
            }
          ],
          "contributorType": "ProjectLeader",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-7285-027X",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        }
      ],
      "dates": [
        {
          "date": "2021-01-26",
          "dateType": "Updated",
          "dateInformation": "Updated with 4.4 properties"
        },
        {
          "date": "2014",
          "dateType": "Issued",
          "dateInformation": null
        }
      ],
      "alternateIdentifiers": [
        {
          "alternateIdentifierType": "URL",
          "alternateIdentifier": "https://schema.datacite.org/meta/kernel-4.4/example/datacite-example-full-v4.4.xml"
        }
      ],
      "language": "en",
      "types": {
        "resourceType": "XML",
        "resourceTypeGeneral": "Software"
      },
      "relatedIdentifiers": [
        {
          "schemeUri": "https://github.com/citation-style-language/schema/raw/master/csl-data.json",
          "schemeType": null,
          "relationType": "HasMetadata",
          "relatedIdentifier": "https://data.datacite.org/application/citeproc+json/10.5072/example-full",
          "resourceTypeGeneral": null,
          "relatedIdentifierType": "URL",
          "relatedMetadataScheme": "citeproc+json"
        },
        {
          "relationType": "IsReviewedBy",
          "relatedIdentifier": "arXiv:0706.0001",
          "resourceTypeGeneral": "Text",
          "relatedIdentifierType": "arXiv"
        },
        {
          "relationType": "Other",
          "relatedIdentifier": "10.82433/e34e-y143",
          "resourceTypeGeneral": "JournalArticle",
          "relatedIdentifierType": "DOI",
          "relationTypeInformation": "is reply to"
        }
      ],
      "relatedItems": [
        {
          "titles": [
            {
              "title": "Physics letters B"
            }
          ],
          "volume": "776",
          "lastPage": "264",
          "firstPage": "249",
          "relationType": "IsPublishedIn",
          "publicationYear": "2018",
          "relatedItemType": "Journal",
          "relatedItemIdentifier": {
            "relatedItemIdentifier": "0370-2693",
            "relatedItemIdentifierType": "ISSN"
          }
        }
      ],
      "sizes": [
        "4 kB"
      ],
      "formats": [
        "application/xml"
      ],
      "version": "4.2",
      "rightsList": [
        {
          "rights": "Creative Commons Zero v1.0 Universal",
          "rightsUri": "https://creativecommons.org/publicdomain/zero/1.0/legalcode",
          "schemeUri": "https://spdx.org/licenses/",
          "rightsIdentifier": "cc0-1.0",
          "rightsIdentifierScheme": "SPDX"
        }
      ],
      "descriptions": [
        {
          "lang": "en-US",
          "description": "XML example of all DataCite Metadata Schema v4.4 properties.",
          "descriptionType": "Abstract"
        }
      ],
      "geoLocations": [
        {
          "geoLocationBox": {
            "eastBoundLongitude": -68.211,
            "northBoundLatitude": 42.893,
            "southBoundLatitude": 41.09,
            "westBoundLongitude": -71.032
          },
          "geoLocationPlace": "Atlantic Ocean",
          "geoLocationPoint": {
            "pointLatitude": 31.233,
            "pointLongitude": -67.302
          }
        }
      ],
      "fundingReferences": [
        {
          "awardUri": "https://www.moore.org/grants/list/GBMF3859.01",
          "awardTitle": "Full DataCite XML Example",
          "funderName": "National Science Foundation",
          "awardNumber": "CBET-106",
          "funderIdentifier": "https://ror.org/021nxhr62",
          "funderIdentifierType": "ROR"
        }
      ],
      "url": "https://example.org"
    }
  }
}
```

#### Response

As with the previous example, a successful request will result in a 201 Created response. This will include the full DOI name as specified.

### Create Findable DOI using DataCite XML

In the previous examples, we included DataCite metadata in the `“attributes”` of the JSON payload. Here, we will submit DataCite XML to the REST API.

The example payload includes:

- The attribute `"event"` with value `"publish"` to trigger creation of a Findable DOI.
- The attribute `"doi"` with the full DOI name (prefix/suffix).
  - Change the prefix to the one associated with your Repository account.
- The attribute `"xml"`, containing base64-encoded DataCite XML.
- The `"url"` to which the DOI will resolve.

#### Example XML

This example uses the following XML with the minimum required metadata properties:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<resource xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://datacite.org/schema/kernel-4" xsi:schemaLocation="http://datacite.org/schema/kernel-4 http://schema.datacite.org/meta/kernel-4/metadata.xsd">
  <identifier identifierType="DOI">10.5438/2wnw-c484</identifier>
  <creators>
    <creator>
      <creatorName>DataCite Metadata Working Group</creatorName>
    </creator>
  </creators>
  <titles>
    <title>DataCite Metadata Schema Documentation for the Publication and Citation of Research Data v4.0</title>
  </titles>
  <publisher>DataCite e.V.</publisher>
  <publicationYear>2016</publicationYear>
  <resourceType resourceTypeGeneral="Text"/>
</resource>
```

To include this XML in the JSON payload, it must be base-64 encoded. There are various libraries and command-line tools that can be used for encoding. You can also check the encoding with <https://www.base64encode.org/>.

#### Request Payload

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "event": "publish",
      "doi": "10.5438/2wnw-c484",
      "xml": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHJlc291cmNlIHhtbG5zOnhzaT0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEtaW5zdGFuY2UiIHhtbG5zPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCIgeHNpOnNjaGVtYUxvY2F0aW9uPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCBodHRwOi8vc2NoZW1hLmRhdGFjaXRlLm9yZy9tZXRhL2tlcm5lbC00L21ldGFkYXRhLnhzZCI+CiAgPGlkZW50aWZpZXIgaWRlbnRpZmllclR5cGU9IkRPSSI+MTAuNTQzOC8yd253LWM0ODQ8L2lkZW50aWZpZXI+CiAgPGNyZWF0b3JzPgogICAgPGNyZWF0b3I+CiAgICAgIDxjcmVhdG9yTmFtZT5EYXRhQ2l0ZSBNZXRhZGF0YSBXb3JraW5nIEdyb3VwPC9jcmVhdG9yTmFtZT4KICAgIDwvY3JlYXRvcj4KICA8L2NyZWF0b3JzPgogIDx0aXRsZXM+CiAgICA8dGl0bGU+RGF0YUNpdGUgTWV0YWRhdGEgU2NoZW1hIERvY3VtZW50YXRpb24gZm9yIHRoZSBQdWJsaWNhdGlvbiBhbmQgQ2l0YXRpb24gb2YgUmVzZWFyY2ggRGF0YSB2NC4wPC90aXRsZT4KICA8L3RpdGxlcz4KICA8cHVibGlzaGVyPkRhdGFDaXRlIGUuVi48L3B1Ymxpc2hlcj4KICA8cHVibGljYXRpb25ZZWFyPjIwMTY8L3B1YmxpY2F0aW9uWWVhcj4KICA8cmVzb3VyY2VUeXBlIHJlc291cmNlVHlwZUdlbmVyYWw9IlRleHQiLz4KPC9yZXNvdXJjZT4=",
      "url": "https://example.org/"
    }
  }
}
```

#### Response

The response will include the metadata submitted via XML as JSON. 

```json
{
  "data": {
    "id": "10.82247/2wnw-c484",
    "type": "dois",
    "attributes": {
      "doi": "10.82247/2wnw-c484",
      "prefix": "10.82247",
      "suffix": "2wnw-c484",
      "identifiers": [],
      "alternateIdentifiers": [],
      "creators": [
        {
          "name": "DataCite Metadata Working Group",
          "nameIdentifiers": [],
          "affiliation": []
        }
      ],
      "titles": [
        {
          "title": "DataCite Metadata Schema Documentation for the Publication and Citation of Research Data v4.0"
        }
      ],
      "publisher": "DataCite e.V.",
      "container": {},
      "publicationYear": 2016,
      "subjects": [],
      "contributors": [],
      "dates": [
        {
          "date": "2016",
          "dateType": "Issued"
        }
      ],
      "language": null,
      "types": {
        "schemaOrg": "ScholarlyArticle",
        "citeproc": "article-journal",
        "bibtex": "article",
        "ris": "RPRT",
        "resourceTypeGeneral": "Text"
      },
      "relatedIdentifiers": [],
      "relatedItems": [],
      "sizes": [],
      "formats": [],
      "version": null,
      "rightsList": [],
      "descriptions": [],
      "geoLocations": [],
      "fundingReferences": [],
      "xml": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHJlc291cmNlIHhtbG5zOnhzaT0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEtaW5zdGFuY2UiIHhtbG5zPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCIgeHNpOnNjaGVtYUxvY2F0aW9uPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCBodHRwOi8vc2NoZW1hLmRhdGFjaXRlLm9yZy9tZXRhL2tlcm5lbC00L21ldGFkYXRhLnhzZCI+CiAgPGlkZW50aWZpZXIgaWRlbnRpZmllclR5cGU9IkRPSSI+MTAuNTQzOC8yd253LWM0ODQ8L2lkZW50aWZpZXI+CiAgPGNyZWF0b3JzPgogICAgPGNyZWF0b3I+CiAgICAgIDxjcmVhdG9yTmFtZT5EYXRhQ2l0ZSBNZXRhZGF0YSBXb3JraW5nIEdyb3VwPC9jcmVhdG9yTmFtZT4KICAgIDwvY3JlYXRvcj4KICA8L2NyZWF0b3JzPgogIDx0aXRsZXM+CiAgICA8dGl0bGU+RGF0YUNpdGUgTWV0YWRhdGEgU2NoZW1hIERvY3VtZW50YXRpb24gZm9yIHRoZSBQdWJsaWNhdGlvbiBhbmQgQ2l0YXRpb24gb2YgUmVzZWFyY2ggRGF0YSB2NC4wPC90aXRsZT4KICA8L3RpdGxlcz4KICA8cHVibGlzaGVyPkRhdGFDaXRlIGUuVi48L3B1Ymxpc2hlcj4KICA8cHVibGljYXRpb25ZZWFyPjIwMTY8L3B1YmxpY2F0aW9uWWVhcj4KICA8cmVzb3VyY2VUeXBlIHJlc291cmNlVHlwZUdlbmVyYWw9IlRleHQiLz4KPC9yZXNvdXJjZT4=",
      "url": "https://example.org/"
      ...
    }
  }
}
```

### Create an identifier in Draft state

To reserve an identifier in Draft state, you will need to send a request **without the attribute `"event"`**. This will reserve the DOI name without publishing it.

When creating a Draft record, the minimum required metadata and the URL may be included, but are not required or validated.

The example payload includes:

- No attribute `"event"`, unlike when creating a Findable DOI.
- The attribute `"doi"` with the full DOI name (prefix/suffix).

Similar to creating a Finable DOI, you also create a Draft record with an auto-generated suffix by specifying the `"prefix"` attribute instead of the `"doi"` attribute.

#### Request Payload

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "doi": "10.5438/0012"
    }
  }
}
```

#### Response

The response will look something like the following, but containing your Repository information:

```json
{
  "data": {
    "id": "10.5438/0012",
    "type": "dois",
    "attributes": {
      "doi": "10.5438/0012",
      "prefix": "10.5438",
      "suffix": "0012",
      "identifiers": [{
        "identifier": "https://doi.org/10.5438/0012",
        "identifierType": "DOI"
      }],
      "creators": [],
      "titles": [],
      "publisher": null,
      "container": {},
      "publicationYear": null,
      "subjects": [],
      "contributors": [],
      "dates": [],
      "language": null,
      "types": {},
      "relatedIdentifiers": [],
      "sizes": [],
      "formats": [],
      "version": null,
      "rightsList": [],
      "descriptions": [],
      "geoLocations": [],
      "fundingReferences": [],
      "xml": null,
      "url":null,
      "contentUrl": null,
      "metadataVersion": 1,
      "schemaVersion": "http://datacite.org/schema/kernel-4",
      "source": null,
      "isActive": true,
      "state": "draft",
      "reason": null,
      "created": "2016-09-19T21:53:56.000Z",
      "registered": null,
      "updated": "2019-02-06T14:31:27.000Z"
    },
    "relationships": {
      "client": {
        "data": {
          "id": "datacite.datacite",
          "type": "clients"
        }
      },
      "media": {
        "data": []
      }
    }
  },
  "included": [{
    "id": "datacite.datacite",
    "type": "clients",
    "attributes": {
      "name": "DataCite",
      "symbol": "DATACITE.DATACITE",
      "year": 2011,
      "contactName": "DataCite",
      "contactEmail": "support@datacite.org",
      "description": null,
      "domains": "*",
      "url": null,
      "created": "2011-12-07T13:43:39.000Z",
      "updated": "2019-01-02T17:33:06.000Z",
      "isActive": true,
      "hasPassword": true
    },
    "relationships": {
      "provider": {
        "data": {
          "id": "datacite",
          "type": "providers"
        }
      },
      "prefixes": {
        "data": [{
          "id": "10.5438",
          "type": "prefixes"
        }]
      }
    }
  }]
}
```

You have now created a Draft record. It has a DOI string assigned, but is not visible for users, so it will not be functional.

To publish the Draft record as a Findable DOI, you will need to send an update request. This is covered in the next section: [Updating DOIs with the REST API](doc:updating-metadata-with-the-rest-api).
