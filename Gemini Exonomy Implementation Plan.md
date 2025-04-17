\# Exonomy/Exocracy  
Implementation Plan  
Table of Contents

\#\# Introduction  
\#\#\# 1.1 Purpose & Scope (MVP Focus)  
This document outlines the implementation plan for the Exonomy and Exocracy ecosystem, focusing on delivering the Minimum Viable Product (MVP) with core functionalities, including voucher-based exchanges, project management, and community governance. The MVP emphasizes decentralized infrastructure, selective replication, and trust-driven interactions.

\#\#\# 1.2 Target Platforms (Web PWA, Mobile via Capacitor)  
The system will be developed as a Progressive Web App (PWA) and wrapped using Capacitor for mobile deployment on Android and iOS.

\#\# Technology Stack Summary  
\- \*\*Framework\*\*: Nuxt 3 \+ Ionic Vue  
\- \*\*Mobile/Desktop Wrapper\*\*: Capacitor  
\- \*\*State Management\*\*: Pinia  
\- \*\*P2P Database\*\*: OrbitDB  
\- \*\*P2P File Storage & Networking\*\*: IPFS via Helia  
\- \*\*UI Components\*\*: Ionic Framework Components  
\- \*\*Identity\*\*: DIDs (Public Key based)  
\- \*\*Permissions\*\*: UCANs

\#\# Repository & Environment Setup  
\#\#\# 3.1 Project Initialization (Nuxt 3, Ionic CLI integration, Capacitor)  
Initialize the project using Nuxt 3 and integrate Ionic CLI for UI components. Configure Capacitor for cross-platform builds.

\#\#\# 3.2 Recommended Folder Structure Review  
Organize the project into modular directories for clarity and maintainability.

\#\#\# 3.3 Dependency Installation (Core libs: \`@ionic/vue\`, \`@capacitor/core\`, \`helia\`, \`orbit-db\`, \`pinia\`)  
Install necessary dependencies for the tech stack, replacing \`js-ipfs\` with \`helia\`.

\#\#\# 3.4 Development Tooling (Linting, Formatting, TypeScript Config)  
Set up linting, formatting, and TypeScript configurations to enforce coding standards.

\#\# Core P2P Infrastructure Setup (Nuxt Plugins)  
\#\#\# 4.1 Helia Node Initialization & Management Plugin  
Initialize and manage Helia nodes for decentralized storage and communication.

\#\#\# 4.2 OrbitDB Instance Initialization Plugin (Depends on Helia)  
Set up OrbitDB instances for decentralized data storage and synchronization.

\#\#\# 4.3 Global Error Handling for P2P Services  
Implement error handling mechanisms for P2P services.

\#\# State Management Setup (Pinia)  
\#\#\# 5.1 Core Stores Definition (e.g., User Profile/DID, App State)  
Define Pinia stores for managing user profiles, app state, and other core functionalities.

\#\#\# 5.2 Pinia Plugin for Nuxt Integration  
Integrate Pinia with Nuxt for centralized state management.

\#\# Identity Management (DID)  
\#\#\# 6.1 DID Generation (Keypair generation) & Persistence (Secure storage)  
Generate and securely store DIDs for user identification.

\#\#\# 6.2 User Profile Data Structure & OrbitDB Store Setup  
Define user profile data structures and set up OrbitDB stores for profile management.

\#\#\# 6.3 Profile Creation / Import Flow  
Implement flows for creating or importing user profiles.

\#\#\# 6.4 DID Switching Logic within the Host App  
Enable switching between multiple DIDs within the app.

\#\# Exonomy Host Application Shell  
\#\#\# 7.1 Main Layout (\`app.vue\`) framed with CSS:Grid with Ionic Structure (\`IonApp\`, \`IonRouterOutlet\`)  
Set up the main application layout using CSS:Grid and Ionic components.

\#\#\# 7.2 Carousel Navigation (IonSlides for Vallet, vBay, Exocracy)  
Implement a carousel-based navigation system for accessing different modules. The carousel will display the core modules—Vallet, vBay, and Exocracy—as swipeable panels, allowing users to horizontally scroll through the modules for seamless access to their functionalities.

\#\#\# 7.3 Initialization Sequence (Connect P2P services, Load Profile)  
Define the initialization sequence for connecting P2P services and loading user profiles.

\#\# 'Vallet' Module (a distinct Nuxt app that can communicate with Exonomy as a tenant app) (Voucher Wallet \- MVP)  
\#\#\# 8.1 Voucher Data Model Definition (JSON Schema)  
Define the data model for vouchers using JSON Schema.

\#\#\# 8.2 Voucher OrbitDB Store Setup (\`docs\` store recommended, indexed by ID)  
Set up OrbitDB stores for managing vouchers.

\#\#\# 8.3 Voucher Pinia Store (State management, actions interfacing with OrbitDB)  
Create a Pinia store for voucher-related state management.

\#\#\# 8.4 UI Components (\`VoucherCard\`, \`VoucherDetail\`)  
Develop UI components for displaying and interacting with vouchers.

\#\#\# 8.5 UI: Display Owned Vouchers (List View)  
Implement a list view for displaying owned vouchers.

\#\#\# 8.6 UI: Voucher Minting Form & Logic (\`db.put\`)  
Create a form for minting new vouchers and handle the logic for storing them in OrbitDB.

\#\#\# 8.7 UI: View Voucher Details  
Develop a detailed view for individual vouchers.

\#\#\# 8.8 Voucher State Updates (e.g., Draft \-\> Listed, handling OrbitDB updates)  
Handle state transitions for vouchers and update them in OrbitDB.

\#\# 'vBay' Module (Also a tenant app, Marketplace \- MVP)  
\#\#\# 9.1 Public Voucher Discovery Mechanism (Shared/Public OrbitDB \`feed\` or \`docs\` store)  
Implement mechanisms for discovering public vouchers.

\#\#\# 9.2 UI: Display Discoverable Vouchers (Listening to public DB)  
Develop UI components for displaying discoverable vouchers.

\#\#\# 9.3 Basic Client-Side Search/Filtering (Based on replicated OrbitDB data)  
Add search and filtering capabilities for vouchers.

\#\#\# 9.4 UI: Initiating Interaction (e.g., Navigate to Voucher Detail/Chat)  
Enable users to initiate interactions with vouchers.

\#\# 'Exocracy' Module (Also a tenant app, Project Management \- MVP)  
\#\#\# 10.1 Project & Task Data Model Definition  
Define data models for projects and tasks.

\#\#\# 10.2 Project/Task OrbitDB Store Setup (Separate stores or nested structure)  
Set up OrbitDB stores for managing projects and tasks.

\#\#\# 10.3 Project/Task Pinia Store  
Create a Pinia store for project/task-related state management.

\#\#\# 10.4 UI: Display Project/Task Lists  
Develop UI components for displaying project/task lists.

\#\#\# 10.5 UI: Basic Project/Task Creation Form  
Create forms for adding new projects and tasks.

\#\#\# 10.6 Conceptual Voucher Linking (Storing voucher CIDs/references in task data)  
Link vouchers to tasks for crowdfunding and compensation.

\#\# Decentralized Communication (Chat via OrbitDB \- MVP)  
\#\#\# 11.1 Chat Message Data Model  
Define the data model for chat messages.

\#\#\# 11.2 Chat OrbitDB Store Setup (\`feed\` store per chat room, linked to Voucher/Task ID)  
Set up OrbitDB stores for chat messages.

\#\#\# 11.3 UI: Chat Interface Component  
Develop UI components for chat interactions.

\#\#\# 11.4 Logic: Sending & Receiving Messages (Adding to/replicating OrbitDB feed)  
Handle sending and receiving chat messages.

\#\#\# 11.5 Linking Chat Rooms to Vouchers/Tasks  
Vouchers and tasks can host chat sessions. Anyone can initiate a chat with anyone else “under” a voucher or a task so that there is a history of any discussion about that one item.

\#\# Core P2P Workflows (MVP)  
\#\#\# 12.1 Voucher Exchange Process (Simplified: Chat negotiation \+ Application-level state updates in OrbitDB reflecting ownership change)  
Implement the voucher exchange process.

\#\#\# 12.2 Following Users (Subscribing to Peer's Public OrbitDB Feed Address)  
Enable users to follow other users and subscribe to their public feeds.

\#\#\# 12.3 OrbitDB Access Control Configuration (Basic: Public read, owner write; Preparing for more granular controls)  
Configure access controls for OrbitDB stores.

\#\# Persistence & Offline Support  
\#\#\# 13.1 Leveraging OrbitDB/Helia Caching  
Utilize caching mechanisms for offline support.

\#\#\# 13.2 State Hydration/Rehydration (Pinia with P2P data)  
Implement state hydration and rehydration for offline-first functionality.

\#\#\# 13.3 Handling Offline Mutations  
Handle mutations made while offline and synchronize them when connectivity is restored. To which extent does OrbitDB with Helia not provide this?

\#\# Testing Strategy  
\#\#\# 14.1 Unit Testing (Vitest for Composables, Pinia Stores)  
Write unit tests for composables and Pinia stores.

\#\#\# 14.2 Component Testing (Vue Test Utils, Vitest)  
Test UI components using Vue Test Utils and Vitest.

\#\#\# 14.3 E2E Testing Considerations (Simulating P2P interactions)  
Plan for end-to-end testing of P2P interactions.

\#\# Build & Deployment (Initial Targets)  
\#\#\# 15.1 Nuxt Build Configuration (Static/Hybrid/SSR considerations)  
Configure Nuxt for static, hybrid, or SSR builds.

\#\#\# 15.2 Capacitor Configuration (\`capacitor.config.ts\`)  
Set up Capacitor configuration for mobile builds.

\#\#\# 15.3 Building for Web (PWA) \- Deployment Steps  
Define steps for deploying the PWA.

\#\#\# 15.4 Building for Mobile (Capacitor Android/iOS) \- Sync, Build Steps  
Outline steps for building and deploying the app on Android and iOS.

\#\#\# 15.5 Native Permissions (Camera, Filesystem for media uploads to Helia)  
Request and handle native permissions for media uploads.

\#\# MVP Review & Future Considerations  
\#\#\# 16.1 Summary of MVP Scope & Functionality  
Summarize the scope and functionality of the MVP.

\#\#\# 16.2 Known Limitations  
Acknowledge limitations in the MVP.

\#\#\# 16.3 Roadmap Items (Post-MVP):  
\- Advanced Exocracy Features (Crowdfunding logic, Consensus)  
\- Enhanced Reputation System Implementation  
\- Payment Processor Integration (Stripe, PayPal, Square, etc.)  
\- UCAN Integration for Permissions  
\- Advanced Search/Indexing (Beyond basic OrbitDB query)  
\- Improved Conflict Resolution Handling  
\- Desktop Build (Capacitor or alternative)

\#\# User Interface  
\- \*\*Top Navbar\*\*: Occupies 1/10 of the screen height, providing access to DID profiles, payment options, and authenticator management.  
\- \*\*Left Navbar\*\*: Occupies 1/5 of the screen width, housing the Reputation Card panel.  
\- \*\*Tenant App Area\*\*:  
  \- Divided into two decks:  
    \- Upper deck: Dashboard panels (2/5 of tenant app area height).  
    \- Lower deck: Tenant apps (3/5 of tenant app area height).  
  \- Supports up to three visible tenant apps at a time, with synchronized swiping for navigation.  
\- On mobile devices, only one tenant app is visible at a time, requiring swiping to navigate.

\#\# 'vBay' Module (Marketplace \- MVP)  
Public Voucher Discovery Mechanism (Shared/Public OrbitDB \`feed\` or \`docs\` store)  
UI: Display Discoverable Vouchers (Listening to public DB)  
Basic Client-Side Search/Filtering (Based on replicated OrbitDB data)  
UI: Initiating Interaction (e.g., Navigate to Voucher Detail/Chat)

\#\#\# Additional Features  
\- \*\*Broadcasting Vouchers\*\*: Implement functionality for Exonomists to broadcast vouchers to contact lists, project inboxes, individual Exonomists, existing communities, or newly defined communities.  
\- \*\*Notification Expiry\*\*: Add logic to handle notification expiry, removing expired vouchers from vBay unless manually pinned.  
\- \*\*Pinning Logic\*\*: Develop a mechanism for Exonomists to leverage IPFS’s pinning feature for vouchers in vBay, ensuring persistent visibility.

