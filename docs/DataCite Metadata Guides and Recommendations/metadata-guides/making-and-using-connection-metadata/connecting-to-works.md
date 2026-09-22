---
title: Connecting to Works
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: connecting-to-people
      title: Connecting to People
---
## Related identifiers

The DataCite Metadata Schema includes a `RelatedIdentifier` property to facilitate links to related research outputs. 

The relatedIdentifier property has a mandatory attribute, `relationType`, which is used to describe the type of relationship. All relationTypes in the DataCite Metadata Schema are listed below ([Summary of all relationTypes](#summary-of-all-relationtypes)).

Specific use cases are highlighted below.

## Citations and references

Citations and references can be provided through the relatedIdentifier property with specific relationTypes:

- _Citations_ use the relationTypes **IsCitedBy**, **IsReferencedBy**, and **IsSupplementTo**.
- _References_ use the relationTypes **Cites**, **References**, and **IsSupplementedBy**.

For more information, see the [Citations and References](doc:citations-and-references) section of the documentation, including:

- [Contributing Citations and References](doc:contributing-citations-and-references)
- [Consuming Citations and References](doc:consuming-citations-and-references)

## Parts and versions

Whole/part relationships can be represented using related identifiers with the relationTypes **HasPart** and **IsPartOf**.

Version relationships can be represented using related identifiers with the relationTypes **HasVersion** and **IsVersionOf**. When one version supersedes another, use the pair IsNewVersionOf and IsPreviousVersionOf. For more information on versioning, see [Versioning](doc:versioning). 

Information about parts and versions is exposed in the “relationships” section of the DataCite REST API. 

## Summary of all relationTypes

[block:parameters]
{
  "data": {
    "h-0": "relationType",
    "h-1": "Interpretation",
    "h-2": "Equivalent to",
    "h-3": "Event Data Interpretation",
    "0-0": "IsCitedBy",
    "0-1": "A is cited by B",
    "0-2": "B cites A",
    "0-3": "_Citation_ for A  \n_Reference_ for B",
    "1-0": "Cites",
    "1-1": "A cites B",
    "1-2": "B is cited by A",
    "1-3": "_Reference_ for A  \n_Citation_ for B",
    "2-0": "IsReferencedBy",
    "2-1": "A is referenced by B",
    "2-2": "B references A",
    "2-3": "_Citation_ for A  \n_Reference_ for B",
    "3-0": "References",
    "3-1": "A references B",
    "3-2": "B is referenced by A",
    "3-3": "_Reference_ for A  \n_Citation_ for B",
    "4-0": "IsSupplementTo",
    "4-1": "A is supplement to B",
    "4-2": "B is supplemented by A",
    "4-3": "_Citation_ for A  \n_Reference_ for B",
    "5-0": "IsSupplementedBy",
    "5-1": "A is supplemented by B",
    "5-2": "B is supplement to A",
    "5-3": "_Reference_ for A  \n_Citation_ for B",
    "6-0": "IsPartOf",
    "6-1": "A is part of B",
    "6-2": "B has part A",
    "6-3": "_PartOf_ for A  \n_Parts_ for B",
    "7-0": "HasPart",
    "7-1": "A has part B",
    "7-2": "A is part of B",
    "7-3": "_Parts_ for A  \n_PartOf_ for B",
    "8-0": "HasVersion",
    "8-1": "A has version B",
    "8-2": "B is version of A",
    "8-3": "_Versions_ for A  \n_VersionOf_ for B",
    "9-0": "IsVersionOf",
    "9-1": "A is version of B",
    "9-2": "B has version A",
    "9-3": "_VersionOf_ for A  \n_Versions_ for B",
    "10-0": "IsContinuedBy",
    "10-1": "A is continued by B",
    "10-2": "B continues A",
    "10-3": "n/a",
    "11-0": "Continues",
    "11-1": "A continues B",
    "11-2": "B is continued by A",
    "11-3": "n/a",
    "12-0": "IsDescribedBy",
    "12-1": "A is described by B",
    "12-2": "B describes A",
    "12-3": "n/a",
    "13-0": "Describes",
    "13-1": "A describes B",
    "13-2": "B is described by A",
    "13-3": "n/a",
    "14-0": "HasMetadata",
    "14-1": "A has metadata B",
    "14-2": "B is metadata for A",
    "14-3": "n/a",
    "15-0": "IsMetadataFor",
    "15-1": "A is metadata for B",
    "15-2": "B has metadata A",
    "15-3": "n/a",
    "16-0": "IsNewVersionOf",
    "16-1": "A is new version of B",
    "16-2": "B is previous version of A",
    "16-3": "n/a",
    "17-0": "IsPreviousVersionOf",
    "17-1": "A is previous version of B",
    "17-2": "B is new version of A",
    "17-3": "n/a",
    "18-0": "IsDocumentedBy",
    "18-1": "A is documented by B",
    "18-2": "B documents A",
    "18-3": "n/a",
    "19-0": "Documents",
    "19-1": "A documents B",
    "19-2": "B is documented by B",
    "19-3": "n/a",
    "20-0": "IsCompiledBy",
    "20-1": "A is compiled by B",
    "20-2": "B compiles A",
    "20-3": "n/a",
    "21-0": "Compiles",
    "21-1": "A compiles B",
    "21-2": "B is compiled by A",
    "21-3": "n/a",
    "22-0": "IsVariantFormOf",
    "22-1": "A is variant form of B",
    "22-2": "B is original form of A",
    "22-3": "n/a",
    "23-0": "IsOriginalFormOf",
    "23-1": "A is original form of B",
    "23-2": "B is variant form of A",
    "23-3": "n/a",
    "24-0": "IsReviewedBy",
    "24-1": "A is reviewed by B",
    "24-2": "B reviews A",
    "24-3": "n/a",
    "25-0": "Reviews",
    "25-1": "A reviews B",
    "25-2": "B is reviewed by A",
    "25-3": "n/a",
    "26-0": "IsDerivedFrom",
    "26-1": "A is derived from B",
    "26-2": "B is source of A",
    "26-3": "n/a",
    "27-0": "IsSourceOf",
    "27-1": "A is source of B",
    "27-2": "B is derived from A",
    "27-3": "n/a",
    "28-0": "IsRequiredBy",
    "28-1": "A is required by B",
    "28-2": "B requires A",
    "28-3": "n/a",
    "29-0": "Requires",
    "29-1": "A requires B",
    "29-2": "B is required by A",
    "29-3": "n/a",
    "30-0": "IsObsoletedBy",
    "30-1": "A is obsoleted by B",
    "30-2": "B obsoletes A",
    "30-3": "n/a",
    "31-0": "Obsoletes",
    "31-1": "A obsoletes B",
    "31-2": "B is obsoleted by A",
    "31-3": "n/a",
    "32-0": "IsPublishedIn",
    "32-1": "A is published in B",
    "32-2": "n/a",
    "32-3": "n/a",
    "33-0": "IsIdenticalTo",
    "33-1": "A is identical to B",
    "33-2": "B is identical to A",
    "33-3": "n/a",
    "34-0": "IsCollectedBy",
    "34-1": "A is collected by B",
    "34-2": "B collects A",
    "34-3": "n/a",
    "35-0": "Collects",
    "35-1": "A collects B",
    "35-2": "B is collected by A",
    "35-3": "n/a",
    "36-0": "IsTranslationOf",
    "36-1": "A is translation of B",
    "36-2": "B has translation A",
    "36-3": "n/a",
    "37-0": "HasTranslation",
    "37-1": "A has translation B",
    "37-2": "B is translation of A",
    "37-3": "n/a",
    "38-0": "Other",
    "38-1": "A is related to B and the relationship does not fit into an existing category",
    "38-2": "n/a",
    "38-3": "n/a"
  },
  "cols": 4,
  "rows": 39,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


For more information and usage examples for relationTypes, see the [DataCite Metadata Schema](https://schema.datacite.org/) documentation.