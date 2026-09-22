---
title: DataCite Metadata Dashboard
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: Our Metadata Guides can help you improve your metadata quality.
  pages:
    - type: basic
      slug: metadata-guides
      title: Metadata Guides
---
The DataCite metadata dashboard is a tool for monitoring DataCite metadata quality and identifying opportunities to advance the discoverability and impact of scholarly resources.

The metadata dashboard is publicly accessible at <https://metadata.datacite.org>.

## Search Organizations and Repositories

Search for a DataCite Member, Consortium Organization, or Repository to view a metadata quality snapshot and explore opportunities for improvement. You can search by the organization/repository name or account identifier. For example, try searching "DataCite Canada Consortium", "CERN", or "rpht.nifs".

For more information on the DataCite account types and structure, see [Accounts in DataCite](doc:datacite-account-types).

## Explore Metadata Quality

When a DataCite Member, Consortium Organization or Repository is selected, the dashboard displays a metadata quality snapshot for all the DOIs under that account.

At the top, the interface displays:

- the total number of DOIs
- DOI registrations by year
- DOI resource types (from [resourceTypeGeneral](https://datacite-metadata-schema.readthedocs.io/en/4/properties/resourcetype/#a-resourcetypegeneral))

Below, metadata completeness (as a percentage of DOIs) and top values are surfaced for all metadata properties and key sub-properties. The "High Impact" properties are recommended to improve discoverability.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3ee30662c9dc3303d48bdf4f3476b9f20cde8500cef14c638da6827bc79e08b5-Screenshot_2026-02-27_at_13.12.13.png",
        "",
        "Screenshot of the metadata dashboard for the DataCite Blog Repository (datacite.blog)"
      ],
      "align": "center",
      "caption": "Screenshot of the metadata dashboard for the DataCite Blog Repository (datacite.blog)"
    }
  ]
}
[/block]


For some properties, in addition to completeness, the top 10 values are shown in a "Values of" section. These values show the percentage of populated records containing each value. For example, in this repository, 95.9% of records have a nameIdentifier with a nameIdentifierScheme. Within those records, 98.2% of the nameIdentifierSchemes are ORCID.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9f46a31a91b74dfed2fd77c9ab0b5d229d21f9576dc8f9636b46aadf49861e1f-Screenshot_2026-03-02_at_12.29.47.png",
        "",
        "Values of nameIdentifierScheme, showing the percentage of populated records containing each value"
      ],
      "align": "center",
      "caption": "Values of nameIdentifierScheme, showing the percentage of populated records containing each value"
    }
  ]
}
[/block]


### Navigation and Filters

The breadcrumbs at the top of the dashboard can be used to navigate between Repositories (within a Direct Member or Consortium Organization view) and between Consortium Organizations (within a Consortium Lead view).

Filters can be applied to adjust which DOIs are included in the dashboard. Available options include:

- Filter by Registration Year (for the top 10 Registration Years by volume)
- Filter by Resource Type
- Filter using [query string syntax](https://support.datacite.org/docs/queries)

When filters are applied, the visualizations will update to reflect the filtered set of DOIs.

Use the links to "View in Commons" or "View in REST API" to get a list of DOIs included in the view, with any filters applied.

> 📘 
> 
> We welcome your feedback on the metadata dashboard via [DataCite Suggestions](https://github.com/datacite/datacite-suggestions/discussions/categories/general-suggestions).
> 
> For support questions, please contact us at [support@datacite.org](mailto:support@datacite.org).

_The metadata dashboard was developed in collaboration with the [Generalist Repository Ecosystem Initiative (GREI)](https://datascience.nih.gov/data-ecosystem/generalist-repository-ecosystem-initiative)._