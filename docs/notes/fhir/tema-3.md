---
title: 3. FHIR Data Types and Elements
---

# 3. FHIR Data Types and Elements

!!! note
    Overview of the different data types by categories

## Primitive Data Types

FHIR defines several primitive data types for basic values:

| Type | Description | Example |
| --- | --- | --- |
| boolean | True or false | true |
| integer | Whole number | 42 |
| decimal | Decimal number | 3.14159 |
| string | Unicode character sequence | "Hello World" |
| uri | Uniform Resource Identifier | "http://example.org" |
| url | Uniform Resource Locator | "http://fhir.example.org/Patient/123" |
| canonical | Canonical URL | "http://hl7.org/fhir/StructureDefinition/Patient" |
| base64Binary | Base64 encoded data | "SGVsbG8gV29ybGQ=" |
| instant | Precise timestamp | "2023-05-23T15:30:40.123Z" |
| date | Calendar date | "2023-05-23" |
| dateTime | Date and optional time | "2023-05-23T15:30:40-05:00" |
| time | Time of day | "15:30:40" |
| code | Restricted string (code values) | "male" |
| oid | Object Identifier | "1.2.840.114350" |
| id | Resource identifier | "pat123" |
| markdown | Markdown formatted text | "# Heading\nText" |
| unsignedInt | Non-negative integer | 123 |
| positiveInt | Positive integer | 42 |

## Complex Data Types

Complex data types combine multiple elements into reusable structures:

### Identifier

Used for business identifiers like medical record numbers:

```json
{
  "use": "official",
  "system": "http://hospital.example.org/identifiers/mrn",
  "value": "123456789"
}
```

### HumanName

Structured representation of a person's name:

```json
{
  "use": "official",
  "family": "Smith",
  "given": ["John", "Jacob"],
  "prefix": ["Mr."],
  "suffix": ["Ph.D."]
}
```

### Address

Physical or postal addresses:

```json
{
  "use": "home",
  "line": ["123 Main St", "Apt 4B"],
  "city": "Anytown",
  "state": "CA",
  "postalCode": "12345",
  "country": "USA"
}
```

### ContactPoint

Phone numbers, email addresses, etc.:

```json
{
  "system": "phone",
  "value": "+1-555-123-4567",
  "use": "home",
  "rank": 1
}
```

### CodeableConcept

Represents coded values with translations:

```json
{
  "coding": [
    {
      "system": "http://snomed.info/sct",
      "code": "73211009",
      "display": "Diabetes mellitus"
    },
    {
      "system": "http://hl7.org/fhir/sid/icd-10",
      "code": "E11.9",
      "display": "Type 2 diabetes mellitus without complications"
    }
  ],
  "text": "Type 2 Diabetes"
}
```

### Quantity

Measurements with units:

```json
{
  "value": 70,
  "unit": "kg",
  "system": "http://unitsofmeasure.org",
  "code": "kg"
}
```

### Reference

Links to other resources:

```json
{
  "reference": "Patient/123",
  "display": "John Smith"
}
```

## Choice Properties

Some FHIR elements allow for a choice of data types. For example, an element might be able to hold a string or an integer. When terminology is involved, sometimes you'll see a choice between a CodeableConcept or a Coding. This allows for flexibility in how coded information is represented.

!!! note
    Example of Choice Properties

## Resource Elements and Cardinality

Each element in a FHIR resource has defined cardinality indicating how many times it can appear:

### Cardinality Notation

- **0..1**: Optional, maximum one occurrence
- **1..1**: Required, exactly one occurrence
- **0..***: Optional, any number of occurrences
- **1..***: Required, at least one occurrence

!!! note
    Here we can see how cardinality is displayed in the resource description per each element.

### Element Properties

Elements have additional properties, which are also called flags:

- **Must Support**: Systems must recognize and handle these elements
- **Modifier**: Elements that change resource interpretation
- **Summary**: Elements that appear in resource summaries

!!! note
    Detailed descriptions of these properties for each data element can be found in the Detailed Descriptions tabs.

### Elements vs. Extensions

- **Standard Elements**: Defined in the base resource and universally recognized
- **Extensions**: Custom additions that may not be recognized by all systems

## FHIR Backbone element

In FHIR, a BackboneElement is a base type for elements that are complex and contained within other resources. It's used to define repeating patterns of elements.

Unlike FHIR data types, which define the type of data (e.g., string, date), BackboneElement defines a structure within a resource.

Example: In the Patient resource, the contact element is a BackboneElement, containing elements like relationship, name, and address.

## Working with Coding and Terminology

FHIR includes robust support for coded terminology:

### Coding Data Types

- **code**: Simple string code from a defined value set
- **Coding**: Code from a specific coding system:

```json
{
  "system": "http://snomed.info/sct",
  "code": "44054006",
  "display": "Type 2 diabetes mellitus"
}
```

- **CodeableConcept**: Multiple translations of the same concept:

```json
{
  "coding": [
    {
      "system": "http://snomed.info/sct",
      "code": "44054006",
      "display": "Type 2 diabetes mellitus"
    },
    {
      "system": "http://hl7.org/fhir/sid/icd-10",
      "code": "E11.9",
      "display": "Type 2 diabetes mellitus without complications"
    }
  ],
  "text": "Type 2 diabetes"
}
```

Key terminology resources:

- **CodeSystem**: Defines a set of codes and their meanings
- **ValueSet**: Defines a set of codes selected from one or more CodeSystems
- **ConceptMap**: Defines mappings between codes in different CodeSystems

These resources enable precise representation of clinical concepts and facilitate semantic interoperability.

### Terminology Example

Here's an example to illustrate how code, CodeSystem, ValueSet, and ConceptMap work together:

**Terminology Example: Blood Pressure**

**CodeSystem:**

- We might have a CodeSystem (e.g., LOINC -) that defines codes for clinical observations.
- LOINC includes a code like "8480-6" for "Systolic blood pressure".
- In FHIR, the CodeSystem resource would represent LOINC and its codes.

**Code:**

- The specific code "8480-6" is a code within the LOINC CodeSystem.
- This code is used within a Coding element.

**Coding and CodeableConcept:**

- A Coding instance:

```json
{
"system": "http://loinc.org",
"code": "8480-6",
"display": "Systolic blood pressure"
}
```

- A CodeableConcept might include this Coding, and potentially codes from other systems:

```json
{
"coding": [
{
"system": "http://loinc.org",
"code": "8480-6",
"display": "Systolic blood pressure"
},
{
"system": "http://snomed.info/sct",
"code": "162673000",
"display": "Systolic blood pressure"
}
],
"text": "Systolic BP"
}
```

**ValueSet:
**A ValueSet might be defined for "Blood Pressure Measurements".

- This ValueSet would include the LOINC code "8480-6" (and other relevant codes) to specify the allowed codes for recording blood pressure.
- FHIR elements would then bind to this ValueSet.

**ConceptMap:**

- A ConceptMap could be used to map the LOINC code "8480-6" to an equivalent code in a different coding system (e.g., a local hospital coding system).
- This allows for translation and interoperability between systems using different terminologies.

### FHIR Terminology Services

FHIR Terminology Services provide standardized access to code systems, value sets, and concept maps.

FHIR defines standard operations for terminology services:

- **$validate-code**: Validate a code in a value set or code system
- **$expand**: Expand a value set into its constituent codes
- **$translate**: Translate a code from one system to another
- **$lookup**: Look up a code's details
- **$subsumes**: Check if one code subsumes (includes) another
