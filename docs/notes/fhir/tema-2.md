---
title: 2. FHIR Resources
---

# 2. FHIR Resources

## Resource Structure and Components

Every FHIR resource includes:

- **resourceType**: Identifies the type of resource (e.g., "Patient", "Observation")
- **id**: A unique identifier for this specific resource instance
- **meta**: Metadata about the resource, including version and security tags
- **text**: A human-readable representation of the resource content
- **contained**: Other resources contained within this resource (for resources that can't stand alone)

Here’s a simplified example of a FHIR Patient resource in JSON format:

```json
{
  "resourceType": "Patient",
  "id": "example",
  "meta": {
    "versionId": "1",
    "lastUpdated": "2023-05-22T15:30:40Z"
  },
  "text": {
    "status": "generated",
    "div": "<div xmlns=\"http://www.w3.org/1999/xhtml\">John Smith</div>"
  },
  "identifier": [
    {
      "system": "http://example.org/identifiers",
      "value": "12345"
    }
  ],
  "active": true,
  "name": [
    {
      "use": "official",
      "family": "Smith",
      "given": ["John"]
    }
  ],
  "gender": "male",
  "birthDate": "1974-12-25"
}
```

The description of each resource in the IG, should include:

- **Scope and Usage**: The resource's purpose and intended use
- **Boundaries**: What data belongs in the resource and what doesn't
- **Relationships**: How the resource relates to other resources
- **Structure View**: A hierarchical, tree-like view of resource elements
- **Data Elements: ** The specific data points within the resource, each with a defined: Element ID, Definition, Short Display, and Notes.

### Resource Narrative

The text element provides a human-readable version of the resource content, which is important for:

- Ensuring data can be understood even without FHIR-specific tools
- Providing a fallback when receiving systems don't recognize extensions
- Supporting human validation of resource content

!!! note
    Human readability is key. In FHIR, all resources SHOULD have a human-readable narrative.

### Resource Identification

Resources can be identified through several mechanisms:

- **Logical ID**: The id element unique within a FHIR server
- **Business Identifiers**: The identifier element containing domain-specific identifiers
- **URL-based Identity**: Full URL path to the resource on a specific server

!!! note
    Logical id as used by a FHIR-enabled application; the “primary key” of the database entry

## Common Resources Overview

!!! note
    To locate the full list of available FHIR resources (https://hl7.org/fhir/R4/resourcelist.html), navigate 
    to the FHIR R4 landing page and from the header, click on Resources.

Some fundamental FHIR resources include:

- **Patient**: Demographic and administrative information about a person receiving healthcare services
- **Practitioner**: Information about healthcare providers
- **Organization**: Details about healthcare organizations
- **Encounter**: An interaction between a patient and healthcare providers
- **Observation**: Measurements, test results, or assertions about a patient
- **Condition**: Clinical conditions, problems, or diagnoses
- **Procedure**: Actions performed on or for a patient
- **MedicationRequest**: Orders for medications
- **DiagnosticReport**: Results of diagnostic tests or procedures

These core resources represent the most common healthcare concepts and form the foundation of most FHIR implementations.

!!! note
    The Resource Index displays all the resources available by categories.

## Resource References and Relationships

Resources reference each other to create a connected web of healthcare information.

!!! note
    Examples of references

### Reference Types

FHIR supports different types of references:

- **Literal References**: Direct references to a specific resource by URL (e.g., <https://example.org/fhir/Patient/456>)
- **Logical References**: References using a resource type and identifier (e.g., Patient/123)
- **Contained Resources**: Resources embedded directly within another resource

### Reference Example

A MedicationRequest referencing both a patient and a medication:

```json
{
  "resourceType": "MedicationRequest",
  "id": "med-request-123",
  "status": "active",
  "intent": "order",
  "subject": {
    "reference": "Patient/pat123",
    "display": "John Smith"
  },
  "medicationReference": {
    "reference": "Medication/med456",
    "display": "Lisinopril 10mg tablet"
  }
}
```

### Reference Resolution

When a system receives a resource with references, it may need to:

- Resolve those references to access complete information
- Follow a chain of references to understand the full clinical context
- Bundle related resources together for complete information transfer

### Reference Integrity

FHIR systems must maintain reference integrity:

- References should point to valid resources
- When resources are deleted, systems must handle dangling references
- Circular references should be avoided or handled carefully

The Reference data type includes:

- reference: The actual reference path
- type: Resource type being referenced
- identifier: Business identifier for the referenced resource
- display: Human-readable text representing the reference

## Extensions and Profiles

FHIR's extension mechanism allows for customization while maintaining interoperability.

### Extensions

Extensions add elements not present in the base resource definition. They consist of:

- A URL that uniquely identifies the extension
- A value that provides the extended data

#### Extension Example

Adding a patient's preferred pharmacy to a Patient resource:

```json
{
  "resourceType": "Patient",
  "id": "example",
  "extension": [
    {
      "url": "http://example.org/fhir/StructureDefinition/preferred-pharmacy",
      "valueReference": {
        "reference": "Organization/pharm123",
        "display": "Downtown Pharmacy"
      }
    }
  ],
  "name": [
    {
      "family": "Smith",
      "given": ["John"]
    }
  ]
}
```

### Profiles

Profiles constrain resources for specific use cases by:

- Restricting cardinality (making optional fields required)
- Limiting allowed values
- Adding must-support flags on elements
- Incorporating extensions consistently
- Providing implementation guidance

Profiles are represented as StructureDefinition resources and are typically part of Implementation Guides.

### Modifiers vs. Regular Extensions

- **Regular Extensions**: Add information without changing the meaning of the resource
- **Modifier Extensions**: Change the interpretation of the resource and are flagged with isModifier=true

### Best Practices for Extensions

- Reuse existing extensions when possible
- Define extensions clearly with StructureDefinition resources
- Use URLs that you control for extension definitions
- Document extensions thoroughly
- Consider creating profiles when using extensions consistently

## Provenance resource

The Provenance resource is used to track the origin and history of FHIR resources. It records information about who created, modified, or deleted a resource, and when and how these actions occurred. Provenance is essential for audit trails and data integrity.
