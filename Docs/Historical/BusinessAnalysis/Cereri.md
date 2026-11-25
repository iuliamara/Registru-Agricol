> **Historical document — preserved from the recovery directory.** Its original requirements, examples, diagrams, attribution, and conclusions follow below. Implementation claims and legal references describe their original context; consult the current documentation index in `Docs/README.md` for verified behavior. Historical links and paths may refer to removed files or other branches.

---

# Business Analysis: Cereri (Applications / Petitions / Ticketing)

## 1. Overview
The "Cereri" module acts as the workflow and ticketing engine for the Agricultural Register. It manages all applications initiated by citizens (via the Portal or at the physical counter) and tracks them through their lifecycle until resolution by the municipal clerks.

## 2. Domain Entities & Attributes

### 2.1. Cerere (Application)
*   **Numar Inregistrare (Registration Number)**: Unique registry number (Numar de inregistrare Primarie).
*   **Data Depunerii (Submission Date)**
*   **Tip Cerere (Application Type)**: Eliberare Adeverinta (Certificate Issuance), Modificare Date (Data Amendment), Deschidere Rol (Open Role), Radiere (Closure).
*   **Solicitant (Applicant)**: Link to Persoana ID.
*   **Gospodarie ID**: Relevant household.
*   **Stare (Status)**: Noua (New), In Lucru (In Progress), Aprobata (Approved), Respinsa (Rejected), Finalizata (Completed).
*   **Functionar Asignat (Assigned Clerk)**: System User ID.
*   **Termen Legal (Legal Deadline)**: Date by which it must be resolved (e.g., 30 days).

### 2.2. Documente Atasate (Attachments)
*   User-uploaded proofs (ID scans, contracts, deeds).
*   System-generated outputs (Draft certificates).

## 3. Functional Requirements (Use Cases)
*   **UC-C01**: Register a new application (automatically from Portal or manually by clerk).
*   **UC-C02**: Route application to the appropriate department/clerk based on "Tip Cerere".
*   **UC-C03**: Approve a data amendment application, automatically applying the changes to the core databases.
*   **UC-C04**: Reject a application and send a justification message to the citizen.
*   **UC-C05**: Generate an audit trail of all state changes for a application.

## 4. Business Rules & Validations
*   **BR-01 (Legal Deadlines)**: The system must visually flag applications that are within 5 days of their Legal Deadline.
*   **BR-02 (Mandatory Attachments)**: Certain application types (e.g., "Deschidere Rol") cannot be submitted without specific mandatory document types (e.g., Title Deed, ID).
*   **BR-03 (State Transitions)**: A application cannot move from "Aprobata" back to "Noua". State transitions are strictly one-way forward, with specific rollback protocols requiring supervisor overrides.

## 5. Integrations & Dependencies
*   **Portal Cetateni**: Primary source of incoming applications.
*   **Registratura Generala (General Registry)**: Integration with the Town Hall's main document registry system to sync "Numar Inregistrare".
*   **All Core Modules**: Approved applications trigger data updates in Persoane, Terenuri, Parcele, etc.
