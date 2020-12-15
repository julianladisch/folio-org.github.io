---
layout: page
title: Assess API definitions, schema, and examples
permalink: /guides/api-lint/
menuInclude: no
menuTopTitle: Guides
---

## Introduction

For server-side projects that utilise RAML or OpenAPI (OAS), use the tool `api-lint` to assess the API definition files and schema and examples.

The tool is available for use during FOLIO Continuous Integration builds, and also for local use prior to commit.

For [RAML-using](/start/primer-raml/) projects, this new "api-lint" tool is preferred. The previous tool "[lint-raml](/guides/raml-cop/)" is still available. However its behind-the-scenes technology is outdated.

## Procedure

Each discovered API definition file is provided to the nodejs script.

That utilises the AML Modeling Framework [AMF](https://github.com/aml-org/amf), specifically the `amf-client-js` library, to parse and validate the definition.

## Usage

For use during FOLIO CI builds, refer to the Jenkinsfile [configuration](#jenkinsfile) below.

For local use, clone the "[folio-tools](https://github.com/folio-org/folio-tools)" repository parallel to clones of back-end project repositories, and use its [api-lint](https://github.com/folio-org/folio-tools/tree/master/api-lint) facilities.
Refer to that document for local installation instructions.

### Python

The Python script will search the configured directories to find relevant API definition files, and will then call the node script to process each file.

Where the main options are:

* `-t,--types` -- The type of API definition files to search for.
  Required. Space-separated list.
  One or more of: `RAML OAS`
* `-d,--directories` -- The list of directories to be searched.
  Required. Space-separated list.
* `-e,--excludes` -- List of additional sub-directories and files to be excluded.
  Optional. Space-separated list.
  By default it excludes certain well-known directories (such as `raml-util`).
  Use the option `--loglevel debug` to report what is being excluded.

See help for the full list:

```
python3 ../folio-tools/api-lint/api_lint.py --help
```

Example for RAML:

```
cd $GH_FOLIO/mod-notes
python3 ../folio-tools/api-lint/api_lint.py \
  -t RAML \
  -d ramls
```

Example for both RAML and OpenAPI (OAS), i.e. when preparing for transition:

```
cd $GH_FOLIO/mod-foo
python3 ../folio-tools/api-lint/api_lint.py \
  -t RAML OAS \
  -d ramls src/main/resources/oas
```

### Node

The node script can also be used stand-alone to process a single file.

See usage notes with: `node amf.js --help`

### Jenkinsfile

To use "api-lint" with FOLIO Continuous Integration, add this configuration to the project's Jenkinsfile:

```
buildMvn {
...
  doApiLint = true
  apiTypes = 'RAML' // Required. Space-separated list: RAML OAS
  apiDirectories = 'ramls' // Required. Space-separated list
  apiExcludes = 'types.raml' // Optional. Space-separated list
```

Examples:

* [mod-tags](https://github.com/folio-org/mod-tags/blob/master/Jenkinsfile)
  -- RAML

## Interpretation of messages

When errors are encountered, then a summary of conformance "Violations" and "Warnings" is presented at the top, followed by detail about each.
The detail includes the location of the relevant file and the line number of the problem.

Note that if there are only warnings but no violations, then nothing is presented.

Note that this `api-lint` tool is more thorough than our previous CI tool (based on raml-cop and its underlying raml-1-parser).
So projects might find new violations being reported.
