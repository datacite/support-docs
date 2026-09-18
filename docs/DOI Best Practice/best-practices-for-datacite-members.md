---
title: Best Practices for DOI Registration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    More detailed guides can be found in the Best Practices section of the
    support site.
  pages:
    - type: basic
      slug: doi-basics
      title: DOI Basics
---
## Overview

A DataCite Member/Consortium/Consortium Organization is an organization that has joined to DataCite in order  to register DataCite DOIs.

This document summarises some of the key best practices for DOI registration and management.

## What can a DataCite DOI be assigned to? 

DataCite Members and Consortium Organizations must follow the [DOI Registration Policy](doc:doi-registration-policy).

This policy specifies that:

1. An organization can only assign a DOI to content that their organization has responsibility for. DataCite expects all Members (and Consortium Organizations) to be active stewards of the content they are assigning DOIs to. This means they need to be able to update the content and metadata. It is not permissible to provide or resell DOIs to third parties.

2. DOIs should not be assigned to an identical version of the content if the same content is already published somewhere else with a DOI. You can assign a new DOI to an author-deposited manuscript, but this must not be the final published version. Please check copyright before assigning a DOI.

3. DOIs can be assigned to multiple types of research outputs. The [DataCite Metadata Schema](https://schema.datacite.org) must be suitable for describing these items.

4. DOIs must resolve to a publicly available [landing page](doc:landing-pages). The underlying content does not need to be publicly available, but the metadata must be open.

## Forming DOIs

A DOI consists of a numeric “prefix”  followed by a “suffix”. DataCite recommends using opaque suffixes that do not convey any semantic information. Our APIs allow the automatic creation of opaque suffixes using random strings.

More information: [What characters should I use in the suffix of my DOI? ](doc:what-characters-should-i-use-in-the-suffix-of-my-doi)

## Displaying DOIs

DOIs should be displayed as a full clickable URL of the form: `https://doi.org/10.7939/r3qz22k64`

DataCite DOIs should be displayed as the full URL when bibliographic information about content is displayed. DataCite encourages all Members to display DataCite DOIs on their Repository landing pages. We also recommend that DataCite DOIs be displayed or distributed anywhere users are directed to a permanent, stable, or persistent link to the content including:

- abstracts
- tables of contents
- full-text HTML and PDF articles, and other scholarly documents
- citation downloads to reference management systems
- metadata feeds to third parties
- “How to Cite This” instructions
- social media links

More information: [DataCite DOI Display Guidelines ](doc:datacite-doi-display-guidelines)

## Landing pages

1. DOIs should resolve to a landing page containing metadata about the item.
2. DOIs should not resolve directly to the content. 
3. The landing page should contain a full bibliographic citation. 
4. The DOI should be displayed on the landing page (so humans can read it). 
5. The DOI should be appropriately tagged (so that machines can read it). 
6. The landing page should provide a way to access the item.

More information: [Best Practices for DOI Landing Pages ](doc:landing-pages)

## Tombstone pages

A tombstone page should be created whenever the item a DOI describes is no longer available, for whatever reason. In general, however, it is better to avoid creating a situation in which a DOI's item is removed, if at all possible. This means being very careful not to accidentally create DOIs, or to put safeguards in place so that users of your service are not able to accidentally create DOIs.

1. In general, the guidelines for landing pages still apply, with the exception that it is not necessary for the user to be able to access the item from the landing page (since the item has been removed).
2. A statement of unavailability should be included that details the circumstances that led to the item’s removal.
3. DataCite DOIs that describe removed content should be updated to the “Registered” state so that they remain resolvable without being publicly indexed.
4. The DOI must be updated to change its associated URL to the URL of the tombstone page.

More information: [Best Practices for Tombstone Pages](doc:tombstone-pages)

## Versioning

The [DataCite Metadata Schema](https://schema.datacite.org) documentation recommends that a new DOI should be assigned when there is a new major version of the resource you are sharing. DataCite recommends adding a relatedIdentifier to each DOI with the relationType as follows:

- `HasVersion`: Indicates A has a version B. The registered resource such as a software package or code repository has a versioned instance (indicates A has the instance B). It may be used, e.g., to relate an un-versioned code repository to one of its specific software versions.
- `IsVersionOf`: Indicates A is a version of B. The registered resource is an instance of a target resource (indicates that A is an instance of B). It may be used, e.g., to relate a specific version of a software package to its software code repository.
- `IsPreviousVersionOf`:  Indicates A is a previous edition of B.
- `IsNewVersionOf`: Indicates A is a new edition of B, where the new edition has been modified or updated.

For minor versions, a new DOI may not be necessary. DOI metadata can be updated, which allows for correcting errors, adding additional files, or incrementing a minor version number.

More information: [Versioning](doc:versioning)

## DOI states

The DataCite APIs and DataCite Fabrica allow the creation of Draft records. Draft records are useful in cases where a user wants to “reserve” a DOI name for later use. We recommend reviewing our documentation on [DOI States](doc:doi-states), which covers the differences between the Findable, Registered, and Draft states. Unlike DOIs in Registered or Findable State, Draft records can be deleted and are not resolvable.
