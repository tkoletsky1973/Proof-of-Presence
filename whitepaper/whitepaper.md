# Proof of Presence
## A Privacy-Preserving Protocol for Verifiable Human Presence

**Version:** 0.1 (Draft)  
**Status:** Public Working Paper  
**Last Updated:** 2025  
**Repository:** https://github.com/tkoletsky1973/Proof-of-Presence

---

### Abstract
Presence is a fundamental fact of human life.

Where we have been determines our right to work, travel, study, receive aid, attend events, and participate in society. Yet today, presence is either poorly documented or excessively monitored. Passports prove nationality, not lived reality. GPS tracking collects far more data than necessary and places control in the hands of governments and corporations. Databases centralize trust while exposing individuals to surveillance, misuse, and exclusion.

Proof of Presence (PoP) introduces a different model.

Rather than tracking people continuously, Proof of Presence allows individuals to obtain cryptographically verifiable attestations of presence at specific moments, issued by trusted entities such as airports, employers, universities, event organizers, or local authorities. Each attestation confirms that a person was present within a defined location zone and time window, without revealing exact coordinates, identity, or behavioral data.

Only a minimal cryptographic commitment is recorded on a public blockchain to ensure integrity and verifiability. All detailed information remains encrypted and under the individual’s control. Over time, individual attestations can be combined into higher-level claims—such as duration of presence in a country or participation in a program—using deterministic public rules that can be verified by any third party.

Proof of Presence is not an identity system, a tracking platform, or a financial product. It requires no native token to function. It is a neutral protocol for making lived reality provable while preserving privacy, autonomy, and freedom of movement.

By separating proof from surveillance, Proof of Presence enables a future where individuals can demonstrate real-world facts without surrendering ownership of their lives to centralized systems.


## Table of Contents

1. Introduction  

2. The Problem of Presence  

3. Design Principles  

4. The Core Idea: Presence Without Surveillance  

5. System Overview  

6. Technical Architecture  

7. Protocol Layers  

8. Blockchain Design  

9. Attestations  

10. Aggregated Presence Claims  

11. Privacy and User Control  

12. Real-World Operation  

13. Economic Model (No Token)  

14. Governance and Trust Model  

15. Security Considerations  

16. Legal and Regulatory Context  

17. Limitations and Non-Goals  

18. Implementation Roadmap  

19. Conclusion


## 1. Introduction

Physical presence is a foundational input to modern systems of governance, commerce, education, and civil participation. Whether an individual was present in a country, at a workplace, within a jurisdiction, or at a specific event often determines eligibility, compliance, access, or rights. Despite its importance, presence remains difficult to prove in a precise, privacy-preserving, and portable way.

Existing mechanisms for documenting presence rely on indirect proxies. Passports and visas record nationality and authorization, not lived duration. Employment and education systems depend on centralized records that are difficult to transfer or independently verify. Location technologies such as GPS enable continuous tracking but require surrendering control of personal movement data to centralized platforms. These approaches create gaps between lived reality and documented reality, while introducing unnecessary surveillance, data risk, and administrative cost.

Proof of Presence (PoP) addresses this gap by defining a protocol for verifiable physical presence that does not require continuous monitoring, identity disclosure, or centralized data ownership. The protocol enables individuals to obtain cryptographically signed attestations of presence at specific moments, issued by trusted entities, and to later prove higher-level claims derived from those attestations using deterministic public rules.

From a technical perspective, Proof of Presence separates three concerns that are commonly conflated in existing systems:
1. **Observation** (who confirms presence)
2. **Proof** (how presence is made verifiable)
3. **Disclosure** (what is revealed, to whom, and when)

By decoupling these concerns, the protocol allows presence to be proven without exposing raw location data, behavioral patterns, or identity beyond what is strictly required for a given use case.

While Proof of Presence is designed as a neutral protocol, its relevance spans multiple institutional domains. Governments and public agencies may rely on verifiable presence to support immigration, residency, voting eligibility, or benefit distribution. Employers and organizations may require presence proofs for labor compliance, remote work validation, or contractual obligations. Educational and research institutions may use presence verification to support accreditation, attendance-based funding, or field research validation. Event organizers and humanitarian organizations may use presence attestations to prevent fraud and improve accountability.

For individuals, the protocol enables presence records that are portable across institutions and jurisdictions, controlled by the individual rather than the issuer, and disclosed selectively based on context. For institutions, it reduces reliance on opaque databases, manual audits, and invasive tracking technologies, while increasing trust in claims derived from physical presence.

This paper defines the Proof of Presence protocol, its technical architecture, trust model, and economic structure. It is written to support implementation, evaluation, and adoption by independent parties, without requiring reliance on a single operator, token, or proprietary system.


## 2. The Problem of Presence

Physical presence is frequently treated as an implicit or assumed condition rather than a verifiable fact. Many systems depend on presence to grant rights, enforce rules, or distribute resources, yet lack a reliable, privacy-preserving method to confirm that presence occurred as claimed.

### 2.1 Presence Is Indirectly Inferred

Most existing systems infer presence through indirect indicators rather than proving it directly. Passports and visas indicate authorization to enter a country, not whether an individual actually remained there for a given duration. Employment records may assert that work was performed, but often rely on self-reporting or centralized logs rather than independently verifiable proof of on-site presence. Educational attendance is typically recorded in institution-specific systems that are difficult to audit or transfer.

*Example:* An individual may be authorized to stay in a country for 90 days but has no standardized, portable way to prove that they were physically present for 60 of those days without surrendering travel records, hotel bookings, or bank data.

### 2.2 Tracking Systems Over-Collect Data

Technologies capable of precisely locating individuals, such as GPS and mobile network telemetry, collect far more information than is required to prove presence. Continuous location tracking exposes detailed movement patterns, routines, and associations. This data is typically stored and controlled by centralized entities, creating risks of misuse, unauthorized access, and long-term surveillance.

From a systems perspective, tracking solves a different problem than presence verification. Tracking answers the question “Where is this person at all times?” whereas most institutional use cases only require answers to questions such as “Was this person present in this location during this time window?”

*Example:* A remote worker may need to prove they were physically present in a specific jurisdiction during a contract period, yet GPS tracking would unnecessarily reveal every location visited during that time.

### 2.3 Presence Records Are Fragmented and Non-Portable

When presence is documented, it is usually stored in siloed databases maintained by individual organizations. These records are rarely interoperable, difficult to verify externally, and often inaccessible to the individual they describe. Transferring proof of presence between institutions typically requires manual processes, attestations by authority, or repeated verification.

This fragmentation increases administrative cost and reduces trust. Verifiers must either accept unverified claims or require redundant documentation from multiple sources.

*Example:* An individual attending multiple international conferences may need separate attendance confirmations for employers, visa authorities, and funding bodies, each relying on different formats and verification standards.

### 2.4 Presence Is Vulnerable to Fraud and Exclusion

Because presence is poorly defined and inconsistently documented, systems that depend on it are vulnerable to both fraud and wrongful exclusion. Fraud may occur when individuals falsely claim presence without robust verification. Exclusion occurs when individuals who were present cannot easily prove it, often due to lack of documentation, displacement, or institutional failure.

These failures disproportionately affect mobile populations, remote workers, researchers, refugees, and individuals operating across jurisdictions.

*Example:* A humanitarian aid recipient may be physically present in a designated area but unable to access services due to missing or unverifiable records.

### 2.5 Centralized Control of Presence Creates Power Imbalances

When presence data is centrally controlled, individuals have limited ability to audit, correct, or reuse records that affect them. Institutions become gatekeepers of truth, and errors or policy changes can retroactively alter access or eligibility. This dynamic reduces transparency and places individuals at a structural disadvantage.

From a protocol perspective, the problem is not the absence of data, but the absence of a neutral, verifiable, and user-controlled mechanism for asserting presence as a fact.

### 2.6 Requirements for a Viable Solution

Any system intended to address the problem of presence must satisfy several constraints:

- Presence must be verifiable by third parties.
- Verification must not require continuous tracking.
- Data disclosure must be minimal and context-dependent.
- Records must be portable across institutions and jurisdictions.
- Individuals must retain control over their presence data.
- The system must be resistant to fraud without relying on centralized authority.

Existing approaches fail to satisfy these constraints simultaneously. The following sections describe how Proof of Presence is designed to meet them.


## 3. Design Principles

Proof of Presence is governed by a set of strict design principles that constrain both technical implementation and institutional use. These principles are not aspirational; they are requirements. Any implementation that violates them is not considered compliant with the protocol.

### 3.1 Opt-In Participation Only

All presence records within the Proof of Presence protocol are created through explicit user action. Presence is never inferred, harvested, or passively collected. An individual must actively consent to each attestation event.

This principle ensures that presence cannot be recorded without awareness, preventing covert tracking or retroactive reconstruction of movement.

### 3.2 Attestation Over Tracking

Proof of Presence relies on discrete attestations issued by trusted entities at specific moments, rather than continuous monitoring of location.

Tracking systems answer where an individual is at all times. Proof of Presence answers whether an individual was present within a defined context and time window. The protocol is intentionally designed to support the latter and reject the former.

### 3.3 Minimal Disclosure by Default

The protocol requires that only the minimum information necessary to verify a claim is disclosed. Exact coordinates, continuous timelines, behavioral data, and identity are excluded unless explicitly required for a specific use case.

Presence is represented using coarse location zones and bounded time windows. Higher-resolution data is neither required nor encouraged.

### 3.4 User Control of Data

All detailed presence data remains under the control of the individual. The blockchain stores only cryptographic commitments sufficient to prove the existence and validity of attestations, not the underlying data itself.

Users control if, when, and how presence information is disclosed to third parties, including the ability to generate different claims from the same underlying attestations.

### 3.5 Public Verifiability Without Central Authority

Presence claims must be verifiable by any third party using public information and deterministic rules, without reliance on a central operator or proprietary database.

Verification does not require contacting the original attester, the user, or a governing organization, provided the necessary proofs are disclosed.

### 3.6 Separation of Observation, Proof, and Disclosure

The protocol explicitly separates:
- **Observation**: the act of confirming presence (performed by an attester)
- **Proof**: the cryptographic representation of that confirmation
- **Disclosure**: the selective revelation of derived claims

This separation prevents attesters from controlling how presence is later used and prevents verifiers from accessing more information than necessary.

### 3.7 Neutrality and Interoperability

Proof of Presence is designed to be neutral with respect to jurisdiction, industry, and blockchain implementation. The protocol does not privilege any single chain, institution, or operator.

Interoperability across chains, applications, and verification contexts is a core requirement, not an extension.

### 3.8 No Financialization of Truth

Presence itself is not a financial asset. The protocol does not require a native token to function, and presence claims do not represent ownership, value transfer, or entitlement beyond their specific verification context.

This principle ensures that truth is not subject to speculation, incentives, or market manipulation.

These principles define the boundaries within which Proof of Presence operates. The following sections describe how these constraints are realized in system architecture and protocol design.


## 4. The Core Idea: Presence Without Surveillance

The central idea of Proof of Presence is that physical presence can be proven as a discrete fact without observing, recording, or reconstructing a person’s continuous movement.

Most existing systems conflate presence with tracking. They assume that in order to prove that an individual was present in a location for a period of time, it is necessary to monitor where that individual was before, during, and after that period. This assumption leads to systems that collect excessive data, centralize control, and expose individuals to long-term surveillance.

Proof of Presence rejects this assumption.

Instead, the protocol treats presence as a **verifiable event**, not a continuous state. Presence is confirmed at specific moments by trusted entities and represented as attestations that describe *where*, *when*, and *under what context* presence occurred—without attempting to reconstruct everything in between.

### Presence as a Fact, Not a Trail

In the Proof of Presence model, presence is defined as a factual claim that can be independently verified:

> An individual was physically present within a defined location zone during a defined time window, as confirmed by a trusted attester.

This claim does not require knowledge of how the individual arrived, where they went afterward, or what other locations they visited. The protocol deliberately avoids generating trails, paths, or timelines beyond what is strictly required.

By limiting proof to bounded facts rather than continuous data, Proof of Presence enables verification without behavioral surveillance.

### Moment-Based Attestation

Presence is recorded through **moment-based attestations**. Each attestation corresponds to a specific interaction between an individual and an attester, such as:
- entering or exiting a controlled area,
- attending a verified event,
- reporting to a workplace or institution,
- enrolling in or completing a program.

These moments are intentional and explicit. The individual opts in to receiving an attestation, and the attester confirms presence within the scope they are authorized to verify.

There is no background monitoring, passive sensing, or inferred presence.

### Aggregation Without Observation

While individual attestations represent discrete moments, many real-world use cases require reasoning over time, such as duration of stay or repeated participation.

Proof of Presence addresses this through **aggregation**, not observation.

Higher-level claims—such as cumulative days in a country or number of verified attendances—are derived by combining multiple attestations according to deterministic public rules. These rules operate on attestations as inputs and produce claims as outputs, without introducing new data collection.

The protocol therefore distinguishes between:
- *observing presence* (performed once per attestation), and
- *reasoning about presence* (performed later, without further observation).

### Proof Without Identity

The core idea of Proof of Presence does not require global identity disclosure. Presence attestations are bound cryptographically to a user-controlled key, not to a publicly visible identity.

This allows presence to be proven:
- without revealing name or nationality,
- without linking attestations across contexts unless the user chooses,
- without creating a universal movement profile.

Identity may be introduced only where a specific use case explicitly requires it, and even then, it remains orthogonal to the presence proof itself.

### Neutral Verification

Presence claims generated under this model can be verified by any third party with access to the disclosed proofs and the public verification rules. Verification does not require trust in the verifier, the user, or a central authority beyond the attesters whose signatures are referenced.

This neutrality ensures that presence remains a shared fact rather than an institutional assertion.

### Summary

Proof of Presence demonstrates that it is possible to make physical presence verifiable without turning human movement into a dataset. By treating presence as a moment-based, attestable fact rather than a continuously tracked condition, the protocol enables verification, privacy, and portability simultaneously.

The following sections describe how this idea is realized in system design and technical architecture.


## 5. System Overview

The Proof of Presence protocol is composed of a small number of clearly defined actors and a minimal set of interactions between them. The system is intentionally designed to avoid complex dependencies, centralized coordination, or continuous data flows.

At a high level, the protocol enables an individual to receive verifiable attestations of physical presence from trusted entities, anchor cryptographic commitments to those attestations on a public blockchain, and later derive and disclose presence claims to third parties for verification.

### Core Actors

The system involves four primary actors:

**Individual (User)**  
The individual is the subject of the presence being attested. The individual controls a cryptographic keypair used to receive attestations, store encrypted presence data, and generate selective disclosures. The individual is the sole authority over whether and how their presence information is shared.

**Attester**  
An attester is an entity authorized to confirm physical presence within a specific context. Examples include border authorities, employers, universities, event organizers, or humanitarian organizations. Attesters issue signed presence attestations only when an individual is physically present and has opted in to receiving an attestation.

Attesters do not control how attestations are later used or disclosed.

**Verifier**  
A verifier is any party that needs to confirm a presence claim. Verifiers may include government agencies, employers, service providers, or auditors. Verification is performed using public cryptographic proofs and deterministic rules, without requiring direct communication with the attester or access to raw presence data.

**Public Ledger**  
The public ledger provides an immutable, timestamped record of cryptographic commitments corresponding to presence attestations. The ledger does not store personal data, location coordinates, or identity information. Its sole role is to provide integrity, ordering, and public verifiability.

### High-Level Flow

The protocol operates through the following sequence:

1. The individual interacts with an attester at a specific place and time.
2. The attester confirms physical presence within its authorized scope.
3. The attester issues a signed presence attestation to the individual.
4. A cryptographic commitment to the attestation is anchored on a public ledger.
5. The individual stores the full attestation data off-chain under their control.
6. At a later time, the individual derives a presence claim from one or more attestations.
7. The claim is disclosed to a verifier, who independently verifies it using public data and rules.

This flow separates presence confirmation from later verification, allowing presence to be proven without ongoing interaction between parties.

### Data Ownership and Control

At no point does the system require centralized storage of raw presence data. Attesters may retain their own operational records as required by their internal policies, but the protocol does not depend on those records being accessible to verifiers.

Individuals retain custody of their attestations and determine which claims are generated and disclosed. Verifiers receive only the information required to evaluate a specific claim.

### Trust Boundaries

Trust within the system is localized and explicit. Verifiers trust attesters only within the scope of what they are authorized to attest. Individuals trust attesters to issue accurate attestations at the moment of presence. The public ledger is trusted solely for integrity and ordering, not for correctness of claims.

No single actor has global authority over presence truth.

### System Characteristics

The resulting system has several defining characteristics:

- No continuous data collection
- No global identity requirement
- No centralized database of movement
- No reliance on a single operator
- Verifiability without disclosure

The next section describes the technical architecture that enables this system while enforcing the design principles defined earlier.


## 6. Technical Architecture

The Proof of Presence protocol is designed as a modular system composed of clearly separated technical components. Each component has a narrowly defined role, enabling independent implementation, replacement, and scaling without compromising the integrity of the protocol as a whole.

The architecture enforces the design principles described earlier by separating data custody, verification, and settlement across distinct layers.

### Architectural Components

At a high level, the protocol consists of the following components:

**Client Layer**  
The client layer is operated by the individual. It manages cryptographic keys, receives and stores presence attestations, constructs presence claims, and controls disclosure. The client may be implemented as a mobile application, hardware wallet integration, browser-based wallet, or other secure user-controlled environment.

The client is the sole location where full, decrypted presence data exists.

**Attester Systems**  
Attesters operate systems capable of confirming physical presence within their authorized context. These systems may include kiosks, secure terminals, mobile devices, or backend services integrated with existing infrastructure. Attesters generate signed attestations only at the moment presence is confirmed and do not require access to the blockchain to perform confirmation.

Attester systems are responsible for key management, authorization scope enforcement, and attestation signing.

**Public Ledger Interface**  
The public ledger interface handles the anchoring of cryptographic commitments corresponding to attestations. This interface abstracts the underlying blockchain implementation, allowing different chains or settlement layers to be used without altering higher-level protocol logic.

Only minimal commitment data and metadata required for verification are submitted on-chain.

**Verification Logic**  
Verification logic consists of deterministic rules and cryptographic checks used to evaluate presence claims. This logic can be implemented by any verifier and does not require proprietary software, trusted execution environments, or privileged access.

Verification relies solely on disclosed proofs, public ledger data, and known attester public keys.

### Data Separation

A core architectural property of the protocol is strict data separation:

- Raw presence data and contextual details remain off-chain.
- Encrypted attestations are stored under user control.
- On-chain records contain only cryptographic commitments and timestamps.
- Verification operates on proofs, not databases.

This separation minimizes data exposure while preserving verifiability.

### Cryptographic Foundations

The protocol relies on established cryptographic primitives rather than novel constructions. These include:

- Public-key cryptography for identity binding and signatures
- Cryptographic hash functions for commitments
- Merkle structures for aggregation and proof construction
- Optional zero-knowledge techniques for advanced disclosure control

All cryptographic choices are intended to be implementation-agnostic and replaceable as standards evolve.

### Chain Neutrality

The architecture does not assume a specific blockchain or consensus mechanism. Any public ledger capable of providing immutable ordering, timestamping, and data availability may be used. Multiple ledgers may be supported simultaneously to reduce dependency on a single network.

This neutrality allows Proof of Presence to evolve alongside underlying infrastructure without protocol redesign.

### Failure Isolation

Each architectural component is designed to fail independently without collapsing the system:

- Attester outages do not affect existing attestations.
- Ledger congestion delays anchoring but does not invalidate attestations.
- Client loss does not expose data but may require recovery mechanisms.
- Verifier errors do not affect record integrity.

This isolation is critical for real-world deployment across jurisdictions and institutions.

### Summary

The technical architecture of Proof of Presence enforces minimal disclosure, user control, and public verifiability through clear separation of responsibilities. By avoiding centralized storage and monolithic systems, the protocol remains resilient, auditable, and adaptable.

The next section introduces the protocol layer model that organizes these components into a coherent, multi-layered system.


## 7. Protocol Layers

The Proof of Presence protocol is organized as a layered system in which each layer serves a distinct purpose and enforces specific constraints. Layers are conceptual, not necessarily tied to software boundaries, and may be implemented independently or combined depending on deployment context.

This layered approach ensures that trust, verification, data custody, and application logic are separated and can evolve without breaking the protocol.

### Layer 0: Trust and Attestation Authority

Layer 0 defines the real-world trust anchors of the system. It consists of entities authorized to attest to physical presence within a defined scope. These entities may include governments, employers, educational institutions, event organizers, humanitarian organizations, or other accredited bodies.

Layer 0 operates entirely off-chain. Its function is to answer a single question: *was this individual physically present within the context I am authorized to verify?*

Layer 0 responsibilities include:
- Physical or contextual confirmation of presence
- Scope enforcement (where and when an attester is authorized)
- Attestation signing
- Attestation revocation when required

Layer 0 does not store global records, perform aggregation, or participate in verification beyond issuing signed attestations.

### Layer 1: Public Settlement and Integrity Layer

Layer 1 provides immutable ordering, timestamping, and public availability of cryptographic commitments corresponding to attestations. This layer ensures that attestations cannot be altered, reordered, or backdated after issuance.

Only minimal data is recorded at this layer:
- Cryptographic commitment (hash) of the attestation
- Attester identifier
- Timestamp or block reference
- Optional revocation reference

Layer 1 does not contain raw presence data, identity information, or claim logic. Its sole purpose is to anchor proof integrity.

### Layer 2: Attestation Aggregation and Claim Construction

Layer 2 defines how multiple attestations can be combined to form higher-level presence claims. Aggregation rules are deterministic and publicly defined, ensuring that identical inputs produce identical outputs.

Examples of Layer 2 operations include:
- Calculating cumulative presence duration
- Counting verified attendances
- Evaluating threshold conditions
- Constructing Merkle proofs for subsets of attestations

Layer 2 operates on user-held data and produces proofs suitable for verification. It does not introduce new observations or data collection.

### Layer 3: Disclosure and Verification

Layer 3 governs how claims are disclosed and verified. It defines the verification logic used by third parties to validate presence claims against public ledger data and known attester keys.

Verification at this layer is:
- Stateless
- Deterministic
- Independent of any central service

Verifiers require no access to raw presence data beyond what is explicitly disclosed for a given claim.

### Layer 4: Applications and Policy Contexts

Layer 4 consists of applications, policies, and institutional processes that consume presence claims. These may include visa systems, employment audits, educational accreditation, event access control, or aid distribution mechanisms.

Layer 4 is explicitly outside the protocol’s control. The protocol does not dictate how claims are interpreted, only how they are proven.

### Layer Separation Guarantees

The layered structure enforces the following guarantees:
- Observation occurs only at Layer 0
- Integrity is enforced at Layer 1
- Reasoning occurs at Layer 2
- Disclosure is controlled at Layer 3
- Policy decisions occur at Layer 4

No layer has sufficient information or authority to reconstruct full movement history or override user control.

### Summary

By separating trust, integrity, aggregation, disclosure, and application logic into distinct layers, Proof of Presence enables verifiable physical presence without centralized surveillance or control. Each layer can evolve independently while preserving the protocol’s core guarantees.

The next section examines the blockchain design choices that support Layer 1 without imposing unnecessary constraints on higher layers.


## 8. Blockchain Design

The Proof of Presence protocol uses a blockchain as a public integrity and settlement layer, not as a data store, identity system, or execution environment. The blockchain’s role is intentionally narrow: to provide immutable ordering, timestamping, and public availability of cryptographic commitments that correspond to presence attestations.

This section defines what the blockchain is used for, what it is explicitly not used for, and how chain selection remains flexible without affecting protocol correctness.

### Purpose of the Blockchain Layer

The blockchain serves four essential functions within the protocol:

1. **Immutability**  
   Once a cryptographic commitment to an attestation is recorded, it cannot be altered or removed without detection.

2. **Timestamping**  
   The ledger provides a publicly verifiable time reference that anchors when an attestation existed, independent of the attester or the individual.

3. **Ordering**  
   Attestations can be ordered relative to one another, enabling deterministic aggregation and claim construction.

4. **Public Verifiability**  
   Any verifier can independently confirm that a disclosed attestation or claim corresponds to a commitment recorded on the ledger.

No other functions are delegated to the blockchain.

### On-Chain Data Model

Only minimal, non-sensitive data is written on-chain. A typical on-chain record includes:

- A cryptographic hash or commitment derived from the attestation
- An identifier for the attester’s public key
- A timestamp or block reference
- Optional metadata required for revocation or versioning

The blockchain never stores:
- Raw presence data
- Location coordinates
- Identity information
- Behavioral or movement history
- Aggregated claims

This minimalism is essential to privacy, scalability, and long-term sustainability.

### Chain Neutrality

The protocol does not depend on any specific blockchain network, consensus mechanism, or virtual machine. Any ledger capable of providing immutable ordering and public accessibility may be used.

This includes, but is not limited to:
- Layer 1 blockchains
- Layer 2 rollups
- Permissioned public ledgers
- Multiple ledgers operating in parallel

Chain neutrality allows implementations to adapt to regulatory, performance, and cost constraints without altering higher-level protocol logic.

### Multiple Ledger Support

To reduce dependency on a single network, the protocol may support anchoring commitments to multiple ledgers. In such cases, attestations may reference one or more ledger commitments, and verifiers may accept proofs anchored on any supported ledger.

This approach increases resilience against censorship, network failure, or governance changes at the ledger level.

### Smart Contract Usage

Smart contracts, where used, are limited to:
- Recording commitments
- Managing attester key registries
- Publishing revocation references

No application logic, aggregation rules, or disclosure policies are enforced on-chain. This minimizes attack surface and avoids locking protocol behavior into immutable code prematurely.

### Cost Considerations

Blockchain transaction costs are treated as an operational expense rather than a protocol-level incentive. The protocol does not require users to hold tokens or interact directly with the ledger in most cases. Anchoring may be performed by attesters, service operators, or aggregators on behalf of users.

Cost optimization strategies, such as batching or rollups, are implementation details and do not affect protocol semantics.

### Summary

By restricting the blockchain’s role to integrity, ordering, and public verifiability, Proof of Presence avoids the common failure modes of overloading ledgers with personal data or business logic. This design ensures privacy, scalability, and adaptability while preserving strong cryptographic guarantees.

The next section defines the structure and lifecycle of presence attestations themselves.


## 9. Attestations

Attestations are the fundamental data objects of the Proof of Presence protocol. Each attestation represents a discrete, verifiable confirmation that an individual was physically present within a defined context at a defined time.

Attestations are intentionally narrow in scope. They do not describe continuous movement, behavioral patterns, or identity attributes beyond what is strictly required to establish presence.

### Attestation Definition

An attestation is a cryptographically signed statement issued by an authorized attester to an individual-controlled key. It asserts the following minimal facts:

- The subject was physically present
- The presence occurred within a defined location zone
- The presence occurred within a defined time window
- The attestation was issued by a specific attester acting within its authorized scope

The attestation does not assert intent, purpose, duration beyond the defined window, or any information outside the attester’s verification authority.

### Attestation Structure

An attestation includes, at minimum, the following components:

- **Subject Identifier**  
  A reference to the individual’s public key or derived identifier. This identifier binds the attestation to the individual without requiring disclosure of real-world identity.

- **Attester Identifier**  
  A reference to the attester’s public key and accreditation scope.

- **Location Zone**  
  A coarse-grained geographic or contextual identifier, such as a country, campus, facility, or event boundary. Exact coordinates are explicitly excluded.

- **Time Window**  
  A bounded interval during which presence was confirmed. This may be a single moment or a short duration, depending on attester policy.

- **Context Metadata**  
  Optional metadata describing the context of the attestation, such as event type or verification method, expressed in a standardized, non-sensitive format.

- **Signature**  
  A cryptographic signature produced by the attester, binding all fields together.

### Issuance Process

Attestations are issued only through explicit interaction between the individual and the attester. The issuance process consists of:

1. The individual opts in to receive an attestation.
2. The attester confirms physical presence using its authorized verification method.
3. The attester constructs and signs the attestation.
4. The individual receives the attestation and stores it off-chain under their control.
5. A cryptographic commitment to the attestation is anchored on the public ledger.

At no point is continuous monitoring required or permitted.

### Validity and Scope

Each attestation is valid only within the scope defined by the attester’s authority. Verifiers evaluate attestations based on:
- Whether the attester is trusted for the relevant context
- Whether the attestation falls within the required time bounds
- Whether the attestation has been revoked or superseded

Attestations do not imply trust beyond their explicit scope.

### Revocation and Expiry

Attestations may be revoked or marked as expired under defined conditions, such as:
- Issuance error
- Fraud detection
- Policy changes
- Time-based expiration

Revocation references are recorded on the public ledger to ensure verifiers can detect invalid attestations without accessing private data.

### Non-Transferability

Attestations are non-transferable by design. They are bound cryptographically to the subject’s key and cannot be reassigned or reused by another individual.

This property prevents resale, duplication, or delegation of presence.

### Summary

Attestations provide a precise, privacy-preserving unit of presence proof. By limiting their scope, structure, and lifecycle, the protocol ensures that presence can be verified as a fact without enabling surveillance or misuse.

The next section describes how multiple attestations can be combined to form higher-level presence claims.


## 10. Aggregated Presence Claims

Aggregated presence claims allow multiple individual attestations to be combined into higher-level statements about presence over time. These claims are derived entirely from existing attestations and do not introduce new observation, data collection, or trust assumptions.

Aggregation is a computational and logical process, not a sensing process.

### Purpose of Aggregation

Many real-world requirements depend on cumulative or threshold-based presence rather than single moments. Examples include minimum days spent within a jurisdiction, repeated attendance at an institution, or participation across multiple events.

Aggregated claims enable such requirements to be evaluated while preserving the privacy and minimal disclosure properties of individual attestations.

### Deterministic Aggregation Rules

All aggregation within the protocol is governed by deterministic, publicly defined rules. Given the same set of attestations and the same aggregation parameters, the resulting claim must be identical.

Aggregation rules specify:
- Which attestations are eligible for inclusion
- How time windows are interpreted
- How overlaps are handled
- How totals or thresholds are calculated

This determinism ensures that aggregation is verifiable and reproducible by any verifier.

### Claim Construction

An aggregated presence claim consists of:
- A statement of the asserted condition (e.g., “present for at least 30 days”)
- A cryptographic proof linking the claim to a specific set of attestations
- References to the corresponding on-chain commitments
- Optional metadata describing the aggregation method used

The claim does not require disclosure of individual attestation details beyond what is necessary to validate the aggregation.

### Proof Generation

Claims are constructed by the individual using attestations stored under their control. The individual selects which attestations to include and generates a proof that demonstrates the claim’s validity according to the aggregation rules.

Proofs may use Merkle trees or equivalent structures to allow selective inclusion and efficient verification.

### Verification Process

To verify an aggregated presence claim, a verifier performs the following steps:

1. Validate the cryptographic proof against the disclosed attestations.
2. Confirm that each referenced attestation commitment exists on the public ledger.
3. Verify that none of the attestations have been revoked or expired.
4. Apply the public aggregation rules to confirm the claim.

Verification does not require access to undisclosed attestations or private data.

### Granularity Control

Aggregated claims are designed to support varying levels of granularity. An individual may prove:
- A minimum duration without revealing exact dates
- Presence within a region without revealing specific locations
- Participation count without revealing individual events

This flexibility allows claims to be tailored to different verification contexts.

### Summary

Aggregated presence claims transform discrete attestations into meaningful, verifiable statements without expanding data collection or surveillance. By relying on deterministic rules and user-controlled proof generation, the protocol supports complex real-world requirements while maintaining privacy and trust.

The next section addresses how privacy and user control are enforced throughout the system.


## 11. Privacy and User Control

Privacy and user control are not optional features of the Proof of Presence protocol; they are structural requirements enforced through design choices at every layer. The protocol assumes that presence information is sensitive by default and must remain under the control of the individual unless explicitly disclosed.

### Data Minimization by Design

The protocol is constructed to minimize data creation and retention at every stage. Only information strictly necessary to establish verifiable presence is generated, and no component of the system requires access to full movement histories, behavioral data, or identity attributes.

Presence is represented using bounded time windows and coarse location zones rather than continuous timelines or precise coordinates. This ensures that even valid attestations reveal as little information as possible.

### User-Controlled Data Custody

All detailed presence data, including full attestations, is stored off-chain under the control of the individual. The protocol does not require centralized storage, custodial accounts, or third-party data vaults.

Users control:
- Where attestations are stored
- Which attestations are used to construct claims
- What information is disclosed to verifiers
- When disclosures occur

Loss of access to attestations affects only the individual’s ability to prove presence; it does not expose data to others.

### Selective Disclosure

The protocol supports selective disclosure, allowing individuals to prove specific facts without revealing underlying details. For example, an individual may prove:
- A minimum duration of presence without revealing dates
- Presence within a country without revealing cities or venues
- Attendance count without revealing event identities

Selective disclosure ensures that verifiers receive only the information necessary to evaluate a claim.

### Separation of Identity and Presence

Proof of Presence does not require global identity disclosure. Attestations are bound to cryptographic keys rather than to names, passport numbers, or national identifiers.

Where identity is required for a specific use case, it is introduced as an external dependency and remains logically separate from the presence proof itself. This prevents the protocol from becoming an identity registry or tracking system.

### Expiration and Revocation

Presence information is not assumed to be permanently relevant. Attestations and claims may include explicit expiration conditions, after which they are no longer valid for verification.

Revocation mechanisms allow attesters to invalidate attestations in cases of error, fraud, or policy change. Revocation status is recorded on the public ledger without revealing private data.

### Resistance to Correlation

The protocol is designed to minimize unintended correlation between attestations. Attestations from different contexts are not automatically linkable unless the individual chooses to link them when constructing a claim.

This property reduces the risk of creating comprehensive movement profiles across institutions or jurisdictions.

### Summary

By enforcing data minimization, user custody, selective disclosure, and separation of identity from presence, Proof of Presence enables verifiable physical presence without centralized surveillance or loss of autonomy. Privacy is not layered on after the fact; it is embedded into the protocol’s core structure.

The next section describes how these properties are applied in real-world operational contexts.


## 12. Real-World Operation

This section describes how the Proof of Presence protocol operates in practical, real-world environments. The focus is on operational flows rather than policy outcomes or technical internals, demonstrating how the protocol integrates into existing systems with minimal disruption.

### Operational Contexts

Proof of Presence is designed to function across a wide range of environments where physical presence is relevant. These include controlled environments, semi-controlled environments, and open environments.

Controlled environments are locations or contexts where presence verification is already part of standard operations, such as border crossings, secured facilities, campuses, or registered events. Semi-controlled environments include workplaces, research sites, or temporary program locations. Open environments may include humanitarian zones or informal gatherings where verification authority is limited but still possible.

### Attestation at the Point of Presence

In all contexts, presence attestations are issued at the point where presence is confirmed. The individual interacts directly with the attester using a device or interface appropriate to the environment, such as a kiosk, mobile terminal, or secured application.

The attester confirms presence using its existing verification methods and issues a signed attestation to the individual’s client. The process is explicit and opt-in, requiring active participation by the individual.

### Handling Duration-Based Requirements

Duration-based requirements are satisfied through aggregation rather than extended monitoring. Attestations may represent entry, exit, periodic check-ins, or discrete participation moments depending on the context.

The protocol does not require continuous presence confirmation. Duration is inferred later through aggregation rules applied to multiple attestations.

### Integration with Existing Systems

Proof of Presence is designed to integrate with existing institutional systems rather than replace them. Attesters may continue to maintain internal records as required by law or policy. Verifiers may incorporate presence claims into existing workflows without modifying their underlying decision logic.

The protocol provides a standardized, verifiable proof layer that can be adopted incrementally.

### Offline and Intermittent Connectivity

The protocol supports environments with limited or intermittent connectivity. Attestations may be issued and stored locally and anchored to a public ledger at a later time without affecting validity.

This capability is critical for field research, humanitarian operations, and remote locations.

### Cross-Jurisdiction Operation

Because presence proofs are independent of jurisdiction-specific databases, the protocol supports cross-border and cross-institution verification. Presence claims generated in one context may be verified in another without requiring bilateral data-sharing agreements.

### Summary

Real-world operation of Proof of Presence relies on moment-based attestation, user-controlled storage, and later verification through aggregation. The protocol aligns with existing operational practices while eliminating the need for centralized tracking or redundant documentation.

The next section describes how the protocol is financially sustained without introducing a native token.


## 13. Economic Model (No Token)

The Proof of Presence protocol is designed to be economically sustainable without relying on a native token or speculative incentives. Financial flows within the system support operation, integration, and maintenance, while preserving the neutrality and integrity of presence proofs.

### Principles of the Economic Model

The economic design of the protocol follows several core principles:

- Truth is not monetized or traded.
- Individuals are not required to pay to possess or control their presence data.
- Costs are borne by entities that derive operational or compliance value from verification.
- Financial mechanisms must not influence the validity of presence claims.

These principles ensure that economic incentives do not distort or undermine the protocol’s purpose.

### Who Pays

Costs within the system are primarily covered by institutional participants rather than individuals. Entities that benefit from reliable, privacy-preserving presence verification include:

- Governments and public agencies
- Employers and organizations
- Educational and research institutions
- Event organizers
- Humanitarian and aid organizations

These entities already incur costs related to verification, audits, fraud prevention, and compliance. Proof of Presence reduces these costs by providing a standardized verification layer.

### What Is Paid For

Payments within the ecosystem may cover:

- Attester infrastructure and integration
- Issuance and anchoring of attestations
- Verification services and tooling
- Compliance support and service-level guarantees
- Long-term archival or availability services

Fees are associated with services, not with presence itself.

### Cost Structure

Operational costs include:

- Infrastructure for attester systems
- Ledger transaction costs for anchoring commitments
- Maintenance of reference implementations and verification tools
- Governance and accreditation processes
- Security audits and protocol updates

These costs are predictable and scale with usage rather than speculation.

### Revenue Models

Organizations operating or supporting Proof of Presence may generate revenue through:

- Software-as-a-service offerings for attesters
- Verification and analytics services for verifiers
- Enterprise support and integration services
- Hosted or managed deployments for governments and large institutions

All revenue models are optional and do not affect the core protocol.

### Financial Neutrality

The protocol does not require users to hold balances, stake assets, or engage in financial transactions to generate or verify presence proofs. This neutrality is critical for adoption by public institutions and regulated environments.

### Summary

Proof of Presence separates economic sustainability from proof integrity. By funding operation through institutional services rather than financializing presence, the protocol remains neutral, trustworthy, and accessible.

The next section defines how trust is governed and maintained without central authority.


## 14. Governance and Trust Model

Proof of Presence operates without a central authority controlling truth, yet it requires structured governance to define trust boundaries, accredit attesters, and maintain protocol integrity over time. This section describes how trust is established, maintained, and corrected without concentrating power.

### Trust as Scoped Authority

Trust in Proof of Presence is intentionally scoped and contextual. An attester is trusted only within the domain it is authorized to verify. No attester has global authority, and no presence claim inherits trust beyond the specific attestations it references.

Verifiers evaluate trust by examining:
- The identity and accreditation of the attester
- The attester’s authorized scope
- The relevance of that scope to the verification context

This model prevents overreach and reduces systemic risk.

### Attester Accreditation

Attesters are accredited through transparent, publicly documented processes. Accreditation defines:
- What contexts an attester may verify
- What verification methods are acceptable
- What revocation obligations exist

Accreditation may be managed by a neutral foundation, consortium, or regulatory-aligned body depending on deployment context. Multiple accreditation bodies may coexist without breaking protocol compatibility.

### Key Management and Rotation

Attester trust is represented cryptographically through public keys. Governance processes define how keys are issued, rotated, and revoked. Verifiers rely on public key registries to evaluate attestation validity.

Key compromise or misuse does not invalidate the protocol; it is addressed through revocation and re-accreditation.

### Dispute and Correction Mechanisms

Governance includes defined procedures for addressing disputes, errors, or fraud. These procedures may include:
- Attestation revocation
- Accreditation suspension
- Public disclosure of violations
- Protocol updates where necessary

Dispute resolution does not require access to private presence data beyond what is voluntarily disclosed.

### Protocol Evolution

Proof of Presence is designed to evolve over time. Governance processes define how protocol updates are proposed, reviewed, and adopted. Updates may address:
- Cryptographic standards
- Verification rules
- Accreditation requirements
- Interoperability improvements

Backward compatibility and transparency are prioritized to preserve long-term verifiability.

### Neutrality and Independence

No single organization owns or controls Proof of Presence. Governance structures are designed to prevent capture by commercial, political, or institutional interests. The protocol remains open for independent implementation and verification.

### Summary

The governance and trust model of Proof of Presence distributes authority, scopes trust, and provides correction mechanisms without centralizing control. This structure preserves both integrity and neutrality while enabling real-world adoption.

The next section examines security considerations and threat models relevant to the protocol.


## 15. Security Considerations

Security in Proof of Presence focuses on preserving the integrity of presence proofs, protecting user-controlled data, and preventing misuse or abuse of the protocol without introducing centralized surveillance or control. This section outlines the primary threat models and corresponding mitigations.

### Attester Compromise

If an attester’s signing keys are compromised or misused, false attestations may be issued. The protocol mitigates this risk through scoped trust, key rotation, and revocation mechanisms. Compromised attestations can be invalidated without affecting unrelated attestations or claims.

No single attester compromise can invalidate the system as a whole.

### False Presence Claims

Individuals may attempt to construct invalid claims using altered or incomplete attestations. Deterministic verification rules and cryptographic proofs prevent such claims from passing verification. Claims must reference valid, unrevoked attestations anchored on the public ledger.

### Replay and Duplication Attacks

Attestations are bound to specific subjects and contexts and cannot be reused by other individuals. Cryptographic binding prevents replay or duplication of attestations across identities.

### Correlation and Privacy Attacks

Although the protocol minimizes linkability, adversaries may attempt to correlate disclosures across contexts. This risk is mitigated by selective disclosure, non-transferable attestations, and the absence of centralized data stores. Users retain control over when and how attestations are linked.

### Ledger-Level Risks

Blockchain-related risks include censorship, reorganization, congestion, or governance changes. The protocol mitigates these risks through chain neutrality, optional multi-ledger anchoring, and minimal reliance on on-chain logic.

Temporary ledger failures may delay anchoring but do not invalidate attestations.

### Client-Side Security

Loss or compromise of user-controlled keys may prevent an individual from proving presence. This risk is addressed through standard cryptographic recovery mechanisms, optional hardware security, and client-side best practices. Compromise of a user’s client does not expose data beyond what is locally stored.

### Denial-of-Service and Abuse

The protocol minimizes attack surfaces by avoiding centralized endpoints. Attesters and verifiers may implement rate limits and access controls without affecting protocol correctness.

### Summary

Security in Proof of Presence is achieved through isolation, minimalism, and cryptographic verification rather than centralized enforcement. By limiting trust scope and reducing data exposure, the protocol remains resilient against both technical and institutional threats.

The next section addresses legal and regulatory considerations.


## 16. Legal and Regulatory Context

Proof of Presence is designed to operate within existing legal and regulatory frameworks while reducing the need for invasive data collection and centralized record keeping. This section outlines how the protocol aligns with common legal principles without being jurisdiction-specific.

### Data Protection and Privacy Law

The protocol is consistent with data minimization, purpose limitation, and user control requirements found in modern data protection regimes. Because raw presence data is stored off-chain under user control and only minimal cryptographic commitments are anchored publicly, the protocol reduces exposure to data breaches and misuse.

Individuals retain the ability to control disclosure, request deletion of locally held data, and limit retention, aligning with rights commonly granted under privacy regulations.

### Jurisdictional Neutrality

Proof of Presence does not depend on any single legal jurisdiction, identity framework, or regulatory authority. Presence proofs are portable across borders and institutions, allowing each verifier to apply local legal interpretation to verified claims without requiring shared databases or cross-border data transfer agreements.

### Evidence and Auditability

Presence attestations and claims may be used as supporting evidence in administrative, contractual, or compliance contexts. The protocol provides verifiable timestamps, issuer authentication, and integrity guarantees while avoiding centralized custody of evidence.

The protocol does not assert legal conclusions; it provides verifiable facts that may be evaluated under applicable law.

### Regulatory Adoption and Integration

Public institutions may adopt Proof of Presence incrementally, integrating it into existing workflows rather than replacing established systems. The protocol’s neutrality and lack of financialization reduce regulatory friction and enable pilot deployments within regulated environments.

### Liability and Responsibility

Responsibility within the protocol is scoped and explicit. Attesters are responsible for the accuracy of attestations within their authorized scope. Individuals are responsible for managing their keys and disclosures. Verifiers are responsible for applying appropriate policies to validated claims.

The protocol itself does not assume liability for policy outcomes.

### Summary

Proof of Presence is designed to complement legal and regulatory systems rather than challenge them. By reducing data exposure and clarifying responsibility boundaries, the protocol enables compliance while preserving individual autonomy.

The next section outlines the explicit limitations and non-goals of the protocol.


## 17. Limitations and Non-Goals

Proof of Presence is intentionally limited in scope. These limitations are not shortcomings; they are design decisions that preserve neutrality, privacy, and long-term viability. This section explicitly defines what the protocol does not attempt to do.

### Not an Identity System

Proof of Presence does not establish, verify, or manage identity. It does not replace passports, national IDs, KYC systems, or credential registries. Identity may be required by specific applications, but it remains external to the protocol.

### Not Continuous Tracking

The protocol does not provide real-time location tracking, historical movement reconstruction, or behavioral monitoring. Any system that attempts to infer continuous presence or movement from Proof of Presence artifacts is operating outside protocol guarantees.

### Not a Source of Intent or Purpose

Presence attestations confirm that an individual was physically present within a defined context. They do not assert why the individual was present, what actions were taken, or what obligations were fulfilled.

### Not a Policy Engine

Proof of Presence does not make eligibility determinations, grant rights, or enforce outcomes. It provides verifiable facts. Interpretation and decision-making remain the responsibility of verifiers and institutions.

### Not Fraud-Proof in Isolation

No protocol can prevent all forms of fraud. Proof of Presence mitigates many common failure modes but cannot eliminate risks arising from compromised attesters, collusion, or coercion. These risks are addressed through governance, scope limitation, and revocation, not technical absolutism.

### Not a Financial Instrument

Presence proofs do not represent value, ownership, or entitlement beyond their verification context. The protocol does not support speculation, staking, or monetization of presence itself.

### Dependence on Attester Integrity

The protocol assumes that attesters act honestly within their accredited scope. While misuse can be detected and corrected, Proof of Presence cannot retroactively guarantee correctness if false attestations are deliberately issued.

### Summary

By clearly defining its limitations and non-goals, Proof of Presence avoids misuse, overextension, and mission creep. These boundaries are essential to maintaining trust and ensuring the protocol remains focused on its core purpose.

The next section outlines a practical roadmap for implementation and adoption.


## 18. Implementation Roadmap

This roadmap outlines a practical, phased approach to implementing and deploying Proof of Presence. The objective is to validate core assumptions early, enable real-world pilots, and scale adoption without locking the protocol into premature technical or institutional commitments.

### Phase 1: Protocol Definition and Reference Design

The initial phase focuses on formalizing the protocol specification and providing reference materials sufficient for independent implementation.

Key objectives include:
- Finalizing attestation formats and aggregation rules
- Publishing verification logic and public schemas
- Defining attester accreditation requirements
- Producing reference client and verifier implementations

This phase prioritizes clarity, auditability, and interoperability over performance optimization.

### Phase 2: Pilot Deployments

Pilot deployments validate the protocol in controlled, real-world contexts. These pilots involve a limited number of attesters and verifiers operating within clearly defined scopes.

Potential pilot contexts include:
- Events or conferences
- Academic programs or research initiatives
- Employer-based presence verification
- Cross-border travel or residency pilots

Pilots are used to test usability, operational integration, and governance processes.

### Phase 3: Ledger Integration and Scaling

Once pilot deployments demonstrate viability, the protocol expands ledger support and optimizes anchoring strategies.

This phase may include:
- Support for multiple public ledgers
- Batching or rollup mechanisms for cost reduction
- Performance optimization for high-volume attesters
- Expanded verification tooling

Scalability improvements must not compromise privacy or verifiability.

### Phase 4: Institutional Adoption

The final phase focuses on broader adoption by public institutions, enterprises, and international organizations.

Activities include:
- Formal governance structures
- Accreditation of additional attesters
- Compliance alignment with jurisdictional requirements
- Long-term support and maintenance planning

Institutional adoption remains voluntary and incremental.

### Continuous Evaluation

Throughout all phases, the protocol is subject to continuous evaluation and refinement. Feedback from implementers, users, and verifiers informs updates, provided core design principles are preserved.

### Summary

The implementation roadmap emphasizes gradual validation, modular growth, and institutional compatibility. By avoiding premature scaling or centralization, Proof of Presence can evolve into durable infrastructure.

The final section concludes the paper by summarizing its purpose and long-term significance.


## 19. Conclusion

Proof of Presence addresses a foundational gap in modern digital systems: the inability to prove physical presence without surrendering privacy, autonomy, or control. Existing approaches either fail to document presence reliably or rely on invasive tracking and centralized data ownership. This tradeoff is neither necessary nor sustainable.

By treating presence as a verifiable fact rather than a continuously monitored condition, Proof of Presence demonstrates that verification and privacy can coexist. Moment-based attestations, user-controlled data custody, deterministic aggregation, and public integrity anchoring together enable presence to be proven without reconstructing a person’s life.

The protocol deliberately avoids financialization, centralized authority, and identity entanglement. It provides infrastructure, not outcomes; verifiable facts, not policy decisions. Governments, institutions, and organizations may apply their own rules and interpretations to presence claims while relying on a shared, neutral foundation for verification.

Proof of Presence is designed to integrate with existing systems rather than replace them. Its layered architecture allows incremental adoption, independent implementation, and long-term evolution without locking users or institutions into proprietary control.

In a world where mobility, remote participation, and cross-border interaction are increasingly common, the ability to prove lived reality without surveillance becomes essential infrastructure. Proof of Presence offers a path toward that future by making presence verifiable, portable, and human-centered.

Presence does not need to be tracked to be true.
It only needs to be proven.


## Appendix A: Glossary

**Aggregation**  
The deterministic process of combining multiple presence attestations to produce a higher-level presence claim, such as cumulative duration or attendance count, without introducing new data collection.

**Aggregation Rules**  
Public, deterministic rules that define how attestations may be combined, how overlaps are handled, and how thresholds are evaluated. Identical inputs must always produce identical outputs.

**Attestation**  
A cryptographically signed statement issued by an authorized attester confirming that an individual was physically present within a defined location zone during a defined time window.

**Attester**  
An entity authorized to verify and attest to physical presence within a specific scope, such as a government agency, employer, university, event organizer, or humanitarian organization.

**Blockchain (Public Ledger)**  
A public, append-only ledger used to anchor cryptographic commitments to attestations, providing immutability, ordering, and timestamping without storing personal data.

**Claim (Presence Claim)**  
A verifiable statement derived from one or more attestations asserting a condition about presence, such as duration, frequency, or participation, suitable for third-party verification.

**Client**  
User-controlled software or hardware that manages cryptographic keys, stores encrypted attestations, constructs claims, and controls disclosure.

**Commitment**  
A cryptographic hash or equivalent representation derived from an attestation and recorded on a public ledger to prove existence and integrity without revealing underlying data.

**Context**  
The bounded environment or situation in which presence is verified, such as a country, facility, campus, event, or program.

**Disclosure**  
The act of selectively revealing a presence claim and the minimum supporting information required for verification.

**Deterministic Verification**  
Verification logic that produces the same result for the same inputs, independent of who performs the verification.

**Identity (External)**  
Any real-world identification system (e.g., passport, employee ID) that may be used by applications but is not managed or required by the Proof of Presence protocol.

**Layer 0 (Trust Layer)**  
The off-chain layer consisting of attesters and real-world verification authority.

**Layer 1 (Settlement Layer)**  
The blockchain layer providing immutable anchoring of attestation commitments.

**Layer 2 (Aggregation Layer)**  
The logical layer responsible for combining attestations into claims.

**Layer 3 (Disclosure and Verification Layer)**  
The layer governing claim disclosure and third-party verification.

**Layer 4 (Application Layer)**  
External systems and policies that consume presence claims to make decisions.

**Location Zone**  
A coarse-grained geographic or contextual boundary used in attestations, such as a country or facility, excluding precise coordinates.

**Moment-Based Attestation**  
An attestation issued at a specific point in time rather than through continuous monitoring.

**Presence**  
The fact of an individual being physically present within a defined context at a defined time.

**Protocol**  
The open set of rules, data formats, and verification logic that define Proof of Presence.

**Public Verifiability**  
The ability for any verifier to independently validate a claim using public information and disclosed proofs.

**Revocation**  
The invalidation of an attestation due to error, fraud, or policy change, recorded in a publicly verifiable manner.

**Selective Disclosure**  
The ability for an individual to prove specific facts without revealing unnecessary underlying details.

**Verifier**  
Any party that evaluates a presence claim to determine whether it satisfies a given requirement.

**Zero-Knowledge Techniques**  
Optional cryptographic methods that allow claims to be verified without revealing underlying data beyond the truth of the claim itself.


