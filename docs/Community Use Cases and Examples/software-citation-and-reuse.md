---
title: Software Citation and Reuse
deprecated: false
hidden: false
metadata:
  robots: index
---
nameIdentifier
Creators of, or contributors to the software
ORCID iDs (for individuals), ROR IDs (for organizations)As a DataCite member, you can assign DataCite DOIs and metadata to research software shared by your organization. This is important to increase visibility and discoverability of research software, ensure it aligns with the FAIR (Findable, Accessible, Interoperable, Reusable) principles, and can be cited in publications. The DataCite Metadata Schema defines Software as:

<br />

a computer program other than a computational notebook, in either source code (text) or compiled form. Use this type for general software components supporting scholarly research.
To register a DOI for software, you must use the resourceTypeGeneral: Software.
Below is an example of the XML metadata for a Software DOI: <resourceType resourceTypeGeneral="Software">Simulation tool</resourceType>

Metadata for Software DOIs
To support discovery, reuse, and accurate attribution, software DOIs should be registered with rich, structured metadata according to the DataCite Metadata Schema. This metadata is made openly available and can be retrieved in downstream services and search engines.
Connection metadata establishes links between software and other entities across the research ecosystem. Include persistent identifiers (PIDs) like ORCID iDs and ROR IDs in the relevant DataCite metadata properties to connect software to researchers, research organizations, and funders.

<br />

| Metadata Property:    | Connecting to:                                                                                              | Recommended PIDs / Identifiers:                          |
| --------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| relatedIdentifier     | Related research outputs like journal articles that cite the software                                       | DOIs, URLs, Handles                                      |
| nameIdentifier        | Creators of, or contributors to the software                                                                | ORCID iDs (for individuals), ROR IDs (for organizations) |
| affiliationIdentifier | Organizational affiliations of the creators and contributors                                                | ROR IDs                                                  |
| funderIdentifier      | Uniquely identifies the entity that funded the software development                                         | ROR IDs                                                  |
| publisherIdentifier   | The entity that holds, archives, publishes, prints, distributes, releases, issues, or produces the resource | ROR IDs                                                  |
