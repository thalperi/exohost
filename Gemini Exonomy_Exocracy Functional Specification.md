\# Exonomy/Exocracy Functional Specification

\#\# 1\. Introduction  
\#\#\# 1.1 Purpose  
This document defines the functional specifications for the Exonomy and Exocracy ecosystem, a decentralized, peer-to-peer platform designed to facilitate voucher-based economic interactions and community-driven project management. Exonomy aims to establish a decentralized platform for voucher-based exchanges, fostering trust and economic resilience. The platform leverages decentralized P2P technology, primarily OrbitDB built upon Helia, as its core communication and data persistence infrastructure, ensuring offline-first operations, selective data replication, and decentralized governance triggers.

\#\#\# 1.2 Scope  
This document outlines the architecture, workflows, governance, and technical details of both Exonomy and Exocracy. It emphasizes asset autonomy, selective replication, and consensus mechanisms to promote trust, local economic resilience, and community impact.

\- \*\*Exonomy\*\*: Peer-to-peer exchange of vouchers representing specific goods/services. Hosted within the Exonomy controller app via modules like 'Vallet' (wallet) and 'vBay' (marketplace).  
\- \*\*Exocracy\*\*: Collaborative task management with hierarchical potential and community oversight, hosted as a module within the Exonomy controller app.

\#\#\# 1.3 Key Objectives  
\- \*\*Decentralized Infrastructure\*\*: Utilize OrbitDB's CRDT-based synchronization capabilities over Helia to minimize dependency on central servers for core data exchange and persistence.  
\- \*\*Local-First Resilience\*\*: Ensure uninterrupted voucher interactions and community governance workflows, even in offline or low-connectivity environments, leveraging OrbitDB's offline capabilities. The system is designed to function fully P2P, though optional community-run Helia/OrbitDB nodes can bootstrap connectivity and ensure data availability.  
\- \*\*Trust-Driven Interactions\*\*: Implement reputation systems and consensus mechanisms triggered by OrbitDB events for secure, community-auditable interactions.  
\- \*\*Scalable Replication\*\*: Implement data sharing rules primarily for interaction-relevant parties, followed users, or project members, managed through OrbitDB access controls and application logic, minimizing resource overhead.  
\- \*\*Fiat Integration\*\*: Bridge traditional payment processors (Stripe, PayPal, Square, etc.) with decentralized voucher exchanges, using payment confirmation events to trigger state changes or enable voucher acquisition within the OrbitDB-based system.

\#\#\# 1.4 Definitions  
| Term | Definition |  
| \--- | \--- |  
| Exonomist | A user who mints, exchanges, or redeems vouchers. |  
| Exocrat | A user managing/contributing to Exocracy projects. |  
| Voucher | A cryptographically signed promise of a specific product/service at a predetermined value. |  
| Task | A unit of work within an Exocracy project, potentially linked to a method of funding including vouchers. |  
| OrbitDB | A serverless, distributed, peer-to-peer database built on Helia, enabling decentralized data storage & sync. |  
| Helia | A peer-to-peer hypermedia protocol for distributed file storage. |  
| CRDTs | Conflict-free replicated data types enabling seamless offline/online state merging (used by OrbitDB). |  
| UCAN | User Controlled Authorization Network; capability tokens for granular, delegable permissions. |  
| DID | Decentralized Identifier used for users, communities, assets. |

\#\# 2\. System Architecture  
\#\#\# 2.1 System Layers  
\*\*Data Layer\*\*: (Managed via OrbitDB databases over Helia)  
\- \*\*Vouchers\*\*: JSON-LD/RDF-like documents stored in OrbitDB (e.g., Docs or KeyValue stores) with semantic metadata (author DID, owner DID, value, currency, expiry, terms, state, IPFS links for media).  
\- \*\*Tasks\*\*: Data structures in OrbitDB representing project tasks, potentially hierarchical, linking to parent projects, assigned Exocrats, status, and associated voucher CIDs or references for funding/compensation.  
\- \*\*Reputation\*\*: Scores (EXO-SCORE) stored and updated in user profile databases (OrbitDB). User profiles (settings, followed users, etc.) also reside here.  
\- \*\*Chat Data\*\*: Messages stored in OrbitDB Feed or Log stores, linked to vouchers or tasks.

\*\*Protocol Layer\*\*:  
\- \*\*OrbitDB\*\*: P2P database replication engine using pub/sub over Helia for synchronization and CRDT-based state merging. Manages various database types (Docs, KeyValue, Feed, Log).  
\- \*\*Helia\*\*: Decentralized storage for immutable assets like voucher media (images, videos), task evidence (photos), potentially large static files, and underlying storage for OrbitDB. Also supports OrbitDB operations.  
\- \*\*UCAN\*\*: Capability tokens potentially used for granting specific, often temporary, permissions (e.g., authorizing a specific voucher exchange, granting write access to a task database for an assigned Exocrat) that can also be iteratively delegated.  
\- \*\*Libp2p\*\*: Networking stack used by Helia and OrbitDB for peer discovery, transport, and communication.

\*\*Application Layer (Exonomy Controller App & Modules)\*\*:  
\- \*\*Exonomy Host App\*\*: The main container application (e.g., built with Nuxt/Ionic/Capacitor). Manages overall P2P connections (Helia/OrbitDB initialization), DID switching, and provides a framework for hosting pluggable modules.  
\- \*\*'Vallet' Module\*\*: Manages user's owned/minted vouchers, DID profiles, interacts with OrbitDB voucher stores.  
\- \*\*'vBay' Module\*\*: Public voucher marketplace interface. Queries public OrbitDB feeds/indices for discoverable vouchers, facilitates initiating exchanges.  
\- \*\*'Exocracy' Module\*\*: Interface for creating, managing, browsing, and participating in projects and tasks. Interacts with OrbitDB project/task stores, handles crowdfunding/sourcing UI flows.  
\- \*\*Decentralized Chat Module\*\*: Integrates with voucher/task views, using OrbitDB Feed/Log stores for P2P messaging.  
\- \*\*(Potential Future Modules)\*\*: Voucher-aware versions of apps like AirBnB, Uber, etc., plugging into the Exonomy host and leveraging its P2P infrastructure and voucher system.

\#\#\# 2.2 Core Components & Principles (OrbitDB Focus)  
The platform’s architecture relies on OrbitDB over Helia for decentralized communication and data persistence.

\- \*\*Decentralized Data Layer\*\*: OrbitDB provides serverless databases (Docs, KV, Feed, Log) stored on Helia. Each user runs a Helia node and opens/connects to relevant OrbitDB databases.  
\- \*\*Data Synchronization\*\*: Occurs directly between peers via Helia pub/sub channels associated with each OrbitDB database.  
\- \*\*Local-First Repositories\*\*: Each Exonomist maintains local copies of the OrbitDB databases they access, with CRDTs ensuring consistent merging.  
\- \*\*Selective Replication via Access Control & Subscription\*\*: Data sharing is controlled by OrbitDB's Access Controllers and subscription mechanisms.

\#\#\# 2.3 Decentralized Identifiers (DIDs)  
Unique identifiers for users, communities, and potentially assets. Likely based on public keys associated with the user's device/profile.

\#\#\# 2.4 Data Structures & Semantic Modeling (OrbitDB Context)  
\- \*\*Voucher Metadata\*\*: Modeled as structured data (JSON-like) within OrbitDB Docs stores, potentially using schemas for semantic meaning.  
\- \*\*Decentralized Indexing\*\*: Public voucher feeds might use OrbitDB Feed stores or Docs stores indexed by fields.  
\- \*\*Provenance Tracking\*\*: OrbitDB's log structure immutably records operations with cryptographic hashes.

\#\#\# 2.5 Replication Controls & Selective Sharing (OrbitDB Context)  
\- \*\*OrbitDB Access Controllers\*\*: Define write permissions for databases.  
\- \*\*Capability Tokens (UCANs)\*\*: Grant fine-grained, temporary, or delegable permissions.  
\- \*\*Encryption & Privacy\*\*: End-to-end encryption for sensitive data implemented at the application layer.

\#\# 3\. Exonomy Mechanics  
\#\#\# 3.1 Voucher Lifecycle  
\- \*\*Minting\*\*: Vouchers are minted by Exonomists and stored in OrbitDB.  
\- \*\*Publication\*\*: To make a voucher public, its data is added to the Exonomist's public OrbitDB Feed store.  
\- \*\*Exchange\*\*: Peer-to-peer exchanges involve negotiation and updating ownership data in OrbitDB.  
\- \*\*Redemption\*\*: The current voucher owner presents it to the original author for validation and state update.  
\- \*\*State\*\*: Voucher entries in OrbitDB include a state field (Draft, Listed, Pending, Exchanged, Redeemed, Expired).

\#\#\# 3.2 Interactions & Integrations  
\- \*\*Barter/Exchange\*\*: Direct voucher-for-voucher exchange between Exonomists.  
\- \*\*Cash Integration\*\*: Payment processors handle cash transactions outside the core P2P voucher system.

\#\#\# 3.3 Wallet as Social Feed Interface  
The 'Vallet' module interfaces with OrbitDB to present feeds:  
\- \*\*Internal Feed\*\*: Displays curated content based on subscriptions.  
\- \*\*External Feed\*\*: Represents the Exonomist's own public OrbitDB Feed store.

\#\# Voucher Market: vBay  
vBay is implemented as a tenant app within the Exonomy controller application, serving as a decentralized marketplace for voucher discovery and exchange. It leverages OrbitDB for decentralized data storage and replication, ensuring efficient and selective propagation of voucher notifications.

\#\#\# Data Structures  
\- \*\*Voucher Notifications\*\*: Stored in OrbitDB Feed stores, representing notifications broadcast by Exonomists.  
\- \*\*Pinned Vouchers\*\*: Stored in a separate OrbitDB Docs store, allowing Exonomists to curate persistent listings.

\#\#\# Broadcasting Mechanism  
\- \*\*Broadcast Targets\*\*:  
  \- Contact Lists: Notifications are replicated to the OrbitDB feeds of all contacts.  
  \- Project Inboxes: Notifications are added to the OrbitDB stores associated with specific Exocracy projects.  
  \- Individual Exonomists: Notifications are sent directly to the target Exonomist's OrbitDB feed.  
  \- Communities: Notifications are replicated to the OrbitDB stores of existing or newly defined communities.  
\- \*\*Notification Expiry\*\*: Notifications expire based on predefined TTL (Time-To-Live) values unless manually pinned.

\#\#\# Pinning Logic  
\- \*\*Manual Pinning\*\*: Exonomists can update the state of a voucher in their OrbitDB store to "Pinned," ensuring it remains visible beyond its notification expiry.  
\- \*\*Pinned Voucher Store\*\*: A dedicated OrbitDB Docs store maintains a list of pinned vouchers, enabling persistent visibility.

\#\#\# Integration with Exocracy  
\- \*\*Project Contributions\*\*: Exonomists can broadcast vouchers directly to Exocracy project inboxes, facilitating voucher-based crowdfunding and crowdsourcing.  
\- \*\*Community Engagement\*\*: Notifications can be targeted at specific communities, fostering collaboration and resource pooling.

\#\# Communities  
Communities are implemented as dynamic entities within the Exonomy ecosystem, leveraging OrbitDB for decentralized data storage and governance.

\#\#\# Data Structures  
\- \*\*Community Metadata\*\*: Stored in OrbitDB Docs stores, containing properties such as membership lists, governance rules, and smart contract references.  
\- \*\*Interaction Logs\*\*: Stored in OrbitDB Log stores, recording all voucher interactions within the community.

\#\#\# Automatic Creation  
\- \*\*Trigger\*\*: Communities are automatically created whenever a voucher interaction occurs between two or more Exonomists.  
\- \*\*Membership Updates\*\*: Membership lists are dynamically updated in the OrbitDB Docs store as new interactions occur.

\#\#\# Governance Features  
\- \*\*Governance Properties\*\*: Stored in the community's OrbitDB Docs store, enabling decentralized decision-making.  
\- \*\*Smart Contracts\*\*: Optional smart contracts can be deployed to automate governance processes, such as voting or dispute resolution.

\#\#\# Role in Exonomy and Exocracy  
\- \*\*Collaboration Framework\*\*: Communities provide a structured environment for Exonomists to collaborate on projects and initiatives.  
\- \*\*Governance Support\*\*: The properties and smart contracts within communities facilitate decentralized governance, ensuring transparency and fairness.

\#\# 4\. Exocracy Mechanics  
\#\#\# 4.1 Project Management  
\- \*\*Project/Task Creation\*\*: Projects and tasks are created as data entries in dedicated OrbitDB stores.  
\- \*\*Crowdfunding\*\*: Exocrats pledge vouchers to specific tasks.  
\- \*\*Crowdsourcing & Exocrat Selection\*\*: Exocrats browse tasks and offer service vouchers.  
\- \*\*Approval & Consensus\*\*: Project Managers review bids and approve via consensus mechanisms.  
\- \*\*Overfunding & Voucher Release\*\*: Tasks can show pledged value exceeding target value.

\#\#\# 4.2 Community Governance and Trust  
\- \*\*Unanimous Consent\*\*: Required for specific critical actions.  
\- \*\*Asset Freezing\*\*: Only the author of a voucher can freeze it temporarily.  
\- \*\*Reputation System\*\*: Unified under \*\*EXO-SCORE\*\*, calculated from OrbitDB records.  
\- \*\*Dispute Resolution\*\*: Transparency and community arbitration protocols ensure equitable resolution.  
