---
id: changelog
title: CHANGELOG
sidebar_label: CHANGELOG
---
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## Unreleased

## 0.8.2 - 21/03/2022

### Fixed

- Prevent status routes to run into the OPA Middleware 

## 0.8.1 - 14/03/2022

### Update

- glogger v2.1.3 that implements `http.Flusher` interface, useful to fix flushing behavior in reverse proxy for streaming APIs

### Fixed

- set reverse proxy flush interval to -1 to fix issues with streaming APIs passing through the container
- Fixed fallback path registration

## 0.8.0 - 08/03/2022

### Added

 - Added `/grant/bindings/resource/{resourceType}` api to handle the grant of a user role on a single resource
 - Added `/revoke/bindings/resource/{resourceType}` api to handle the revoke of a user role on a set resources

## 0.7.0 - 02/03/2022

### Fixed

 - prevent response policy evaluation if API invocation has a status code outside the [200,299] range

### Added

- RBAC now supports standalone mode. The new mode can be set up with the use of `STANDALONE` and `PATH_PREFIX_STANDALONE` environment variables

## 0.6.0 - 17/02/2022

### Changed

- optimized query evaluation with precomputed evaluators

### Fixed

- provide `application/json` Content-Type header when sending error responses
- response policy proper evaluation when the same API has also a request filter policy

## 0.5.0 - 07/02/2022

### Added

- added support for `find_many` builtin in Rego policies

## 0.4.0 - 01/02/2022

### Added

- added support for `find_one` builtin in Rego policies

## 0.3.1 - 31/01/2022

### Changed

- when the filter row query is empty and content-type is application json, the rbac handler return empty array

### Fixed

- supporting OAS with brackets params notation in internal policy resolver

## 0.3.0 - 25/01/2022

### Changed

- Implemented column filtering on response body base on policy evaluation
- refactor: User struct now contains userBindings and Roles
- If no userId header is provided now mongo is not called in order to retrive user bindings and roles.

### Added

- Added `pathParameter` to rego input request.
- routes sorting during registration to prevent pathParams retrieval error
- better business errors for policies evaluation
- support body serialization in Rego input for specific content type and methods
- Removed limitation to dashed routes

## 0.2.0 - 14/01/2022

### Changed

- refactored rowFiltering data structure

### Added

- Added resource field in binding struct.
- support the method all in the manual routes oas file
- rbac service now support row filtering query for mongo forwarded in a custom header to the requested service
- handle path prefix for manual route
- documentation route handled correctly

### BREAKING

- bindings and roles are now given as input to the OPA evaluator. The old check on user permission is no more performed and the entire ownership is given to rego

### Updated

- OPA v0.36.0

## 0.1.0 - 17/12/2021

### Changed

- Convert API path with variables according the gorilla mux requirements
- Support dot character as divider in the x-permission string, replaced as underscore for rego policy query
- ignoring healthiness routes when defining proxied routes

### Added

- Added the check on user permission before evaluating the query
- Added the user infos in the input rego
- mongodb integrated to load roles and bindings collections
- Created get_header custom built-in rego function
- Added support for the target service documentation API, with a evaluation skip if is set targetServiceOASPath env
- Support API permission specification from file
- OPA integration with single module loading and handler validation
- rbac service initial configuration from openApi specifications
