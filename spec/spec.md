Verifiable Credentials (VC) Marketplace Interfaces
==================

**Specification Status:** Pre-Draft

**Latest Draft:**
[identity.foundation/vc-marketplace](https://identity.foundation/vc-marketplace)
<!-- -->
**Editors:**
~ [Martin Riedel](https://www.linkedin.com/in/rado0x54/) (Consensys Mesh)

**Contributors:**


**Participate:**
~ [GitHub repo](https://github.com/decentralized-identity/vc-marketplace)
~ [File a bug](https://github.com/decentralized-identity/vc-marketplace/issues)
~ [Commit history](https://github.com/decentralized-identity/vc-marketplace/commits/master)

------------------------------------

## Abstract

------------------------------------
Work in copy of Hack.md

## Marketplace Use Cases

### Payment-motivated UC
- Payment during issuance
- Payment during presentation

### Buying art at a swiss auction.
Swimlanes.

### Beibehaltungsgenehmigung and Citizenship
- need

## Proposed Generalized (Interface) Marketplace Definitions

### Issuer: VC / Issuer Validation Process Capability Registration (TODO: What about one to many?)
- A Marketplace is the collection of Issuer-based Credenial Manifests
- Issuer Metadata (incl. Reputation information)
    - Issuer self-reported information
    - Collected through crawling
    - Attestations about the Issuer from 3rd parties
- VC Type Metadata
    - what it's required for? (provided by Verifier)
    - where can get it? (provided by Issuer)
    - price
- What "Issuing Processes" should a Credential Manifest Support
    - Presentation Definition (Requirements are known before, one-time request/response)
    - Other: "Manual": NYC DMV issues digital DL, but only by walking into an office.
    - Other: "Multi-Step" Workflow Verification Process (Delegate)
- Versioning
    - Should the format allow to specify previous versions
    - Should this chain of versions be available to external requesters
  
### Further Notes Issuer Registration
- Issuer Service: put it as a service endpoint in DID. Responsibility of the Issuer to host and maintain this information.
- One can image Issuance Use-Cases where a single Action/Process can result in >1 Credential from the Issuer.
  - --> Manifest Binding of Issuer <-> Credential is not ideal for that.
  - 1st Solution: Data format defines Issuing Process --> multiple Credential
  - 2nd Solution: Marketplace is able to programmatically discover credentials from the Issuer that share the same Validation Process (Presentation Definition)
- Marketplace can drive convergance if the usage data for Credential Types is transparent.

# Call 03.09 — Discovery stage (of VC Issuers & Verifiers?)

Discovery is the responsibility of Marketplace operator / system, rather than every individual issuer / verifier.

What are the options to collect credential data?
- Active registration by the issuer ("triggers crawling of targeted domain").
- Web crawler
- P2P gossip (Would not require participant to be discoverable via DNS).


How the data is stored?
- Registry is just a list of issuer / verifier DIDs, stored in
  - Centralized Registry
  - Decentralized Registry (Blockchain, IPFS, etc.)
- Registry might be useful for payments, where issuers need to specify payment details
- Effcient search through marketplace metadata by maintaining (decentralized) indinces

What goes into metadata?
- Every VC type can have a VC (or VC manifest) describing:
  - Issuer DID
  - Signature
  - Description
  - Verification Process (e.g. Presentation Definition)
    - Credential Type A (Schema URI...)
    - Credential Type B
    - ...
  - Price tag

How do we support updates of metadata?
- Issuer publish DID and then DID service endpoint points to the up-to-date hosted metadata document
- Issuers need a guide of (1) how to publish metadata in a correct way and (2) how to keep it up-to-date along the way

How do we collect vc metadata from the issuers & verifier?
- We need to collect metadata from issuers and keep it open.
- Use structured data to publish the metadata: https://developers.google.com/search/docs/guides/intro-structured-data
  - Can help with adoption as it is a widespread and familiar format
  - The team reponsible for maintaining a website will be able to publish metadata (options: calatog of cred manifests, marketplace-specific data)
  - Crawling can be manual (meaning small marketplace operator can reach out to issuers and ask them to submit links directly)

How Holders discover right issuers / VCs?
- Query VC Marketplace for:
  - Price
  - Issuer
  - ??

How does the VC Issuer Data stay up to date?
- Regular "recrawling" by the Marketplace
- Active notification by the issuer
- Should the dataformat allow for versioning?
- Credential Mapping within a VC Manifest.
  Credential (Type) -> Verification Process (e.g. Presentation Defintion)
  1:1
  Verification Process (Presentation Definition) -> 3x Credential (Type)
  1:n
  Multiple Verification Process -> 1x Credential (DOES NOT MAKE SENSE)
  m:1
  Multiple Verification Process -> Multiple Credentials (DOES NOT MAKE SENSE)
  n:m

#### Why Display and Styling should not be part of a VC Registration Process
- Styling is commonly extracted into a dedicated filestructure format (css, sass)
- Display/Styling requirements will grow and the format requirements will grow.
- Crawlers / Marketplaces / Search Engines would not require this information

### Subject-initiated Issuer-Discovery
Subject trying to discover a VC/Issuer (with certain matched constraints) that can be issued from an issuer?

### Reputation
- Reputation for all entities
#### Notes:
- Should we add Reputation into the Marketplace UC?
- Indepenent of other things all Marketplaces need a standardized interface for issuers to register the Credential Capabilities
- These Capabilities
- Reputation "should be up the Marketplace". E.g. some may use token-based incentive Model. Others might use free market forces ("cheapest"), others might use "traditional web" reputation systems.
- How can an individual query different reputation systems in a standardized way?
- E.g. this group should define a standardized interface to be able to query reputation for a DID?
- 0-100 with the following distribution: normal?
- Marketplace can chose to not expose any reputation score.
- Can Reputation Systems be dynamically integrated into Marketplace implementations (e.g. plugs in external provider.)
- Reputation for Holder/Subject should be out-of-scope.
- Reputation Scope for Marketplace should be limited to Verifier/Issuer.
- For the Holder we might want to have p2p reputation proof
- Can we enable Reputation system with only using VCs but not designing the whole reputation methodology?
- Holder can issue their Reputation VC ad-hoc, compiling from data they already have

### Track Credential Issuance (& Payment Coordination)
- Transaction Record (Issuance)
- Start of TX should be recorded (by Issuer)
- Stop (Issuance) of TX should be recorded (Holder)

### Track Credential Presentation (& Payment Coordination)
- Transaction Record (Presentation)

### Track Credential Revocation (& Payment Coordination)
- Transaction Record (Revocation)

## Cross-sectional concerns

## Marketplace Bootstrapping
- Initial Issuer-Vetting by Marketplace during Registration

## Payment (Detail Section)
- Payment is often controversial, however a egalitarian marketplace would be able to drive standardization of Credential Schema and Formats.
- "Traffic" is hidden for general public, but accessible to participants

## Discussion Points

### Open Discussion
1. Registration of Verifiers? Collection of Metadata Collection?
- Issuer may want to "block" usage of credentials for certain verifiers: **Consensus: Should not be supported**
- Payment Problem: "A Verifier has a "special price" for consuming certain issuer-credentials." (ideally "hidden"). Privacy Coins.
  - "Cashback" Option.
- Discoverability: @Talk to Stephan


## Subject-initiated Issuer-Discovery
- What does the query look like?
- Incl. Issuer-Based Reputation Score
- Can we use Presentation Exchange