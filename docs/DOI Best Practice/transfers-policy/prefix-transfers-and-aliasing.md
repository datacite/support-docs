---
title: Prefix Transfers, DOI Distributed Administation and Aliasing
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
## DataCite's prefix transfers, DOI distributed administration and aliasing policy:

- All transfers must be approved by the Member, by DataCite and the other Registration Agency.
- All DOI metadata must be re-registered with the new RA.
- Prefixes and DOIs belonging to generalist repositories (e.g. Dryad, Figshare, Zenodo) cannot be transferred to a different Registration Agency. 

## DOI Registration Agency (RA) Transfers

It is possible to transfer prefixes (and the associated DOIs) between the different **DOI Registration Agencies (RAs)**. Most transfers are between DataCite and [Crossref](https://www.crossref.org/) or [mEDRA](https://www.meddra.org/).

## Transfer a prefix and DOIs from DataCite to another Registration Agency

This process is coordinated by the new RA to which the prefix will be transferred.

> 👍 
> 
> To transfer a prefix from DataCite to Crossref, please contact Crossref first.

These are the steps to transfer a prefix from DataCite to Crossref:

1. Crossref contact DataCite to request approval.
2. DataCite contact the Member/Consortium Lead to request approval.
3. If the prefix transfer is approved, DataCite will send an official form for the DataCite Member/Consortium Lead to sign.
4. Once the signed form is received, DataCite will contact Crossref to confirm that the request is approved.
5. The DataCite Repository account is deactivated and the transfer can begin.
6. Crossref coordinate the transfer of the prefix with CNRI.
7. Once the prefix is transferred, all existing DOIs must be re-registered in Crossref with Crossref metadata.
8. Crossref send confirmation to DataCite once the DOIs have been re-registered.
9. The prefix is removed from DataCite and the DataCite DOIs are set to [registered state](doc:doi-states).

> 🚧 
> 
> All existing DataCite metadata must be converted into the Crossref metadata format and re-registered with Crossref.

## Transfer a prefix and DOIs from another Registration Agency to DataCite

This is coordinated by DataCite.

> 👍 
> 
> To transfer a prefix from Crossref to DataCite, please contact DataCite first.

These are the steps to transfer a prefix over to DataCite from a different RA. You will be asked to fill in this template:

- Prefix:
- Number of DOIs:
- From (RA agency and specific member):
- To: DataCite
- DataCite Member:
- DataCite Repository:

Once that information is provided, the transfer can be started. These are the steps to complete  
the transfer:

1. DataCite contact the previous registration agency to ask for permission to transfer the prefix and make sure the prefix is only used by that member.
2. DataCite confirm the transfer request to CNRI.
3. CNRI change admin and home the prefix to DataCite (only changing the the admin at this stage).
4. DataCite import the prefix into Fabrica and assign it to a DataCite Repository.
5. The Repository or DataCite Member (re-)register all DOIs and metadata. The Member must let DataCite know once this has been completed.
6. Previous RA performs system updates and cleanup (optional).

> 🚧 
> 
> All existing metadata needs to be re-registered with DataCite. If the number of DOIs to re-register is large, we recommend using the DataCite [REST API](doc:api). There is no charge for re-registering the existing DOIs in DataCite.

## DOI distributed administration

When only a subset of DOIs within a prefix need to be migrated from one Registration Agency (RA) to another RA, DataCite and Crossref members can request DOI distributed administration. Unlike a prefix transfer, this option allows a subset of the DOIs within a prefix assigned to one RA to be managed by the other RA as opposed to all DOIs within a prefix. Unlike aliasing (see [below](doc:prefix-transfers-distributed admin-aliasing#aliasing-dois-between-registration-agencies), the DOI names remain the same and can be cited with the same identifier. Members will still need to coordinate the registration of migrated DOI metadata with the new RA.

> 👍 
>
>  DOI distributed administration is coordinated and set up by the Registration Agency that will hold the new DOIs and is set up by [CNRI](https://www.cnri.reston.va.us/). This is currently only available between DataCite and Crossref DOIs.

These are the steps to set up DOI distributed administration from DataCite to Crossref:

1. Crossref contacts DataCite to request the migration, including the list of DOIs they wish to migrate.
2. DataCite contacts the Member/Consortium Lead that manages the existing DOIs to request approval.
3. The DataCite Member/Consortium Lead will be sent an official form to sign to confirm they approve the distributed administration request.
4. DataCite contacts Crossref to confirm that the migration is approved.
5. Crossref coordinates the next steps with the member on their side.

These are the steps to set up DOI distributed administration from Crossref to DataCite:

1. The DataCite Member/Consortium Lead contacts DataCite to request the migration, including the list of DOIs they wish to migrate.
2. DataCite contacts Crossref to request approval.
3. Once approved, DataCite contacts CNRI to request the migration.
4. DataCite will create draft records for the migrated DOIs for the member to populate with metadata.
5. The member will add the metadata and transition the DOIs to findable state.

## Aliasing DOIs between Registration Agencies

Aliasing is a redirect from one DOI to another - so when you click on DOI A (held by RA 1) it resolves to DOI B (held by RA 2). Aliasing is an additional option when only a subset of DOIs within a prefix need to be migrated from one Registration Agency (RA) to another RA; for example, when an organization wants to manage DOIs with a new RA and their prefix is shared with another organization. Aliasing is normally the last option because it creates more than one DOI name for a given resource, creating problems for citation.

> 👍 
> 
> Aliasing is coordinated and set up by the Registration Agency that will hold the new DOIs and is set up by [CNRI](https://www.cnri.reston.va.us/).

These are the steps to set up aliasing from DataCite to Crossref:

1. Crossref contacts DataCite to request the aliasing.
2. DataCite contacts the Member/Consortium Lead that the existing DOIs belong to request approval.
3. The DataCite Member/Consortium Lead will be sent an official form to sign to confirm they approve the aliasing.
4. DataCite contacts Crossref to confirm that aliasing can be set up.
5. A new set of DOIs are registered in Crossref.
6. Crossref contacts CNRI to request the aliasing.

> ❗️ 
> 
> Aliasing cannot be set up from DOIs that were registered by generalist repositories and platforms in DataCite.

These are the steps to set up aliasing from Crossref to DataCite:

1. The DataCite Member/Consortium Lead contacts DataCite to request the aliasing.
2. DataCite contacts Crossref to request approval.
3. Once approved, the DataCite Member/Consortium Lead coordinates the registration of the new set DOIs in DataCite.
4. The Member/Consortium Lead provides a spreadsheet with a list of the old Crossref DOIs in the left column and the new DataCite DOIs in the right column (the number of DOIs must match exactly).
5. DataCite contacts CNRI to request the aliasing.
6. Once CNRI confirms this is set up there, Crossref DOIs will redirect to the DataCite DOIs.
