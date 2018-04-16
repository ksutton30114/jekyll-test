---
title: "REST API Standards"
date: 2017-02-13 00:00:00 -0400
last_modified_at: 
categories:
  - Code Management
tags: 
  - backend
  - go

author: Naga Sathyanarayana
author_profile: true
sidebar:
  title: ""
  nav: content-nav
toc: true
---

## Introduction
Resources form the nucleus of any REST API design. Resource identifiers (URI), Resource representations, API operations (using various HTTP methods), etc. are all built around the concept of Resources. It is very important to select the right resources and model the resources at the right granularity while designing the REST API so that the API consumers get the desired functionality from the APIs, the APIs behave correctly and the APIs are maintainable. To help guide the decision making process, below are some requirements that the API must strive for:
- It should use web standards where they make sense
- It should be friendly to the developer and be explorable via a browser address bar
- It should be simple, intuitive and consistent to make adoption not only easy but pleasant
- It should provide enough flexibility to power majority of the UI
- It should be efficient, while maintaining balance with the other requirements

The key principles of **REST** involve separating your API into logical resources. These resources are manipulated using HTTP requests where the method (GET, POST, PUT, PATCH, DELETE) has specific meaning. 

## Resource
The resources should be nouns(Not Verbs) that make sense from the perspective of the API consumer. Although your internal models may map neatly to resources, it isn't necessarily a one-to-one mapping. 

Once you have your resources defined, you need to identify what actions apply to them and how those would map to your API. RESTful principles provide strategies to handle **CRUD** actions using HTTP methods mapped as follows:
- GET /assets - Retrieves a list of assets
- GET /assets/1482 - Retrieves a specific asset
- POST /assets - Creates a new asset
- PUT /assets/1482 - Updates asset #1482
- PATCH /assets/1482 - Partially updates asset #1482
- DELETE /assets/1482 - Deletes asset #1482

## Relations
If a relation can only exist within another resource, RESTful principles provide useful guidance. For example:
- GET /assets/1482/blocks - Retrieves list of blocks for asset #1482
- GET /assets/1482/blocks/5 - Retrieves blocks #5 for asset #1482
- POST /assets/1482/blocks - Creates a new block in asset #1482
- PUT /assets/1482/blocks/5 - Updates block #5 for asset #1482
- PATCH /assets/1482/blocks/5 - Partially updates block #5 for asset #1482
- DELETE /assets/1482/blocks/5 - Deletes block #5 for asset #1482

## Result filtering, sorting & searching
### Filtering 
Use a unique query parameter for each field that implements filtering. For example, when requesting a list of assets from the /assets endpoint, you may want to limit these to only those in the "Active" state. This could be accomplished with a request like `GET /assets?state=Active`. Here, state is a query parameter that implements a filter.

### Sorting 
Similar to filtering, a generic parameter sort can be used to describe sorting rules. Accommodate complex sorting requirements by letting the sort parameter take in list of comma separated fields, each with a possible unary negative to imply descending sort order. For example:
- GET /assets?sort=-name - Retrieves a list of assets in descending order of name
- GET /assets?sort=-name,created_at - Retrieves a list of assets in descending order of name. Within a specific priority, older assets are ordered first.

## Limiting which fields are returned by the API
The API consumer doesn't always need the full representation of a resource. The ability select and chose returned fields goes a long way in letting the API consumer minimize network traffic and speed up their own usage of the API. Use a fields query parameter that takes a comma separated list of fields to include. For example, the following request would retrieve just enough information to display a sorted listing of open tickets:
- GET /assets?fields=id,customer_name,updated_at&state=active&sort=-updated_at

## Updates & creation should return a resource representation
A `PUT`, `POST` or `PATCH` call may make modifications to fields of the underlying resource that weren't part of the provided parameters (for example: created_at or updated_at timestamps). To prevent an API consumer from having to hit the API again for an updated representation, have the API return the updated (or created) representation as part of the response.

In case of a `POST` that resulted in a creation, use a **HTTP 201 status code** and include a **Location header** that points to the URL of the new resource.

## API Documentation
Swagger is recommended for documenting the APIs.  <a href="http://swagger.io/" target="_blank">http://swagger.io</a> provides detailed description on creating the API documentation.  We can also use <a href="http://editor.swagger.io/#" target="_blank">http://editor.swagger.io/#</a> to create the document visually and generate the client/server stubs.  API document creates contract for using a service.  Using tools like Swagger, the service implementation can be language agnostic.  This means, the API document can be passed through a code generator to generate the stub in any of the supported languages.

One of the regular issues we find is the mismatch in pace between front end and backend development.  In such case, backend developer can create a API document and provide stub implementation. This stub helps unblock the front-end and also validate the implementation.  Backend developer replaces the stub with the actual service when it is ready.

## How to version API?
It is recommended to use the version number in the URL.  For example: /api/v1/assets.  When any changes are made to the API, the version number is bumped. For example: `/api/v2/assets`.