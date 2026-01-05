---
title: "DNSSEC Signing with an Offline KSK"
# abbrev: "Offline KSK"
category: info

docname: draft-mekking-dnsop-offlineksk-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Internet"
workgroup: DNSOP Working Group
keyword:
 - DNS
 - DNSSEC
venue:
  group: DNSOP
  type: Working Group
  mail: dnsop@ietf.org
  arch: https://datatracker.ietf.org/wg/dnsop/about/
  github: matje/offline-ksk-draft

author:
 -
    fullname: Matthijs Mekking
    organization: ISC
    email: matthijs@isc.org
 -
    fullname: Libor Peltan
    organization: CZNIC
    email: libor.peltan@nic.cz

normative:

informative:

  ICANN-KEYMGMT:
     author:
     -
         fullname: Jakob Schlyter
         organization: Kirei AB
         email: jakob@kirei.se
     -
         fullname: Richard Lamb
         organization: Internet Corporation For Assigned Names and Numbers
         email: richard.lamb@icann.org
     -
         fullname: Ramesh Balasubramanian
         organization: VeriSign, Inc.
         email: rbalasubramanian@verisign.com

     title: DNSSEC Key Management Implementation for the Root Zone (2010)
     target: https://www.iana.org/archive/root-dnssec-launch/files/draft-icann-dnssec-keymgmt-01.txt
     date: 2010-05-11

--- abstract

TODO. How to perform DNSSEC signing with an Offline KSK.

--- middle

# Introduction

The Domain Name System (DNS) is described in {{!RFC1034}} and {{!RFC1035}}.
The DNS Security extensions (DNSSEC) are described in {{!RFC9364}}.

When operating DNSSEC, one of the things to consider is how to generate and
store your keys. While the DNSSEC validation protocol does not distinguish
between different types of DNSKEYs, for operational reasons it is possible to
split the set of keys into Key Signing Keys (KSKs) and Zone Signing Keys (ZSKs).

{{?RFC6781}} argues that where keys are stored offline, the risk that keys can
be compromised through theft of loss is relatively low. However, storing keys
offline makes daily signing operations more complex. Separating the KSK and ZSK
functionality allows the risk to be managed for the KSK, while a readily
available ZSK can be used for automatic signing of the zone, and can be rolled
quickly without any parent interaction required.

This document describes the protocol for DNSSEC signing while the KSK is stored
offline. The procedural steps are based in part on ICANN/IANA DNSSEC Key
Management Implementation for the Root Zone {{ICANN-KEYMGMT}}.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Terminology

DNSSEC Policy, KSK, ZSK, Key Lifetime, Signature Validity, Key Signing Request,
Signed Key Response, ZSK Operator, KSK Operator.

# Procedural steps

These are the steps for DNSSEC signing with an offline KSK.
- Pregenerate ZSKs,
- Request to sign the public keys,
- Sign the public key material,
- Load the signed response into the name server.

TODO: Add more detail.

## Key Signing Request (KSR)

TODO: Desribe how to construct, validate, process.

## Signed Key Response (SKR)

TODO: Describe how to construct, validate, process, and activate.

# Security Considerations {#security}

TODO (if any).

# IANA Considerations {#IANA}

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

TODO: acknowledgements.
