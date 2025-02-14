
# System Requirements Document: TACLink

## Objective

Develop TACLink as a replacement for the TAK (Tactical Assault Kit) and FreeTAKServer ecosystems, leveraging Golang as the core technology. TACLink aims to provide a modern, secure, and scalable solution for geospatial mapping, situational awareness, and tactical communication.  It aims to address limitations of existing solutions while offering improved features and usability, and maintaining interopability.

**TAC** stands for **Tactical Adaptive Coordination**, reflecting the system's focus on dynamic adaptability and collaborative functionality within a **multi-tenant federated architecture**.

## Functional Requirements

### Core Features

1. **Geo-spatial Mapping and Visualization:**

   - Interactive, real-time mapping capabilities.
   - Support for standard map layers (e.g., satellite, topographic).
   - Integration of overlays for mission-critical data (e.g., boundaries, points of interest, routes).

2. **Situational Awareness:**

   - Real-time position tracking of users or assets.
   - Dynamic updates for mission-critical events and status changes.

3. **Data Sharing:**

   - Secure sharing of mission-related data (e.g., documents, images, videos).
   - Support for packaging and transmitting data between users.
   - Data visibility and interaction governed by the **multi-tenant federated architecture** rules, ensuring granular control over data access and sharing across federated servers.

4. **Communication Tools:**

   - Real-time chat and messaging between users.
   - Support for broadcast messages to teams or all users.

5. **User and Team Management:**

   - Role-based access control (RBAC) for users and groups.
   - Users can hold multiple roles and switch between them based on context.
   - Roles can span across federated servers with predefined access levels and permissions.

6. **Mobile and Multi-Platform Support:**

   - Cross-platform mobile applications (Android, iOS).
   - Support for desktop environments (Windows, Linux, macOS).

### Infrastructure Requirements

1. **Multi-Tenant Federated Architecture:**

   - Servers operate independently but can federate with other servers to share selected data and resources.
   - Federation allows for controlled data visibility and access:
     - Example: Server 1 (5 clients) federates with Server 2 (300 clients). Server 2 allows Server 1 to view specific data but not interact with it, except for a single user from Server 1 who is granted a subset of permissions in Server 2.
   - Clients are tied to their respective servers, but federated servers can selectively grant or restrict cross-server client access.
   - Supports hierarchical and scoped access models to ensure precise control over shared data.

2. **Deployment Options and Ease of Installation:**

   - Deployable on any Linux-based system, regardless of hosting environment.
   - On-premises deployment for secure environments.
   - Cloud-hosted options for scalability and ease of access.
   - Target support for small servers, including Raspberry Pi.
   - Flexible installation options, including Docker-based or script-based setups for simplicity and portability.

3. **Ease of Installation:**

   - Docker-based installations for containerized environments.
   - Script-based installations for flexibility and simplicity.

4. **Data Encryption and Security:**

   - End-to-end encryption for communication and data storage.
   - Compliance with industry standards for cybersecurity.
   - Ensures that data shared across federated servers is encrypted and subject to access policies defined by the server owners.

5. **Two-Level Security Framework:**

   - **Device-Level Authentication:** Verify whether a device is authorized to access the system.
   - **User-Level Authentication:**
     - Utilize Public Key Infrastructure (PKI) for user authentication, inspired by cryptocurrency-style systems (keys are not blockchain-based).
     - Users can create, recreate, and manage their keys through a secure mechanism.
     - System validates both device and user credentials before granting access.
     - Incorporate Role-Based Access Control (RBAC) allowing users to have multiple roles and switch between them dynamically across federated servers.

### Deployment Requirements

1. **Central and Decentralized Options:**

   - While the initial release will support central server-based architecture, future releases will prioritize **multi-tenant federated architecture**, allowing for selective and secure data sharing across servers.

2. **Scalability:**

   - Support for environments ranging from small tactical teams to large-scale deployments.

### User Interface Requirements

1. **User-Friendly Interface:**

   - Intuitive design for non-technical users.
   - Customizable dashboard for different roles and missions.

2. **Real-Time Feedback:**

   - Immediate updates and notifications for events or changes.

3. **Localization:**

   - Multi-language support for global users.                    |
