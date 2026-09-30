---
title: Software Citation and Reuse
deprecated: false
hidden: false
metadata:
  robots: index
---
As a DataCite member, you can assign DataCite DOIs and metadata to research software shared by your organization. This is important to increase visibility and discoverability of research software, ensure it aligns with the [FAIR (Findable, Accessible, Interoperable, Reusable)](https://doi.org/10.1038/sdata.2016.18) principles, and can be cited in publications. The [DataCite Metadata Schema](https://schema.datacite.org/) defines [Software](https://datacite-metadata-schema.readthedocs.io/en/4.7/appendices/appendix-1/resourceTypeGeneral/#software) as:

_a computer program other than a computational notebook, in either source code (text) or compiled form. Use this type for general software components supporting scholarly research._<br /><br />To register a DOI for software, you must use the resourceTypeGeneral: **Software**. Below is an example of the XML metadata for a Software DOI:&#x20;


```text xml
<resourceType resourceTypeGeneral="Software">Simulation tool</resourceType>
```

<br />##Metadata for Software DOIs<br /><br />To support discovery, reuse, and accurate attribution, software DOIs should be registered with rich, structured metadata according to the [DataCite Metadata Schema](https://schema.datacite.org/). This metadata is made openly available and can be retrieved in downstream services and search engines.<br />
Connection metadata establishes links between software and other entities across the research ecosystem. Include persistent identifiers (PIDs) like [ORCID iDs](https://orcid.org/) and[ ROR IDs](https://ror.org/) in the relevant DataCite metadata properties to connect software to researchers, research organizations, and funders.

<br />

| Metadata Property:    | Connecting to:                                                                                              | Recommended PIDs / Identifiers:                          |
| --------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| relatedIdentifier     | Related research outputs like journal articles that cite the software                                       | DOIs, URLs, Handles                                      |
| nameIdentifier        | Creators of, or contributors to the software                                                                | ORCID iDs (for individuals), ROR IDs (for organizations) |
| affiliationIdentifier | Organizational affiliations of the creators and contributors                                                | ROR IDs                                                  |
| funderIdentifier      | Uniquely identifies the entity that funded the software development                                         | ROR IDs                                                  |
| publisherIdentifier   | The entity that holds, archives, publishes, prints, distributes, releases, issues, or produces the resource | ROR IDs                                                  |

\##RelatedIdentifiers<br /><br />The [relatedIdentifier](https://datacite-metadata-schema.readthedocs.io/en/4.7/properties/relatedidentifier/#) property connects the primary DOI to another identifier, e.g a Software DOI and the DOI of a publication that cites it. Apply the appropriate [relationType](https://datacite-metadata-schema.readthedocs.io/en/4.7/properties/relatedidentifier/#b) to the Software DOI to manage [versions](https://support.datacite.org/docs/versioning), allocate [citations](https://support.datacite.org/docs/citations-and-references), and more.

Example: relatedIdentifier metadata for a Software DOI connecting with [IsCitedBy](https://datacite-metadata-schema.readthedocs.io/en/4.7/appendices/appendix-1/relationType/#iscitedby) and [Compiles](https://datacite-metadata-schema.readthedocs.io/en/4.7/appendices/appendix-1/relationType/#compiles) relationTypes:

```text xml
<relatedIdentifiers>
  <relatedIdentifier relatedIdentifierType="DOI" relationType="IsCitedBy">10.1038/s41597-022-01710-x</relatedIdentifier>
    <relatedIdentifier relatedIdentifierType="DOI" relationType="Compiles">10.5281/zenodo.1234567</relatedIdentifier>
</relatedIdentifiers>
```

<br />

\###Further reading:<br /><br />Blog Post: Levchenko, M., Fiedler, M., Knodel, O., & Pape, D. (2026). Recognizing Research Software: DataCite Journey of the Helmholtz-Zentrum Dresden-Rossendorf. DataCite. [https://doi.org/10.5438/5TCR-Q032](https://doi.org/10.5438/5TCR-Q032)<br /><br />Barker, M., Chue Hong, N.P., Katz, D.S. et al. Introducing the FAIR Principles for research software. Sci Data 9, 622 (2022). [https://doi.org/10.1038/s41597-022-01710-x](https://doi.org/10.1038/s41597-022-01710-x)<br /><br />Smith, A. M., Katz, D. S., & Niemeyer, K. E. (2016). Software citation principles. PeerJ Computer Science, 2, e86. [https://doi.org/10.7717/peerj-cs.86](https://doi.org/10.7717/peerj-cs.86)
