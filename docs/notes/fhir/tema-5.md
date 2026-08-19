---
title: 5. FHIR Implementation Guides
---

# 5. FHIR Implementation Guides

## Understanding Implementation Guides

Implementation Guides (IGs) provide practical guidance for implementing FHIR in specific contexts:

- **Purpose**: Define how FHIR should be used to solve specific healthcare interoperability problems
- **Components**: Profiles, extensions, terminology, examples, and documentation
- **Audience**: Developers implementing FHIR-based systems for particular use cases
- **Authority**: May be published by standards bodies, governments, or organizations

IGs translate FHIR's general capabilities into specific, implementable solutions for real-world healthcare scenarios.

## Common Implementation Guides

Notable FHIR Implementation Guides include:

- **US Core**: Base profiles for the US healthcare system
- **International Patient Summary (IPS)**: Standardized health data for cross-border care
- **SMART App Launch**: Framework for launching apps from EHRs
- **Argonaut Project**: Industry-led implementation guides for common healthcare scenarios
- **Da Vinci Project**: Payer-provider exchange implementation guides
- **QI-Core**: Quality improvement core profiles
- **Bulk Data Access**: Framework for efficiently transferring large FHIR datasets

The FHIR IG Registry (<https://registry.fhir.org/guides>) provides a comprehensive listing of published guides.

## Profiles, Extensions, and Constraints

Implementation Guides use profiles to constrain resources for specific use cases.

### Profile Components

- **Cardinality Changes**: Making optional fields required
- **Value Constraints**: Limiting possible values
- **Slicing**: Defining patterns for repeated elements
- **Extension Definitions**: Adding new elements
- **Terminology Bindings**: Specifying code systems and value sets

### Profile Definition

Profiles are defined using StructureDefinition resources:

```json
{
  "resourceType": "StructureDefinition",
  "url": "http://example.org/fhir/StructureDefinition/pediatric-patient",
  "name": "PediatricPatient",
  "status": "active",
  "kind": "resource",
  "abstract": false,
  "type": "Patient",
  "baseDefinition": "http://hl7.org/fhir/StructureDefinition/Patient",
  "derivation": "constraint",
  "differential": {
    "element": [
      {
        "id": "Patient.birthDate",
        "path": "Patient.birthDate",
        "min": 1
      },
      {
        "id": "Patient.contact",
        "path": "Patient.contact",
        "min": 1
      }
    ]
  }
}
```

!!! note
    Here is an example of the same Patient resource we saw earlier, but as profiled by the US Core FHIR Profile

### Extension Definition

Custom extensions are also defined using StructureDefinition resources:

```json
{
  "resourceType": "StructureDefinition",
  "url": "http://example.org/fhir/StructureDefinition/birth-weight",
  "name": "BirthWeight",
  "status": "active",
  "kind": "complex-type",
  "abstract": false,
  "type": "Extension",
  "baseDefinition": "http://hl7.org/fhir/StructureDefinition/Extension",
  "derivation": "constraint",
  "differential": {
    "element": [
      {
        "id": "Extension.url",
        "path": "Extension.url",
        "fixedUri": "http://example.org/fhir/StructureDefinition/birth-weight"
      },
      {
        "id": "Extension.value[x]",
        "path": "Extension.value[x]",
        "type": [
          {
            "code": "Quantity"
          }
        ]
      }
    ]
  }
}
```

### Using Profiles in Resources

Resources declare conformance to profiles using the meta.profile

```json
{
  "resourceType": "Patient",
  "meta": {
    "profile": [
      "http://example.org/fhir/StructureDefinition/example-patient-profile"
    ]
  },
  "id": "patient-example",
  "text": {
    "status": "generated",
    "div": "<div xmlns=\"http://www.w3.org/1999/xhtml\">Patient example</div>"
  },
  "identifier": [
    {
      "system": "http://example.org/fhir/identifier/mrn",
      "value": "12345"
    }
  ],
  "active": true,
  "name": [
    {
      "use": "official",
      "family": "Smith",
      "given": [
        "John"
      ]
    }
  ],
  "gender": "male",
  "birthDate": "1974-12-25",
  "address": [
    {
      "use": "home",
      "line": [
        "123 Main St"
      ],
      "city": "Anytown",
      "state": "CA",
      "postalCode": "12345",
      "country": "USA"
    }
  ]
}
```

The meta.profile element contains a list of URLs that identify the profiles the resource claims to conform to. Systems processing the resource can use these profile references to understand the context of the resource and to validate that the resource meets the requirements of the referenced profiles.

### Constraints

- Limit value sets for specific elements
- Enforce business rules and relationships
- Ensure consistency across implementations

### Bindings

FHIR uses "bindings" to connect elements (especially those with coded data types like CodeableConcept) to ValueSets. A binding specifies the set of codes that *should* or *may* be used for that element.

FHIR defines different binding strengths:

- **Required:** Only codes from the specified ValueSet *can* be used. The server *must* reject resources with codes outside the ValueSet.
- **Extensible:** Codes from the ValueSet are *preferred*, but codes outside the ValueSet *may* be used. The server *should* provide a warning if an unknown code is used.
- **Preferred:** Codes from the ValueSet are *preferred*, but codes

## Validation Against Profiles

Validation ensures resources conform to profiles:

**Methods**:

- Server-side validation using $validate operation
- Client-side validation using FHIR validators
- Validation during testing and quality assurance

**Process**:

- Choose validation method
- Execute validation against specific profiles
- Interpret results (success or errors)
- Address validation issues

**Handling Issues**:

- Locate errors in the resource
- Determine corrective actions
- Consider message severity (error, warning, information)
- Revalidate after corrections
