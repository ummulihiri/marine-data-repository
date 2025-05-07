# Marine Data Repository (OceanVault)

A decentralized repository for marine scientific data, enabling secure storage, validation, and access control of critical ocean-related research information.

## Overview

OceanVault is a blockchain-based platform that serves the marine research community by providing:
- Immutable storage of marine research metadata
- Verifiable data attribution and citation tracking
- Flexible access control mechanisms
- Governance system for community decision-making
- Monetization options for valuable datasets

The platform connects researchers, oceanographers, and marine conservationists in a trustless environment where data integrity and proper attribution are guaranteed by blockchain technology.

## Architecture

The system is built around a primary smart contract that manages:

```mermaid
graph TD
    A[Researchers] -->|Register| B[OceanVault Contract]
    B -->|Manages| C[Datasets]
    B -->|Controls| D[Access Permissions]
    B -->|Tracks| E[Citations]
    B -->|Facilitates| F[Governance]
    C -->|Types| G[Open/Paid/Permissioned]
    H[Users] -->|Access| C
    H -->|Vote on| F
```

### Core Components:
- Researcher Registry
- Dataset Management
- Access Control System
- Citation Tracking
- Governance Mechanism

## Contract Documentation

### ocean-vault.clar

The main contract handling all core functionality of the OceanVault platform.

#### Key Features:
- Researcher registration and verification
- Dataset registration and metadata storage
- Flexible access control (Open, Paid, Permissioned)
- Citation tracking and attribution
- Governance proposal system

#### Access Types:
- `ACCESS-TYPE-OPEN` (u1): Freely accessible data
- `ACCESS-TYPE-PAID` (u2): Requires payment for access
- `ACCESS-TYPE-PERMISSIONED` (u3): Requires explicit permission

## Getting Started

### Prerequisites
- Clarinet
- Stacks wallet for deployment/interaction

### Basic Usage

1. Register as a researcher:
```clarity
(contract-call? .ocean-vault register-researcher "John Doe" "Marine Institute" "PhD Marine Biology")
```

2. Register a dataset:
```clarity
(contract-call? .ocean-vault register-dataset 
    "dataset-001"
    "Coral Reef Survey 2023"
    "Environmental Data"
    "Great Barrier Reef"
    u1683849600
    "Standard sampling methodology"
    0x... ;; data hash
    u1    ;; open access
    u0    ;; free
)
```

3. Access a dataset:
```clarity
(contract-call? .ocean-vault check-dataset-access "dataset-001" tx-sender)
```

## Function Reference

### Public Functions

#### Researcher Management
- `register-researcher`: Register a new researcher
- `get-researcher`: Retrieve researcher information

#### Dataset Management
- `register-dataset`: Register a new dataset
- `verify-dataset`: Verify a dataset (admin only)
- `get-dataset`: Retrieve dataset information

#### Access Control
- `grant-dataset-access`: Grant access to permissioned dataset
- `access-paid-dataset`: Purchase access to paid dataset
- `check-dataset-access`: Check access permissions

#### Citations
- `cite-dataset`: Cite a dataset in research
- `get-citation`: Retrieve citation information

#### Governance
- `create-proposal`: Create a governance proposal
- `vote-on-proposal`: Vote on active proposals
- `finalize-proposal`: Finalize proposal after voting period

## Development

### Testing
1. Clone the repository
2. Install Clarinet
3. Run tests:
```bash
clarinet test
```

### Local Development
1. Start Clarinet console:
```bash
clarinet console
```
2. Deploy contracts:
```clarity
(contract-call? .ocean-vault ...)
```

## Security Considerations

### Access Control
- Only registered researchers can register datasets
- Dataset access is strictly controlled based on type
- Paid access requires successful STX transfer
- Permission grants only by dataset owners

### Governance
- Only registered researchers can participate
- Proposals have fixed voting periods
- Vote counting is transparent and immutable
- Status changes are permanent once finalized

### Limitations
- On-chain storage limited to metadata
- Actual dataset storage should be off-chain
- Access control applies to metadata only
- Citations must be by registered researchers