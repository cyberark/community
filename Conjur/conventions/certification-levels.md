# Conjur OSS Suite Certification Levels

This document details the certification levels used for components of the
CyberArk Conjur [Open Source Suite](https://cyberark.github.io/conjur/).

CyberArk defines three levels of certification to indicate the degree to which
a project is supported and guaranteed secure by CyberArk:

- **Community**: CyberArk Engineering does not provide official support and has
not reviewed the project for security or quality considerations.

- **Trusted**: CyberArk Engineering does not provide official support but
regularly reviews the project to ensure it conforms to secure development
practices and meets a certain level of quality with regards to documentation
and automated testing.

- **Certified**: CyberArk Engineering officially supports the project and
guarantees that it follows secure coding practices, has automated testing for
most use-cases, and includes comprehensive documentation.

Note that if a project is not explicitly labeled with a certification level,
it should be assumed to be Community with no guarantees made about its
quality or security.

## Certification Levels at a Glance

| Level | Supported by CyberArk | Reviewed by CyberArk |
| ----- | --------------------- | -------------------- |
| **Community** | No  | No  |
| **Trusted**   | No  | Yes |
| **Certified** | Yes | Yes |

---

## Community

### Description
Community projects are contributed by the community and are not guaranteed
to be reviewed or supported by CyberArk Engineering. In particular, Community
projects **have not been reviewed** by CyberArk engineering to guarantee a
certain level of security and quality.

For the purposes of this certification level, community members may include:
- CyberArk Conjur Engineering team members
- Other CyberArk employees including BizDev, Extensions team, Pre-sales,
Professional / Security Services
- Non-CyberArk contributors: Partners, End Users, DevSecOps Engineers, etc.

### Characteristics
Characteristics of a Community Level project:

- Basic documentation (e.g. a README.md file) that includes:
  - A clear indication of its Certification Level
  - Description of project and covered use case
  - Usage instructions
  - Supported versions of relevant platforms / tooling
  - Known limitations
- Availability as a tagged version
  - For CyberArk software, GitHub tags will be used
  - For non-CyberArk software, versioned release artifacts will be uploaded to
    CyberArk Marketplace with the correct Certification Level
- A [software license](https://opensource.org/licenses) should be specified

## Trusted

### Description
A project with a **Trusted** Certification Level is regularly reviewed by
CyberArk Engineering to verify that it follows secure development development
practices that are comprable to those used for our own internal development.

### Characteristics
Taking a project from the Community certification level to the Trusted level
involves a quality and security review effort to ensure that it meets the
following criteria:

- All Community level criteria must be met, plus:
- Feature implementation is largely complete
- Documentation includes basic troubleshooting information
- Project has passed a security review by a CyberArk Security Champion or
Security Architect to ensure that it follows security best practices (e.g. 
STRIDE, OWASP Top 10)
- No known CVEs of `Critical` or `High` severity exist
- Project has automated unit and integrations tests for all positive and most
negative test cases

If the project is maintained by CyberArk, the following additional criteria
must be met:
- Documentation is published on appropriate CyberArk documentation site(s)
- Automated vulnerability scanning integrated into its pipeline
- Up-to-date acknowledgements file and all dependencies licenses that are
pre-approved (MIT, Apache 2.0, BSD) or have been individually approved by legal

New versions of Trusted projects will be reviewed to verify they
continue to meet the Trusted criteria before they may continue to be
included in a new version at the Trusted level.

## Certified

### Description
A project with a **Certified** Certification Level was either developed using
our internal CyberArk SDLC process or is regularly reviewed by CyberArk
Engineering to verify that it follows the secure development practices that we
use for our own internal development.

### Characteristics
In order for a Trusted feature to become Certified, the following criteria must
be met:

- All Community and Trusted level criteria must be met, plus:
- Code coverage meets targets for Enterprise-level products.