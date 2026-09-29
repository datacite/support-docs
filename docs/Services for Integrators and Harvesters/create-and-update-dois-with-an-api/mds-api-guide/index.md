---
title: DataCite MDS API
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
## Purpose

The [DataCite Metadata Store (MDS) API](https://support.datacite.org/reference/mds) allows users to register DataCite DOIs and associated metadata. The API requires authentication. To retrieve DOI metadata records users should use our [DataCite REST API](doc:api). To become a member, interested parties should contact the [DataCite support](mailto:support@datacite.org) team. [DataCite Fabrica](https://support.datacite.org/docs/doi-fabrica) provides an alternative for registering DataCite DOIs via a web interface. 

## Authentication

All requests to the MDS API require authentication. For this reason, only traffic via a secure connection (HTTPS) is supported. The DataCite Metadata Store (MDS) uses  [HTTP Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication). 

> 📘 To create DOIs with the MDs API, you will need:
> - Repository account credentials or a corresponding [API key](doc:api-keys). Only Repository accounts have the ability to create and update DOIs. For more information on account types and permissions, see [Accounts in DataCite](docs:datacite-account-types). 
> - Prefix. The prefix associated with your Repository account must be included in the API request. The request will fail with an error message if the prefix used is not associated with your Repository ID. 

## How to Use

The DataCite Metadata Store (MDS) API can be used directly by making HTTP requests with packages such as [cURL](https://curl.haxx.se/docs/manpage.html). Besides using the API directly there are a number of integrations with the MDS API that allow the creation of DataCite DOIs. Please review the documentation of the respective package for installation instructions.

## Fetch a DOI

Let's start by testing our setup. In this guide, the examples we will use would employ the _MDS Production endpoint_ (i.e., <https://mds.datacite.org> ) We will use the curl command-line tool. 

### Fetch the URL

Now, open up a command prompt and enter the following command:

```shell
$ curl --user username:password https://mds.datacite.org/doi/10.5438/0012
https://schema.datacite.org/meta/kernel-4.0/index.html%
```

The response will be the URL registered for the DOI you requested. 

> 🚧 Warning
> 
> If you got a wrong credentials error when retrieving the example DOI 10.5438/0012. Use a DOI name that belongs to your organization.

### Fetch the metadata

Next, let's register the metadata associated with the DOI:

```shell
# GET /metadata/doi
$ curl --user username:password https://mds.datacite.org/metadata/10.5438/0012
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<resource xmlns="http://datacite.org/schema/kernel-4" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://datacite.org/schema/kernel-4 http://schema.datacite.org/meta/kernel-4/metadata.xsd">
    <identifier identifierType="DOI">10.5438/0012</identifier>
    <creators>
        <creator>
            <creatorName>DataCite Metadata Working Group</creatorName>
        </creator>
    </creators>
    <titles>
        <title>DataCite Metadata Schema Documentation for the Publication and Citation of Research Data v4.0</title>
    </titles>
    <publisher>DataCite e.V.</publisher>
    <publicationYear>2016</publicationYear>
    <contributors>
        <contributor contributorType="ProjectLeader">
            <contributorName>Starr, Joan</contributorName>
            <givenName>Joan</givenName>
            <familyName>Starr</familyName>
            <nameIdentifier nameIdentifierScheme="ORCID" schemeURI="http://orcid.org">0000-0002-7285-027X</nameIdentifier>
            <affiliation>California Digital Library</affiliation>
        </contributor>
        <contributor contributorType="ProjectLeader">
            <contributorName>Smaele, Madeleine de</contributorName>
            <givenName>Madeleine de</givenName>
            <familyName>Smaele</familyName>
            <affiliation>TU Delft</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Ashton, Jan</contributorName>
            <givenName>Jan</givenName>
            <familyName>Ashton</familyName>
            <affiliation>British Library</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Barton, Amy</contributorName>
            <givenName>Amy</givenName>
            <familyName>Barton</familyName>
            <affiliation>Purdue University Library</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Bradford, Tina</contributorName>
            <givenName>Tina</givenName>
            <familyName>Bradford</familyName>
            <affiliation>NRC/CISTI</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Ciolek‐Figiel, Anne</contributorName>
            <givenName>Anne</givenName>
            <familyName>Ciolek-Figiel</familyName>
            <affiliation>Inist‐CNRS</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Dietiker, Stefanie</contributorName>
            <givenName>Stefanie</givenName>
            <familyName>Dietiker</familyName>
            <affiliation>ETH Zürich</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Elliott, Jannean</contributorName>
            <givenName>Jannean</givenName>
            <familyName>Elliot</familyName>
            <affiliation>DOE/OSTI</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Genat, Berrit</contributorName>
            <givenName>Berrit</givenName>
            <familyName>Genat</familyName>
            <affiliation>TIB</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Harzenetter, Karoline</contributorName>
            <givenName>Karoline</givenName>
            <familyName>Harzenetter</familyName>
            <affiliation>GESIS</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Hirschmann, Barbara</contributorName>
            <givenName>Barbara</givenName>
            <familyName>Hirschmann</familyName>
            <nameIdentifier nameIdentifierScheme="ORCID" schemeURI="http://orcid.org">0000-0003-0289-0345</nameIdentifier>
            <affiliation>ETH Zürich</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Jakobsson, Stefan</contributorName>
            <givenName>Stefan</givenName>
            <familyName>Jakobsson</familyName>
            <affiliation>SND</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Mailloux, Jean‐Yves</contributorName>
            <givenName>Jean-Yves</givenName>
            <familyName>Mailloux</familyName>
            <affiliation>NRC/CISTI</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Newbold, Elizabeth</contributorName>
            <givenName>Elizabeth</givenName>
            <familyName>Newbold</familyName>
            <nameIdentifier nameIdentifierScheme="ORCID" schemeURI="http://orcid.org">0000-0002-8255-9013</nameIdentifier>
            <affiliation>British Library</affiliation>
        </contributor>
                <contributor contributorType="Editor">
            <contributorName>Nielsen, Lars Holm </contributorName>
            <givenName>Lars Holm</givenName>
            <familyName>Nielsen</familyName>
            <nameIdentifier nameIdentifierScheme="ORCID" schemeURI="http://orcid.org">0000-0001-8135-3489</nameIdentifier>
            <affiliation>CERN</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName>Yahia, Mohamed</contributorName>
            <givenName>Mohamed</givenName>
            <familyName>Yahia</familyName>
            <affiliation>Inist-CNRS</affiliation>
        </contributor>
        <contributor contributorType="Supervisor">
            <contributorName>Ziedorn, Frauke</contributorName>
            <givenName>Frauke</givenName>
            <familyName>Ziedorn</familyName>
            <nameIdentifier nameIdentifierScheme="ORCID" schemeURI="http://orcid.org">0000-0002-1143-781X</nameIdentifier>
            <affiliation>TIB</affiliation>
        </contributor>
    </contributors>
    <language>eng</language>
    <resourceType resourceTypeGeneral="Text">Documentation</resourceType>
    <relatedIdentifiers>
        <relatedIdentifier relatedIdentifierType="DOI" relationType="Documents">10.5438/0013</relatedIdentifier>
        <relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.5438/0010</relatedIdentifier>
    </relatedIdentifiers>
    <sizes>
        <size>45 pages</size>
    </sizes>
    <formats>
        <format>application/pdf</format>
    </formats>
    <version>4.0</version>
    <descriptions>
        <description descriptionType="TableOfContents">1 Introduction<br/>
1.1 The DataCite Consortium<br/>
1.2 DataCite Community Participation<br/>
1.3 The Metadata Schema<br/>
1.4 Version 4.0 Update<br/>
2 DataCite Metadata Properties<br/>
2.1 Overview<br/>
2.2 Citation<br/>
2.3 DataCite Properties<br/>
3 XML Example<br/>
4 XML Schema<br/>
5 Other DataCite Services<br/>
Appendices<br/>
Appendix 1: Controlled List Definitions<br/>
Appendix 2: Earlier Version Update Notes</description>
    </descriptions>
</resource>
```

The response is metadata in DataCite XML format. Let's add the `-i` flag to include headers:

```shell
# GET /metadata/doi
$ curl --user username:password https://mds.datacite.org/metadata/10.5438/0012 -i
```

```shell
HTTP/2 200
date: Mon, 06 Aug 2018 17:43:48 GMT
content-type: application/xml; charset=utf-8
status: 200 OK
cache-control: max-age=0, private, must-revalidate
vary: Accept-Encoding, Origin
etag: W/"3122a5d037aa7b46e5e9c60de67b6459"
x-runtime: 0.053340
x-credential-username: xxx
x-request-id: cb98f390-d65c-4b16-b7d4-7bb84e37bc22
x-powered-by: Phusion Passenger 5.3.4
server: nginx/1.14.0 + Phusion Passenger 5.3.4

<?xml version="1.0" encoding="UTF-8"?>
<resource xmlns="http://datacite.org/schema/kernel-4" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
```

There are a few interesting bits in the response headers. As expected, the Content-Type is `application/xml`. The response status can be one of: 

- `200 OK`: operation successful; 
- `204 No Content`:  the DOI is known to DataCite Metadata Store (MDS), but no metadata have been registered; 
- `401 Unauthorized`: no login; 
- `403 Forbidden`: permission problem or dataset belongs to another party; 
- `404 Not Found`: DOI does not exist in our database;
- `422 Unprocessable Entity`: metadata failed validation against the [DataCite Schema](https://schema.datacite.org/).

## Register a DOI

In this tutorial we will look at the three steps needed to register a DOI in the DataCite Metadata Store (MDS): 

- picking a DOI name,
- creating metadata records, and 
- creating DOI names. Both operations are necessary to register DOIs.

### Picking a DOI name

The DOI suffix (the suffix is the part after your prefix 10.xxxx) can be any alphanumeric string, as long as it hasn't been used before.  Limited punctuation is allowed, the approved character set for DOI suffixes is: "a-z", "A-Z", "0-9" and "-.\_;()/".  An expanded set of characters was supported prior to July 2018, so you may see DOIs with other characters as well. (such as #, +, \<, and >). An example of a DOI name would be `10.5438/0012`.

If you don't want to pick a DOI name, the MDS API can generate a random DOI name for you. For details see below in section [Auto-generated DOI names](#section-auto-generated-doi-names).

### Register metadata

To add metadata to a DOI, we need to `PUT`  XML containing the metadata conforming to the [DataCite Metadata Schema](http://schema.datacite.org). There you will find the preferred version and example XML documents. Please remember that all your documents must specify the correct schema location in the root element. 

> 📘 Metadata in other formats can also be registered via the MDS API. These formats include:
> 
> - RIS
> - BibTeX
> - Schema.org (as JSON-LD or URL pointing to a web page with embedded schema.org)
> - Citeproc JSON
> - Codemeta
> - Crossref XML

The `identifier` in the DataCite XML metadata file can be left empty, as the value from the `PUT URL` will be used. The content type for the request must be `application/xml`.

> 📘 Validating metadata
> 
> The metadata you submit must include all of the mandatory metadata properties as outlined in the [DataCite Metadata Schema](http://schema.datacite.org). The validation for MDS does not allow creation of drafts with no, incomplete, or invalid metadata.

```shell
# PUT /metadata/10.5438/JQX3-61AT
$ curl -H "Content-Type: application/xml;charset=UTF-8" -X PUT -i --user username:password -d @10.5438/JQX3-61AT.xml https://mds.test.datacite.org/metadata/10.5438/JQX3-61AT
```

The response to this call will return a short explanation of status code e.g. CREATED, HANDLE_ALREADY_EXISTS etc. The response status can be one of: 

- `201 Created`: operation successful,
- `401 Unauthorised`: no login, 
- `403 Forbidden`: login problem, , wrong prefix, 
- `415 Wrong Content Type`: Not including the correct content type in the header.
- `422 Unprocessable Entity`: invalid XML

Once you have created the record, you can fetch the metadata record as described earlier in this guide.

### Register the URL

The next step is to register the DOI name and associated URL. We can `PUT` DOIs in a similar way to how we fetched DOI details earlier. A file with the DOI name for the new resource and the URL where the resource is located needs to be provided. 

Please note that the new lines specified in the payload are important to ensure whichever method you use keeps them intact. You can use the newline character (\\n) instead.

```text
#Content-Type:text/plain;charset=UTF-8
doi= 10.5438/JQX3-61AT
url= http://example.org/
```

```shell
# PUT /doi
$ curl -H "Content-Type:text/plain;charset=UTF-8" -X PUT --user username:password -d "$(printf 'doi=10.5438/JQX3-61AT\nurl=http://example.org/')" https://mds.test.datacite.org/doi/10.5438/JQX3-61AT
```

This method will attempt to update the URL if you specify a DOI with an existing URL, otherwise, the DOI will be registered in the handle system, and will resolve via <https://doi.org>. 

The response is a short explanation of status code (e.g. CREATED, HANDLE_ALREADY_EXISTS etc). The response status can be one of: 

- `201 Created`: operation successful; 
- `400 Bad Request`: request body must be exactly two lines: DOI and URL; wrong domain, wrong prefix;
- `401 Unauthorised`: no login; 
- `403 Forbidden`: login problem; 
- `412 Precondition failed`: metadata must be uploaded first.

In the same way, we can fetch the URL for the DOI we just registered. There is a small delay (usually a few minutes) before a newly registered DOI becomes visible in the handle system. 

```shell
$ curl -X GET --user username:password https://mds.test.datacite.org/doi/10.5438/JQX3-61AT
https://doi.org/10.5438/JQX3-61AT
```

Now you know the basics of the DataCite Metadata Store (MDS) API. You learned:

- Basic authentication
- Fetching and registering DOI names and metadata records.
- Register DOIs and metadata

Keep learning with the [API Live Reference](https://support.datacite.org/reference/overview) where you can make requests directly to the MDS test service.

## Auto-generated DOI names

If you want DataCite to generate a random DOI name for you, provide only the prefix when you register metadata:

```shell
# PUT /metadata/10.5438
$ curl -H "Content-Type: application/xml;charset=UTF-8" -X PUT -i --user username:password -d @10.5438/JQX3-61AT.xml https://mds.test.datacite.org/metadata/10.5438
```

This will register metadata with a random DOI using the prefix you indicated (which in the above example is 10.5438). The DOI in the metadata file will be overwritten and can therefore be left empty.

## DOI States

DOIs can exist in three states: **draft**, **registered**, and **findable**. The **draft** state is when metadata have been registered but are not public facing and will transition to the **findable** state when registering a URL. 

Findable DOIs can be transitioned to the **registered** state (the metadata are no longer included in the search index) using this command:

```shell
# DELETE /metadata/10.5438/JQX3-61AT
$ curl -H "Content-Type: application/plain;charset=UTF-8" -X DELETE -i --user username:password  https://mds.test.datacite.org/metadata/10.5438/JQX3-61AT
```

Send another `PUT /metadata` request to transition the DOI back to the **findable** state.

Drafts can be deleted using this command:

```shell
# DELETE /doi/10.5438/JQX3-61AT
$ curl -H "Content-Type: application/plain;charset=UTF-8" -X DELETE -i --user username:password  https://mds.test.datacite.org/doi/10.5438/JQX3-61AT
```

Find out more about DOI states [here](https://support.datacite.org/docs/doi-states).

> 📘 Would you like to know more?
> 
> If you have any questions, requests or ideas please [contact us!](doc:how-to-contact-datacite)
