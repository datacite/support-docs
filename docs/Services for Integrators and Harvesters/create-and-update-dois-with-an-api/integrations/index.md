---
title: What is an Integration?
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
DataCite Members and Consortium Organizations have access to APIs which enable DOI registration. In order to use the APIs, many users take advantage of existing repository integrations or build their own integrations.

DataCite has two main APIs for DOI registration:

- The [DataCite REST API](doc:api) is our primary API for retrieving, registering, and updating DOIs and their associated metadata. Authentication is required for creating and updating DOIs. New integrations should use the REST API. 

- The [DataCite MDS API](doc:mds-api-guide) is also used to register DOIs and their associated metadata.

> 📘 
> 
> If you are developing a new integration, refer to the [Best Practices for Integrators](doc:best-practices-for-integrators) guide.

## Repository accounts

To enable DOI registration, an integration must enable authentication using [Repository credentials](doc:datacite-account-types#repository-account) or [an API key corresponding to a Repository account](doc:api-keys). A Repository is a type of account in DataCite systems and is the only account that can be used to register DOIs. Repositories represent a store where all the DOIs for a group of resources are registered and will stay together. A Repository has its own set of credentials and one prefix for DOI registration.

The Repository account ID includes the ID of the associated Direct Member or Consortium Organization.

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


DataCite users wishing to register and update DOIs and metadata via the APIs or Fabrica must use their Repository account credentials or [an API key corresponding to a Repository account](doc:api-keys).

A single organization (DataCite Member or Consortium Organization) can have multiple Repository accounts that can be used to create DOIs. Each Repository account has a separate set of credentials. 

## Registered Service Provider integrations

DataCite Registered Service Providers are organizations that provide software that integrates with a DataCite API to enable DOI registration for their users. Registered Service Providers maintain [integrations for repository platforms and CRIS systems](https://support.datacite.org/docs/service-provider-software-integrations).

Any organization that wishes to create DOIs through a Registered Service Provider’s integration with a DataCite API will need to use their own Repository account credentials to do so. [API keys](doc:api-keys) can also be used in place of Repository account credentials with integrations. 

## Other platform integrations

In addition to integrations developed and maintained by DataCite Service Providers, there exist other DataCite integrations that are not maintained by an organization participating in our Service Providers program. While these integrations have not been verified by DataCite, they are also an option for registering DOIs.

## Custom integrations

DataCite Members (including Consortia) and Consortium Organizations are welcome to build their own integrations using the DataCite APIs. If there is not an existing integration for the software being used, this is often the best option. 

For new integrations, we recommend using the DataCite REST API over the DataCite MDS API. For more information on the DataCite REST API, see the [REST API Guide](doc:api) and [API Reference](https://support.datacite.org/reference/introduction).

## Integrations in the consortium model

A DataCite Consortium Lead may administer a platform for depositing resources, with an integration with the DataCite API to enable DOI registration for its users. Each organization that wishes to register DOIs on the platform must have their own Repository account credentials.

DataCite Consortium leads administering platforms which meet the [requirements for Registered Service Providers](https://datacite.org/service-provider-program.html) may optionally go through the registration process to become DataCite Service Providers.

> 📘 
> 
> If multiple Repositories within a consortium are registering DOIs through the same repository platform instance, the integration will need to support more than one set of Repository credentials.
> 
> When there is a transition from a single Repository account to a multiple Repository account model, any associated integration must be updated to allow multiple sets of Repository credentials to be used for DOI registration.
