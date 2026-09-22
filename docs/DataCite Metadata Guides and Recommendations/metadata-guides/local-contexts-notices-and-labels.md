---
title: Local Contexts Notices and Labels
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
## About Local Contexts Notices and Labels

[Local Contexts](https://localcontexts.org/) supports Indigenous communities to manage their intellectual and cultural property, cultural heritage, environmental data and genetic resources within digital environments. Local Contexts recognizes the inherent sovereignty that Indigenous communities have over knowledge and data that comes from their lands, territories, and waters.

The [Local Contexts Hub](https://localcontexts.org/tk-label-hub/) provides an interface to apply the Traditional Knowledge (TK) and Biocultural (BC) Notices and Labels to ground Indigenous data sovereignty.

### Notices

[Notices](https://localcontexts.org/notice) are a mechanism for researchers and institutional staff to identify Indigenous collections and Indigenous interests in data. The Notices can function as place-holders on collections, data, or in a sample field until a TK or a BC Label is added by an Indigenous community. 

**Researchers and institutional staff can apply Notices to a project through the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/).**

There are four Notices:

- [TK (Traditional Knowledge) Notice](https://localcontexts.org/notice/tk-notice/) recognizes that there could be accompanying cultural rights, protocols and responsibilities that need further attention for future sharing and use of this material.
- [BC (Biocultural) Notice](https://localcontexts.org/notice/bc-notice/) recognizes the rights of Indigenous peoples to define the use of information, collections, data and digital sequence information generated from the biodiversity and genetic resources associated with their traditional lands, waters, and territories.
- [Attribution Incomplete Notice](https://localcontexts.org/notice/attribution-incomplete/) is attached to a collection or at an item level where there is incomplete, inaccurate, or missing attribution. This Notice indicates to the public that the record and/or metadata is incomplete.
- [Open to Collaboration Notice](https://localcontexts.org/notice/open-to-collaborate/) indicates that an institution is committed to developing new modes of collaboration, engagement, and partnership with Indigenous peoples for the care and stewardship of past and future collections and data.

### Labels

[Labels](https://localcontexts.org/labels) allow Indigenous communities to express local and specific conditions for sharing and engaging in future research and relationships in ways that are consistent with already existing community rules, governance and protocols for using, sharing and circulating knowledge and data.

**Indigenous communities can apply Labels to a project through the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/) through a Community Account.** Labels _cannot_ be applied through Researcher Accounts or Institution Accounts. For more information on account types, see [Local Contexts Hub Support](https://localcontexts.org/tk-label-hub/).

There are two types of Labels, and many specific Labels within each type:

- [Traditional Knowledge (TK) Labels](https://localcontexts.org/labels/traditional-knowledge-labels) define attribution, access, and use rights for Indigenous cultural heritage
- [Biocultural (BC) Labels](https://localcontexts.org/labels/biocultural-labels/) define community expectations and consent about appropriate use of collections and data

Label text is customized by each community, giving the Labels specificity and context using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/), which allows community control over customization and delivery to institutions, data repositories and other organizations. 

### When to use Notices vs. Labels

A key difference between Notices and Labels is that **Notices are generated and applied by institutions and researchers**, while **Labels are generated and applied by Indigenous communities**. 

Institutions should begin by applying Notices to identify Indigenous collections and Indigenous interests in data. Using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/), collections managers and researchers can communicate their use of Notices to a community, signalling an intent to collaborate on labeling items with Indigenous interests and facilitating creation of customized Labels.

> 🚧 
> 
> Labels should only be used when they have been generated and applied by an Indigenous community using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/).

## Using the Rights property for Notices and Labels

### Prerequisites

#### Prerequisites for Notices

##### Institutions

1. Your institution is working in collaboration with Indigenous communities.
2. Your institution has registered for the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 
3. Your institution has generated Notices for collection(s)/items using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 

#### Prerequisites for Labels

##### Institutions

1. Your institution is working in collaboration with Indigenous communities.

- Using Local Contexts Labels requires collaboration between Indigenous communities and institutions/researchers in order for communities to determine the appropriate Label(s) and Label text for collections/items. 

2. Your institution has registered for the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 
3. Your institution has generated Notices for collection(s)/items using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/) and shared the Notices with an Indigenous community. 
4. A community has applied one or more Labels to your collection(s)/items using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 

##### Indigenous communities

1. Your community has registered for the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 
2. Your community has applied one or more Labels to your collection(s)/items using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/). 

> 🚧 
> 
> If your institution or community is not already using the [Local Contexts Hub](https://localcontexts.org/tk-label-hub/) or needs additional guidance on using Notices and Labels, please [contact the Local Contexts team](https://localcontexts.org/contact/).

### Rights metadata for Notices

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Value",
    "h-2": "Example value(s)",
    "0-0": "Rights",
    "0-1": "Notice text from the landing page of the Notice.  \n  \nFor clarity, this should be preceded by the name of the Notice and the URL for the Notice.  \n  \nUse the exact text from the landing page; do not adapt or change the text.",
    "0-2": "Local Contexts Traditional Knowledge (TK) Notice <https://localcontexts.org/notice/tk-notice>: The TK Notice is a visible notification that there are accompanying cultural rights and responsibilities that need further attention for any future sharing and use of this material. The TK Notice may indicate that TK Labels are in development and their implementation is being negotiated.",
    "1-0": "rightsURI",
    "1-1": "The URL of the project in the Local Contexts hub.",
    "1-2": "<https://localcontextshub.org/projects/7894f2fd-bbcb-423c-afff-ea67b4e1e4f7/>",
    "2-0": "rightsIdentifier",
    "2-1": "The identifier of the specific Notice being applied.",
    "2-2": "TK-Notice  \n  \nBC-Notice  \n  \nAttribution-Incomplete  \n  \nOpen-To-Collaborate",
    "3-0": "rightsIdentifierScheme",
    "3-1": "Local Contexts",
    "3-2": "Local Contexts",
    "4-0": "schemeURI",
    "4-1": "Local Contexts website URI",
    "4-2": "<https://localcontexts.org>"
  },
  "cols": 3,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


```xml Example XML for Notices
<rightsList>
  <rights rightsURI="https://localcontextshub.org/projects/7894f2fd-bbcb-423c-afff-ea67b4e1e4f7/" rightsIdentifier="TK-Notice" 
  rightsIdentifierScheme="Local Contexts" 
  schemeURI="https://localcontexts.org"> 
  Local Contexts TK Notice https://localcontexts.org/notice/tk-notice: The TK Notice is a visible notification that there are accompanying cultural rights and responsibilities that need further attention for any future sharing and use of this material. The TK Notice may indicate that TK Labels are in development and their implementation is being negotiated.
  </rights>
</rightsList>
```

```json Example JSON for Notices
"rightsList": [
  {
    "rights": "Local Contexts TK Notice https://localcontexts.org/notice/tk-notice: The TK Notice is a visible notification that there are accompanying cultural rights and responsibilities that need further attention for any future sharing and use of this material. The TK Notice may indicate that TK Labels are in development and their implementation is being negotiated. ",
    "rightsUri": "https://localcontextshub.org/projects/7894f2fd-bbcb-423c-afff-ea67b4e1e4f7/",
    "rightsIdentifier": "tk-notice",
    "rightsIdentifierScheme": "Local Contexts",
    "schemeUri": "https://localcontexts.org"
  }
]
```

> 📘 
> 
> When viewing a DOI's Work page in [DataCite Commons](doc:datacite-commons) , rights containing 1) rightsIdentifiers `TK-Notice`, `BC-Notice`, and `Attribution-Incomplete` and 2) rightsIdentifierScheme `Local Contexts` will appear with their Local Contexts Notice icon.

### Rights metadata for Labels

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Value",
    "h-2": "Example value(s)",
    "0-0": "Rights",
    "0-1": "The custom Label text created by a community for this collection/item using the Local Contexts Hub.  \n  \nFor clarity, this should be preceded by the name of the Label. Do not include the generic URL for the Label.",
    "0-2": "Local Contexts TK Attribution: This Label is being used to correct historical mistakes or exclusions pertaining to this material. This is especially in relation to the names of the people involved in performing or making this work and/or correctly naming the community from which it originally derives. As a user you are being asked to also apply the correct attribution in any future use of this work.",
    "1-0": "rightsURI",
    "1-1": "The URL of the project in the Local Contexts hub.",
    "1-2": "<https://localcontextshub.org/projects/259854f7-b261-4c8c-8556-4b153deebc18/>",
    "2-0": "rightsIdentifier",
    "2-1": "The identifier of the specific Label being applied.",
    "2-2": "TK-A  \n  \nBC-P",
    "3-0": "rightsIdentifierScheme",
    "3-1": "Local Contexts",
    "3-2": "Local Contexts",
    "4-0": "schemeURI",
    "4-1": "Local Contexts website URI",
    "4-2": "<https://localcontexts.org>"
  },
  "cols": 3,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


```xml Example XML for Labels
<rightsList>
  <rights rightsURI="https://localcontextshub.org/projects/259854f7-b261-4c8c-8556-4b153deebc18/ " rightsIdentifier="TK-A" 
  rightsIdentifierScheme="Local Contexts" 
  schemeURI="https://localcontexts.org">
  Local Contexts TK Attribution: This Label is being used to correct historical mistakes or exclusions pertaining to this material. This is especially in relation to the names of the people involved in performing or making this work and/or correctly naming the community from which it originally derives. As a user you are being asked to also apply the correct attribution in any future use of this work.
  </rights>
</rightsList>
```

```json Example JSON for Labels
"rightsList": [  
  {  
    "rights": "Local Contexts TK Attribution: This Label is being used to correct historical mistakes or exclusions pertaining to this material. This is especially in relation to the names of the people involved in performing or making this work and/or correctly naming the community from which it originally derives. As a user you are being asked to also apply the correct attribution in any future use of this work.",  
    "rightsUri": "https://localcontextshub.org/projects/259854f7-b261-4c8c-8556-4b153deebc18/",  
    "rightsIdentifier": "TK-A",  
    "rightsIdentifierScheme": "Local Contexts",  
    "schemeUri": "https://localcontexts.org"  
  }  
]
```

### Rights metadata without Label or Notice text

Alternatively, if a repository does not store specific Notices or Labels, the Rights text may be replaced with a reference to the project page on the Local Context Hub. rightsIdentifier may also be omitted.

| Property               | Value                                                   | Example value(s)                                                                                                                                                                                              |
| :--------------------- | :------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Rights                 | Reference to the project page on the Local Context Hub. | This project has Labels and/or Notices applied through the Local Contexts Hub. For more information, refer to the project page: <https://localcontextshub.org/projects/259854f7-b261-4c8c-8556-4b153deebc18/> |
| rightsURI              | The URL of the project in the Local Contexts hub.       | <https://localcontextshub.org/projects/259854f7-b261-4c8c-8556-4b153deebc18/>                                                                                                                                 |
| rightsIdentifier       | If referring to the entire project, leave blank.        |                                                                                                                                                                                                               |
| rightsIdentifierScheme | Local Contexts                                          | Local Contexts                                                                                                                                                                                                |
| schemeURI              | Local Contexts website URI                              | <https://localcontexts.org>                                                                                                                                                                                   |

> 📘 
> 
> For more information, visit the Local Contexts website: <https://localcontexts.org/>