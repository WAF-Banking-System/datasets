# Blockchain Healthcare System - Architecture Diagrams

## Overview
This document provides detailed architectural diagrams for the proposed blockchain-enhanced healthcare platform, complementing the main research document.

---

## 1. Complete System Architecture

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                          PRESENTATION LAYER                                ║
╠═══════════════════════════════════════════════════════════════════════════╣
║                                                                            ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌──────────────┐   ║
║  │   Patient   │  │  Provider   │  │    Admin    │  │    Mobile    │   ║
║  │   Portal    │  │   Portal    │  │  Dashboard  │  │     App      │   ║
║  │  (React)    │  │  (React)    │  │  (React)    │  │ (React Native)│   ║
║  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬───────┘   ║
║         │                │                 │                 │            ║
║         └────────────────┴─────────────────┴─────────────────┘            ║
║                                   │                                        ║
╚═══════════════════════════════════╪════════════════════════════════════════╝
                                    │
                          ┌─────────▼──────────┐
                          │    API Gateway     │
                          │   (Kong/Nginx)     │
                          │   Authentication   │
                          │   Rate Limiting    │
                          └─────────┬──────────┘
                                    │
╔═══════════════════════════════════╪════════════════════════════════════════╗
║                        APPLICATION LAYER                                   ║
╠═══════════════════════════════════╪════════════════════════════════════════╣
║                                   │                                        ║
║         ┌─────────────────────────┴─────────────────────────┐             ║
║         │     Healthcare Application Backend                │             ║
║         │     (Node.js / Python FastAPI)                   │             ║
║         │                                                   │             ║
║         │  ┌─────────────────────────────────────────────┐ │             ║
║         │  │         Core Services                        │ │             ║
║         │  ├─────────────────────────────────────────────┤ │             ║
║         │  │ • Patient Management    • Appointments      │ │             ║
║         │  │ • Clinical Records      • AI Diagnostics    │ │             ║
║         │  │ • Lab Integration       • Prescription Mgmt │ │             ║
║         │  └─────────────────────────────────────────────┘ │             ║
║         │                                                   │             ║
║         │  ┌─────────────────────────────────────────────┐ │             ║
║         │  │     Blockchain Integration Service          │ │             ║
║         │  ├─────────────────────────────────────────────┤ │             ║
║         │  │ • Consent Management API                    │ │             ║
║         │  │ • Audit Logging Service                     │ │             ║
║         │  │ • Data Integrity Verification               │ │             ║
║         │  │ • Smart Contract Interface                  │ │             ║
║         │  │ • Event Listener (Blockchain Events)        │ │             ║
║         │  └─────────────────────────────────────────────┘ │             ║
║         └────────────┬──────────────────┬──────────────────┘             ║
║                      │                  │                                 ║
╚══════════════════════╪══════════════════╪═════════════════════════════════╝
                       │                  │
        ┌──────────────▼──────────┐      │
        │  Blockchain SDK         │      │
        │  (Hyperledger Fabric    │      │
        │   Node.js SDK)          │      │
        └──────────────┬──────────┘      │
                       │                  │
╔══════════════════════╪══════════════════╪═════════════════════════════════╗
║               BLOCKCHAIN LAYER          │                                 ║
╠══════════════════════╪══════════════════╪═════════════════════════════════╣
║                      │                  │                                 ║
║  ┌───────────────────▼──────────────────▼───────────────────────────┐   ║
║  │         Private/Consortium Blockchain Network                     │   ║
║  │         (Hyperledger Fabric / Quorum)                            │   ║
║  │                                                                    │   ║
║  │  ┌─────────────────────────────────────────────────────────────┐ │   ║
║  │  │              Smart Contracts (Chaincode)                     │ │   ║
║  │  ├─────────────────────────────────────────────────────────────┤ │   ║
║  │  │  • ConsentManagement     • AccessControl                    │ │   ║
║  │  │  • AuditLogger           • DataIntegrityVerifier            │ │   ║
║  │  │  • ProviderRegistry      • PatientIdentityManager           │ │   ║
║  │  └─────────────────────────────────────────────────────────────┘ │   ║
║  │                                                                    │   ║
║  │  ┌─────────────────────────────────────────────────────────────┐ │   ║
║  │  │                    Ledger State                              │ │   ║
║  │  ├─────────────────────────────────────────────────────────────┤ │   ║
║  │  │  • Consent Records      • Access Logs                       │ │   ║
║  │  │  • Data Hashes          • Provenance Chains                 │ │   ║
║  │  │  • Permission Mappings  • Audit Trails                      │ │   ║
║  │  └─────────────────────────────────────────────────────────────┘ │   ║
║  │                                                                    │   ║
║  └────────────────────────────────────────────────────────────────────┘   ║
║                                                                            ║
║  ┌─────────────────────────────────────────────────────────────────────┐ ║
║  │                    Blockchain Nodes (Peers)                         │ ║
║  ├─────────────────────────────────────────────────────────────────────┤ ║
║  │                                                                       │ ║
║  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐           │ ║
║  │  │Hospital A│  │Hospital B│  │  Clinic  │  │   Lab    │           │ ║
║  │  │  Node    │  │  Node    │  │  Node    │  │  Node    │           │ ║
║  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘           │ ║
║  │                                                                       │ ║
║  │  ┌──────────┐  ┌──────────┐  ┌──────────────┐                      │ ║
║  │  │Insurance │  │ Pharmacy │  │  Regulatory  │                      │ ║
║  │  │  Node    │  │  Node    │  │  Authority   │                      │ ║
║  │  └──────────┘  └──────────┘  └──────────────┘                      │ ║
║  │                                                                       │ ║
║  └───────────────────────────────────────────────────────────────────────┘ ║
║                                                                            ║
╚════════════════════════════════════════════════════════════════════════════╝
                                    │
╔═══════════════════════════════════╪════════════════════════════════════════╗
║                        DATA STORAGE LAYER                                  ║
╠═══════════════════════════════════╪════════════════════════════════════════╣
║                                   │                                        ║
║  ┌────────────────────────────────▼─────────────────────────────────────┐ ║
║  │              Traditional Database (PostgreSQL / MongoDB)             │ ║
║  ├──────────────────────────────────────────────────────────────────────┤ ║
║  │  • Patient Demographics         • Appointments                       │ ║
║  │  • Medical History              • Prescriptions                      │ ║
║  │  • Clinical Notes               • Lab Results (full data)            │ ║
║  │  • Metadata and Indexes         • User Profiles                      │ ║
║  └──────────────────────────────────────────────────────────────────────┘ ║
║                                                                            ║
║  ┌──────────────────────────────────────────────────────────────────────┐ ║
║  │          Encrypted Off-Chain Storage (S3 / Azure Blob / IPFS)        │ ║
║  ├──────────────────────────────────────────────────────────────────────┤ ║
║  │  • Medical Imaging (DICOM)      • Large Documents                    │ ║
║  │  • X-rays, MRIs, CT Scans       • PDF Reports                        │ ║
║  │  • ECG Recordings               • Pathology Images                   │ ║
║  │  • Genomic Data                 • Video Consultations                │ ║
║  └──────────────────────────────────────────────────────────────────────┘ ║
║                                                                            ║
╚════════════════════════════════════════════════════════════════════════════╝

Legend:
  ║  System Boundary
  ┌─┐ Component/Service
  │  Data/Control Flow
  ═  Layer Separator
```

---

## 2. Data Flow Diagram - Patient Grants Consent

```
┌──────────────┐
│   Patient    │
│   (Maria)    │
└──────┬───────┘
       │ 1. Login & Navigate to Consent Management
       │
       ▼
┌─────────────────────┐
│  Patient Portal UI  │
│  • Select Provider  │
│  • Choose Data      │
│  • Set Duration     │
└──────┬──────────────┘
       │ 2. Submit Consent Form
       │    {provider: "Dr. Chen", data: ["cardiac"], duration: 30days}
       │
       ▼
┌───────────────────────────────┐
│  Backend API                  │
│  POST /api/consent/grant      │
│                               │
│  • Validate input             │
│  • Authenticate patient       │
│  • Prepare blockchain tx      │
└──────┬────────────────────────┘
       │ 3. Call Smart Contract
       │    grantConsent(hash(maria_id), dr_chen_id, ["cardiac"], 30days)
       │
       ▼
┌──────────────────────────────────────┐
│  Blockchain Network                  │
│  ConsentManagement Smart Contract    │
│                                      │
│  • Verify caller identity            │
│  • Create consent record             │
│  • Update ledger state              │
│  • Emit ConsentGranted event        │
└──────┬───────────────────────────────┘
       │ 4. Transaction Confirmed
       │    Block added to chain
       │    ConsentID: CNS-2024-001
       │
       ▼
┌────────────────────────────────────┐
│  Event Listener                    │
│  (Backend Service)                 │
│                                    │
│  • Capture ConsentGranted event    │
│  • Update local cache              │
│  • Send notification               │
└──────┬─────────────────────────────┘
       │ 5. Notify Provider
       │
       ▼
┌────────────────────────────┐
│  Dr. Chen's System         │
│  • Receives notification   │
│  • Access now available    │
│  • Can query records       │
└────────────────────────────┘

       ┌─ Parallel ─┐
       │            │
       ▼            ▼
┌─────────────┐  ┌──────────────┐
│  Maria      │  │  Dr. Chen    │
│  Dashboard  │  │  Dashboard   │
│  ✓ Consent  │  │  ✓ New       │
│    Active   │  │    Access    │
└─────────────┘  └──────────────┘
```

---

## 3. Data Flow Diagram - Provider Accesses Medical Record

```
┌──────────────────┐
│  Dr. Chen        │
│  (Provider)      │
└────────┬─────────┘
         │ 1. Request patient record
         │
         ▼
┌──────────────────────────┐
│  Provider Portal         │
│  • Enter Patient ID      │
│  • Specify Access Reason │
└────────┬─────────────────┘
         │ 2. API Request
         │    GET /api/records/patient/{id}
         │    Headers: {provider_id: "dr_chen"}
         │
         ▼
┌────────────────────────────────────────────┐
│  Backend API - Authorization Middleware    │
│                                            │
│  Step 1: Query Blockchain                 │
│  └─> checkAccess(patient_id, dr_chen)     │
└────────┬───────────────────────────────────┘
         │ 3. Smart Contract Query
         │
         ▼
┌─────────────────────────────────────────┐
│  Blockchain Network                     │
│  ConsentManagement Smart Contract       │
│                                         │
│  • Lookup consent records               │
│  • Check expiration                     │
│  • Verify data categories               │
│  • Return: {authorized: true}           │
└────────┬────────────────────────────────┘
         │ 4. Authorization Response
         │    {authorized: true, categories: ["cardiac"]}
         │
         ▼
┌─────────────────────────────────────────────┐
│  Backend API - Data Retrieval               │
│                                             │
│  IF authorized:                             │
│  Step 2: Query Database                    │
│  └─> SELECT * FROM medical_records         │
│       WHERE patient_id = maria             │
│       AND category IN ("cardiac")          │
│                                            │
│  Step 3: Retrieve Files from S3            │
│  └─> GET s3://bucket/maria/cardiac/*       │
└────────┬────────────────────────────────────┘
         │ 5. Retrieved Data
         │
         ▼
┌──────────────────────────────────────────┐
│  Backend API - Audit Logging             │
│                                          │
│  • Prepare audit record                  │
│  • Calculate data hash                   │
│  • Submit to blockchain                  │
└────────┬─────────────────────────────────┘
         │ 6. Log Access
         │    logAccess(dr_chen, maria, ["cardiac"], timestamp)
         │
         ▼
┌─────────────────────────────────────────────┐
│  Blockchain Network                         │
│  AuditLogger Smart Contract                 │
│                                             │
│  • Create immutable access log              │
│  • Update audit trail                       │
│  • Emit AccessLogged event                  │
└────────┬────────────────────────────────────┘
         │ 7. Access Logged
         │
         ▼
┌──────────────────────────────────────────┐
│  Backend API - Response                  │
│  • Compile data                          │
│  • Return to provider                    │
└────────┬─────────────────────────────────┘
         │ 8. Medical Record Data
         │    {demographics, history, ecg_results, ...}
         │
         ▼
┌─────────────────────────┐
│  Dr. Chen's Dashboard   │
│  • View cardiac data    │
│  • Make diagnosis       │
│  • Update notes         │
└─────────────────────────┘

         ┌─ Async Notification ─┐
         │                      │
         ▼                      │
┌──────────────────┐           │
│  Maria's Mobile  │           │
│  • Push Notif:   │◄──────────┘
│  "Dr. Chen       │
│   accessed your  │
│   cardiac data"  │
└──────────────────┘
```

---

## 4. Smart Contract Architecture

```
╔═══════════════════════════════════════════════════════════════╗
║              SMART CONTRACTS (CHAINCODE)                      ║
╠═══════════════════════════════════════════════════════════════╣
║                                                                ║
║  ┌─────────────────────────────────────────────────────────┐  ║
║  │           ConsentManagement Contract                    │  ║
║  ├─────────────────────────────────────────────────────────┤  ║
║  │  Functions:                                             │  ║
║  │  • grantConsent(patient, provider, categories, duration)│  ║
║  │  • revokeConsent(patient, provider)                     │  ║
║  │  • checkAccess(patient, provider, category) → bool      │  ║
║  │  • listConsents(patient) → Consent[]                    │  ║
║  │  • extendConsent(consentId, newDuration)               │  ║
║  │                                                         │  ║
║  │  State:                                                 │  ║
║  │  • consents: Map<ConsentID, Consent>                   │  ║
║  │  • patientToConsents: Map<PatientID, ConsentID[]>      │  ║
║  │                                                         │  ║
║  │  Events:                                                │  ║
║  │  • ConsentGranted(patient, provider, timestamp)         │  ║
║  │  • ConsentRevoked(patient, provider, timestamp)         │  ║
║  └─────────────────────────────────────────────────────────┘  ║
║                                                                ║
║  ┌─────────────────────────────────────────────────────────┐  ║
║  │              AuditLogger Contract                       │  ║
║  ├─────────────────────────────────────────────────────────┤  ║
║  │  Functions:                                             │  ║
║  │  • logAccess(accessor, patient, action, records)        │  ║
║  │  • getAuditTrail(patient, startDate, endDate) → Log[]   │  ║
║  │  • queryAccessByProvider(provider) → Log[]              │  ║
║  │  • emergencyAccessLog(accessor, patient, reason)        │  ║
║  │                                                         │  ║
║  │  State:                                                 │  ║
║  │  • accessLogs: Map<LogID, AccessLog>                   │  ║
║  │  • patientLogs: Map<PatientID, LogID[]>                │  ║
║  │                                                         │  ║
║  │  Events:                                                │  ║
║  │  • AccessLogged(accessor, patient, action, timestamp)   │  ║
║  │  • EmergencyAccess(accessor, patient, reason)           │  ║
║  └─────────────────────────────────────────────────────────┘  ║
║                                                                ║
║  ┌─────────────────────────────────────────────────────────┐  ║
║  │         DataIntegrityVerifier Contract                  │  ║
║  ├─────────────────────────────────────────────────────────┤  ║
║  │  Functions:                                             │  ║
║  │  • registerRecord(recordId, hash, metadata)             │  ║
║  │  • updateRecord(recordId, newHash, reason)              │  ║
║  │  • verifyIntegrity(recordId, providedHash) → bool       │  ║
║  │  • getProvenance(recordId) → History[]                  │  ║
║  │                                                         │  ║
║  │  State:                                                 │  ║
║  │  • recordHashes: Map<RecordID, Hash>                   │  ║
║  │  • recordHistory: Map<RecordID, HistoryEntry[]>        │  ║
║  │                                                         │  ║
║  │  Events:                                                │  ║
║  │  • RecordRegistered(recordId, hash, timestamp)          │  ║
║  │  • RecordUpdated(recordId, oldHash, newHash)            │  ║
║  │  • IntegrityViolation(recordId, expectedHash, actualHash)│ ║
║  └─────────────────────────────────────────────────────────┘  ║
║                                                                ║
║  ┌─────────────────────────────────────────────────────────┐  ║
║  │            AccessControl Contract                       │  ║
║  ├─────────────────────────────────────────────────────────┤  ║
║  │  Functions:                                             │  ║
║  │  • defineRole(roleName, permissions)                    │  ║
║  │  • assignRole(userAddress, role)                        │  ║
║  │  • checkPermission(user, action) → bool                 │  ║
║  │  • revokeRole(userAddress, role)                        │  ║
║  │                                                         │  ║
║  │  Roles:                                                 │  ║
║  │  • PATIENT: Full control over own data                 │  ║
║  │  • PROVIDER: Access with consent                       │  ║
║  │  • ADMIN: System administration                        │  ║
║  │  • AUDITOR: Read-only audit trail access               │  ║
║  │  • EMERGENCY: Override access (logged)                 │  ║
║  └─────────────────────────────────────────────────────────┘  ║
║                                                                ║
╚════════════════════════════════════════════════════════════════╝
```

---

## 5. Deployment Architecture - Hyperledger Fabric

```
╔══════════════════════════════════════════════════════════════════╗
║                    HYPERLEDGER FABRIC NETWORK                    ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  ┌────────────────────────────────────────────────────────────┐  ║
║  │                 Ordering Service                           │  ║
║  │  (Raft Consensus - 3 or 5 Orderer Nodes)                  │  ║
║  │  • Ensures consistent transaction ordering                 │  ║
║  │  • Handles channel creation and configuration              │  ║
║  └────────────────────────────────────────────────────────────┘  ║
║                              │                                   ║
║                              │ Orders Transactions               ║
║                              │                                   ║
║  ┌──────────────────────────┴───────────────────────────────┐   ║
║  │                    Channel: healthcare-main              │   ║
║  │  • Shared ledger for all consortium members              │   ║
║  │  • Privacy through private data collections              │   ║
║  └──────────────────────────┬───────────────────────────────┘   ║
║                              │                                   ║
║         ┌────────────────────┼────────────────────┐             ║
║         │                    │                    │             ║
║  ┌──────▼─────┐      ┌──────▼─────┐      ┌──────▼─────┐       ║
║  │Organization│      │Organization│      │Organization│       ║
║  │     A      │      │     B      │      │     C      │       ║
║  │ (Hospital) │      │ (Clinic)   │      │  (Lab)     │       ║
║  │            │      │            │      │            │       ║
║  │ ┌────────┐ │      │ ┌────────┐ │      │ ┌────────┐ │       ║
║  │ │ Peer 0 │ │      │ │ Peer 0 │ │      │ │ Peer 0 │ │       ║
║  │ │(Leader)│ │      │ │(Leader)│ │      │ │(Leader)│ │       ║
║  │ └────────┘ │      │ └────────┘ │      │ └────────┘ │       ║
║  │            │      │            │      │            │       ║
║  │ ┌────────┐ │      │ ┌────────┐ │      │ ┌────────┐ │       ║
║  │ │ Peer 1 │ │      │ │ Peer 1 │ │      │ │ Peer 1 │ │       ║
║  │ │        │ │      │ │        │ │      │ │        │ │       ║
║  │ └────────┘ │      │ └────────┘ │      │ └────────┘ │       ║
║  │            │      │            │      │            │       ║
║  │  ┌──────┐  │      │  ┌──────┐  │      │  ┌──────┐  │       ║
║  │  │  CA  │  │      │  │  CA  │  │      │  │  CA  │  │       ║
║  │  │(MSP) │  │      │  │(MSP) │  │      │  │(MSP) │  │       ║
║  │  └──────┘  │      │  └──────┘  │      │  └──────┘  │       ║
║  │   Certs    │      │   Certs    │      │   Certs    │       ║
║  └────────────┘      └────────────┘      └────────────┘       ║
║                                                                 ║
║  Each Organization:                                            ║
║  • Runs 2 peer nodes (redundancy)                              ║
║  • Has Certificate Authority (CA) for identity management      ║
║  • Maintains copy of ledger on each peer                       ║
║  • Executes and endorses smart contracts                       ║
║  • Can have private data collections                           ║
║                                                                 ║
╚═════════════════════════════════════════════════════════════════╝

Transaction Flow:
1. Client submits transaction proposal
2. Peers execute chaincode (smart contract)
3. Peers return endorsed proposal responses
4. Client submits transaction to ordering service
5. Orderers create block and distribute
6. Peers validate and commit to ledger
```

---

## 6. Security Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                    Security Layers                             │
└────────────────────────────────────────────────────────────────┘

Layer 1: Network Security
┌──────────────────────────────────────────────────────────────┐
│  • VPC with Private Subnets                                  │
│  • TLS 1.3 for all communications                            │
│  • Firewall rules (only necessary ports open)                │
│  • DDoS protection (CloudFlare/AWS Shield)                   │
│  • VPN for admin access                                      │
└──────────────────────────────────────────────────────────────┘

Layer 2: Identity & Access Management
┌──────────────────────────────────────────────────────────────┐
│  • OAuth 2.0 / OpenID Connect for authentication            │
│  • Multi-Factor Authentication (MFA) required                │
│  • Certificate-based identity (X.509) on blockchain          │
│  • Role-Based Access Control (RBAC)                          │
│  • Attribute-Based Access Control (ABAC) via smart contracts │
│  • Regular credential rotation                               │
└──────────────────────────────────────────────────────────────┘

Layer 3: Data Encryption
┌──────────────────────────────────────────────────────────────┐
│  At Rest:                                                    │
│  • AES-256 encryption for database                           │
│  • Encrypted S3 buckets (SSE-KMS)                            │
│  • Encrypted blockchain ledger                               │
│  • Hardware Security Modules (HSM) for keys                  │
│                                                              │
│  In Transit:                                                 │
│  • TLS 1.3 for API communications                            │
│  • gRPC with mutual TLS for blockchain                       │
│  • End-to-end encryption for sensitive data                  │
└──────────────────────────────────────────────────────────────┘

Layer 4: Blockchain Security
┌──────────────────────────────────────────────────────────────┐
│  • Private/Permissioned network (controlled membership)      │
│  • Cryptographic signatures for all transactions             │
│  • SHA-256 hashing for data integrity                        │
│  • Smart contract auditing before deployment                 │
│  • Formal verification of critical contracts                 │
│  • Consensus mechanism (Raft/PBFT) prevents tampering        │
│  • Channel-level isolation for privacy                       │
│  • Private data collections for sensitive info               │
└──────────────────────────────────────────────────────────────┘

Layer 5: Application Security
┌──────────────────────────────────────────────────────────────┐
│  • Input validation and sanitization                         │
│  • SQL injection prevention (parameterized queries)          │
│  • XSS protection (Content Security Policy)                  │
│  • CSRF tokens                                               │
│  • Rate limiting and throttling                              │
│  • Security headers (HSTS, X-Frame-Options, etc.)            │
│  • Regular penetration testing                               │
│  • Dependency scanning (Snyk, Dependabot)                    │
└──────────────────────────────────────────────────────────────┘

Layer 6: Monitoring & Incident Response
┌──────────────────────────────────────────────────────────────┐
│  • SIEM integration (Splunk, ELK)                            │
│  • Real-time security alerts                                 │
│  • Blockchain transaction monitoring                         │
│  • Anomaly detection (unauthorized access attempts)          │
│  • Automated incident response playbooks                     │
│  • Regular security audits                                   │
│  • Compliance monitoring (HIPAA, GDPR)                       │
└──────────────────────────────────────────────────────────────┘
```

---

## 7. Disaster Recovery & High Availability

```
╔═══════════════════════════════════════════════════════════════════╗
║              HIGH AVAILABILITY ARCHITECTURE                        ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                    ║
║     Region 1 (Primary)                 Region 2 (DR)              ║
║  ┌─────────────────────┐         ┌─────────────────────┐         ║
║  │  Load Balancer      │         │  Load Balancer      │         ║
║  │  (Active)           │◄────────┤  (Standby)          │         ║
║  └──────────┬──────────┘  Sync   └──────────┬──────────┘         ║
║             │                               │                     ║
║   ┌─────────┴─────────┐         ┌─────────┴─────────┐           ║
║   │  App Servers      │         │  App Servers      │           ║
║   │  (3 instances)    │◄────────┤  (2 instances)    │           ║
║   └─────────┬─────────┘  Sync   └─────────┬─────────┘           ║
║             │                              │                     ║
║   ┌─────────┴─────────┐         ┌─────────┴─────────┐           ║
║   │ Blockchain Nodes  │         │ Blockchain Nodes  │           ║
║   │ (3 peers)         │◄────────┤ (2 peers)         │           ║
║   │ Distributed       │  P2P    │ Distributed       │           ║
║   └─────────┬─────────┘ Sync    └─────────┬─────────┘           ║
║             │                              │                     ║
║   ┌─────────┴─────────┐         ┌─────────┴─────────┐           ║
║   │  Database         │         │  Database         │           ║
║   │  (Primary)        │────────→│  (Read Replica)   │           ║
║   └───────────────────┘ Streaming└───────────────────┘          ║
║             │            Replication                             ║
║   ┌─────────┴─────────┐         ┌───────────────────┐           ║
║   │  S3 Bucket        │         │  S3 Bucket        │           ║
║   │  (Primary)        │◄────────┤  (Replicated)     │           ║
║   └───────────────────┘ Cross-  └───────────────────┘           ║
║                         Region                                   ║
║                         Replication                              ║
║                                                                   ║
║  Backup Strategy:                                                ║
║  • Blockchain: Distributed by design (each node has copy)        ║
║  • Database: Daily automated backups, retained 30 days           ║
║  • S3: Versioning enabled, lifecycle policies                    ║
║  • RTO (Recovery Time Objective): < 4 hours                      ║
║  • RPO (Recovery Point Objective): < 15 minutes                  ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
```

---

## 8. Privacy Architecture - Private Data Collections

```
┌────────────────────────────────────────────────────────────────┐
│         Hyperledger Fabric Private Data Collections            │
│         (Enables privacy within consortium)                    │
└────────────────────────────────────────────────────────────────┘

Scenario: Hospital A and Hospital B share patient data, but 
          Lab C should not see medical history, only lab results.

┌─────────────────────────────────────────────────────────────────┐
│  Channel: healthcare-main                                       │
│  (All members: Hospital A, Hospital B, Lab C)                   │
└─────────────────────────────────────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ Collection:  │ │ Collection:  │ │ Collection:  │
│ medical-hist │ │ lab-results  │ │ shared-meta  │
├──────────────┤ ├──────────────┤ ├──────────────┤
│ Members:     │ │ Members:     │ │ Members:     │
│ • Hospital A │ │ • Hospital A │ │ • Hospital A │
│ • Hospital B │ │ • Hospital B │ │ • Hospital B │
│              │ │ • Lab C      │ │ • Lab C      │
├──────────────┤ ├──────────────┤ ├──────────────┤
│ Data:        │ │ Data:        │ │ Data:        │
│ • Diagnoses  │ │ • Test name  │ │ • Patient ID │
│ • Treatment  │ │ • Results    │ │ • Timestamp  │
│ • Notes      │ │ • Reference  │ │ • Hash       │
└──────────────┘ └──────────────┘ └──────────────┘

Public Ledger (All Members):
• Hashes of private data
• Transaction metadata
• Audit logs (who accessed what)

Private Data:
• Stored only on authorized peers
• Not shared with unauthorized members
• Queryable only by collection members
```

---

## 9. Integration Points

```
┌────────────────────────────────────────────────────────────────┐
│              External System Integration                       │
└────────────────────────────────────────────────────────────────┘

Healthcare App Backend
        │
        ├──────────────┬──────────────┬──────────────┬────────────
        │              │              │              │
        ▼              ▼              ▼              ▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│  EHR System │ │  FHIR API   │ │   HL7 v2    │ │  DICOM      │
│  (Epic)     │ │  Server     │ │  Interface  │ │  Server     │
└─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘
        │              │              │              │
        └──────────────┴──────────────┴──────────────┘
                       │
                       ▼
              ┌──────────────────┐
              │  HL7 Translator  │
              │  Middleware      │
              └────────┬─────────┘
                       │
                       ▼
            ┌─────────────────────┐
            │  Blockchain Gateway │
            │  • REST API         │
            │  • Event Publisher  │
            └────────┬────────────┘
                     │
                     ▼
            ┌──────────────────────┐
            │  Blockchain Network  │
            └──────────────────────┘

Integration Patterns:
1. Write-Through: Update database + blockchain simultaneously
2. Event-Driven: Database change triggers blockchain transaction
3. Read-Through: Check blockchain authorization before database query
4. Audit-Sync: Periodic sync of audit logs to blockchain
```

---

This architecture document provides visual representations complementing the main research document. All diagrams are text-based for easy version control and editing.

**Document Version:** 1.0  
**Last Updated:** February 2026
