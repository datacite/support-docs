---
title: Formatted Citations and DataCite Metadata
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
In order to generate formatted citations from DataCite DOI metadata, DataCite uses [Citeproc JSON](https://citeproc-js.readthedocs.io/en/latest/csl-json/markup.html) as an intermediate metadata format. Citeproc JSON is used with [Citation Style Language](http://citationstyles.org/) styles and locales to generate a formatted citation from DataCite DOI metadata in over 5,000 citation styles.

## Retrieving formatted citations

There are several ways to retrieve formatted citations based on DataCite DOI metadata. All methods rely on the Citeproc JSON mapping documented above.

### Content Negotiation

Content Negotiation allows a user to request a particular representation of a web resource. DataCite supports formatted citations via the text/bibliography content type.  These are the output of the [Citation Style Language](https://citationstyles.org/) processor. The content type can take two additional parameters to customise its response format: "style" (from the list of style names in the [CSL styles repository](https://github.com/citation-style-language/styles)) and "locale" (from the list of locale names in the [CSL locales repository](https://github.com/citation-style-language/locales)).

For more information, see our documentation on [DataCite Content Negotiation](https://support.datacite.org/docs/datacite-content-resolver), including how to make requests for [Formatted Citations](https://support.datacite.org/docs/datacite-content-resolver#formatted-citations).

### DOI Citation Formatter

The DOI Foundation’s [DOI Citation Formatter](https://citation.doi.org/) takes the metadata description of a DOI and uses the information to build a citation following more than 5,000 citation styles made available by the [citationstyles.org ](http://citationstyles.org/)project. This service is built using [DOI Content Negotiation](https://citation.doi.org/docs.html) and works across DOI Registration Agencies, including DataCite.

### DataCite Commons

On DataCite Commons Work pages, the "Cite as" section displays a formatted citation for the  DOI. Use the dropdown menu to select different citation styles:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ccb13f68609e18c54fe383561c39da1c8e581b82f8f18396515cbbc32281b197-Screenshot_2025-11-27_at_12.53.51.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


### DataCite REST API

The DataCite REST API supports link-based content type requests, including requests for formatted citations using the text/x-bibliography type.

Example requests:

- <https://api.datacite.org/text/x-bibliography/10.14454/mzv1-5b55?style=vancouver&lang=en>
- <https://api.datacite.org/text/x-bibliography/10.14454/mzv1-5b55?style=ieee&lang=de>
- <https://api.datacite.org/text/x-bibliography/10.14454/mzv1-5b55?style=apa&lang=en> 

This method works with DataCite DOIs only—in contrast with Content Negotiation, which works across DOI Registration Agencies. If you aren’t sure which DOI Registration Agency a DOI is associated with, we recommend using Content Negotiation.

### DataCite Fabrica

When logged into DataCite Fabrica, formatted citations can be retrieved from  individual DOI pages under the "Citation" heading.

## Adding series information for formatted citations

When registering a DOI for an item in a series, include series information via the RelatedItem property with relationType="IsPublishedIn". This information will be included in the formatted citation.

For example, when registering a DOI for a journal article, add a RelatedItem for the journal information:

```xml
<relatedItem relationType="IsPublishedIn" relatedItemType="Journal">
	<relatedItemIdentifier relatedItemIdentifierType="ISSN">1234-5678</relatedItemIdentifier>
	<titles>
		<title>Journal of Metadata Examples</title>
	</titles>
	<publicationYear>2022</publicationYear>
	<volume>3</volume>
	<issue>4</issue>
	<firstPage>20</firstPage>
	<lastPage>35</lastPage>
</relatedItem>

```

For more information, see the DataCite Metadata Schema guidance for [Using RelatedItem for publication information and related resources](https://datacite-metadata-schema.readthedocs.io/en/4/guidance/related-item-guide/).

> 📘 Using Description with descriptionType="SeriesInformation"
> 
> A Description with descriptionType="SeriesInformation" can also be used to provide series information. When using this method, the following text structure is required:
> 
> `series title, volume(issue), firstpage-lastpage`
> 
> Here is an example XML snippet for a Description with descriptionType="SeriesInformation":
> 
> ```xml
> <description descriptionType="SeriesInformation">Journal of Metadata Examples, 3(4), 20-35</description>
> ```
> 
> If a RelatedItem with relationType="IsPublishedIn" is also present, the RelatedItem metadata will take precedence over the Description with descriptionType="SeriesInformation" when generating the formatted citation.



## Mapping from the DataCite Metadata Schema to Citeproc JSON

This table shows how DataCite metadata properties are mapped to Citeproc JSON elements. The Citeproc JSON elements are used by CSL styles to produce formatted citations.

| Citeproc JSON attribute | DataCite metadata                                      | If relatedItem with "IsPublishedIn" relationType is present | If description with "SeriesInformation" descriptionType is present               |
| :---------------------- | :----------------------------------------------------- | :---------------------------------------------------------- | :------------------------------------------------------------------------------- |
| type                    | types.resourceTypeGeneral mapped to Citeproc JSON type |                                                             |                                                                                  |
| id                      | doi                                                    |                                                             |                                                                                  |
| categories              | subjects                                               |                                                             |                                                                                  |
| language                | language                                               |                                                             |                                                                                  |
| author                  | creators                                               |                                                             |                                                                                  |
| contributor             | contributors                                           |                                                             |                                                                                  |
| editor                  | contributors with "Editor" contributorType             |                                                             |                                                                                  |
| translator              | contributors with "Translator" contributorType         |                                                             |                                                                                  |
| available-date          | date with “Available" dateType                         |                                                             |                                                                                  |
| issued                  | date with “Issued" dateType                            |                                                             |                                                                                  |
| submitted               | date with “Submitted" dateType                         |                                                             |                                                                                  |
| abstract                | First of descriptions.description                      |                                                             |                                                                                  |
| chapter-number          |                                                        | relatedItems.number if numberType is “Chapter"              |                                                                                  |
| container-title         |                                                        | First of relatedItems.titles.title                          | descriptions.description = "**Series Title**, volume(issue), firstpage-lastpage" |
| DOI                     | doi                                                    |                                                             |                                                                                  |
| edition                 |                                                        | relatedItems.edition                                        |                                                                                  |
| issue                   |                                                        | relatedItems.issue                                          | descriptions.description = "Series Title, volume(**issue**), firstpage-lastpage" |
| number                  |                                                        | relatedItems.number                                         |                                                                                  |
| page                    |                                                        | [relatedItems.firstPage]-[relatedItems.lastPage]            | descriptions.description = "Series Title, volume(issue), **firstpage-lastpage**" |
| page-first              |                                                        | relatedItems.firstPage                                      | descriptions.description = "Series Title, volume(issue), **firstpage**-lastpage" |
| publisher               | publisher.name                                         |                                                             |                                                                                  |
| title                   | First of titles                                        |                                                             |                                                                                  |
| URL                     | url                                                    |                                                             |                                                                                  |
| version                 | version                                                |                                                             |                                                                                  |
| volume                  |                                                        | relatedItems.volume                                         | descriptions.description = "Series Title, **volume**(issue), firstpage-lastpage" |

##