# Conjur Suite Certification Levels

This document provides detailed information about certification levels of components
that are part of the CyberArk Conjur [Open Source Suite](https://cyberark.github.io/conjur/)
of tools.

CyberArk maintains three levels of certification to indicate how far a particular
component has been reviewed and tested by CyberArk:
- **Community**: Briefly. We want to help you contribute and get out of the way.
- **Trusted**: CyberArk has reviewed and tested this component and trusts it to be
  used with Conjur Open Source.
- **Certified**: CyberArk has reviewed, tested, and approved this component to be
  used with the _[CyberArk Conjur Enterprise](https://docs.cyberark.com/Product-Doc/OnlineHelp/AAM-DAP/Latest/en/Content/Resources/_TopNav/cc_Home.htm)_
  (formerly DAP) product. Note that Conjur Enterprise itself is built directly from Conjur certified core components.

## Certification Levels at a Glance

|  Level       	| Description                                                            	| Documentation 	| Completeness                                          | Tests                                                                                                         | Security                                                                                  | Support                                     	|
|:-------------:|-------------------------------------------------------------------------|-----------------|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|-----------------------------------------------|
| **Community** | Community contributions: Easy to add value                              | Basic         	| Feature can be demonstrated with a single use case    | Not required                                                                                                  | Not reviewed                                                                             	| Community                                   	|
| **Trusted**   | Tested and trusted to work with **Conjur Open Source**                         	| Full          	| Feature implementation is largely complete            | Comprehensive tests <br><br>No known `Critical` or `High` severity bugs | Automated security scans<br><br>Follows security best practices       | Community support with CyberArk assistance  	|
| **Certified** | Officially approved for use with **Conjur Enterprise**           	| Comprehensive 	| Feature implementation is complete when used with **Conjur Enterprise** | Comprehensive tests <br><br>No known `Critical` or `High` severity bugs<br><br>load-tested at expected Enterprise production loads | Automated security scans<br><br>Security level complies with **Conjur Enterprise** requirements             | Fully supported by CyberArk for use in **Conjur Enterprise**  	|

---


## Community

### Description
Community features or projects are **contributed by the community** and **are not
reviewed or supported by CyberArk Engineering**. In particular, Community features
or projects **have not had a CyberArk security review**.

For the purposes of this certification level, community members may include:
- CyberArk Conjur Engineering team members
- Other CyberArk employees including BizDev, Extensions team, Pre-sales,  Professional / Security Services
- Non-CyberArk contributors: Partners, End Users, DevSecOps Engineers, etc

### Characteristics
Characteristics of a Community Level feature:

- Feature/Product has a name.
- Feature can be demonstrated with a single use case.
- Feature has value to our customers.
- Feature is available in a tagged version.
  - For CyberArk-maintained software, GitHub tags will be used. If the feature
    is part of a larger project, it must be feature-flagged off by default.
  - For non-CyberArk maintained software, versioned release artifacts will be
    uploaded to CyberArk Marketplace with the "Community" Certification Level.
    A [software license](https://opensource.org/licenses) should be specified.
- Basic documentation (e.g. a README.md file) has been written for the feature, and includes:
  - A clear indication of its **Community** Certification Level.
  - Description of covered use case.
  - Supported versions of relevant components (eg tools that it integrates with,
    etc).
  - Known limitations.

## Trusted

### Description
A feature or project with a **Trusted** Certification Level has been reviewed by
CyberArk Engineering to verify that it will securely work with Conjur Open Source as documented.

### Characteristics
Taking a feature from the Community certification level to the Trusted level involves
a development, documentation, and testing effort to meet the following criteria:

- Feature implementation is largely complete
  - Majority of edge cases for the key feature use case have been implemented.
  - No known bugs of `Critical` or `High` severity exist. (TBA - link to rubric for defining bug severity)
- Feature is available in a tagged version:
  - For CyberArk-maintained software, GitHub tags will be used.
  - For non-CyberArk maintained software, versioned release artifacts will be
    uploaded to CyberArk Marketplace with the "Trusted" Certification Level.
- Feature has been fully documented and includes:
  - Supported versions of relevant components (eg tools that it integrates with,
    etc).
  - Known limitations.
  - Basic troubleshooting information.
  - API documentation updates (if relevant, e.g. for updates to the Conjur API).
- Feature has comprehensive tests
  - Automated unit and integration test suite has been implemented for use case.
    - All main positive tests exist.
    - Many negative tests exist.
    - Might be some edge cases remaining to test, but the covered edge cases
      should be tested.
- Feature passed a basic security review and follows security best practices
  (e.g. STRIDE, OWASP Top 10, GDPR).

In addition, if the feature is maintained by CyberArk, the following conditions must be met:
  - Documentation is published on appropriate CyberArk documentation site(s)
  - Feature is clearly labeled as **Trusted** Certification Level.
  - Feature has automated vulnerability scanning integrated into its pipeline
    which runs with no Critical or High vulnerabilities.
  - Project has an up-to-date acknowledgements file and all dependencies use
    approved licenses (MIT, Apache 2.0, BSD) or have been individually approved.

New versions of "Trusted" features will be re-reviewed to verify they continue
to meet the "Trusted" criteria before they may continue to be included in a new
version at the "Trusted" level.


## Certified

### Description
A "Trusted" feature or project may be **Certified** to work with CyberArk Conjur Enterprise.
Features that are "Certified" have been reviewed by CyberArk Engineering to verify
that they will securely work with CyberArk Conjur Enterprise as documented. In addition, CyberArk
offers Enterprise-level support for these features.

### Characteristics
In order for a "Trusted" feature to become "Certified" for CyberArk Conjur Enterprise, the
following **additional** criteria must be met:
- Feature implementation is complete when used with CyberArk Conjur Enterprise.
  - All identified edge cases have been implemented.
  - No known bugs of `Critical` or `High` severity exist.
- Feature includes automated tests to validate functional workflows with CyberArk Conjur Enterprise.
  - Feature has been load-tested at expected Enterprise production loads.
  - Performance goals for feature working with CyberArk Conjur Enterprise have been met and
    confirmed by testing/usage data.
  - Code coverage meets targets for Enterprise-level products.
- Feature documentation is complete.
  - Documentation for using the feature with CyberArk Conjur Enterprise exists on the appropriate
    documentation site(s), and includes:
    - Supported versions of relevant components (eg tools that it integrates with,
      etc).
    - Known limitations.
    - Comprehensive troubleshooting information.
    - Updated API documentation (if relevant, e.g. for updates to the Conjur API).
- Feature passed a comprehensive security review, ensuring it complies with the
  CyberArk Conjur Enterprise security requirements.
