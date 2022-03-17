BhargavBhandari90:issue-181 /FULL/PATH/TO/wp-completion.bash Application Server Management Protocol (DRAFT)

## Abstract

The intent of this protocol is to enable web applications to communicate hosting configuration requirements like software components (i.e. database servers), software versions (i.e. an Apache version) or software settings (i.e. a PHP `memory_limit` value) to a hosting environment, request changes as needed, and query the status of these change requests.

A web application defines constraints for known components, and the hosting provider returns the suggested resolution of these constraints. The web application can then initiate the proposed change, or roll back a previously completed change.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## Definitions

**Component**: A component represents the unit of elements that can be 
**Change**:
**Rollback**:
**Status**:

## Discovery

Web applications need to discover:

* if their hosting environment does support ASMP;
* what ASMP version is supported;
* what network endpoint to use.

Discovery is initiated using environment variables, enabling web applications in all major programming languages to retrieve the ASMP discovery configuration.

A hosting environment with ASMP support MUST set an environment variable named `ASMP_DISCOVERY_VERSION`, with a value stating the version identifier. The initial version of ASMP MUST return the version identifier `"v1"`.

For the initial version of ASMP, the hosting environment MUST set an environment variable named `ASMP_DISCOVERY_ENDPOINT`, with a value in the form of a URI.

The URI provided through `ASMP_DISCOVERY_ENDPOINT` represents the base URI of the API that the specified version of ASMP puts forward.

## Transport
