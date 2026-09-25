---
title: DataCite Monthly Data File
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
The DataCite Monthly Data File contains metadata for all publicly available DataCite DOIs registered up to the end of the last month. The data file is distributed via AWS S3 and is currently available to all DataCite Members and Consortium Organizations.

Each month, DataCite generates a new monthly data file containing metadata for all DataCite DOIs, including those recently registered or updated. Each monthly data file is generated within the first few days of the month and replaces the last.

All metadata contained in the file is freely available under a CC0 waiver. For more information, see the [DataCite Data File Use Policy](doc:datacite-data-file-use-policy).

## Contents of the Monthly Data File

### Directory structure

The monthly data file contains a top-level `dois` folder. The `dois` folder contains a series of folders named with an `updated_YYYY-MM` convention. Each of these folders contains:

1. All Findable DataCite DOI records updated during the corresponding month (at the time the monthly data file was generated).
2. Tabular report for the corresponding month. 

The directory structure looks like this:

```
dois
├── updated_2024-07
│   ├── 2024-07.csv.gz
│   ├── part_0000.jsonl.gz
│   ├── part_0001.jsonl.gz
│   ├── part_0002.jsonl.gz
├── updated_2024-08
... ├── 2024-08.csv.gz
    ├── part_0000.jsonl.gz
    ├── part_0001.jsonl.gz
    ├── part_0002.jsonl.gz
    ├── part_0003.jsonl.gz
    ...
```

### DataCite DOI records

DataCite DOI records are compressed in a series of gzip files within each  `updated_YYYY-MM` folder. Each gzip file contains up to 10,000 DataCite DOI records in JSON Lines format. The `.gz` files are named with a `part_[four-digit part number].jsonl.gz` convention. 

#### What DataCite DOI records are included?

The monthly data file contains a record of every Findable state DOI at the time the file was generated. Each record is represented once in a folder corresponding to the month the DOI was last updated. 

#### What is the format of individual records?

The format of individual records in the file will reflect [a DOI singleton response from the DataCite REST API](https://support.datacite.org/docs/api-get-doi#response) with the following adjustments:

- The records contain additional affiliation and publisher metadata returned when the following REST API URL parameters are set: `affiliation=true` and `publisher=true`. See [Can I see more detailed affiliation and publisher information in the REST API?](doc:can-i-see-more-detailed-affiliation-information-in-the-rest-api) for more details.
- The records do not contain the `xml` attribute. 

### Tabular reports

Each  `updated_YYYY-MM` folder contains a tabular report in CSV format, compressed with gzip, that contains:

- A list of all registered DataCite DOIs (in Findable or Registered state) updated during the corresponding month at the time the file was generated
- The date they were updated
- Their current state (`findable` or `registered`)
- Their current Repository ID.

Rows in the CSV file are structured like the following:

| doi                               | state      | client_id    | updated              |
| --------------------------------- | ---------- | ------------ | -------------------- |
| 10.0166/fk2.stagefigshare.9753211 | findable   | figshare.dud | 2024-08-01T00:20:45Z |
| 10.15493/dea.mims.20210317        | registered | nrf.saeon    | 2024-08-01T00:32:57  |

Registered state DOIs are included to identify [DOIs that are no longer publicly available](https://support.datacite.org/docs/doi-states#registered-doi-name) . Repository IDs aid in identifying DOIs that have moved between repositories.

### MANIFEST files

The root of the S3 bucket contains two manifest files, one called `MANIFEST` and one called `MANIFEST.json`, both of which contains a list of all the files in the bucket, their size in bytes, and an SHA-256 checksum of the file contents.

The `MANIFEST` file is plain text, and the fields are separated by a whitespace character. For example:

```
dois/updated_2011-03/part_0000.jsonl.gz 41 2/YPZ3bPUHVfdgVK0DR/91/mZP9PzN9HrOXI9MxAzHQ=
dois/updated_2011-03/2011-03.csv.gz 375 oSaWWfhPoMnQAyJxi/pYP5CSbzQ4zownJwypHO6/IUc=
dois/updated_2011-04/part_0000.jsonl.gz 668 UZzfRjVOkgA6JphWYmQJ02Jhky3iVuOa2BiNQGYJmAc=
dois/updated_2011-04/2011-04.csv.gz 154 aHOpSku+DgXBj9X2WOskv2Akj8Q8S1iLozca2wSH+Og=
...
```

The `MANIFEST.json` file contains a JSON array of dictionaries, one per file, with the fields keyed. For example:

```json
[
  {
    "filename": "dois/updated_2011-03/part_0000.jsonl.gz",
    "size": 41,
    "sha256": "2/YPZ3bPUHVfdgVK0DR/91/mZP9PzN9HrOXI9MxAzHQ="
  },
  {
    "filename": "dois/updated_2011-03/2011-03.csv.gz",
    "size": 375,
    "sha256": "oSaWWfhPoMnQAyJxi/pYP5CSbzQ4zownJwypHO6/IUc="
  },
  // ...
]
```

These files can be used to generate the S3 URLs for individual files without needing to recursively list the contents.

### STATUS file

The root of the S3 bucket also contains a simple indicator of the status of the data file generation process called`STATUS.json`. You can use this to check if each monthly release is complete and ready for consumption.

This file contains a JSON dictionary with three keys, `month` (the "version" of the data file in `YYYY-MM` format), `datetime` (the timestamp of the status), and `status` (either "In progress", "Uploading", or "Complete"):

```json
{
  "month": "2026-02",
  "datetime": "2026-03-01T07:53:35.713625+00:00",
  "status": "Complete"
}
```

## Access the Monthly Data File

This service is currently available to all DataCite Members and Consortium Organizations, who can use their existing Member, Consortium Organization, or Repository credentials to authenticate and download the contents of the data file. [API keys](doc:api-keys) can also be used for authentication.

### Access credentials

To obtain a set of AWS credentials permitting access to the S3 bucket, you must make an authenticated HTTP GET request to the DataCite REST API using your existing Member, Consortium Organization, or Repository credentials. [API keys](doc:api-keys) can also be used.

Here is an example curl command to retrieve AWS credentials: 

```shell
curl --user YOUR_ACCOUNT_ID:YOUR_PASSWORD https://api.datacite.org/credentials/datafile
```

This endpoint will return the three parts of the AWS credentials required: the access key ID, the secret access key, and the session token. All three parts must be supplied in your subsequent requests to the S3 bucket.

By default, the response is a JSON object, but a preconfigured AWS Credential block suitable for use with the AWS CLI can be accessed by appending `?format=text` to the request URL, or by passing an HTTP Accept header of `text/plain`.

Issued credentials are temporary and valid for one hour. If you require access beyond this, you must request a new set of credentials from the DataCite REST API.

### Data file location

The monthly data file is stored in an Amazon S3 bucket with the following bucket name: `s3://monthly-datafile.datacite.org`.

### Using the credentials

Once you have obtained a set of temporary access credentials, you can access the contents of the Data File using the [AWS CLI tools](https://aws.amazon.com/cli/), the [AWS SDK for your chosen language](https://docs.aws.amazon.com/sdkref/latest/), or other tools such as [cURL](https://curl.se) and supplying the credentials. Get started with the guide below.

### Getting started with the Data File using AWS CLI

First, install AWS CLI if you haven’t already: <https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html>

To access the Data File, you will need to retrieve AWS credentials from the DataCite REST API using your Member, Consortium Organization, or Repository credentials. Use a curl command like the following to retrieve AWS credentials from DataCite: 

```shell
curl --user YOUR_ACCOUNT_ID:YOUR_PASSWORD https://api.datacite.org/credentials/datafile?format=text
```

A successful response will look like this:

```text
[datacite-datafile]
aws_access_key_id=EXAMPLE_KEY_ID
aws_secret_access_key=EXAMPLE_SECRET_KEY
aws_session_token=EXAMPLE_SESSION_TOKEN
```

Add these temporary credentials to your AWS credentials file using the following guide: <https://docs.aws.amazon.com/cli/v1/userguide/cli-authentication-short-term.html> You may need to create the credentials file at `~/.aws/credentials` on Linux and macOS systems and `%USERPROFILE%\.aws\credentials` on Windows if it doesn’t exist already. 

Once added to your credentials file, an AWS credential profile named `datacite-datafile` will be available for use with the AWS CLI tools.

Now you can use AWS CLI commands to explore the file and retrieve metadata. Use the following to get a list of all of the folders in the `/dois/` directory:

```shell
aws --profile datacite-datafile s3 ls s3://monthly-datafile.datacite.org/dois/
```

Try downloading the MANIFEST file to the current directory: 

```shell
aws --profile datacite-datafile s3 cp s3://monthly-datafile.datacite.org/MANIFEST ./
```

Try downloading all of the DataCite DOI records created or updated in November 2025 to the current directory:

```shell
aws --profile datacite-datafile s3 cp s3://monthly-datafile.datacite.org/dois/updated_2025-11/ ./ --recursive
```

### Checking the status of the Monthly Data File

If you are using the monthly data file regularly, it can be helpful to know when the updated version is released each month. There are two methods to accomplish this:

#### Inspect the `Last Modified` property of the MANIFEST file

Each month, the MANIFEST file is only created and uploaded after the main data file generation and upload is complete. Therefore, if the last modified date of the MANIFEST file is within the current month, it means that the previous month's data file is released.

Using the AWS CLI tools, you can get the metadata of the MANIFEST file with the `s3api` tool:

```shell
aws --profile datacite-datafile s3api head-object --bucket monthly-datafile.datacite.org --key MANIFEST
```

For example, if the metadata contains `"LastModified": "Sun, 01 Mar 2026 07:53:36 GMT"`, it signifies that the data file for February 2026 is complete and uploaded to the bucket. 

#### Download the `STATUS.json` file

Each month the STATUS.json file is updated after the data file generation is complete, so it can be used to determine if each data file is ready.

Using the AWS CLI tools, you can read the file without storing it locally:

```shell
aws --profile datacite-datafile s3 cp s3://monthly-datafile.datacite.org/STATUS.json -
```

For example, if the file contains `"month": "2026-02"` and `"status": "Complete"`, it signifies that the data file for February 2026 is complete and uploaded to the bucket.

### Other access methods and integration support

There are many other ways to access and work with the Data File using command line tools like AWS CLI as well as AWS SDKs available for Python, Ruby, and other programming languages.

More detailed instructions and example code (including "copy-and-go" code) for each of these pathways can be found in a dedicated GitHub repository: <https://github.com/datacite/datafile-access-examples>.
