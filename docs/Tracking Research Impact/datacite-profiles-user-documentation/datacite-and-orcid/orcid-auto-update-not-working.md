---
title: ORCID Auto-Update Troubleshooting Guide
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
For information about how to enable ORCID auto-update, see our [guide on how to activate ORCID auto-update](doc:datacite-and-orcid#2-orcid-auto-update) .

If everything is set up correctly but auto-update is not working as expected, then there are a few things you can check.

## The date auto-update was enabled

Auto-update will only trigger for [findable](doc:doi-states#findable-dois) DOIs registered or updated **after** the user enables the auto-update token. To trigger ORCID auto-update for existing DOIs (registered before the token was enabled), you can add the DOIs [using DataCite Commons](doc:orcid-claiming). You can also make an update to one of the following metadata fields:

- Creator
- RelatedIdentifier
- FundingReference

## Invalid token

Some claims may not work if permission has been revoked in your ORCID settings and the token that DataCite has is no longer valid. To fix this you can:

1. Check the third party permission settings in your ORCID record. 
2. Log into [DataCite Profiles](https://profiles.datacite.org/) to delete the token and then authorize a new one.

## Contributors

ORCID auto update claiming only works if your ORCID iD is included in the "creators" field in the DOI metadata. If your ORCID iD is only included in the "contributors" metadata field of the DOI, then this won't be picked up by ORCID auto-update. 

In the DataCite Metadata Schema, the contributor has a much broader meaning than author/creator. If users claim works as a "contributor," it may appear that they actually authored the work.

## Parts

If a DOI record contains a RelatedIdentifier with relationType "IsPartOf" in its metadata, it will not be picked up by  ORCID auto-update. This filter avoids pushing many component parts of a single work; for example, many files within a dataset. Only the DOI representing the "parent" or "whole" is pushed via auto-update.

> 👍 
> 
> You can still add part DOIs to your ORCID record using [ORCID's "Import works from other services" tool](doc:datacite-and-orcid#1-orcid-import-works-from-other-services) or [DataCite Commons](doc:datacite-and-orcid#adding-a-work-to-your-orcid-record).

## Versions

If a DOI record contains RelatedIdentifier metadata connecting it to other versions of the same resource, the connected works will be grouped together in your ORCID record. This will occur when DOI metadata contains a RelatedIdentifier for a DOI (relatedIdentifierType “DOI”) with one the following relationTypes: “IsVersionOf”, “HasVersion”, “IsNewVersionOf”, “IsPreviousVersionOf”, or “IsIdenticalTo”. The targeted DOI must also be represented in your ORCID record.

You can manage grouped works in your ORCID record. See [ORCID's documentation about grouped works](https://support.orcid.org/hc/en-us/articles/360006894774-Group-multiple-versions-of-the-same-work-together) for more information.

If none of the above helps, please contact DataCite support [support@datacite.org](mailto:support@datacite.org)
