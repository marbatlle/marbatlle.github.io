---
title: 4. FHIR Exchange
---

# 4. FHIR Exchange

FHIR defines several exchange paradigms, which are methods for exchanging FHIR resources between systems. The choice of paradigm depends on the specific requirements of the interoperability scenario.

- **Four paradigms: REST, Documents, Messages and Services.**
- Architectures will be driven by legacy requirements, architectural preferences, enterprise architecture commitments, etc.
- Data (generally) shared easily across paradigm boundaries

## RESTful Operations

FHIR implements the standard HTTP operations in a RESTful manner:

### Basic CRUD Operations

| Operation | HTTP Method | URL Pattern | Description |
| --- | --- | --- | --- |
| Create | POST | /[resourceType] | Create a new resource |
| Read | GET | /[resourceType]/[id] | Retrieve a specific resource |
| Update | PUT | /[resourceType]/[id] | Update an existing resource |
| Delete | DELETE | /[resourceType]/[id] | Delete a resource |

!!! note
    Each FHIR resource definition includes an "Operations" section, detailing specific actions that can be performed on instances of that resource.

### Additional Standard Operations

- **vread**: GET /[resourceType]/[id]/_history/[version] - Read a specific version
- **history**: GET /[resourceType]/[id]/_history - Get resource version history
- **patch**: PATCH /[resourceType]/[id] - Partial update of a resource

### Example: Creating a New Patient

```http
POST /Patient HTTP/1.1
Host: fhir.example.org
Content-Type: application/fhir+json

{
  "resourceType": "Patient",
  "name": [
    {
      "family": "Smith",
      "given": ["John"]
    }
  ],
  "gender": "male",
  "birthDate": "1980-01-15"
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/fhir+json
Location: http://fhir.example.org/Patient/123

{
  "resourceType": "Patient",
  "id": "123",
  "meta": {
    "versionId": "1",
    "lastUpdated": "2023-05-24T10:15:30Z"
  },
  "name": [
    {
      "family": "Smith",
      "given": ["John"]
    }
  ],
  "gender": "male",
  "birthDate": "1980-01-15"
}
```

## Search Parameters and Capabilities

FHIR provides a powerful search framework for finding resources.

### Search Parameter Types

- **string**: Simple string matching
- **token**: Code or identifier matching
- **reference**: References to other resources
- **quantity**: Numeric comparisons with units
- **date**: Date/time comparisons
- **number**: Numeric comparisons
- **uri**: URI matching
- **special**: Special purpose parameters

### Common Search Parameters

| Resource | Parameter | Type | Description |
| --- | --- | --- | --- |
| Patient | name | string | Search by name |
| Patient | identifier | token | Search by identifier |
| Observation | patient | reference | Observations for a patient |
| Observation | code | token | Search by observation type |
| Observation | date | date | Search by observation date |
| MedicationRequest | patient | reference | Medications for a patient |
| Encounter | patient | reference | Encounters for a patient |
| * | _id | token | Search by resource id |
| * | _lastUpdated | date | Search by update date |

### Search Modifiers

- **exact**: Exact string match
- **contains**: Contains substring
- **missing**: Whether element exists
- **not**: Negates the search condition
- **gt, lt, ge, le**: Greater than, less than operators

In FHIR search, these modifiers allow for more precise control over how search parameters are applied. For example:

- name:exact=Smith would match only the exact name "Smith"
- name:contains=mi would match "Smith", "Smithson", "Hamilton", etc.
- telecom:missing=true would find patients with no contact information
- status:not=completed would find items that don't have a "completed" status
- date=gt2023-01-01 would find dates greater than January 1, 2023

### Combining Search Parameters

- Multiple parameters are combined with logical AND
- Use the , operator for OR within a parameter
- Complex combinations require the _filter parameter

### Example: Search Queries

Find patients with name "Smith":

```http
GET /Patient?name=Smith
```

Find observations of type "blood pressure" for a specific patient:

```http
GET /Observation?patient=Patient/123&code=85354-9
```

Find all active medication requests for a patient:

```http
GET /MedicationRequest?patient=Patient/123&status=active
```

### Paging and Limiting Results

- **_count**: Control number of results per page
- **_offset**: Skip a number of results (less common)
- **page navigation**: Using Bundle.link elements

### Search Result Structure

Search results are returned as a Bundle resource of type "searchset":

```json
{
  "resourceType": "Bundle",
  "type": "searchset",
  "total": 35,
  "link": [
    {
      "relation": "self",
      "url": "http://fhir.example.org/Patient?name=Smith&_count=10"
    },
    {
      "relation": "next",
      "url": "http://fhir.example.org/Patient?name=Smith&_count=10&_page=2"
    }
  ],
  "entry": [
    {
      "fullUrl": "http://fhir.example.org/Patient/123",
      "resource": {
        "resourceType": "Patient",
        "id": "123",
        "name": [
          {
            "family": "Smith",
            "given": ["John"]
          }
        ]
      },
      "search": {
        "mode": "match",
        "score": 1.0
      }
    },
    // More results...
  ]
}
```

## Transactions and Batch Operations

FHIR allows sending multiple operations in a single request using Bundle resources.

### Types of Bundle Operations

- **Batch**: Collection of operations processed independently
- **Transaction**: All-or-nothing set of operations

### Bundle Structure

```json
{
  "resourceType": "Bundle",
  "type": "transaction",
  "entry": [
    {
      "fullUrl": "urn:uuid:61ebe359-bfdc-4613-8bf2-c5e300945f0a",
      "resource": {
        "resourceType": "Patient",
        "name": [
          {
            "family": "Smith",
            "given": ["John"]
          }
        ]
      },
      "request": {
        "method": "POST",
        "url": "Patient"
      }
    },
    {
      "request": {
        "method": "GET",
        "url": "Patient?name=Jones"
      }
    }
  ]
}
```

### Transaction Processing Rules

- Resources can reference each other using temporary IDs
- Operations are processed in the order provided
- For transactions, if any operation fails, all changes are rolled back
- For batch operations, each entry is processed independently

### Common Use Cases

- Creating a patient and related resources in one request
- Bulk updates to related resources
- Atomic updates across multiple resources

## Operations Framework

Beyond basic CRUD operations, FHIR defines a framework for more complex operations.

### Named Operations

Called using the $ prefix, e.g., $everything or $validate:

```http
POST /Patient/123/$everything
```

### Common Standard Operations

- **$everything**: Get all resources related to a specific resource
- **$validate**: Validate a resource against profiles
- **$expand**: Expand a value set
- **$translate**: Translate between code systems
- **$meta**: Get or add metadata to a resource
- **$process-message**: Process a FHIR message

### Operation Definition

Operations are defined using OperationDefinition resources:

```json
{
  "resourceType": "OperationDefinition",
  "name": "everything",
  "status": "active",
  "kind": "operation",
  "code": "everything",
  "resource": ["Patient"],
  "system": false,
  "type": false,
  "instance": true,
  "parameter": [
    {
      "name": "start",
      "use": "in",
      "min": 0,
      "max": "1",
      "type": "date"
    },
    {
      "name": "end",
      "use": "in",
      "min": 0,
      "max": "1",
      "type": "date"
    },
    {
      "name": "return",
      "use": "out",
      "min": 1,
      "max": "1",
      "type": "Bundle"
    }
  ]
}
```

### Custom Operations

Organizations can define custom operations for specific use cases:

- Must be defined using OperationDefinition resources
- Should follow the same patterns as standard operations
- Should be documented in Implementation Guides

### Simple vs. Complex Operations

- **Simple operations** are usually invoked with GET and parameters in the URL.
    - *Example:* GET /Patient/123/$everything?start=2023-01-01
- **Complex operations** often use POST and pass parameters in the request body.
    - *Example:* POST /Patient/$validate (because the resource being validated is a complex input).

This distinction is important for practical implementation because:

- GET operations are easier to debug and can be executed in a browser
- POST operations can handle larger inputs and more complex parameter structures
- Some operations can be invoked using either method, depending on parameter complexity

## Capability Statement

A CapabilityStatement resource describes the capabilities of a FHIR server. It provides information about:

- Supported resources.
- Supported RESTful interactions (e.g., CREATE, READ, UPDATE, DELETE, SEARCH).
- Supported operations.
- Supported search parameters.
- Security features.

The CapabilityStatement is crucial for clients to understand how to interact with a FHIR server.

## Messaging

FHIR Messaging enables asynchronous exchange of information between systems. It's useful for event-driven scenarios where systems need to be notified of specific events.

Key aspects of FHIR Messaging:

- **Asynchronous Communication:** Messaging doesn't require an immediate, synchronous response, allowing systems to communicate even if they are temporarily unavailable. This is in contrast to REST, which is typically synchronous.
- **Loosely Coupled Systems:** Messaging promotes loose coupling between systems, meaning they don't need to be tightly integrated or have detailed knowledge of each other's implementation.
- **Store-and-Forward:** Messaging often uses a store-and-forward architecture, where messages are stored and forwarded to the destination system, ensuring delivery even if the system is temporarily offline.
- **Trigger Events:** Messaging is often triggered by specific business events, which initiate the exchange of information and define the context of the message.
- **Message Bundles:** Messages are often packaged within a Bundle resource, with the type element set to "message". This allows for the inclusion of multiple related resources within a single message.
- **MessageHeader Resource:** A MessageHeader resource is used to define the purpose, source, and destination of a message, as well as any correlation information. It provides context for the message and helps with routing and processing.
- **Request/Response Patterns:** While primarily asynchronous, messaging can also support request/response interactions, where a system sends a message and expects a response.
- **Example Structure:**

```json
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "resource": {
        "resourceType": "MessageHeader",
        // ... MessageHeader details ...
      }
    },
    // ... Other resources ...
  ]
}
```

## Other FHIR Exchange Mechanisms

FHIR also supports other exchange paradigms:

### Services:

- For interactions and workflows that go beyond simple CRUD operations.
- Used when REST's capabilities are insufficient.
- Examples include operations other than CRUD (e.g., decision support), complex workflows, and scenarios needing a mix of document persistence and workflow behavior

### Database/Persistence:

- This paradigm involves using FHIR resources directly for data storage within a database system.
- FHIR can be employed as a repository model.
- This approach can be part of various architectural patterns, such as FHIR as a REST API, FHIR Facade, or FHIR Data Repository

### Subscriptions Framework:

- Provides a mechanism for real-time notifications of events.
- Involves a server that checks for resource creation, updates, or deletions that match predefined criteria.
- When a match occurs, a notification is sent to a defined channel.
- Notifications are delivered as Bundles, with the first entry being a SubscriptionStatus resource.
- Search criteria are used to define the conditions that trigger notifications.
    - In R4, these criteria are search strings (query URLs).
    - In R5, SubscriptionTopic resources define the queryCriteria.

### Bulk Data Access:

- FHIR defines a mechanism for efficiently exchanging large sets of FHIR resources. This is important for use cases like population health reporting or analytics.
- It uses a format called FHIR NDJSON (Newline Delimited JSON), where each resource is on a separate line.
- Bulk data access is typically initiated using an operation at the server level (e.g., GET /fhir/$export).
- This paradigm is designed for asynchronous processing, as retrieving large datasets can take time.
