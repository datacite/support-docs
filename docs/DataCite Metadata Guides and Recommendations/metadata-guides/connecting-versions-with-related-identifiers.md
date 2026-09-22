---
title: Connecting different versions, formats and more with Related Identifiers
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
When registering DOIs for closely related resources—such as different versions or formats of the same work—you can connect these resources in the metadata to support discovery and disambiguation. 

These examples demonstrate how to connect resources using the [RelatedIdentifier](https://datacite-metadata-schema.readthedocs.io/en/4/properties/relatedidentifier/) property in the DataCite Metadata Schema and select an accurate [relationType](https://datacite-metadata-schema.readthedocs.io/en/4/appendices/appendix-1/relationType/)  for the scenario. 

## Scenarios and relationType guidance

Each example demonstrates the relevant properties for the scenario and is not a complete XML/JSON record. For more information on the DataCite Metadata Schema, visit the [DataCite Metadata Schema website](https://schema.datacite.org).

### Content updates

For major content updates, a new DOI is registered for the new version of the resource. This forms a sequence of version-specific DOIs. 

Connect these DOIs to each other with the relationTypes `IsNewVersionOf ` and `IsPreviousVersionOf`.

##### Metadata for Version 1 DOI, connecting to Version 2 DOI

```xml XML
<identifier>10.21384/xc1g-pq90></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsPreviousVersionOf">10.21384/hcqn-2w70</relatedIdentifier>
</relatedIdentifiers>
<version>1</version>
```
```json JSON
{
  "doi": "10.21384/xc1g-pq90",
  "relatedIdentifiers": [
    {
      "relationType": "IsPreviousVersionOf",
      "relatedIdentifier": "10.21384/hcqn-2w70",
      "relatedIdentifierType": "DOI"
    }
  ],
  "version": 1
}
```

##### Metadata for Version 2 DOI, connecting to Version 1 DOI

```xml XML
<identifier>10.21384/hcqn-2w70></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.21384/xc1g-pq90</relatedIdentifier>
</relatedIdentifiers>
<version>2</version>
```
```json JSON
{
  "doi": "10.21384/hcqn-2w70",
  "relatedIdentifiers": [
    {
      "relationType": "IsNewVersionOf",
      "relatedIdentifier": "10.21384/xc1g-pq90",
      "relatedIdentifierType": "DOI"
    }
  ],
  "version": 2
}
```

Some systems create a “canonical” DOI that represents all versions of a work. connecting the version-specific DOIs to the canonical DOI. 

Connect the version-specific DOIs to the canonical DOI with the relationType `IsVersionOf`, and the canonical DOI to each version-specific DOI with the relationType `HasVersion`. For more information on this use case, see  [Versioning](doc:versioning) .

##### Metadata for canonical DOI, connecting to Version 1 and Version 2 DOIs

```xml XML
<identifier>10.21384/p91r-jy42></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="HasVersion">10.21384/xc1g-pq90</relatedIdentifier>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="HasVersion">10.21384/hcqn-2w70</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/p91r-jy42",
  "relatedIdentifiers": [
    {
      "relationType": "HasVersion",
      "relatedIdentifier": "10.21384/xc1g-pq90",
      "relatedIdentifierType": "DOI"
    },
    {
      "relationType": "HasVersion",
      "relatedIdentifier": "10.21384/hcqn-2w70",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

##### Metadata for Version 1 DOI, connecting to Version 2 DOI and canonical DOI

```xml XML
<identifier>10.21384/xc1g-pq90></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsPreviousVersionOf">10.21384/hcqn-2w70</relatedIdentifier>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsVersionOf">10.21384/p91r-jy42</relatedIdentifier>
</relatedIdentifiers>
<version>1</version>
```
```json JSON
{
  "doi": "10.21384/xc1g-pq90",
  "relatedIdentifiers": [
    {
      "relationType": "IsPreviousVersionOf",
      "relatedIdentifier": "10.21384/hcqn-2w70",
      "relatedIdentifierType": "DOI"
    },
    {
      "relationType": "IsVersionOf",
      "relatedIdentifier": "10.21384/p91r-jy42",
      "relatedIdentifierType": "DOI"
    }
  ],
  "version": 1
}
```

##### Metadata for Version 2 DOI, connecting to Version 1 DOI and canonical DOI

```xml XML
<identifier>10.21384/hcqn-2w70></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.21384/xc1g-pq90</relatedIdentifier>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsVersionOf">10.21384/p91r-jy42</relatedIdentifier>
</relatedIdentifiers>
<version>2</version>
```
```json JSON
{
  "doi": "10.21384/hcqn-2w70",
  "relatedIdentifiers": [
    {
      "relationType": "IsNewVersionOf",
      "relatedIdentifier": "10.21384/xc1g-pq90",
      "relatedIdentifierType": "DOI"
    },
    {
      "relationType": "IsVersionOf",
      "relatedIdentifier": "10.21384/p91r-jy42",
      "relatedIdentifierType": "DOI"
    }
  ],
  "version": 2
}
```

### Corrections

When content is corrected, a new DOI may be registered for the corrected version. When the original version should not be used, connect these DOIs to each other with the relationTypes `IsObsoletedBy` and `Obsoletes`.

##### Metadata for obsoleted version DOI, connecting to corrected version DOI

```xml XML
<identifier>10.21384/2vrr-db19></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsObsoletedBy">10.21384/d80j-c329</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/2vrr-db19",
  "relatedIdentifiers": [
    {
      "relationType": "IsObsoletedBy",
      "relatedIdentifier": "10.21384/d80j-c329",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

##### Metadata for corrected version DOI, connecting to obsoleted version DOI

```xml XML
<identifier>10.21384/d80j-c329></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="Obsoletes">10.213842/2vrr-db19</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/d80j-c329",
  "relatedIdentifiers": [
    {
      "relationType": "Obsoletes",
      "relatedIdentifier": "10.21384/2vrr-db19",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

### Release or publication stages

A preprint, an accepted manuscript (also known as a "postprint"), and the version of record each represent different stages of the publication process. These are typically made available in different systems (e.g., preprint servers, institutional repositories, and journal publishing platforms) with separate DOIs.

When a version of record is available, connect preprints and accepted manuscripts to the version of record using the relationType `IsVersionOf`.  Connect the version of record to any associated preprints or accepted manuscripts using the reciprocal relationType `HasVersion`.

##### Metadata for a preprint, connecting to the version of record

```xml XML
<identifier>10.21384/cgkg-j274></identifier>
<resourceType resourceTypeGeneral="Preprint"/>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsVersionOf">10.213842/pddx-xy13</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/cgkg-j274",
  "relatedIdentifiers": [
    {
      "relationType": "IsVersionOf",
      "relatedIdentifier": "10.21384/pddx-xy13",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

##### Metadata for the version of record, connecting to the preprint

```xml XML
<identifier>10.21384/pddx-xy13></identifier>
<resourceType resourceTypeGeneral="JournalArticle"/>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="HasVersion">10.213842/cgkg-j274</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/pddx-xy13",
  "relatedIdentifiers": [
    {
      "relationType": "HasVersion",
      "relatedIdentifier": "10.21384/cgkg-j274",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

##### Metadata for an accepted manuscript (postprint), connecting to the version of record

```xml XML
<identifier>10.21384/0557-d709></identifier>
<resourceType resourceTypeGeneral="JournalArticle">Postprint</resourceType>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsVersionOf">10.213842/10.213842/pddx-xy13</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/0557-d709",
  "relatedIdentifiers": [
    {
      "relationType": "IsVersionOf",
      "relatedIdentifier": "10.21384/pddx-xy13",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```

### Different formats

Some repositories may register separate DOIs for different formats or presentations of the same content. In this example, a CSV file is also available in JSON format.

Connect DOIs for different formats or presentations of the same resource with the relationTypes `IsOriginalFormOf` and `IsVariantFormOf`. If both formats originated at the same time, you can use `IsVariantFormOf` in both directions.

##### Metadata for CSV format version

```xml XML
<identifier>10.21384/zkap-qb12></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsOriginalFormOf">10.213842/xzyg-y712</relatedIdentifier>
</relatedIdentifiers>
<formats>
	<format>text/csv</format>
</formats>
```
```json JSON
{
  "doi": "10.21384/zkap-qb12",
  "relatedIdentifiers": [
    {
      "relationType": "IsOriginalFormOf",
      "relatedIdentifier": "10.21384/xzyg-y712",
      "relatedIdentifierType": "DOI"
    }
  ],
  "formats": [
    "text/csv"
  ]
}
```

##### Metadata for JSON format version

```xml XML
<identifier>10.21384/xzyg-y712></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsVariantFormOf">10.213842/zkap-qb12</relatedIdentifier>
</relatedIdentifiers>
<formats>
	<format>application/json</format>
</formats>
```
```json JSON
{
  "doi": "10.21384/xzyg-y712",
  "relatedIdentifiers": [
    {
      "relationType": "IsVariantFormOf",
      "relatedIdentifier": "10.21384/zkap-qb12",
      "relatedIdentifierType": "DOI"
    }
  ],
  "formats": [
    "application/json"
  ]
}
```

### Translations

Connect translations to the original work with the relationType `IsTranslationOf`, and the original work to its translations with the relationType `HasTranslation`. If multiple languages originated at the same time, use `HasTranslation` to connect the works to each other in both directions.

##### Metadata for the translation

```xml XML
<identifier identifierType="DOI">10.82433/45e5-xy14</identifier>
<creators>
   <creator>
      <creatorName nameType="Personal">Green, Simon</creatorName>
   </creator>
</creators>
<titles>
   <title xml:lang="en">Climate Change and Adaptation Strategies</title>
</titles>
<publisher>Institute for Environmental Research</publisher>
<publicationYear>2024</publicationYear>
<dates>
   <date dateType="Issued">2024-09-15</date>
</dates>
<resourceType resourceTypeGeneral="Report"/>
<language>en</language>
<contributors>
   <contributor contributorType="Translator">
      <contributorName nameType="Personal">Schneider, Anna</contributorName>
   </contributor>
</contributors>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsTranslationOf">10.82433/pma6-nf93</relatedIdentifier>
</relatedIdentifiers>
<descriptions>
   <description xml:lang="en" descriptionType="Abstract">This report examines the impacts of climate change and explores potential adaptation strategies. It addresses issues such as extreme weather events, adaptation measures for urban and rural areas, and policy recommendations to mitigate climate risks.</description>
</descriptions>
```
```json JSON
{
  "doi": "10.82433/45e5-xy14",
  "creators": [
    {
      "name": "Green, Simon",
      "nameType": "Personal"
    }
  ],
  "titles": [
    {
      "lang": "en",
      "title": "Climate Change and Adaptation Strategies"
    }
  ],
  "publisher": {
    "name": "Institute for Environmental Research"
  },
  "publicationYear": 2024,
  "contributors": [
    {
      "name": "Schneider, Anna",
      "nameType": "Personal",
      "contributorType": "Translator",
    }
  ],
  "dates": [
    {
      "date": "2024-09-15",
      "dateType": "Issued"
    }
  ],
  "language": "en",
  "types": {
    "resourceTypeGeneral": "Report"
  },
  "relatedIdentifiers": [
    {
      "relationType": "IsTranslationOf",
      "relatedIdentifier": "10.82433/pma6-nf93",
      "relatedIdentifierType": "DOI"
    }
  ],
  "descriptions": [
    {
      "lang": "en",
      "description": "This report examines the impacts of climate change and explores potential adaptation strategies. It addresses issues such as extreme weather events, adaptation measures for urban and rural areas, and policy recommendations to mitigate climate risks.",
      "descriptionType": "Abstract"
    }
  ]
}
```

##### Metadata for the original work (which has been translated)

```xml XML
<identifier identifierType="DOI">10.82433/pma6-nf93</identifier>
<creators>
   <creator>
      <creatorName nameType="Personal">Green, Simon</creatorName>
   </creator>
</creators>
<titles>
   <title xml:lang="de">Klimawandel und Anpassungsstrategien</title>
</titles>
<publisher>Institut für Umweltforschung</publisher>
<publicationYear>2022</publicationYear>
<dates>
   <date dateType="Issued">2022-07-07</date>
</dates>
<resourceType resourceTypeGeneral="Report"/>
<language>de</language>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="HasTranslation">10.82433/45e5-xy14</relatedIdentifier>
</relatedIdentifiers>
<descriptions>
   <description xml:lang="de" descriptionType="Abstract">Dieser Bericht untersucht die Auswirkungen des Klimawandels und erkundet mögliche Anpassungsstrategien. Er befasst sich mit Themen wie extremen Wetterereignissen, Anpassungsmaßnahmen für städtische und ländliche Gebiete und politischen Empfehlungen zur Minderung von Klimarisiken.</description>
</descriptions>
```
```json JSON
{
  "doi": "10.82433/pma6-nf93",
  "creators": [
    {
      "name": "Green, Simon"
    }
  ],
  "titles": [
    {
      "lang": "de",
      "title": "Klimawandel und Anpassungsstrategien"
    }
  ],
  "publisher": {
    "name": "Institut für Umweltforschung"
  },
  "publicationYear": 2022,
  "dates": [
    {
      "date": "2022-07-07",
      "dateType": "Issued"
    }
  ],
  "language": "de",
  "types": {
    "resourceTypeGeneral": "Report"
  },
  "relatedIdentifiers": [
    {
      "relationType": "HasTranslation",
      "relatedIdentifier": "10.82433/45e5-xy14",
      "relatedIdentifierType": "DOI"
    }
  ],
  "descriptions": [
    {
      "lang": "de",
      "description": "Dieser Bericht untersucht die Auswirkungen des Klimawandels und erkundet mögliche Anpassungsstrategien. Er befasst sich mit Themen wie extremen Wetterereignissen, Anpassungsmaßnahmen für städtische und ländliche Gebiete und politischen Empfehlungen zur Minderung von Klimarisiken.",
      "descriptionType": "Abstract"
    }
  ]
}
```

### Identical content published in multiple locations

> 📘 Policy on DOIs for identical content
> 
> The DataCite [DOI Registration Policy](doc:doi-registration-policy) states that you should not assign a DOI to an identical version of the content if the same content is already published somewhere else with a DOI.

Separate DOIs are sometimes created for the same content in different locations, where each DOI resolves to a different location. 

When this occurs, the metadata of both DOIs can be updated to indicate that there is an identical copy of the resource with the relationType `IsIdenticalTo`. 

To retract the duplicate DOI, follow the steps here: [What if a DOI is created by mistake or the content is retracted?](doc:doi-persistence#what-if-a-doi-is-created-by-mistake-or-the-content-is-retracted)

##### Metadata for a DOI where the identical content was published elsewhere

```xml XML
<identifier>10.21384/dbvb-9c15></identifier>
<relatedIdentifiers>
   <relatedIdentifier relatedIdentifierType="DOI" relationType="IsIdenticalTo">10.213842/sdez-dt48</relatedIdentifier>
</relatedIdentifiers>
```
```json JSON
{
  "doi": "10.21384/dbvb-9c15",
  "relatedIdentifiers": [
    {
      "relationType": "IsIdenticalTo",
      "relatedIdentifier": "10.21384/sdez-dt48",
      "relatedIdentifierType": "DOI"
    }
  ]
}
```