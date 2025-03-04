# Confluent Secrets Provider

version 1.0.2, updated December 1, 2021

## Introduction

With a typical Confluent Kafka Platform installation, secrets are stored within that cluster only.

This CSID Accelerator enables use of external third-party systems for securely storing and retrieving key/value pairs, commonly used for passwords, for example.
In some cases, this can be used to store symmetric keys and asymmetric (public/private) keys.

* [Hashicorp Vault](vault)
* [AWS Secrets Manager](aws)
* [Google Secret Manager](gcloud)
* [Microsoft Azure Key Vault](azure)

# Implementation

## How should I implement this library?

A complete setup of Confluent Secrets will go through the following phases:

1.  Installation of the libraries
2.  Creation and installation of the property files
3.  Restart of the components and health check
4.  Test of the added functionality

## Installation: What files do I need, and where do I put them?

The Confluent Secrets Providers Accelerator is provided as Java jar libraries to be installed in your Java class path.

Note: ordering of libraries in Java class path is important.
Accelerator libraries such as this should be loaded first.

Note: it is not recommended to install libraries for multiple components sharing a node (e.g. Schema Registry and Connect).

If necessary, then use separate class paths to be explicit for each component.

## Installation in the Java class path

Using the table below, copy the libraries required by your use case into your existing class path or a new folder.

The class search path (class path) can be set using either the `-classpath` option when calling a JDK tool (the preferred method) or by setting the `CLASSPATH` environment variable.

The `-classpath` option is preferred because you can set it individually for each application without affecting other applications and without other applications modifying its value.

## Installation via the CLI

Update the following with the specific provider to be installed:

```bash
confluent-hub install confluent/csid-config-provider-aws:latest
```

## List of libraries (current version, supports CP 5.5.x and up)

| Required Libraries | Description
| ---- | ----
| csid-config-provider-common-{version}.jar | Main library for secrets provider, required for all use cases

| Optional Libraries | Description
| ---- | ----
| csid-config-provider-aws-{version}.jar | AWS Secrets library for secrets management
| csid-config-provider-azure-{version}.jar | Azure KeyVault library for secrets management
| csid-config-provider-gcloud-{version}.jar | Google Cloud library for secrets management
| csid-config-provider-vault-{version}.jar | Hashicorp Vault library for secrets management

## Releasing

Change the version
```bash
mvn versions:set -DnewVersion=1.0.3-SNAPSHOT
```

Build the packages
```bash
./build.sh
```

Regenerate Documentation
```bash
./update-readme.sh
```

Update licenses
```bash
./update-license.sh
```

## Evaluation Use Disclaimers

This software was developed as a Confluent CSID Accelerator.
For Accelerators, a Confluent Professional Services (PS) engagement investment and agreement may be required to cover the initial implementation, guidance through testing, and to provide additional time to support release/production readiness activities.
This agreement also includes our issuance of a license, and your acceptance of terms and conditions, to install and for usage of the Accelerator software.
Without a license, this software is not intended to be used outside of the examples or have the examples modified.
Confluent retains all intellectual property rights, in and to the Accelerator Software and any changes and other modifications thereto.

Copyright 2021 Confluent Inc.