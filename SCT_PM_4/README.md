Product Requirements Document (PRD): Q-Chat

📋 1. Document Control & Metadata

Product Name: Sovereign Quantum AI Suite

Feature Name: Q-Chat: Sovereign Offline In-App Collaborative Messaging (Feature ID: F-04-CHAT)

Status: Finalized / Ready for Engineering Build

Lead PM: Ashwin Kumar Sriramoju

Target Audience: Offshore Rig Automation Engineers, LEO Satellite Ground Node Operators, and Mission Operations Teams operating in disconnected environments.

🛰️ 2. Purpose of the Feature & Strategic Vision

In remote operational environments—such as subsea stratigraphic exploration units in the GCC region or orbital tracking stations—teams rely heavily on cloud-tethered channels to pass logs, coordinate manual intervention scripts, and handle system alerts. However, severe regional sandstorms and solar cosmic activities regularly interrupt satellite downlinks, causing extended communication blackouts.

The Problem

During VSAT or satellite signal blackouts, on-site personnel are rendered "operationally blind." They lose the ability to coordinate emergency pressure releases, log manual drill calibrations, or alert neighboring control cabinets. Standard chat applications fail completely because their architectures require active handshakes with remote external clouds (e.g., AWS, Slack APIs).

The Q-Chat Solution

Q-Chat is an offline-first, decentralized, peer-to-peer (P2P) in-app messaging and alert system integrated directly into the local execution runtime. It requires:

Zero Internet Connectivity: Operates entirely over local wireless subnets, physical ethernet loops, and ad-hoc Wi-Fi mesh setups.

Decentralized Synchronization: Uses localized gossip protocols to ensure all active terminal units share a identical copy of the message ledger automatically when connectivity drops.

Cryptographic Verification: Every message is cryptographically signed at the local edge terminal to prevent data sniffing or malicious signal injection during total network isolation.

📝 3. Detailed User Stories & Acceptance Criteria

User Story US-01: Zero-Connectivity Peer-to-Peer Message Synchronization

User Role: As an Offshore Lead Automation Engineer operating in a disconnected subsea drilling platform,

Goal: I want to send real-time coordinates and coordinate calibration scripts with neighboring terminal operators without active internet or cloud server access,

Value: So that we can manage high-pressure stratigraphic hazards safely during a total satellite communication blackout.

Acceptance Criteria (Gherkin Format):

Scenario: Successful P2P node discovery and local sync

Given that VSAT connectivity drops to 0% and the terminal local subnet is physically isolated,

When I log into the localized application interface and open the Q-Chat panel,

Then the local system must auto-discover active terminal nodes over the local Wi-Fi or physical ethernet link using multicast DNS (mDNS) under $\le 5$ seconds,

And allow me to broadcast a structured string mapping format payload directly to all discovered terminal units.

Scenario: Gossip-protocol ledger convergence

Given three disconnected terminals ($T_A$, $T_B$, $T_C$) on the local subnet with unsynced message states,

When $T_A$ broadcasts a new structural density log update to $T_B$,

Then $T_B$ must automatically relay the payload to $T_C$ upon receipt,

And ensure all three terminal ledgers converge to an identical state with a mathematical convergence time bounds of:

$$T_{sync} \le c \log_2(N)$$

where $N$ is the number of active subnet nodes, and $c$ is the local latency constant.

User Story US-02: Local Priority Emergency Alert Override

User Role: As a GCC Field Operations Safety Director,

Goal: I want critical threshold sensor alerts to automatically bypass normal chat lists and trigger fullscreen audio-visual warnings on all active edge nodes,

Value: So that emergency blowout preventer (BOP) procedures can be activated collectively before local hardware parameters face thermal or pressure failure.

Acceptance Criteria (Gherkin Format):

Scenario: High-priority payload overrides active UI

Given that a local system sensor reports a stratigraphic pressure spike exceeding $+185^\circ\text{C}$ threshold constraints,

When the sensor auto-posts an alert payload containing priority: "CRITICAL_OVERRIDE",

Then the Q-Chat client on all connected terminal units must intercept this incoming message,

And immediately bypass normal chat notifications to display a flashing fullscreen alert overlay with an audible warning tone,

And block further typing sequences until the active operator manually logs a "Hazard Acknowledged" click interaction.

User Story US-03: Local Signature Key Validation

User Role: As a Sovereign Security Compliance Officer,

Goal: I want every local message package to be cryptographically signed by the originating operator's terminal security chip,

Value: So that we can prevent unauthorized third-party terminals from spoofing sensor logs or injecting malicious commands into the disconnected local network.

Acceptance Criteria (Gherkin Format):

Scenario: Message validation and signature verification

Given that the local network operates completely offline,

When any operator sends a command or log message through Q-Chat,

Then the terminal client must sign the payload package natively using SHA-256 with ECDSA cryptography,

And append the signature block to the outgoing message,

And the receiving terminals must verify the signature block against the locally cached public key store before rendering the message inside the UI,

And reject and isolate any message failing the verification check.

⚙️ 4. Functional Requirements (FRs)

[FR-4.1] Local Discovery & Socket Management

Requirement: The system must automatically build and manage a local network node map without needing centralized address registers or static DHCP assignments.

Technical Details:

Utilizes Multicast UDP broadcasting on local port 5353 for zero-configuration hostname resolution.

Spawns non-blocking TCP socket streams on local port 9898 for direct peer-to-peer data transfers.

Node discovery rate must actively refresh every $5.0\text{ seconds}$ to account for dynamic operator movement.

[FR-4.2] gossip-Protocol Ledger Sync Engine

Requirement: All chat text packages and sensor alert logs must be organized into a local chronological ledger that maintains structural consistency across all nodes.

Technical Details:

Uses a vector-clock matrix to track relative message causal relationships and prevent out-of-order rendering.

Employs a decentralized hash verification loop. If a node detects a ledger inconsistency, it initiates a recursive diff synchronization over local TCP.

[FR-4.3] Cryptographic Payload Verification

Requirement: No payload may be written to the local chat state without undergoing localized cryptographic signature verification.

Technical Details:

Messages package contains: [Timestamp] [Sender ID] [Text Payload] [Digital Signature].

Every terminal maintains a local database of public keys for authorized operators.

Message processing must reject packets if verification latency exceeds $50\text{ ms}$, logging a local alert to flag potential network tampering.

📊 5. Technical Success Metrics (KPIs)

To evaluate the operational performance and reliability of Q-Chat during disconnected drilling maneuvers, the system will track four main technical success criteria:

Decentralized Synchronization Latency ($L_{sync}$): The average time required for a message sent from Terminal $A$ to be received and verified across all connected terminal units on the isolated local subnet. The target parameter is:

$$L_{sync} \le 120\text{ ms}$$

Ledger Consistency and Packet Loss Recovery Overhead ($\eta_{loss}$): The network overhead required to resolve missing packets or coordinate state differences across nodes over the local UDP multicast pipeline:

$$\eta_{loss} = \frac{\text{Sync Bytes Transmitted}}{\text{Payload Bytes Transmitted}} - 1 \le 0.05$$

Active Local Battery Consumption Draw ($P_{draw}$): The local power footprint drawn by running continuous multicast discovery and socket listener threads on ruggedized portable field terminals. Power profiles must not impact core device battery life:

$$P_{draw} \le 350\text{ mW}$$

Zero-Trust Validation Precision Rate ($R_{auth}$): The accuracy with which the system identifies, blocks, and isolates unverified payloads or spoofed terminals trying to inject invalid metrics:

$$R_{auth} = 100.0\%$$

🎨 6. Wireframe Layout Architectural Blueprint

Refer to the interactive mockup slide in Artifact 2 (task_04_wireframe_slide.html) to see these components running live in our high-fidelity layout:

Module A (Global Sidebar Header): Shows connection diagnostics: Local Subnet Status, Total Active Mesh Nodes, and Local Node IP/Hash.

Module B (Dynamic Node Directory): Displays a live registry of discovered nearby operators, listing their terminal ID, role, and localized signal ping.

Module C (Core Chat Ledger): Features a chronological scroll interface. High-priority alarms trigger bright visual borders and alert icon animations.

Module D (Encrypted Input Drawer): A clean text input field with a digital verification shield overlay. Toggling "Override Alert" formats the payload with high-priority warnings.
