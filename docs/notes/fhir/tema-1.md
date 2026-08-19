---
title: 1. FHIR Fundamentals
---

# 1. FHIR Fundamentals

## What is FHIR?

Fast Healthcare Interoperability Resources (FHIR) is a standard for exchanging healthcare information electronically. Developed by Health Level Seven International (HL7), FHIR combines the best features of previous standards (HL7 v2, HL7 v3, CDA) with modern web technologies to create a more accessible, implementable, and widely usable healthcare interoperability standard.

FHIR is designed to:

- Facilitate seamless exchange of healthcare data
- Support modern web implementation approaches
- Provide a consistent, logical structure for healthcare information
- Enable rapid implementation and adoption

The most widely used version is FHIR R4 (<https://hl7.org/fhir/R4/>), which provides stable APIs for many healthcare scenarios.

## Core Concepts and Terminology

To understand FHIR, you need to grasp several key concepts:

- **Resources**: The fundamental building blocks of FHIR, representing small, logically discrete units of healthcare information (e.g., Patient, Observation, Medication)
- **Profiles**: Customizations of resources for specific use cases or requirements
- **Extensions**: Mechanisms to add new data elements to resources without modifying the base specification
- **Implementation Guides (IGs)**: Collections of profiles, extensions, and rules for implementing FHIR in specific contexts
- **Terminology**: Coded vocabularies and value sets that provide meaning to healthcare data
- **RESTful API**: The primary way to interact with FHIR resources over HTTP using standard web methods

## Resource-Based Architecture

FHIR's architecture is modular and resource-based. Each resource:

- Represents a specific healthcare concept
- Has a defined behavior, meaning, identity, and location
- Is accessible via a unique URL
- Can be standalone or linked to other resources
- Follows a consistent structure

This approach allows for:

- Flexible implementation
- Incremental adoption
- Focused solutions for specific problems
- Clear separation of concerns

## RESTful API Approach

FHIR adopts REST (Representational State Transfer) principles, which means:

- Resources are manipulated using standard HTTP methods (GET, POST, PUT, DELETE)
- Resources have predictable URLs
- Resources can be represented in different formats (JSON, XML, RDF/Turtle)
- Interactions are stateless
- Resources can link to each other using URLs

This approach leverages existing web infrastructure and development patterns, making FHIR easier to implement than previous healthcare standards.

## FHIR Versions and Maturity Levels

FHIR evolves through regular releases:

- DSTU1 (2014): Initial draft
- DSTU2 (2015): Improved version
- STU3 (2017): Significant enhancements
- R4 (2019): The first release with normative content
- R5 (2023): Latest version with additional resources and capabilities

Individual resources within FHIR also have maturity levels:

- **Level 0 (Draft)**: First draft, subject to significant changes
- **Levels 1-3**: Going through review and testing
- **Levels 4-5**: Being trialed in real-world implementations
- **Normative**: Stable and not subject to breaking changes

For production systems, prioritize using normative resources to ensure long-term stability and interoperability.
