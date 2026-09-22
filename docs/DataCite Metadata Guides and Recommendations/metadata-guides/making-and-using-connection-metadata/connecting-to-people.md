---
title: Connecting to People
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
      slug: connecting-to-organizations
      title: Connecting to Organizations
---
The creator and contributor properties can be used to attribute credit to related individuals. Both properties have a nameIdentifier sub-property.

Including identifiers (e.g. ORCID iDs) in the nameIdentifier property helps to create connections between people and works. This enables services including [DataCite Researcher Profiles](doc:datacite-researcher-profiles) (People search in DataCite Commons) and [ORCID auto-update](doc:how-to-activate-orcid-auto-update). 

[ORCID Claiming](doc:orcid-claiming) can also be used if a researcher wants to claim a work that does not include their ORCID iD in the DOI metadata. 

For individual creators and contributors, users are also encouraged to include the familyName and givenName sub-properties when available.

## Examples

Creator with nameIdentifier:

```xml
<creator>
  <creatorName nameType="Personal">Garcia, Sofia</creatorName>
  <givenName>Sofia</givenName>
  <familyName>Garcia</familyName>
  <nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0000-0001-5727-2427</nameIdentifier>
  <affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiiationIdentifierScheme="ROR" SchemeURI="https://ror.org">Arizona State University</affiliation>
</creator>
```

Contributor with nameIdentifier:

```xml
<contributor contributorType="DataCollector">
  <contributorName nameType="Personal">Carberry, Josiah</contributorName>
  <givenName>Josiah</givenName>
  <familyName>Carberry</familyName>
  <nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0000-0002-1825-0097</nameIdentifier>
  <affiliation affiliationIdentifier="https://ror.org/05gq02987" affiiationIdentifierScheme="ROR" SchemeURI="https://ror.org">Brown University</affiliation>
</contributor>
```