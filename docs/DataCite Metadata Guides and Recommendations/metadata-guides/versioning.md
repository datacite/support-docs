---
title: Versioning
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
When content underlying a DOI is updated, we recommend updating the DOI metadata and, for major changes, assigning a new DOI.

- For minor content changes, the same DOI may be used with updated metadata. A new DOI is not required.
- For major content changes, we recommend assigning a new DOI and linking the new DOI to the previous DOI with related identifiers.

Individual stewards may determine which are major vs. minor versions.

## Minor versions: Update DOI metadata

For minor content changes, a new version may be represented with the Version property of the DataCite Metadata Schema. This allows you to indicate what version of the resource is being described. For each minor version, increment the version number. For example:

 `<version>1.1</version>`

Metadata changes are captured in the activities endpoint of the REST API. For more information, see [Tracking metadata provenance](doc:tracking-provenance).

## Major versions: Register a new DOI and add related identifiers

We recommend assigning a new DOI when there is a new major version of the resource. When creating a DOI for a new version, use the RelatedIdentifier property to create links between versions.

There are two relationType pairs that are used for versions. The following definitions are from the [DataCite Metadata Schema](https://schema.datacite.org/) documentation:

### `IsPreviousVersionOf` and `IsNewVersionOf`

- `IsPreviousVersionOf`:  Indicates A is a previous edition of B.
- `IsNewVersionOf`: Indicates A is a new edition of B, where the new edition has been modified or updated.

### `HasVersion` and `IsVersionOf`

- `HasVersion`: Indicates A has a version B. The registered resource such as a software package or code repository has a versioned instance (indicates A has the instance B). It may be used, e.g., to relate an un-versioned code repository to one of its specific software versions.
- `IsVersionOf`: Indicates A is a version of B. The registered resource is an instance of a target resource (indicates that A is an instance of B). It may be used, e.g., to relate a specific version of a software package to its software code repository.

These relationTypes can be used together or separately.

### Linking versions in a sequence

When one version supersedes another, use RelatedIdentifiers with the relationTypes IsNewVersionOf and IsPreviousVersionOf.

- _Existing DOI:_ Update metadata for the earlier version to add a RelatedIdentifier with relationType `IsPreviousVersionOf`, linking to the newer version.
- _New DOI:_ Add a RelatedIdentifier with relationType `IsNewVersionOf`, linking to the previous version.

### Linking a resource to specific versions

In some cases, when there are multiple versions, a DOI may be assigned to represent all versions of a resource. This is sometimes called a “canonical DOI”.

When a resource has both a canonical DOI and specific versions, use RelatedIdentifiers with the relationTypes HasVersion and IsVersionOf.

- _Canonical DOI:_ Add a RelatedIdentifier with relationType `HasVersion` for each specific version of the resource.
- _Specific versions:_ Add a RelatedIdentifier with relationType `IsVersionOf`, linking to the canonical DOI.

We recommend only assigning a “canonical DOI” when there are multiple versions that need to be represented as a group.

### Examples

#### Resource with two versions

A resource has two versions: version 1 (`10.21384/ej3g-gm03`) and version 2 (`10.21384/q8ry-e810`).

[block:parameters]
{
  "data": {
    "h-0": "Metadata",
    "h-1": " Version 1 (10.21384/ej3g-gm03)",
    "h-2": "Version 2 (10.21384/q8ry-e810)",
    "0-0": "RelatedIdentifiers",
    "0-1": "`<relatedIdentifiers>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"IsPreviousVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/q8ry-e810</relatedIdentifier>`  \n  \n`</relatedIdentifiers>`",
    "0-2": "`<relatedIdentifiers>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"IsNewVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/ej3g-gm03</relatedIdentifier>`  \n  \n`</relatedIdentifiers>`",
    "1-0": "Version",
    "1-1": "`<version>1</version>`",
    "1-2": "`<version>2</version>`"
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


#### Resource with two versions and a canonical DOI

As in the previous example, a resource has two versions: version 1 (`10.21384/ej3g-gm03`) and version 2 (`10.21384/q8ry-e810`). There is also a canonical DOI (`10.21384/2t02-sq50`), representing all versions.

[block:parameters]
{
  "data": {
    "h-0": "Metadata",
    "h-1": "Canonical DOI  \n(10.21384/2t02-sq50)",
    "h-2": "Version 1 (10.21384/ej3g-gm03)",
    "h-3": "Version 2 (10.21384/q8ry-e810)",
    "0-0": "RelatedIdentifiers",
    "0-1": "`<relatedIdentifiers>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"HasVersion\" resourceTypeGeneral=\"Dataset\">10.21384/ej3g-gm03</relatedIdentifier>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"HasVersion\" resourceTypeGeneral=\"Dataset\">10.21384/q8ry-e810</relatedIdentifier>`  \n  \n`</relatedIdentifiers>`",
    "0-2": "`<relatedIdentifiers>`  \n  \n`<relatedIdentifierType=\"DOI\" relationType=\"IsVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/2t02-sq50</relatedIdentifier>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"IsPreviousVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/q8ry-e810</relatedIdentifier>`  \n  \n`</relatedIdentifiers>`",
    "0-3": "`<relatedIdentifiers>`  \n  \n`<relatedIdentifierType=\"DOI\" relationType=\"IsVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/2t02-sq50</relatedIdentifier>`  \n  \n`<relatedIdentifier relatedIdentifierType=\"DOI\" relationType=\"IsNewVersionOf\" resourceTypeGeneral=\"Dataset\">10.21384/ej3g-gm03</relatedIdentifier>`  \n  \n`</relatedIdentifiers>`",
    "1-0": "Version",
    "1-1": "n/a",
    "1-2": "`<version>1</version>`",
    "1-3": "`<version>2</version>`"
  },
  "cols": 4,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


## Resources

- The [RDA Data Versioning Interest Group](https://www.rd-alliance.org/groups/data-versioning-ig/outputs/) has documented data versioning best practices and use cases.
- Further guidance is available on Versioning, Data Granularity and Complex Data Citation Practices in the [User guidelines on EOSC PID implementation](https://zenodo.org/records/15081434).
- The DataCite Metadata Schema includes some recommendations for the [Citation of Dynamic Datasets](https://datacite-metadata-schema.readthedocs.io/en/4.6/guidance/dynamic-datasets/).