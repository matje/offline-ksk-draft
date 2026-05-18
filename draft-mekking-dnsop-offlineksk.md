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

This document defines the textual format for regular exchanging data between
the ZSK operator and KSK operator of such offline KSK setup.

It does not define or describe operational practices for Offline KSK, although
it briefly outlines them in the introduction in order to make clear when is
being defined. MM: Do we really need to state this explicitly? What does it
mean exactly?

TODO: What data and metadata are being exchanged and when. MM: Perhaps in
section describing procedural steps?

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Terminology

TODO: DNSSEC Policy, KSK, ZSK, Key Lifetime, Signature Validity,
Key Signing Request (KSR), Signed Key Response (SKR), ZSK Operator,
KSK Operator, Offline KSK.

# Procedural steps

These are the steps for DNSSEC signing with an offline KSK.
- Pregenerate ZSKs,
- Request to sign the public keys,
- Sign the public key material,
- Load the signed response into the name server.

TODO: Add more detail.

## Key Signing Request (KSR)

TODO: Desribe how to construct, validate, process.

TODO: Format of KSR: header line, DNSKEY ZSK records (note: matching SEP bit
setting (to zero) is recommended but not mandated), mentioning that it MAY
contain other types of records from the zone (possibly even out of the apex?)
if the ZSK side is in control of them and wishes to sign them with KSK, but
the KSK side MAY ignore and discard them.

## Signed Key Response (SKR)

TODO: Describe how to construct, validate, process, and activate.

TODO: Format of SKR: header line, DNSKEY ZSK + KSK records, CDS+CDNSKEY
records, other records, RRSIGs of all of the RRsets (MUST be present for
anything that appears there).

# Security Considerations {#security}

TODO (if any).

# IANA Considerations {#IANA}

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

TODO: acknowledgements.

# Appendix A: SKR and KSR format type

Why not JSON?
1) Because the metadata is so trivial that even JSON is an overkill
(unnecessary dependency) where fscanf is just fine.
2) Because the goal here is interoperability and when we already have this
format in use, defining a different (even if better) format would undermine
the compatibility.
