---
layout: page
title: Source Code
permalink: /source-code/
menuInclude: yes
menuLink: yes
menuTopTitle: Source
menuTopIndex: 4
menuSubTitle: Source-code overview
menuSubIndex: 1
---

The FOLIO platform consists of both server-side and client-side components, and
will grow to include library services that run on the platform as modules.
Some sample modules are located in
[folio-sample-modules](https://github.com/folio-org/folio-sample-modules).

Several repositories in the [folio-org GitHub
organization](https://github.com/folio-org) host the core project code.
Third-party modules may be hosted elsewhere.

A good starting point for understanding the FOLIO code is
[Okapi](https://github.com/folio-org/okapi) -- specifically the
[Okapi Guide and Reference](https://github.com/folio-org/okapi/blob/master/doc/guide.md), which
introduces the concepts and architecture of the FOLIO platform, and includes
installation instructions and examples.  Okapi is the central hub for
applications running on the FOLIO platform and enables access to other modules
in the architecture.

The FOLIO system is made up of the code in several GitHub repositories.
Each repository contains the code for a single well-defined element of the
system. These repositories fall into three categories:

- _server-side elements_ that provide services and the
  infrastructure that they run on;
- _client-side elements_ that provide a
  framework for using those services from a Web browser;
- and a few that fall into neither of these categories.

**PLEASE NOTE** that this is a technology preview following the [release early,
release often](https://en.wikipedia.org/wiki/Release_early,_release_often)
philosophy.  **We want your feedback** in the form of pull requests and filed
issues and general discussion via the
[collaboration tools](/community).

## Server-side

The key server-side element is Okapi itself: the FOLIO middleware component
that acts as a gateway for access to all modules, handling redundancy,
sessions, etc.  Individual modules are provided in their own repositories, each
named `mod-`_name_ (note that these are mostly at the proof-of-concept stage).
Each module has its own documentation.

Some of these modules are built from specifications in
[RAML](http://raml.org/), the RESTful API Modeling Language: this process is
facilitated by the code in the `raml-module-builder` repository.

- [okapi](https://github.com/folio-org/okapi)
  -- Okapi API Gateway proxy/discovery/deployment service.

- [raml](https://github.com/folio-org/raml)
  -- Repository of RAML files, including JSON Schemas, traits and
  resource types centralized for re-usability.
  The [API reference](/reference/api/) documentation is also
  generated.
  This repository is the master location for the traits and resource
  types, while each module is the master for its own schemas, examples,
  and actual RAML files.
  It is included in other repositories via a git sub-module, usually called `raml-util`.

- [raml-module-builder](https://github.com/folio-org/raml-module-builder)
  -- Framework facilitating easy module creation based on RAML files.

- [mod-configuration](https://github.com/folio-org/mod-configuration)
  -- Configuration module based on the raml-module-builder and a set
  of RAML and JSON Schemas backed by a PostgreSQL asynchronous implementation.

- [mod-authtoken](https://github.com/folio-org/mod-authtoken)
  -- Filtering requests based on JWT tokens.

- [mod-login](https://github.com/folio-org/mod-login)
  -- Handles username/password login.

- [mod-login-saml](https://github.com/folio-org/mod-login-saml)
  -- Handles SAML login.

- [mod-password-validator](https://github.com/folio-org/mod-password-validator)
  -- Performs password validation and stores validation rules for specified tenant.

- [mod-permissions](https://github.com/folio-org/mod-permissions)
  -- Handles permissions and permissions/user associations.

- [mod-users](https://github.com/folio-org/mod-users)
  -- Provides user management.

- [mod-users-bl](https://github.com/folio-org/mod-users-bl)
  -- Business logic "join" module to provide simple access to all
  user-centric data.

- [mod-user-import](https://github.com/folio-org/mod-user-import)
  -- Importing new or already existing users into FOLIO.

- [mod-inventory](https://github.com/folio-org/mod-inventory)
  -- Provides basic physical item inventory management.

- [mod-inventory-storage](https://github.com/folio-org/mod-inventory-storage)
  -- Persistent storage to complement the inventory module.

- [mod-circulation](https://github.com/folio-org/mod-circulation)
  -- Circulation capabilities, including loan items from the inventory.

- [mod-circulation-storage](https://github.com/folio-org/mod-circulation-storage)
  -- Persistent storage to complement the circulation module.

- [mod-calendar](https://github.com/folio-org/mod-calendar)
  -- Provide calendar functionality.

- [mod-feesfines](https://github.com/folio-org/mod-feesfines)
  -- Provide central management for fees and fines.

- [mod-datasets](https://github.com/folio-org/mod-datasets)
  -- Wrapper for running a Glint server as an Okapi module.

- [mod-graphql](https://github.com/folio-org/mod-graphql)
  -- Executing GraphQL queries.

- [mod-kb-ebsco](https://github.com/folio-org/mod-kb-ebsco)
  -- Broker communication with the EBSCO knowledge base.

- [mod-kb-ebsco-java](https://github.com/folio-org/mod-kb-ebsco-java)
  -- Broker communication with the EBSCO knowledge base.

- [mod-notes](https://github.com/folio-org/mod-notes)
  -- Notes on all types of objects.

- [mod-notify](https://github.com/folio-org/mod-notify)
  -- Notifications to the users.

- [mod-sender](https://github.com/folio-org/mod-sender)
  -- Intermediary for sending prepared messages through appropriate delivery channels.

- [mod-email](https://github.com/folio-org/mod-email)
  -- Provides functionality for sending notifications.

- [mod-event-config](https://github.com/folio-org/mod-event-config)
  -- Provides functionality for the notification events.

- [mod-codex-mux](https://github.com/folio-org/mod-codex-mux)
  -- Codex Multiplexer.

- [mod-codex-mock](https://github.com/folio-org/mod-codex-mock)
  -- Codex mock module - for testing and development.

- [mod-codex-ekb](https://github.com/folio-org/mod-codex-ekb)
  -- Codex wrapper for the EBSCO knowledge base.

- [mod-codex-inventory](https://github.com/folio-org/mod-codex-inventory)
  -- Codex wrapper for local inventory.

- [mod-marccat](https://github.com/folio-org/mod-marccat)
  -- Metadata management and cataloging (MARCcat).

- [acq-models](https://github.com/folio-org/acq-models)
  -- Shared repository for the models of the various acquisition modules.

- [mod-finance](https://github.com/folio-org/mod-finance)
  -- Finance business logic.

- [mod-finance-storage](https://github.com/folio-org/mod-finance-storage)
  -- Persistent storage of finance-related data (i.e. funds, ledgers, transactions, etc.).

- [mod-orders](https://github.com/folio-org/mod-orders)
  -- Orders business logic.

- [mod-orders-storage](https://github.com/folio-org/mod-orders-storage)
  -- Persistent storage of order data.

- [mod-patron](https://github.com/folio-org/mod-patron)
  -- Allow 3rd party discovery services to perform FOLIO patron actions via the discovery service's UI.

- [mod-rtac](https://github.com/folio-org/mod-rtac)
  -- Real Time Availability Check.
  Enable third party discovery services to check for FOLIO inventory availability.

- [mod-tags](https://github.com/folio-org/mod-tags)
  -- Central list of tags that can be assigned to various objects.

- [mod-template-engine](https://github.com/folio-org/mod-template-engine)
  -- Stores templates and generates files by using them.

- [mod-data-import](https://github.com/folio-org/mod-data-import)
  -- Data import.

- [mod-source-record-storage](https://github.com/folio-org/mod-source-record-storage)
  -- Persistent source record storage. Complements the data import module.

- [mod-source-record-manager](https://github.com/folio-org/mod-source-record-manager)
  -- Source record manager.

- [mod-vendors](https://github.com/folio-org/mod-vendors)
  -- Persistent storage of vendor data.

- [mod-agreements](https://github.com/folio-org/mod-agreements)
  -- Electronic resource management (ERM)

- [mod-erm-usage](https://github.com/folio-org/mod-erm-usage)
  -- Gather and store ERM usage statistics.

- [mod-licenses](https://github.com/folio-org/mod-licenses)
  -- Upload, manage and analyze licenses.

- [mod-gobi](https://github.com/folio-org/mod-gobi)
  -- Allows GOBI® (Global Online Bibliographic Information) initiated orders to be fulfilled by FOLIO.

- [mod-oai-pmh](https://github.com/folio-org/mod-oai-pmh)
  -- Open Archives Initiative Protocol for Metadata Harvesting (OAI-PMH).

- [mod-workflow](https://github.com/folio-org/mod-workflow)
  -- Workflow proof-of-concept. With related modules:
  [mod-camunda](https://github.com/folio-org/mod-camunda),
  [spring-module-core](https://github.com/folio-org/spring-module-core),
  [mod-spring-sample](https://github.com/folio-org/mod-spring-sample).

- [mod-audit](https://github.com/folio-org/mod-audit)
  -- Manage audit data.

- [mod-audit-filter](https://github.com/folio-org/mod-audit-filter)
  -- Implements Okapi PRE and POST filters to capture audit data.

- [mod-aes](https://github.com/folio-org/mod-aes)
  -- Provide asynchronous event service (AES).

- [mod-rmb-template](https://github.com/folio-org/mod-rmb-template)
  -- A Maven archetype to commence a new RMB-based module.

- [mod-pg-embed](https://github.com/folio-org/mod-pg-embed)
  -- Helper module to start embedded Postgres.
  Helper for developers that starts the "embedded" postgres server and sets up the environment so that other modules can locate the database.

- [mod-data-loader](https://github.com/folio-org/mod-data-loader)
  -- RMB-based module used to load test data.
  Currently supports loading binary MARC records into the mod-inventory-storage instance table.

- [inventory-sample-data](https://github.com/folio-org/inventory-sample-data)
  -- Provides scripts for data preparation and deployment, e.g. MARC.

- [edge-common](https://github.com/folio-org/edge-common)
  -- Common/Shared library for Edge APIs.

- [edge-oai-pmh](https://github.com/folio-org/edge-oai-pmh)
  -- Edge API for Metadata Harvesting.

- [edge-orders](https://github.com/folio-org/edge-orders)
  -- Edge API to interface with FOLIO for 3rd party ordering services and FOLIO.
  Initially GOBI.

- [edge-patron](https://github.com/folio-org/edge-patron)
  -- Edge API to interface with FOLIO for 3rd party discovery services to allow patrons to perform self-service actions.

- [edge-resolver](https://github.com/folio-org/edge-resolver)
  -- Edge API to bridge the gap between external reporting and analytics systems and FOLIO by allowing these systems to resolve FOLIO UUIDs, such as a FOLIO user id, thereby acquiring a richer set of data.

- [edge-rtac](https://github.com/folio-org/edge-rtac)
  -- Edge API for RTAC (Real Time Availability Check).
  To interface with FOLIO for 3rd party discovery services to determine holdings availability.

## Client-side

Since Okapi represents all the FOLIO functionality as well-behaved web
services, UI code can, of course, be written using any toolkit. However,
we will provide Stripes, a toolkit optimized for accessing Okapi-based
services and wrapping UI functionality into convenient modules. We
envisage that most FOLIO UI work will be done in the context of
Stripes.

The stripes [documentation](https://github.com/folio-org/stripes/blob/master/README.md) is the starting point.
Each module has its own documentation.

Note that Stripes is still in the design phase, so although code
exists and can be run, the APIs are likely to change.

- [stripes](https://github.com/folio-org/stripes)
  -- The Stripes Framework.
  UI framework for building front-end FOLIO modules.
  Includes extensive documentation.

- [stripes-core](https://github.com/folio-org/stripes-core)
  -- The core of the Stripes/UI framework.

- [stripes-components](https://github.com/folio-org/stripes-components)
  -- A component library for Stripes.
  Includes documentation for each library, and guides to assist their development.

- [stripes-smart-components](https://github.com/folio-org/stripes-smart-components)
  -- A suite of smart components. Each communicates with an Okapi web-service in order to provide the facilities that it renders.

- [stripes-util](https://github.com/folio-org/stripes-util)
  -- A library of utility functions to support Stripes modules.

- [stripes-connect](https://github.com/folio-org/stripes-connect)
  -- Manages the connection of UI components to back-end modules.

- [stripes-form](https://github.com/folio-org/stripes-form)
  -- A redux-form wrapper for Stripes.

- [stripes-logger](https://github.com/folio-org/stripes-logger)
  -- Simple category-based logging for Stripes.

- [stripes-cli](https://github.com/folio-org/stripes-cli)
  -- Command-line interface for creating, building, and testing Stripes UI modules.

- [ui-users](https://github.com/folio-org/ui-users)
  -- Stripes UI module: administrating users.

- [ui-inventory](https://github.com/folio-org/ui-inventory)
  -- Stripes UI module: administrating locally created instances, holdings records and items.

- [ui-requests](https://github.com/folio-org/ui-requests)
  -- Stripes UI module: making requests on items.

- [ui-calendar](https://github.com/folio-org/ui-calendar)
  -- Stripes UI module: institutional calendar functions.

- [ui-checkin](https://github.com/folio-org/ui-checkin)
  -- Stripes UI module: checking in items with simulated scans.

- [ui-checkout](https://github.com/folio-org/ui-checkout)
  -- Stripes UI module: checking out items with simulated scans.

- [ui-circulation](https://github.com/folio-org/ui-circulation)
  -- Stripes UI module: Circulation.

- [ui-datasets](https://github.com/folio-org/ui-datasets)
  -- Stripes UI module: FOLIO Datasets based on Glint.

- [ui-data-import](https://github.com/folio-org/ui-data-import)
  -- Stripes UI module: Managing batch data loader.

- [ui-marccat](https://github.com/folio-org/ui-marccat)
  -- Stripes UI module: searching, sorting, filtering, viewing, editing and creating BIB record.

- [ui-orders](https://github.com/folio-org/ui-orders)
  -- Stripes UI module: Orders.

- [ui-receiving](https://github.com/folio-org/ui-receiving)
  -- Stripes UI module: Receiving.

- [ui-eholdings](https://github.com/folio-org/ui-eholdings)
  -- Stripes UI module: E-holdings.

- [ui-agreements](https://github.com/folio-org/ui-agreements)
  -- Stripes UI module: Electronic resource management (ERM).

- [ui-erm-usage](https://github.com/folio-org/ui-erm-usage)
  -- Stripes UI module: Managing ERM usage statistics.

- [ui-licenses](https://github.com/folio-org/ui-licenses)
  -- Stripes UI module: Upload, manage and analyze licenses.

- [ui-search](https://github.com/folio-org/ui-search)
  -- Stripes UI module: searching, sorting, filtering and viewing records from the FOLIO Codex, an aggregation of bibliographic metadata from multiple sources.

- [ui-organization](https://github.com/folio-org/ui-organization)
  -- Stripes UI module: managing organization settings.

- [ui-myprofile](https://github.com/folio-org/ui-myprofile)
  -- Stripes UI module: managing user profile settings.

- [ui-tags](https://github.com/folio-org/ui-tags)
  -- Stripes UI module: managing tag settings.

- [ui-finance](https://github.com/folio-org/ui-finance)
  -- Stripes UI module: management of ledgers, funds, and budgets.

- [ui-servicepoints](https://github.com/folio-org/ui-servicepoints)
  -- Stripes UI module: Service Points handler.

- [ui-vendors](https://github.com/folio-org/ui-vendors)
  -- Stripes UI module: Vendors.

- [ui-audit](https://github.com/folio-org/ui-audit)
  -- Stripes UI module: Viewing audit trails.

- [ui-plugin-find-user](https://github.com/folio-org/ui-plugin-find-user)
  -- Stripes UI plugin: User finder.

- [ui-plugin-find-instance](https://github.com/folio-org/ui-plugin-find-instance)
  -- Stripes UI plugin: Instance finder.

- [ui-plugin-find-vendor](https://github.com/folio-org/ui-plugin-find-vendor)
  -- Stripes UI plugin: Vendor finder.

- [ui-trivial](https://github.com/folio-org/ui-trivial)
  -- Stripes UI module: example application.

- [ui-developer](https://github.com/folio-org/ui-developer)
  -- Stripes UI module: developer facilities,
  e.g. managing local developer settings.

- [eslint-config-stripes](https://github.com/folio-org/eslint-config-stripes)
  -- The shared eslint configuration for stripes applications and extensions.

- [okapi-stripes](https://github.com/folio-org/okapi-stripes)
  -- Server-side module for generating UIs based on Stripes.

- [platform-complete](https://github.com/folio-org/platform-complete)
  -- Stripes platform: Complete.

- [platform-core](https://github.com/folio-org/platform-core)
  -- Stripes platform: Core.

- [platform-erm](https://github.com/folio-org/platform-erm)
  -- Stripes platform: ERM.

- [folio-testing-platform](https://github.com/folio-org/folio-testing-platform)
  -- Stripes platform: Testing.

- [stripes-sample-platform](https://github.com/folio-org/stripes-sample-platform)
  -- Configuration for a sample platform and to run a local
  Stripes UI development server.

- [stripes-demo-platform](https://github.com/folio-org/stripes-demo-platform)
  -- Stripes platform for building the demo site.

- [stripes-testing](https://github.com/folio-org/stripes-testing)
  -- Toolkit for running tests against Stripes UI modules and platforms.

- [stripes-experiments](https://github.com/folio-org/stripes-experiments)
  -- Testing ground for prototype modules that may form part of
  Stripes.

## Other projects

- [folio-sample-modules](https://github.com/folio-org/folio-sample-modules)
  -- Various sample modules, illustrating ways to structure a module for
  use with Okapi (e.g. `hello-vertx` and `simple-vertx` and `simple-perl`).

- [folio-ansible](https://github.com/folio-org/folio-ansible)
  -- Sample Ansible playbook and roles for FOLIO (and Vagrant).
  Get a FOLIO installation up and running quickly.
  Read the docs there, and follow to build the boxes.
  The current built boxes are also available to download from
  [Vagrant Cloud](https://app.vagrantup.com/folio).

- [folio-install](https://github.com/folio-org/folio-install)
  -- Runbooks for FOLIO installation, including [step-by-step instructions for a single-server deployment](https://github.com/folio-org/folio-install/blob/master/single-server.md).

- [folio-tools](https://github.com/folio-org/folio-tools)
  -- Various tools and support glue for FOLIO CI.

- [okapi-cli](https://github.com/folio-org/okapi-cli)
  -- Okapi command-line interface.

- [okapi.rb](https://github.com/thefrontside/okapi.rb)
  -- Ruby client to communicate with an Okapi cluster.

- [cql2pgjson-java](https://github.com/folio-org/cql2pgjson-java)
  -- [CQL](/reference/glossary/#cql) (Contextual Query Language) to PostgreSQL JSON converter in Java.

- [folio-graphiql](https://github.com/folio-org/folio-graphiql)
  -- Explore Okapi's GraphQL endpoint.

- [folio-perf-test](https://github.com/folio-org/folio-perf-test)
  -- Jenkins pipeline to test FOLIO performance.

- [folio-api-tests](https://github.com/folio-org/folio-api-tests)
  -- Postman collections for backend modules.

- [ldp](https://github.com/folio-org/ldp)
  -- Library Data Platform.

- [rfcs](https://github.com/folio-org/rfcs)
  -- RFCs for changes to the FOLIO platform.
  "Request for Comment" for "substantial" changes.
  Co-ordinated through the [FOLIO Technical Council](https://wiki.folio.org/display/TC/Technical+Council).

- [folio-org.github.io](https://github.com/folio-org/folio-org.github.io)
  -- The source for this dev.folio.org website.
