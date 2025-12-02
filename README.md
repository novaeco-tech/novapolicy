# ⚖️ NovaPolicy

> **The Operating System for Regulatory Compliance.**
> A Policy-as-Code engine for automated regulatory checks, trade compliance, and ESG reporting.

[](https://www.google.com/search?q=https://github.com/novaeco-tech/novapolicy/actions)
[](https://opensource.org/licenses/MIT)
[](https://www.google.com/search?q=https://policy.novaeco.tech)

**NovaPolicy** is the Horizontal Enabler responsible for **Governance and Law**. In a highly regulated Circular Economy, every transaction—moving waste across borders, selling chemicals, or hiring labor—has legal implications.

NovaPolicy translates complex legal texts (e.g., **EU Green Deal**, **GDPR**, **REACH**) into executable code. It acts as the ecosystem's "Gatekeeper," intercepting API calls from other sectors to approve or deny actions based on the current rule of law.

-----

## 🎯 Value Proposition

Compliance costs are a major barrier to the circular transition. **NovaPolicy** automates the bureaucracy:

1.  **Automated Gatekeeping:** Instead of waiting for a yearly audit to find violations, NovaPolicy blocks non-compliant actions *before* they happen (e.g., "Error: You cannot ship Lithium Batteries to this region without a Permit").
2.  **Dynamic Adaptation:** When a law changes (e.g., new Carbon Border Tax rates), we update the policy code once, and the entire ecosystem complies instantly.
3.  **Verifiable Audit Trails:** Every decision ("Why was this trade blocked?") is cryptographically logged, providing instant proof for government auditors.

-----

## 🏗️ Architecture (The Rule Engine)

NovaPolicy is built on top of **Open Policy Agent (OPA)**. It decouples policy decision-making from policy enforcement.

```mermaid
graph TD
    User((Trader)) -->|1. Submit Order| Trade[NovaTrade API]
    
    subgraph "The Enforcement Loop"
        Trade -->|2. Check Permission| API[NovaPolicy API]
        API -->|3. Evaluate Input| OPA[OPA Engine (Rego)]
        OPA -->|4. Allow / Deny| API
    end

    subgraph "The Data Sources"
        OPA -->|Fetch Whitelist| Skills[NovaSkills]
        OPA -->|Fetch Hazard Data| Chem[NovaChem]
    end

    subgraph "Governance"
        Lawyer((Legal Eng.)) -->|Write Rules| Git[Policy Repo]
        Git -->|CI/CD| OPA
    end

    API -->|5. Decision| Trade
```

### Integrated Services

  * **[NovaTrade](https://www.google.com/search?q=https://trade.novaeco.tech):** Before executing a trade, it asks NovaPolicy: *"Is this Buyer allowed to purchase this Hazardous Waste?"*
  * **[NovaChem](https://www.google.com/search?q=https://chemicals.novaeco.tech):** Provides the chemical composition data. NovaPolicy checks this against the **REACH** restricted substances list.
  * **[NovaSkills](https://www.google.com/search?q=https://skills.novaeco.tech):** Provides the licenses. NovaPolicy checks: *"Does the truck driver have a valid HazMat transport certificate?"*
  * **[NovaMaterial](https://www.google.com/search?q=https://materials.novaeco.tech):** NovaPolicy verifies that a Digital Product Passport contains all mandatory EU disclosure fields before allowing it to be published.

-----

## ✨ Key Features

### 1\. The "Green Guardrails" (OPA/Rego)

We write laws in **Rego**, a declarative query language.

  * **Rule Example:** `allow = false if input.material == "e-waste" and input.destination.country != "OECD"`.
  * This ensures that illegal waste dumping is technically impossible within the platform.

### 2\. Carbon Border Adjustment (CBAM) Calculator

Automated tariff calculation for imports.

  * **Input:** 100 Tons of Steel from Country X.
  * **Logic:** Checks the Carbon Intensity of Country X vs. EU Standards.
  * **Output:** "Tax Due: €450." Sent to `NovaFin` for settlement.

### 3\. Automated ESG Reporting (CSRD)

Generates the **Corporate Sustainability Reporting Directive (CSRD)** reports required by the EU.

  * Aggregates data from `NovaBalance` (Environment), `NovaEquity` (Social), and `NovaPolicy` (Governance).
  * Formats it into the standardized machine-readable XBRL format for regulators.

### 4\. Dynamic Permitting

Integration with municipal databases.

  * If a `NovaLogistics` truck enters a "Low Emission Zone" (LEZ), NovaPolicy checks its emission class via `NovaInfra`.
  * **Action:** Grants instant digital access or issues a fine.

-----

## 🚀 Getting Started

We use **DevContainers** to provide a consistent development environment.

### Prerequisites

  * Docker Desktop
  * VS Code (with Remote Containers extension)
  * Knowledge of **Rego** (Open Policy Agent language) is helpful but not required for API work.

### Installation

1.  **Clone the repo:**
    ```bash
    git clone https://github.com/novaeco-tech/novapolicy.git
    cd novapolicy
    ```
2.  **Open in VS Code:**
      * Run `code .`
      * Click **"Reopen in Container"** when prompted.
3.  **Start the Enabler:**
    ```bash
    make dev
    ```
      * **Policy Playground:** http://localhost:8181 (OPA Console)
      * **Compliance Dashboard:** http://localhost:3000
      * **API:** http://localhost:8000/docs

### Configuration (`.env`)

```ini
# Engine Settings
OPA_URL=http://localhost:8181/v1/data
DEFAULT_JURISDICTION=EU

# External Lookups
NOVACHEM_URL=http://novachem-api:8000
NOVASKILLS_URL=http://novaskills-api:8000
```

-----

## 📂 Repository Structure

This is a Monorepo containing the sector's specific logic.

```text
novapolicy/
├── api/                # Python/FastAPI (The Gateway)
│   ├── src/
│   │   ├── enforcement/# Logic to query OPA and format responses
│   │   ├── reporting/  # CSRD / XBRL report generators
│   │   └── audit/      # Immutable logging of decisions
├── policies/           # THE LAW (Rego Files)
│   ├── trade/          # Import/Export rules
│   ├── waste/          # Basel Convention rules
│   └── labor/          # ILO convention rules
├── app/                # React/Next.js Frontend (Compliance Officer UI)
│   ├── src/
│   │   ├── rules/      # UI to browse active policies
│   │   └── violations/ # Dashboard of blocked actions
├── website/            # Documentation (Docusaurus)
└── tests/              # Integration tests
```

-----

## 🧪 Testing

We use **Legal Unit Testing**. We treat laws like software specifications.

  * **Policy Tests:** `make test-rego`
      * Runs OPA's built-in testing framework.
      * *Scenario:* "Input: Toxic Waste, Dest: Non-OECD." -\> *Assert:* "Deny".
  * **Integration Tests:** `make test-api`
      * Simulates a `NovaTrade` request. Verifies that the API correctly queries the OPA container and returns a 403 Forbidden response.

-----

## 🤝 Contributing

We actively seek **"Legal Engineers"**—contributors who understand both code and regulation (GDPR, Environmental Law).
See [CONTRIBUTING.md](https://www.google.com/search?q=../.github/CONTRIBUTING.md) for details.

**Maintainers:** `@novaeco-tech/maintainers-enabler-novapolicy`