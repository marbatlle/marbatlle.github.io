---
title: 6. Security and Privacy in FHIR
---

# 6. Security and Privacy in FHIR

## Authentication and Authorization

FHIR implementations require robust security:

**Authentication Methods**:

- OAuth 2.0 (recommended)
- SMART on FHIR extensions
- OpenID Connect integration
- Basic authentication (limited scenarios)

**Authorization Models**:

- Role-based access control (RBAC)
- Attribute-based access control (ABAC)
- Scopes for granular permissions
- Resource-level permissions

**Implementation Patterns**:

- Token-based authentication
- JWT (JSON Web Tokens)
- Refresh token flows
- Session management

**Best Practices**:

- Use HTTPS/TLS for all communications
- Implement token validation
- Apply principle of least privilege
- Regular credential rotation

## Consent Resources

FHIR provides specific resources for managing patient consent:

**Consent Resource**:

- Records patient privacy choices
- Specifies what information can be shared
- Defines who can access information
- Documents consent status and verification

**Consent Categories**:

- Treatment consent
- Research participation
- Information sharing
- Advanced directives

**Implementation Approach**:

- Create and store Consent resources
- Link consents to relevant patients
- Enforce consent rules during access
- Maintain consent versioning and history

**Integration Points**:

- Authorization systems
- Data access policies
- Audit logging
- User interfaces for consent management

## Audit Logging

Proper audit logging is essential for security and compliance:

**AuditEvent Resource**:

- Records security-relevant events
- Captures who, what, when, where, and how
- Documents success or failure
- Links to affected resources

**Auditable Events**:

- Authentication events
- Data access
- Data modification
- System administration actions

**Implementation Guidance**:

- Log all security-relevant events
- Include adequate context
- Ensure logs are tamper-resistant
- Implement retention policies

**Standards and Patterns**:

- Basic Audit Log Patterns IG
- IHE ATNA (Audit Trail and Node Authentication)
- DICOM audit message format
- Local regulatory requirements

## Data Protection Considerations

FHIR implementations must address data protection:

**Data Encryption**:

- Transport Layer Security (TLS) for data in transit
- Database encryption for data at rest
- Field-level encryption for sensitive data
- Key management procedures

**Data Minimization**:

- Only access necessary data
- Implement resource filtering
- Use _summary and _elements parameters
- Apply "need to know" principle

**De-identification**:

- Remove direct identifiers
- Generalize quasi-identifiers
- Implement k-anonymity techniques
- Consider statistical disclosure control

**Regulatory Compliance**:

- HIPAA (US)
- GDPR (Europe)
- Local healthcare privacy laws
- Industry best practices

## Security Implementation Checklist

- **Risk Assessment**: Identify threats and vulnerabilities
- **Authentication**: Implement strong user authentication
- **Authorization**: Control access to resources
- **Transport Security**: Secure data in transit
- **Audit Logging**: Track all security-relevant events
- **Consent Management**: Handle patient privacy preferences
- **Data Protection**: Secure data at rest
- **Incident Response**: Plan for security incidents
- **Regular Testing**: Conduct security assessments
- **Policy Documentation**: Document security practices

By following these guidelines and applying FHIR's capabilities appropriately, healthcare organizations can build secure, interoperable systems that protect patient privacy while enabling effective data exchange.

## SMART on FHIR

SMART (Substitutable Medical Applications, Reusable Technologies) on FHIR provides:

**App Launch Framework**:

- Standardized app launch process
- Integration with EHR systems
- User context and session management

**Authentication and Authorization**:

- OAuth 2.0 authorization
- OpenID Connect integration
- Scoped permissions for resources

**App Registration**:

- Client registration process
- Scopes and permissions
- Redirect URI configuration

**Implementation Steps**:

- Register app with SMART server
- Implement OAuth 2.0 flow
- Request appropriate scopes
- Process authorization response
- Access FHIR resources with obtained token

## FHIR Licensing and IP

### FHIR Licensing and Trademark Use

FHIR, developed by HL7, is licensed under Creative Commons CC0, effectively placing it in the public domain and allowing for unrestricted use. However, HL7® and FHIR® are registered trademarks of HL7 International, requiring specific usage.

### Usage Rights and Restrictions

Users can redistribute FHIR and create derivative specifications or implementation products. However, one cannot redefine FHIR conformance, claim HL7 endorsement for derived works, or publish altered versions without clear identification.

### Trademark Application

When using the "FHIR" trademark or logo, include the ® symbol and acknowledge HL7's ownership. The first prominent mention should be "HL7® FHIR® standard," with subsequent uses as "FHIR® standard" or "FHIR®." The logo must be used in its entirety, unaltered, with the same trademark notices applied.
