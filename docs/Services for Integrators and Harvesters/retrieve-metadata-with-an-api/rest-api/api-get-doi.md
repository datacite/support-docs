---
title: Retrieve a single DOI
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: Retrieving a list of DOIs
  pages:
    - type: basic
      slug: api-get-lists
      title: Retrieving a list of DOIs
---
Almost any meaningful use of the DataCite REST API will involve some level of record retrieval. The responses from each of your requests fall into two basic categories: 

- Singleton: a single record
- List: a list of records

A **singleton** is a single result, i.e., the metadata for a specific DOI. This section of the guide covers singletons. The next section, [Retrieving a list of DOIs](doc:api-get-lists), will cover lists. 

> 📘 
>
> DataCite offers [a community-enriched DOI metadata layer](doc:metadata-enrichments) that enhances the quality and utility of DataCite metadata. Use [the `enriched=true` parameter](doi: metadata-enrichments#retrieve-a-single-enriched-doi-record) with singleton requests to retrieve the latest enriched metadata record for a DOI. 

## Request

Retrieve a single DOI via a GET request by replacing `{id}` in `https://api.datacite.org/dois/{id}` with the DOI name.

For example, retrieving the metadata record for the DOI `10.14454/qdd3-ps68` from the command line with curl can be done by making a request to `https://api.datacite.org/dois/10.14454/qdd3-ps68`:

```shell
# GET /dois
curl "https://api.datacite.org/dois/10.14454/qdd3-ps68"
```

Affiliation and publisher identifiers (supported in Metadata Schema 4.3+) are not included in REST API responses by default. To include affiliation and publisher identifier details, add `?affiliation=true&publisher=true` to your request. For more information, see our FAQ: [Can I see more detailed affiliation and publisher information in the REST API?](https://support.datacite.org/docs/can-i-see-more-detailed-affiliation-information-in-the-rest-api)

```shell
# GET /dois
curl "https://api.datacite.org/dois/10.14454/qdd3-ps68?affiliation=true&publisher=true"
```

The [API Reference](ref:get_dois-id) provides example code for Node, Ruby, Javascript and Python.

## Response

The response would look like this:

```json
{
  "data": {
    "id": "10.14454/qdd3-ps68",
    "type": "dois",
    "attributes": {
      "doi": "10.14454/qdd3-ps68",
      "prefix": "10.14454",
      "suffix": "qdd3-ps68",
      "identifiers": [],
      "alternateIdentifiers": [],
      "creators": [
        {
          "name": "DataCite Metadata Working Group",
          "nameType": "Organizational",
          "givenName": null,
          "familyName": null,
          "affiliation": [],
          "nameIdentifiers": []
        }
      ],
      "titles": [
        {
          "lang": null,
          "title": "DataCite Metadata Schema Documentation for the Publication and Citation of Research Data and Other Research Outputs v4.7",
          "titleType": null
        }
      ],
      "publisher": {
        "name": "DataCite",
        "schemeUri": "https://ror.org/",
        "publisherIdentifier": "https://ror.org/04wxnsj81",
        "publisherIdentifierScheme": "ROR"
      },
      "container": {},
      "publicationYear": 2026,
      "subjects": [],
      "contributors": [
        {
          "name": "Liffers, Matthias",
          "nameType": "Personal",
          "givenName": "Matthias",
          "familyName": "Liffers",
          "affiliation": [
            {
              "name": "Australian Research Data Commons",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/038sjwq14",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "ProjectLeader",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-3639-2080",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Robertson, Wendy",
          "nameType": "Personal",
          "givenName": "Wendy",
          "familyName": "Robertson",
          "affiliation": [
            {
              "name": "University of Iowa",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/036jqmy94",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "ProjectLeader",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-3368-5080",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Ashton, Jan",
          "nameType": "Personal",
          "givenName": "Jan",
          "familyName": "Ashton",
          "affiliation": [
            {
              "name": "British Library",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/05dhe8b71",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-4676-5263",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Bernal, Isabel",
          "nameType": "Personal",
          "givenName": "Isabel",
          "familyName": "Bernal",
          "affiliation": [
            {
              "name": "Spanish National Research Council",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/02gfc7t72",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-2506-9947",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Devaraju, Anusuriya",
          "nameType": "Personal",
          "givenName": "Anusuriya",
          "familyName": "Devaraju",
          "affiliation": [
            {
              "name": "Commonwealth Scientific and Industrial Research Organisation",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/03qn8fb07",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-0870-3192",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Elger, Kirsten",
          "nameType": "Personal",
          "givenName": "Kirsten",
          "familyName": "Elger",
          "affiliation": [
            {
              "name": "GFZ German Research Centre for Geosciences",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/04z8jg394",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0001-5140-8602",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Habermann, Ted",
          "nameType": "Personal",
          "givenName": "Ted",
          "familyName": "Habermann",
          "affiliation": [
            {
              "name": "Metadata Game Changers (United States)",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/05bp8ka05",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-3585-6733",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Harrison, Melissa",
          "nameType": "Personal",
          "givenName": "Melissa",
          "familyName": "Harrison",
          "affiliation": [
            {
              "name": "EMBL-EBI",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/02catss52",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-3523-4408",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Kraus, Robin",
          "nameType": "Personal",
          "givenName": "Robin",
          "familyName": "Kraus",
          "affiliation": [
            {
              "name": "TIB Hanover",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/04aj4c181",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0009-0008-7705-7407",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Mathews, Ian",
          "nameType": "Personal",
          "givenName": "Ian",
          "familyName": "Mathews",
          "affiliation": [
            {
              "name": "Redivis",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/02jdaj147",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-3436-6639",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Medina-Smith, Andrea",
          "nameType": "Personal",
          "givenName": "Andrea",
          "familyName": "Medina-Smith",
          "affiliation": [
            {
              "name": "Sage Data",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/05534qc24",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-1217-701X",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Moore, Adam Vials",
          "nameType": "Personal",
          "givenName": "Adam Vials",
          "familyName": "Moore",
          "affiliation": [
            {
              "name": "Jisc",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/04wxnsj81",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-2085-1908",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Padfield, Joseph",
          "nameType": "Personal",
          "givenName": "Joseph",
          "familyName": "Padfield",
          "affiliation": [
            {
              "name": "National Gallery",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/043kfff89",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-2572-6428",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Raugh, Anne",
          "nameType": "Personal",
          "givenName": "Anne",
          "familyName": "Raugh",
          "affiliation": [
            {
              "name": "University of Maryland, College Park",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/047s2c258",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-8300-9443",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Shallcross, Michael",
          "nameType": "Personal",
          "givenName": "Michael",
          "familyName": "Shallcross",
          "affiliation": [
            {
              "name": "Inter-University Consortium for Political and Social Research",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/02q7mkh03",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0001-6289-5717",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Strecker, Dorothea",
          "nameType": "Personal",
          "givenName": "Dorothea",
          "familyName": "Strecker",
          "affiliation": [
            {
              "name": "Berlin School of Library and Information Science, Humboldt-Universität zu Berlin",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/01hcx6992",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-9754-3807",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Tarocco, Nicola",
          "nameType": "Personal",
          "givenName": "Nicola",
          "familyName": "Tarocco",
          "affiliation": [
            {
              "name": "CERN",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/01ggx4157",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-2227-1229",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Tvrdy, Peyton",
          "nameType": "Personal",
          "givenName": "Peyton",
          "familyName": "Tvrdy",
          "affiliation": [
            {
              "name": "National Transportation Library, United States Department of Transportation",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/02xfw2e90",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-9720-4725",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Vyčítalová, Hana",
          "nameType": "Personal",
          "givenName": "Hana",
          "familyName": "Vyčítalová",
          "affiliation": [
            {
              "name": "National Library of Technology",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/028txef36",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0002-8323-5790",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "Stathis, Kelly",
          "nameType": "Personal",
          "givenName": "Kelly",
          "familyName": "Stathis",
          "affiliation": [
            {
              "name": "DataCite",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/04wxnsj81",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0001-6133-4045",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        },
        {
          "name": "El-Gebali, Sara",
          "nameType": "Personal",
          "givenName": "Sara",
          "familyName": "El-Gebali",
          "affiliation": [
            {
              "name": "DataCite",
              "schemeUri": null,
              "affiliationIdentifier": "https://ror.org/04wxnsj81",
              "affiliationIdentifierScheme": "ROR"
            }
          ],
          "contributorType": "Editor",
          "nameIdentifiers": [
            {
              "schemeUri": "https://orcid.org",
              "nameIdentifier": "https://orcid.org/0000-0003-1378-5495",
              "nameIdentifierScheme": "ORCID"
            }
          ]
        }
      ],
      "dates": [
        {
          "date": "2026-03-03",
          "dateType": "Issued",
          "dateInformation": null
        }
      ],
      "language": "en",
      "types": {
        "ris": "RPRT",
        "bibtex": "article",
        "citeproc": "article-journal",
        "schemaOrg": "ScholarlyArticle",
        "resourceType": "Documentation",
        "resourceTypeGeneral": "Text"
      },
      "relatedIdentifiers": [
        {
          "schemeUri": null,
          "schemeType": null,
          "relationType": "Documents",
          "relatedIdentifier": "10.14454/28a4-kd32",
          "resourceTypeGeneral": null,
          "relatedIdentifierType": "DOI",
          "relatedMetadataScheme": null
        },
        {
          "schemeUri": null,
          "schemeType": null,
          "relationType": "IsNewVersionOf",
          "relatedIdentifier": "10.14454/mzv1-5b55",
          "resourceTypeGeneral": null,
          "relatedIdentifierType": "DOI",
          "relatedMetadataScheme": null
        }
      ],
      "relatedItems": [],
      "sizes": [],
      "formats": [
        "text/html"
      ],
      "version": "4.7",
      "rightsList": [
        {
          "rights": "Creative Commons Attribution 4.0 International",
          "rightsUri": "https://creativecommons.org/licenses/by/4.0/legalcode",
          "schemeUri": "https://spdx.org/licenses/",
          "rightsIdentifier": "cc-by-4.0",
          "rightsIdentifierScheme": "SPDX"
        }
      ],
      "descriptions": [
        {
          "lang": "en",
          "description": "Introduction: About DataCite; About the DataCite Metadata Schema; Version 4.7 Update; Citation. DataCite Metadata Properties: Overview; 1. Identifier; 2. Creator; 3. Title; 4. Publisher; 5. PublicationYear; 6. Subject; 7. Contributor; 8. Date; 9. Language; 10. ResourceType; 11. AlternateIdentifier; 12. RelatedIdentifier; 13. Size; 14. Format; 15. Version; 16. Rights; 17. Description; 18. GeoLocation; 19. FundingReference; 20. RelatedItem. Appendices: Appendix 1: Controlled List Definitions; Appendix 2: Earlier Version Update Notes; Appendix 3: Standard values for unknown information. Mappings: DataCite to Dublin Core Mapping; FORCE11 Software Citation Principles Mapping; PIDINST Schema Mapping. Guidance: Citation of dynamic datasets; Support for software citation; Using RelatedItem for publication information and related resources. XML Schema and Examples.",
          "descriptionType": "TableOfContents"
        }
      ],
      "geoLocations": [],
      "fundingReferences": [],
      "xml": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHJlc291cmNlIHhtbG5zOnhzaT0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEtaW5zdGFuY2UiIHhtbG5zPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCIgeHNpOnNjaGVtYUxvY2F0aW9uPSJodHRwOi8vZGF0YWNpdGUub3JnL3NjaGVtYS9rZXJuZWwtNCBodHRwOi8vc2NoZW1hLmRhdGFjaXRlLm9yZy9tZXRhL2tlcm5lbC00L21ldGFkYXRhLnhzZCI+CiAgPGlkZW50aWZpZXIgaWRlbnRpZmllclR5cGU9IkRPSSI+MTAuMTQ0NTQvUUREMy1QUzY4PC9pZGVudGlmaWVyPgogIDxjcmVhdG9ycz4KICAgIDxjcmVhdG9yPgogICAgICA8Y3JlYXRvck5hbWUgbmFtZVR5cGU9Ik9yZ2FuaXphdGlvbmFsIj5EYXRhQ2l0ZSBNZXRhZGF0YSBXb3JraW5nIEdyb3VwPC9jcmVhdG9yTmFtZT4KICAgIDwvY3JlYXRvcj4KICA8L2NyZWF0b3JzPgogIDx0aXRsZXM+CiAgICA8dGl0bGU+RGF0YUNpdGUgTWV0YWRhdGEgU2NoZW1hIERvY3VtZW50YXRpb24gZm9yIHRoZSBQdWJsaWNhdGlvbiBhbmQgQ2l0YXRpb24gb2YgUmVzZWFyY2ggRGF0YSBhbmQgT3RoZXIgUmVzZWFyY2ggT3V0cHV0cyB2NC43PC90aXRsZT4KICA8L3RpdGxlcz4KICA8cHVibGlzaGVyIHB1Ymxpc2hlcklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wNHd4bnNqODEiIHB1Ymxpc2hlcklkZW50aWZpZXJTY2hlbWU9IlJPUiIgc2NoZW1lVVJJPSJodHRwczovL3Jvci5vcmcvIj5EYXRhQ2l0ZTwvcHVibGlzaGVyPgogIDxwdWJsaWNhdGlvblllYXI+MjAyNjwvcHVibGljYXRpb25ZZWFyPgogIDxyZXNvdXJjZVR5cGUgcmVzb3VyY2VUeXBlR2VuZXJhbD0iVGV4dCI+RG9jdW1lbnRhdGlvbjwvcmVzb3VyY2VUeXBlPgogIDxjb250cmlidXRvcnM+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJQcm9qZWN0TGVhZGVyIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPkxpZmZlcnMsIE1hdHRoaWFzPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+TWF0dGhpYXM8L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+TGlmZmVyczwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAyLTM2MzktMjA4MDwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wMzhzandxMTQiIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5BdXN0cmFsaWFuIFJlc2VhcmNoIERhdGEgQ29tbW9uczwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iUHJvamVjdExlYWRlciI+CiAgICAgIDxjb250cmlidXRvck5hbWUgbmFtZVR5cGU9IlBlcnNvbmFsIj5Sb2JlcnRzb24sIFdlbmR5PC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+V2VuZHk8L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+Um9iZXJ0c29uPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItMzM2OC01MDgwPC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzAzNmpxbXk5NCIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPlVuaXZlcnNpdHkgb2YgSW93YTwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPkFzaHRvbiwgSmFuPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+SmFuPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPkFzaHRvbjwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAzLTQ2NzYtNTI2MzwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wNWRoZThiNzEiIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5Ccml0aXNoIExpYnJhcnk8L2FmZmlsaWF0aW9uPgogICAgPC9jb250cmlidXRvcj4KICAgIDxjb250cmlidXRvciBjb250cmlidXRvclR5cGU9IkVkaXRvciI+CiAgICAgIDxjb250cmlidXRvck5hbWUgbmFtZVR5cGU9IlBlcnNvbmFsIj5CZXJuYWwsIElzYWJlbDwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPklzYWJlbDwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5CZXJuYWw8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDAtMDAwMy0yNTA2LTk5NDc8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDJnZmM3dDcyIiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+U3BhbmlzaCBOYXRpb25hbCBSZXNlYXJjaCBDb3VuY2lsPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+RGV2YXJhanUsIEFudXN1cml5YTwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPkFudXN1cml5YTwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5EZXZhcmFqdTwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAzLTA4NzAtMzE5MjwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wM3FuOGZiMDciIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5Db21tb253ZWFsdGggU2NpZW50aWZpYyBhbmQgSW5kdXN0cmlhbCBSZXNlYXJjaCBPcmdhbmlzYXRpb248L2FmZmlsaWF0aW9uPgogICAgPC9jb250cmlidXRvcj4KICAgIDxjb250cmlidXRvciBjb250cmlidXRvclR5cGU9IkVkaXRvciI+CiAgICAgIDxjb250cmlidXRvck5hbWUgbmFtZVR5cGU9IlBlcnNvbmFsIj5FbGdlciwgS2lyc3RlbjwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPktpcnN0ZW48L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+RWxnZXI8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDAtMDAwMS01MTQwLTg2MDI8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDR6OGpnMzk0IiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+R0ZaIEdlcm1hbiBSZXNlYXJjaCBDZW50cmUgZm9yIEdlb3NjaWVuY2VzPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+SGFiZXJtYW5uLCBUZWQ8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5UZWQ8L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+SGFiZXJtYW5uPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDMtMzU4NS02NzMzPC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzA1YnA4a2EwNSIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPk1ldGFkYXRhIEdhbWUgQ2hhbmdlcnMgKFVuaXRlZCBTdGF0ZXMpPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+SGFycmlzb24sIE1lbGlzc2E8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5NZWxpc3NhPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPkhhcnJpc29uPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDMtMzUyMy00NDA4PC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzAyY2F0c3M1MiIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPkVNQkwtRUJJPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+S3JhdXMsIFJvYmluPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+Um9iaW48L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+S3JhdXM8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDktMDAwOC03NzA1LTc0MDc8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDRhajRjMTgxIiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+VElCIEhhbm92ZXI8L2FmZmlsaWF0aW9uPgogICAgPC9jb250cmlidXRvcj4KICAgIDxjb250cmlidXRvciBjb250cmlidXRvclR5cGU9IkVkaXRvciI+CiAgICAgIDxjb250cmlidXRvck5hbWUgbmFtZVR5cGU9IlBlcnNvbmFsIj5NYXRoZXdzLCBJYW48L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5JYW48L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+TWF0aGV3czwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAyLTM0MzYtNjYzOTwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wMmpkYWoxNDciIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5SZWRpdmlzPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+TWVkaW5hLVNtaXRoLCBBbmRyZWE8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5BbmRyZWE8L2dpdmVuTmFtZT4KICAgICAgPGZhbWlseU5hbWU+TWVkaW5hLVNtaXRoPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItMTIxNy03MDFYPC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzA1NTM0cWMyNCIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPlNhZ2UgRGF0YTwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPk1vb3JlLCBBZGFtIFZpYWxzPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+QWRhbSBWaWFsczwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5Nb29yZTwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAyLTIwODUtMTkwODwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wNHd4bnNqODEiIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5KaXNjPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+UGFkZmllbGQsIEpvc2VwaDwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPkpvc2VwaDwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5QYWRmaWVsZDwvZmFtaWx5TmFtZT4KICAgICAgPG5hbWVJZGVudGlmaWVyIG5hbWVJZGVudGlmaWVyU2NoZW1lPSJPUkNJRCIgc2NoZW1lVVJJPSJodHRwczovL29yY2lkLm9yZyI+aHR0cHM6Ly9vcmNpZC5vcmcvMDAwMC0wMDAyLTI1NzItNjQyODwvbmFtZUlkZW50aWZpZXI+CiAgICAgIDxhZmZpbGlhdGlvbiBhZmZpbGlhdGlvbklkZW50aWZpZXI9Imh0dHBzOi8vcm9yLm9yZy8wNDNrZmZmODkiIGFmZmlsaWF0aW9uSWRlbnRpZmllclNjaGVtZT0iUk9SIj5OYXRpb25hbCBHYWxsZXJ5PC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+UmF1Z2gsIEFubmU8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5Bbm5lPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPlJhdWdoPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItODMwMC05NDQzPC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzA0N3MyYzI1OCIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPlVuaXZlcnNpdHkgb2YgTWFyeWxhbmQsIENvbGxlZ2UgUGFyazwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPlNoYWxsY3Jvc3MsIE1pY2hhZWw8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5NaWNoYWVsPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPlNoYWxsY3Jvc3M8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDAtMDAwMS02Mjg5LTU3MTc8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDJxN21raDAzIiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+SW50ZXItVW5pdmVyc2l0eSBDb25zb3J0aXVtIGZvciBQb2xpdGljYWwgYW5kIFNvY2lhbCBSZXNlYXJjaDwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPlN0cmVja2VyLCBEb3JvdGhlYTwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPkRvcm90aGVhPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPlN0cmVja2VyPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItOTc1NC0zODA3PC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzAxaGN4Njk5MiIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPkJlcmxpbiBTY2hvb2wgb2YgTGlicmFyeSBhbmQgSW5mb3JtYXRpb24gU2NpZW5jZSwgSHVtYm9sZHQtVW5pdmVyc2l0w6R0IHp1IEJlcmxpbjwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPlRhcm9jY28sIE5pY29sYTwvY29udHJpYnV0b3JOYW1lPgogICAgICA8Z2l2ZW5OYW1lPk5pY29sYTwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5UYXJvY2NvPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItMjIyNy0xMjI5PC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzAxZ2d4NDE1NyIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPkNFUk48L2FmZmlsaWF0aW9uPgogICAgPC9jb250cmlidXRvcj4KICAgIDxjb250cmlidXRvciBjb250cmlidXRvclR5cGU9IkVkaXRvciI+CiAgICAgIDxjb250cmlidXRvck5hbWUgbmFtZVR5cGU9IlBlcnNvbmFsIj5UdnJkeSwgUGV5dG9uPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+UGV5dG9uPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPlR2cmR5PC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDItOTcyMC00NzI1PC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzAyeGZ3MmU5MCIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPk5hdGlvbmFsIFRyYW5zcG9ydGF0aW9uIExpYnJhcnksIFVuaXRlZCBTdGF0ZXMgRGVwYXJ0bWVudCBvZiBUcmFuc3BvcnRhdGlvbjwvYWZmaWxpYXRpb24+CiAgICA8L2NvbnRyaWJ1dG9yPgogICAgPGNvbnRyaWJ1dG9yIGNvbnRyaWJ1dG9yVHlwZT0iRWRpdG9yIj4KICAgICAgPGNvbnRyaWJ1dG9yTmFtZSBuYW1lVHlwZT0iUGVyc29uYWwiPlZ5xI3DrXRhbG92w6EsIEhhbmE8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5IYW5hPC9naXZlbk5hbWU+CiAgICAgIDxmYW1pbHlOYW1lPlZ5xI3DrXRhbG92w6E8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDAtMDAwMi04MzIzLTU3OTA8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDI4dHhlZjM2IiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+TmF0aW9uYWwgTGlicmFyeSBvZiBUZWNobm9sb2d5PC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+U3RhdGhpcywgS2VsbHk8L2NvbnRyaWJ1dG9yTmFtZT4KICAgICAgPGdpdmVuTmFtZT5LZWxseTwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5TdGF0aGlzPC9mYW1pbHlOYW1lPgogICAgICA8bmFtZUlkZW50aWZpZXIgbmFtZUlkZW50aWZpZXJTY2hlbWU9Ik9SQ0lEIiBzY2hlbWVVUkk9Imh0dHBzOi8vb3JjaWQub3JnIj5odHRwczovL29yY2lkLm9yZy8wMDAwLTAwMDEtNjEzMy00MDQ1PC9uYW1lSWRlbnRpZmllcj4KICAgICAgPGFmZmlsaWF0aW9uIGFmZmlsaWF0aW9uSWRlbnRpZmllcj0iaHR0cHM6Ly9yb3Iub3JnLzA0d3huc2o4MSIgYWZmaWxpYXRpb25JZGVudGlmaWVyU2NoZW1lPSJST1IiPkRhdGFDaXRlPC9hZmZpbGlhdGlvbj4KICAgIDwvY29udHJpYnV0b3I+CiAgICA8Y29udHJpYnV0b3IgY29udHJpYnV0b3JUeXBlPSJFZGl0b3IiPgogICAgICA8Y29udHJpYnV0b3JOYW1lIG5hbWVUeXBlPSJQZXJzb25hbCI+RWwtR2ViYWxpLCBTYXJhPC9jb250cmlidXRvck5hbWU+CiAgICAgIDxnaXZlbk5hbWU+U2FyYTwvZ2l2ZW5OYW1lPgogICAgICA8ZmFtaWx5TmFtZT5FbC1HZWJhbGk8L2ZhbWlseU5hbWU+CiAgICAgIDxuYW1lSWRlbnRpZmllciBuYW1lSWRlbnRpZmllclNjaGVtZT0iT1JDSUQiIHNjaGVtZVVSST0iaHR0cHM6Ly9vcmNpZC5vcmciPmh0dHBzOi8vb3JjaWQub3JnLzAwMDAtMDAwMy0xMzc4LTU0OTU8L25hbWVJZGVudGlmaWVyPgogICAgICA8YWZmaWxpYXRpb24gYWZmaWxpYXRpb25JZGVudGlmaWVyPSJodHRwczovL3Jvci5vcmcvMDR3eG5zajgxIiBhZmZpbGlhdGlvbklkZW50aWZpZXJTY2hlbWU9IlJPUiI+RGF0YUNpdGU8L2FmZmlsaWF0aW9uPgogICAgPC9jb250cmlidXRvcj4KICA8L2NvbnRyaWJ1dG9ycz4KICA8ZGF0ZXM+CiAgICA8ZGF0ZSBkYXRlVHlwZT0iSXNzdWVkIj4yMDI2LTAzLTAzPC9kYXRlPgogIDwvZGF0ZXM+CiAgPGxhbmd1YWdlPmVuPC9sYW5ndWFnZT4KICA8cmVsYXRlZElkZW50aWZpZXJzPgogICAgPHJlbGF0ZWRJZGVudGlmaWVyIHJlbGF0ZWRJZGVudGlmaWVyVHlwZT0iRE9JIiByZWxhdGlvblR5cGU9IkRvY3VtZW50cyI+MTAuMTQ0NTQvMjhhNC1rZDMyPC9yZWxhdGVkSWRlbnRpZmllcj4KICAgIDxyZWxhdGVkSWRlbnRpZmllciByZWxhdGVkSWRlbnRpZmllclR5cGU9IkRPSSIgcmVsYXRpb25UeXBlPSJJc05ld1ZlcnNpb25PZiI+MTAuMTQ0NTQvbXp2MS01YjU1PC9yZWxhdGVkSWRlbnRpZmllcj4KICA8L3JlbGF0ZWRJZGVudGlmaWVycz4KICA8c2l6ZXMvPgogIDxmb3JtYXRzPgogICAgPGZvcm1hdD50ZXh0L2h0bWw8L2Zvcm1hdD4KICA8L2Zvcm1hdHM+CiAgPHZlcnNpb24+NC43PC92ZXJzaW9uPgogIDxyaWdodHNMaXN0PgogICAgPHJpZ2h0cyByaWdodHNVUkk9Imh0dHBzOi8vY3JlYXRpdmVjb21tb25zLm9yZy9saWNlbnNlcy9ieS80LjAvbGVnYWxjb2RlIj5DcmVhdGl2ZSBDb21tb25zIEF0dHJpYnV0aW9uIDQuMCBJbnRlcm5hdGlvbmFsPC9yaWdodHM+CiAgPC9yaWdodHNMaXN0PgogIDxkZXNjcmlwdGlvbnM+CiAgICA8ZGVzY3JpcHRpb24geG1sOmxhbmc9ImVuIiBkZXNjcmlwdGlvblR5cGU9IlRhYmxlT2ZDb250ZW50cyI+SW50cm9kdWN0aW9uOiBBYm91dCBEYXRhQ2l0ZTsgQWJvdXQgdGhlIERhdGFDaXRlIE1ldGFkYXRhIFNjaGVtYTsgVmVyc2lvbiA0LjcgVXBkYXRlOyBDaXRhdGlvbi4gRGF0YUNpdGUgTWV0YWRhdGEgUHJvcGVydGllczogT3ZlcnZpZXc7IDEuIElkZW50aWZpZXI7IDIuIENyZWF0b3I7IDMuIFRpdGxlOyA0LiBQdWJsaXNoZXI7IDUuIFB1YmxpY2F0aW9uWWVhcjsgNi4gU3ViamVjdDsgNy4gQ29udHJpYnV0b3I7IDguIERhdGU7IDkuIExhbmd1YWdlOyAxMC4gUmVzb3VyY2VUeXBlOyAxMS4gQWx0ZXJuYXRlSWRlbnRpZmllcjsgMTIuIFJlbGF0ZWRJZGVudGlmaWVyOyAxMy4gU2l6ZTsgMTQuIEZvcm1hdDsgMTUuIFZlcnNpb247IDE2LiBSaWdodHM7IDE3LiBEZXNjcmlwdGlvbjsgMTguIEdlb0xvY2F0aW9uOyAxOS4gRnVuZGluZ1JlZmVyZW5jZTsgMjAuIFJlbGF0ZWRJdGVtLiBBcHBlbmRpY2VzOiBBcHBlbmRpeCAxOiBDb250cm9sbGVkIExpc3QgRGVmaW5pdGlvbnM7IEFwcGVuZGl4IDI6IEVhcmxpZXIgVmVyc2lvbiBVcGRhdGUgTm90ZXM7IEFwcGVuZGl4IDM6IFN0YW5kYXJkIHZhbHVlcyBmb3IgdW5rbm93biBpbmZvcm1hdGlvbi4gTWFwcGluZ3M6IERhdGFDaXRlIHRvIER1YmxpbiBDb3JlIE1hcHBpbmc7IEZPUkNFMTEgU29mdHdhcmUgQ2l0YXRpb24gUHJpbmNpcGxlcyBNYXBwaW5nOyBQSURJTlNUIFNjaGVtYSBNYXBwaW5nLiBHdWlkYW5jZTogQ2l0YXRpb24gb2YgZHluYW1pYyBkYXRhc2V0czsgU3VwcG9ydCBmb3Igc29mdHdhcmUgY2l0YXRpb247IFVzaW5nIFJlbGF0ZWRJdGVtIGZvciBwdWJsaWNhdGlvbiBpbmZvcm1hdGlvbiBhbmQgcmVsYXRlZCByZXNvdXJjZXMuIFhNTCBTY2hlbWEgYW5kIEV4YW1wbGVzLjwvZGVzY3JpcHRpb24+CiAgPC9kZXNjcmlwdGlvbnM+CjwvcmVzb3VyY2U+Cg==",
      "url": "https://datacite-metadata-schema.readthedocs.io/en/4.7/",
      "contentUrl": null,
      "metadataVersion": 4,
      "schemaVersion": "http://datacite.org/schema/kernel-4",
      "source": "fabricaForm",
      "isActive": true,
      "state": "findable",
      "reason": null,
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
      "created": "2025-07-30T22:26:39.000Z",
      "registered": "2026-02-26T22:49:26.000Z",
      "published": "2026",
      "updated": "2026-02-26T22:49:26.000Z"
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
          "id": "10.14454/qdd3-ps68",
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

### What's in the response?

The REST API includes the complete DOI metadata record in JSON.

The list below provides a description of the additional fields that appear in the API response and provide extra information about the DOI. This information is different from the DOI metadata.

#### xml

The stored DataCite Metadata Schema XML encoded in Base64 format.

#### url

The landing page URL of the DOI.

#### contentUrl

An array of content URLs associated with the DOI.

#### metadataVersion

The version of the stored DataCite metadata, incremented once per update.

#### schemaVersion

The DataCite Metadata Schema version of the stored DOI metadata represented as a URL.

#### source

The system used to create the DOI. Values include:

| Value       | Source              |
| :---------- | :------------------ |
| mds         | MDS API             |
| api         | REST API            |
| fabricaForm | Fabrica Form        |
| fabrica     | Fabrica File Upload |
| ez          | EZ API              |

#### isActive

"true" if the DOI is in Findable state. Otherwise, "false".

#### state

The state of the DOI. Options are "findable", "registered", and "draft".

#### reason

Legacy attribute for EZID compatibility.

#### viewCount

Total views, pulled from Event Data.

#### downloadCount

Total downloads, pulled from Event Data.

#### referenceCount

Total references, pulled from Event Data.

#### citationCount

Total citations, pulled from Event Data.

#### partCount

Total number of parts, pulled from Event Data.

#### partOfCount

Total number of parents, pulled from Event Data.

#### versionCount

Total number of versions, pulled from Event Data.

#### versionOfCount

Total number to which this DOI is a version, pulled from Event Data.

#### created

Creation date of the DOI record in iso8601.

#### registered

Date the DOI was registered in iso8601.

#### published

The issued date or publication year.

#### updated

Date the DOI record was updated in iso8601.

#### relationships

A dictionary containing relationships to other PIDs and DataCite data objects.

##### relationships.client.data.id

The repository ID of the holding repository

##### relationships.client.data.type

Always "clients".

##### relationships.provider.data.id

The Member or Consortium Organization ID of the associated repository.

##### relationships.provider.data.type"

Always "providers".

##### relationships.media

Legacy attribute for media support. An array of media as dictionaries.

##### relationships.references

An array of references as dictionaries.

##### relationships.references.data.id

The identifier of the reference.

##### relationships.references.data.type

The type of the reference identifier. Always "dois".

##### relationships.citations

An array of citations as dictionaries.

##### relationships.citations.data.id

The identifier of the citation.

##### relationships.citations.data.type

The type of the citation identifier. Always "dois".

##### relationships.parts

An array of parts as dictionaries.

##### relationships.parts.data.id

The identifier of the part.

##### relationships.parts.data.type

The type of the part identifier. Always "dois".

##### relationships.partOf

An array of parents as dictionaries.

##### relationships.partOf.data.id

The identifier of the parent.

##### relationships.partOf.data.type

The type of the parent identifier. Always "dois".

##### relationships.versions

An array of versions as dictionaries.

##### relationships.versions.data.id

The identifier of the version.

##### relationships.versions.data.type

The type of the version identifier. Always "dois".

##### relationships.versionOf

An array of objects to which this DOI is a version as dictionaries.

##### relationships.versionOf.data.id

The identifier of the object to which this DOI is a version.

##### relationships.versionOf.data.type

The type of the object to which this DOI is a version. Always "dois".
