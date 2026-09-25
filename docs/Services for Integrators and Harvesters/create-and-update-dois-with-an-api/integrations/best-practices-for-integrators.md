---
title: Best Practices for Integrators
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
This document outlines best practices for anyone working to develop or maintain a DataCite API integration for DOI registration.

> 📘 Using an existing integration
> 
> Before you build a new integration, check if an integration already exists for your platform or system of choice. Many repository platforms already have DataCite DOI integrations.
> 
> [DataCite Service Providers](doc:datacite-service-providers) are organizations that provide software that integrates with a DataCite API to enable DOI registration for their users. Service Providers maintain [integrations for repository platforms and CRIS systems](doc:service-provider-software-integrations).
> 
> There are also other DataCite integrations that are not maintained by an organization participating in our Service Providers program. While these integrations have not been verified by DataCite, they are also an option for registering DOIs.

## Developing a new integration

We welcome new DataCite integrations built by platform providers, DataCite Members, and Consortium Organizations.

> 🚧 
> 
> When making frequent requests to DataCite APIs using a script or integration, include a `User-Agent` header with 1) an identification of your script or integration and 2) contact information in a `mailto:` . For example:
> 
> ```
>  MyCustomScript/1.0 (https://mycustomscript.org; mailto:youremail@example.com)
> ```
> 
> This information helps DataCite communicate about issues and changes and troubleshoot problems.

### Selecting an API

> 👍 For new integrations, we recommend using the [DataCite REST API](doc:api).

The [DataCite REST API ](doc:api)is our primary API for retrieving, registering, and updating DOIs and associated metadata. Authentication is required for creating and updating DOIs. 

We recommend reviewing our [REST API Reference](ref:introduction) to understand the types of requests your integration can make. Integrations primarily use these requests in the  “dois” section:

- [Add a new DOI (POST)](ref:post_dois)
- [Update a DOI (PUT)](ref:put_dois-id)

The [DataCite MDS API ](doc:mds-api-guide) is also used to register DOIs and associated metadata. However, we don’t recommend it for new integrations.

### Authenticating with a Repository account

An integration must enable authentication using **Repository credentials**. A Repository is a type of account in DataCite systems and is the only account type that can register DOIs and manage DOI metadata. Repositories represent a store where all the DOIs for a group of resources are registered and will stay together.

A Repository has its own set of credentials and one prefix for DOI registration. The Repository account ID includes the ID of the associated Direct Member or Consortium Organization.

Example of a Repository account ID:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8b929b3-Screenshot_2022-11-16_at_15.45.45.png",
        "Screenshot 2022-11-16 at 15.45.45.png",
        378
      ],
      "align": "center",
      "caption": "Example Repository ID: DATACITE.QYACAZ"
    }
  ]
}
[/block]


DataCite users wishing to register and update DOIs and metadata via the APIs must use their Repository account credentials or [an API key corresponding to a Repository account](doc:api-keys). Users may wish to use either with an integration, so we recommend supporting Repository account credentials at minimum or both Repository account credentials and API keys. A Direct Member, Consortium, or Consortium Organization account cannot register DOIs or update DOI metadata.

A single organization (DataCite Member or Consortium Organization) can have multiple Repository accounts that can be used to create DOIs. Each Repository account has a separate set of credentials.

### Reserving a DOI

The DataCite APIs allow the creation of Draft records. Draft records are useful in cases where a user wants to “reserve” a DOI name for later use. Unlike DOIs in Registered or Findable State, Draft records can be deleted and are not resolvable. If your implementation makes use of Draft records, the submitted metadata will be part of the DataCite Repository account.

You are not required to make use of DataCite’s Draft state. Some platforms choose to implement a similar feature locally, where they “reserve” a specific DOI in advance of registering it. However, we highly recommend using the Draft state for both troubleshooting and for preventing accidental DOI creation.

We recommend reviewing our documentation on [DOI States](doc:doi-states) (even if you don’t plan to use the Draft state), which covers the differences between the Findable, Registered, and Draft states.

### Registering a DOI

A DOI should be registered at the same time the metadata record in your platform is published.

- If your platform is not using the Draft state, you can create a Findable DOI by including the “event”: “publish” in your initial request to [add a new DOI](ref:post_dois).
- If your platform is using the Draft state, you can register the DOI by [sending an update](ref:put_dois-id) to change the state to Findable.

For more detail on how to register a DOI, see [Creating DOIs with the REST API](doc:api-create-dois).

### Updating a DOI

When local metadata in your platform is updated, we recommend updating DOI metadata shortly after. You can either send the complete metadata (including the change), or only the properties that are changing.

Only send requests for DOIs that require updates. This means that unless your local repository metadata has changed for a given DOI, please don’t send us an update with the same metadata. (If you don’t have a way to detect local metadata changes when they happen, and need to send updates for all of your DOIs together regardless of whether the metadata will change, please do this at most once per day.)

For more detail on how to update a DOI, see [Updating metadata with the REST API](doc:updating-metadata-with-the-rest-api).

### Testing your integration

> 👍 All integrations should be tested using the DataCite test system.

Integrations should be tested using the DataCite test system. This means using a different API endpoint (<https://api.test.datacite.org>) and a different set of credentials that is specific to the test system.

For more information on testing, including how to get a test account, please see the [Testing Guide](doc:testing-guide) and [Test Accounts Policy](doc:test-accounts-policy).

We ask that you only use the test system for testing your integration. If you have a separate sandbox instance for your platform, we recommend not having your DataCite test account connected to your sandbox except when you are actively testing the DataCite integration functionality.

### Interpreting error codes

A successful request to create or update a DOI will return a 200 or 201 status code. If something went wrong, you’ll receive an error code instead. 

For errors in the 4xx range, integrations should attempt to resolve the source of the error before resending the request. Depending on the error code, this could be incorrect credentials, specifying the wrong prefix, invalid metadata, or attempting to update a DOI that does not yet exist. Our list of [error codes](doc:api-error-codes) outlines some possible solutions, depending on the code.

For errors in the 5xx range, integrations should wait before retrying the request. We recommend attempting retries with an exponential backoff (e.g., 1s, 2s, 4s…). If you keep getting the same 5xx error, please check our [status page](https://status.datacite.org/) and send us an email at [support@datacite.org](mailto:support@datacite.org) if you don’t see anything there.

### Request frequency

Our firewall imposes a rate limit of 3,000 requests per 5 minute window per IP address for all of our APIs.

On our test system, please do not exceed 750 requests per 5 minute window. See the [Test Accounts Policy](doc:test-accounts-policy) for more information.

### Other best practices

We recommend that all integrations follow our [Best Practices for DOI Registration](doc:best-practices-for-datacite-members), which include guidelines for landing pages, displaying DOIs, versioning, and other topics.

## Considerations for Prospective Service Providers

Integrations which are developed for a platform that is used by more than one organization may meet criteria for the DataCite [Service Provider Program](doc:datacite-service-providers). A Service Provider is an organization that has integrated with one of the DataCite APIs to enable other organizations to register DataCite DOIs.

DataCite Service Providers do not offer DOIs, but do offer DataCite Members and Consortium Organizations the ability to register DOIs through their platform. Members and Consortium Organizations register DOIs using their own Repository account credentials. This means that integrations supported by Service Providers must provide users a secure means of entering their own Repository account credentials or [API keys](doc:api-keys).

If you are interested in joining the program or learning more, please contact us at [support@datacite.org](mailto:support@datacite.org).

## Checklist for new integrators

- [ ] Use the [DataCite REST API ](doc:api) to create and update DOIs.
- [ ] Enable authentication using Repository credentials.
- [ ] Reserve a DOI name for unpublished records, either by using a [Draft record](doc:doi-states) or by reserving the name locally.
- [ ] Register a new DOI when a metadata record is published for a resource.
- [ ] Update existing DataCite DOI metadata when local record metadata is updated.
- [ ] During development, test your integration using the [DataCite test system](doc:testing-guide).
- [ ] Check for a success or error response when you create or update a DOI.
- [ ] Before retrying a request when you receive an [error code](doc:api-error-codes), build in wait time using an exponential backoff.
- [ ] Follow our general [Best Practices for DOI Registration](doc:best-practices-for-datacite-members).
- [ ] Consider joining the DataCite [Service Provider Program](doc:datacite-service-providers) if your integration is used by more than one organization.

> 📘 
> 
> If you have feedback or questions on this guide, please contact us at [support@datacite.org](mailto:support@datacite.org).
