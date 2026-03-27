# Digitálna obsluha limitov pre elektronické kanály
sprava limitov pre elektronicke bankovnictvo


# 🧠 COMPONENT

```yaml
contact:
  name: Responsible Team
  email: Team's email alias
```

[[_TOC_]]

### 🎯 Purpose

## 🏗️ Architecture

### 🗄️ Data Model

<!-- TODO: Update example. -->

```mermaid
%%{init: {'theme':'base'}}%%
erDiagram
  CLIENT {
      int id PK
      string name
      string email
  }
  
  PRODUCT {
      int id PK
      string name
      float price
  }
  
  CLIENT ||--o{ PRODUCT : purchases
```

## 📜 API Commons

A shared set of standards or common guidelines applicable across various APIs or Features.

### 🔑 Authorization

### 🔢 Generic Sequence diagram

```mermaid
sequenceDiagram
    autonumber

    participant Client as Client (George store Mobile)
    participant FEapp as FE app
    participant GBO as GBO (OWFE / OZPU process)
    participant Facade as GBO Facade
    participant CHF as CHF
    participant MACNX as MACNX
    participant OMS as OMS
    participant BS as BS
    participant FE as FE

    Client->>FEapp: Start / open onboarding
    FEapp->>Facade: Load corporate clients
    Facade-->>FEapp: Corporate clients
    FEapp-->>Client: List of corporate clients

    alt new
        FEapp->>GBO: user ID load
        GBO-->>FEapp: GBO started / Case created
    else existing
        FEapp->>MACNX: client ID load\n(start params: company CID validation OR GBO process ID)
        MACNX-->>FEapp: validated CID / GBO process ID
        FEapp->>GBO: CorporateAccountCreate (message start)
    end

    %% Verify existing onboarding + load personal details
    GBO->>Facade: Verify existing onboarding / LE\nGET /cases/dedupe
    Facade-->>GBO: dedupe result
    GBO->>CHF: GET /my/profile
    CHF-->>GBO: profile data

    %% Identification + case creation
    GBO->>Facade: POST /identity/identification/token
    Facade-->>GBO: token
    GBO->>Facade: POST /cases
    Facade-->>GBO: caseId

    %% Load case data for screens
    GBO->>Facade: GET /cases/{caseId}
    Facade-->>GBO: case
    GBO->>Facade: GET /cases/{caseId}/company
    Facade-->>GBO: company
    GBO->>Facade: GET /cases/{caseId}/beneficial-owners
    Facade-->>GBO: BOs
    GBO->>Facade: GET /cases/{caseId}/background-checks
    Facade-->>GBO: background checks
    GBO->>Facade: GET /cases/{caseId}/tax-info
    Facade-->>GBO: tax info

    %% Update submitted data
    GBO->>Facade: PUT /cases/{caseId}/company
    GBO->>Facade: PUT /cases/{caseId}/managers
    GBO->>Facade: PUT /cases/{caseId}/beneficial-owners
    GBO->>Facade: PUT /cases/{caseId}/background-checks
    GBO->>Facade: PUT /cases/{caseId}/tax-info
    Facade-->>GBO: updated

    %% Approve + callbacks
    GBO->>Facade: POST /cases/{caseId}/contracts/signatories
    GBO->>Facade: POST /cases/{caseId}/products/signatories
    GBO->>Facade: POST /cases/{caseId}/approve
    GBO->>Facade: POST /case/callbacks
    Facade-->>GBO: callback accepted

    %% Products + signing
    GBO->>Facade: GET /cases/{caseId}/products
    Facade-->>GBO: products
    GBO->>OMS: document generation
    OMS-->>GBO: documents
    GBO->>BS: Sign and update documents
    BS-->>GBO: signed

    %% GWF creation + KYC validation
    GBO->>FE: company data collection for GWF\nLoad all data from GBO v1/users/{CID}
    FE-->>GBO: collected
    GBO->>FE: GWF creation\n(type: existing CID OR existing GBO case)
    FE-->>GBO: GWF created
    GBO->>MACNX: KYC validation
    MACNX-->>GBO: KYC result
```

<!-- TODO: Any other component level details applicable for every supported feature. -->

## 📑 Related documentation

- 🔗 [**Component `COMP-XX`**](https://jira.app.slsp.sk/browse/)
- 🔐 [**List of scopes by specific API endpoint**](_assets/list_of_scopes.md)
