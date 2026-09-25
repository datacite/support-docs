---
title: Update DOIs with the REST API
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
## DOI Update Basics

To update an existing record, you will need to make a PUT request to `https://api.test.datacite.org/dois/{id}` —replacing `{id}` with the DOI you wish to update—with a JSON payload in the request. See the [API Reference](ref:put_dois-id) for more information.

> 📘 
> 
> PUT requests to the /dois endpoint will **update** a DOI record if it already exists and **create** a new record if the DOI name is not already taken.

Your Repository account username and password or [an API key corresponding to a Repository account](doc:api-keys) are needed for authentication. The JSON payload can be specified in a file. Here is an example curl command using the test endpoint:

```shell
# PUT /dois/:id

curl -X PUT -H "Content-Type: application/vnd.api+json" --user YOUR_REPOSITORY_ID:YOUR_PASSWORD -d @my_doi_update.json https://api.test.datacite.org/dois/:id
```

You will need to replace:

- `YOUR_REPOSITORY_ID:YOUR_PASSWORD` with your DataCite repository credentials or API key
- `doi_update.json` with the name of your JSON payload file
- `:id` with the DOI you wish to update
  - For example, replace `https://api.test.datacite.org/dois/:id` with `https://api.test.datacite.org/dois/10.5438/0012`

With the REST API, you can update a DOI either in full or partially via the attributes you specify. Below are some common DOI update actions. These can be used individually, or combined in a single request.

> 👍 All of the example JSON payloads below must be submitted via a PUT request as specified above.

## Changing the DOI State

In the previous examples, you can see an `"event"` attribute added to our JSON payload. The `"event"` attribute corresponds to the DOI state action you want to trigger for the DOI.

Use the `"publish"` attribute value to publish a DOI in findable state. Below are all possible actions:

| "event" attribute value | DOI state action                                                 |
| :---------------------- | :--------------------------------------------------------------- |
| publish                 | Triggers a state move from _draft_ or _registered_ to _findable_ |
| register                | Triggers a state move from _draft_ to _registered_               |
| hide                    | Triggers a state move from _findable_ to _registered_            |

### Example Request Payload: Changing the DOI state from Draft to Findable

This example payload only includes the `"event": "publish"` attribute. If the Draft record already has the required metadata, no other information is necessary.

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "event": "publish"
    }
  }
}
```

A successful request will result in a 200 OK response. In the response, you will find "state": "findable" in the attributes.

## Updating the URL

When updating a record via the REST API, only the attributes included in the payload will be affected.

### Example Request Payload: Updating the URL

The following payload can be used to update the URL without changing the metadata:

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "url": "https://example.org"
    }
  }
}
```

## Updating Metadata

When updating DOI metadata via the REST API, you can either send a complete metadata record, or just the fields that you wish to update. Only the fields included in the JSON payload will be changed.

### Example Request Payload: Adding Rights information

This example updates the Rights property. This would add Rights information to a DOI that did not previously include it.

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "rightsList": [
        {
          "rights": "Creative Commons Zero v1.0 Universal",
          "rightsUri": "https://creativecommons.org/publicdomain/zero/1.0/legalcode",
          "schemeUri": "https://spdx.org/licenses/",
          "rightsIdentifier": "cc0-1.0",
          "rightsIdentifierScheme": "SPDX"
        }
      ]
    }
  }
}
```

 If the DOI already included Rights information, this would be replaced with the new Rights information.

### Example Request Payload: Updating PublicationYear

This example updates the value of publicationYear to 2023.

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "publicationYear": "2023"
    }
  }
}
```

### Example Request Payload: Adding a second RelatedIdentifier

If you have a DOI with one RelatedIdentifer, in order to add a second RelatedIdentifier, the update request must include both RelatedIdentifiers. This is because the entire RelatedIdentifiers property will be replaced with the contents of what is sent.

This example would add the RelatedIdentifier 10.21384/yyyy to a record that already has RelatedIdentifier 10.21384/xxxxx:

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "relatedIdentifiers": [
        {
          "relatedIdentifier": "https://doi.org/10.21384/xxxxx",
          "relatedIdentifierType": "DOI",
          "relationType": "References",
          "resourceTypeGeneral": "Dataset"
        },
        {
          "relatedIdentifier": "https://doi.org/10.21384/yyyyy",
          "relatedIdentifierType": "DOI",
          "relationType": "References",
          "resourceTypeGeneral": "JournalArticle"
        }
      ]
    }
  }
}
```

### Example Request Payload: Removing FundingReference

This example removes the contents of the FundingReference property:

```json
{
  "data": {
    "type": "dois",
    "attributes": {
      "fundingReferences": []
    }
  }
}
```
