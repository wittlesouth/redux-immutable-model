redux-immutable-model
=====================

This module simplifies working with application data models that are backed by
RESTful APIs in Redux applications. It is a baseline component of a framework
that provides automatically generated code from OpenAPI 3.0 schema
specifications.

Objectives
----------

* Eliminate the need to manually code asynchronous Redux actions (e.g. start,
  success, error) for CRUD operations on data model objects.
* Provide object methods to access data model object attributes directly,
  without needing Immutable paths.
* Simplify common data model state tracking (instance is new, dirty, ...)
* Provide application access to relevant instances of data model objects via
  a data service paradigm. Each data model object has a corresponding service,
  and that service manages Redux state for all instances of that data model
  object.
* Provide simple methods for CRUD operations on an instance via the service.

Integrations
------------

* Facilitates integration with different security frameworks; application can
  provide hooks to collect / set required HTTP security components such as
  cookies and headers.
* Internationalization support for server / async transaction error messages
  via custom result processing.

Integration Classes
-------------------

These classes will be directly accessed by any application using this frameowrk.

* SimpleRIMObject - Implements shared functionality for data model objects, e.g.
  tracking client state relative to persisted state (isDirty, isNew, ...). See
  [here](docs/SimpleRIMObject.md) for more details.
* RelationshipRIMObject - Implements shared functionality for relationships
  between data model objects. See [here](docs/RelationshipRIMObject.md) for
  more details.
* SimpleObjectService - Provides collection management and API interaction for a
  a data model component. See [here](docs/SimpleObjectService.md) for more details.
* RelationshipObjectService - Provides collection management and API interaction for a
  a data model component. See [here](docs/RelationshipObjectService.md) for more details.
* Configuration - Provides applications the ability to customize behavior of
  this framework as needed for different types of integrations. See
  [here](docs/Configuration.md) for more details.

Framework Modules
-----------------

These modules are generally intended to be internal to the framework.

* ActionTypes - Defines Redux action types used by this package
* ExecuteRestAPICall - Performs fetch operations against the data model RESTful
  APIs, including automatic generation of Redux actions. Invoked via persistence
  actions in BaseRIMService.
* ServiceReducers - Includes reducer methods for default CRUD actions / verbs.
  Invoked via reducer() in BaseRIMService.
* ReduxAsyncStatus - Constants for default redux status values for async API 
  calls
* ReduxVerbs - Constants for default verbs, where a verb corresponds to a CRUD
  action

Running Tests
-------------

You must have the environment variable API_URL set with a path that includes the API
version for tests to run successfully. Example:

`export API_PATH='http://localhost/api/v1'`

Changelog
---------

* 0.6.2 - Allows a route to be passed in startEdit
* 0.6.0 - Breaking change introducing relationship objects, and refactoring support for
  simple object. Standardizes Get/Set methods, also adds tracking a selected set. Any code
  based on prior versions will require changes.
* 0.5.4-11 - Steps on the path to correct function in a microservice environment with multiple hydrate endpoints
* 0.5.3 - Fixes bad publish (forgot to build) for 0.5.2
* 0.5.2 - Fixes #18 - Actions should not require a rimObj
* 0.5.1 - Fixes #20 - Adds synchronous actions to start / cancel new and edit workflows
* 0.5.0 - Fixes #15 - getApiHeaders needs to pass verb as well as headers to allow verb-specific behavior
