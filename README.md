# UPI Offline Mesh
### Offline Payment Propagation & Settlement Simulation

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-orange?logo=openjdk" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring%20Boot-Backend-6DB33F?logo=springboot" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/Maven-Build-C71A36?logo=apachemaven" alt="Maven" />
  <img src="https://img.shields.io/badge/Security-Hybrid%20Encryption-blue" alt="Hybrid Encryption" />
  <img src="https://img.shields.io/badge/Project-Prototype-purple" alt="Prototype" />
</p>

<p align="center">
  A Java and Spring Boot-based simulation of how digital payment instructions can propagate across a network of devices without continuous internet connectivity.
</p>

---

## Overview

**UPI Offline Mesh** is a prototype that explores an alternative approach to payment propagation when internet connectivity is unavailable or unreliable.

The system simulates a network of virtual devices that exchange encrypted payment instructions through a decentralized, gossip-based propagation mechanism. Instead of requiring every device to communicate with a central server immediately, payment packets can travel across participating devices and reach a bridge node when connectivity becomes available.

The bridge node receives propagated packets, processes them, and uses idempotency mechanisms to prevent duplicate transaction processing.

The project demonstrates concepts from distributed systems, cryptography, REST API development, concurrent processing, and backend application architecture.

> **Disclaimer:** This project is an educational simulation. It is not an official UPI application, does not connect to NPCI or real banking infrastructure, and does not execute actual financial transactions. Its mesh communication is simulated using virtual devices rather than physical Bluetooth or other wireless hardware.

## Key Features

- **Offline Payment Simulation:** Creates payment instructions that can be propagated without requiring immediate server connectivity.
- **Virtual Device Network:** Simulates communication between multiple devices in a mesh-like environment.
- **Gossip-Based Propagation:** Uses a gossip-style mechanism to distribute payment packets between connected virtual devices.
- **Time-to-Live (TTL):** Limits packet propagation to control how long messages continue circulating through the simulated network.
- **Hybrid Encryption:** Combines AES-256-GCM symmetric encryption with RSA-2048/OAEP for secure key exchange.
- **Bridge Node Ingestion:** Simulates the point at which offline payment packets reach a connected node for processing.
- **Idempotency:** Prevents duplicate processing of the same payment instruction.
- **Concurrent Processing:** Includes concurrency-related handling for bridge-node ingestion and transaction processing.
- **Database Persistence:** Uses Spring Data JPA to manage and persist application data.
- **Dashboard Interface:** Provides a web-based interface for interacting with and observing the simulation.

## System Architecture

The application follows a layered Spring Boot architecture.

```text
              +---------------------------+
              |       Dashboard UI        |
              |       REST API Client     |
              +-------------+-------------+
                            |
                            v
              +---------------------------+
              |       API Controller      |
              +-------------+-------------+
                            |
                            v
              +---------------------------+
              |       Service Layer       |
              |                           |
              |  - Demo Service           |
              |  - Mesh Simulator         |
              |  - Bridge Ingestion       |
              |  - Idempotency Service    |
              |  - Settlement Service     |
              +-------------+-------------+
                            |
             +--------------+--------------+
             |                             |
             v                             v
  +----------------------+      +----------------------+
  | Cryptography Layer   |      | Virtual Device Mesh  |
  |                      |      |                      |
  | AES-256-GCM          |      | Gossip Propagation   |
  | RSA-2048/OAEP        |      | TTL Management       |
  +----------------------+      +----------+-----------+
                                           |
                                           v
                                +----------------------+
                                |    Bridge Node       |
                                |    Packet Ingestion  |
                                +----------+-----------+
                                           |
                                           v
                                +----------------------+
                                |   Persistence Layer  |
                                | Spring Data JPA      |
                                +----------------------+
```

### Main Components

| Component | Responsibility |
|---|---|
| API Controller | Exposes application endpoints and handles incoming requests. |
| Mesh Simulator Service | Coordinates virtual device communication and packet propagation. |
| Virtual Device | Represents an individual device participating in the simulated mesh. |
| Hybrid Crypto Service | Handles encryption and decryption operations. |
| Bridge Ingestion Service | Receives and processes packets reaching a bridge node. |
| Idempotency Service | Helps prevent duplicate processing of payment instructions. |
| Settlement Service | Handles the simulated settlement workflow. |
| Spring Data JPA | Provides database persistence and repository operations. |

## How It Works

The simulation follows a simplified offline payment workflow:

**1. Payment Instruction Creation**

A payment instruction is created within the application to represent a transaction initiated by a user.

**2. Encryption**

The payment data is protected using hybrid encryption:

- AES-256-GCM encrypts the payment payload.
- RSA-2048 with OAEP is used to protect the symmetric encryption key.

**3. Mesh Propagation**

The encrypted packet is distributed across virtual devices using a gossip-based propagation mechanism.

**4. TTL Management**

Each packet has a Time-to-Live (TTL) value that limits its propagation through the simulated network.

**5. Bridge Node Ingestion**

When a virtual device reaches the bridge node, the packet is submitted for ingestion and processing.

**6. Idempotency Check**

The system checks whether the payment instruction has already been processed to reduce the risk of duplicate settlement.

**7. Simulated Settlement**

The accepted instruction proceeds through the application's settlement workflow and relevant data is persisted.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Java 21 |
| Backend Framework | Spring Boot |
| API Architecture | REST APIs |
| Build Tool | Apache Maven |
| Cryptography | AES-256-GCM, RSA-2048/OAEP |
| Persistence | Spring Data JPA |
| Database Access | JPA / Hibernate |
| Frontend | HTML, CSS, JavaScript |
| Testing | JUnit / Spring Boot Test |
| Version Control | Git and GitHub |

## Project Structure

```text
UPI_Without_Internet/
│
├── .mvn/
│   └── wrapper/
│       └── maven-wrapper.properties
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/demo/upimesh/
│   │   │       ├── config/
│   │   │       ├── controller/
│   │   │       ├── crypto/
│   │   │       ├── model/
│   │   │       ├── service/
│   │   │       └── UpiMeshApplication.java
│   │   │
│   │   └── resources/
│   │       ├── application.properties
│   │       └── templates/
│   │           └── dashboard.html
│   │
│   └── test/
│       └── java/
│           └── com/demo/upimesh/
│               └── IdempotencyConcurrencyTest.java
│
├── .gitignore
├── mvnw
├── mvnw.cmd
├── pom.xml
├── README.md
└── LICENSE
```

## Getting Started

### Prerequisites

Make sure the following are installed:

- Java Development Kit (JDK) 21 or later
- Git
- Internet connection for the initial Maven Wrapper download

The Maven Wrapper downloads the configured Maven distribution automatically, so a separate Maven installation is not required.

### 1. Clone the Repository

```bash
git clone https://github.com/thecoderSky/UpiOfflineMesh.git
```

### 2. Navigate to the Project Directory

```bash
cd UpiOfflineMesh
```

### 3. Verify Java Installation

```bash
java -version
```

Ensure that Java 21 or a compatible newer version is available.

### 4. Build the Project

**Windows:**

```powershell
.\mvnw.cmd clean install
```

**Linux / macOS:**

```bash
chmod +x mvnw
./mvnw clean install
```

### 5. Run the Application

**Windows:**

```powershell
.\mvnw.cmd spring-boot:run
```

**Linux / macOS:**

```bash
./mvnw spring-boot:run
```

### 6. Access the Application

Once the application starts, open the local URL configured by the application:

```text
http://localhost:8080
```

If the application uses a different port, check `server.port` in `src/main/resources/application.properties`.

## Testing

The project includes a concurrency-oriented idempotency test.

Run the test suite using:

**Windows:**

```powershell
.\mvnw.cmd test
```

**Linux / macOS:**

```bash
./mvnw test
```

The test suite can be expanded to cover:

- Duplicate payment instruction handling
- Concurrent packet ingestion
- Encryption and decryption
- TTL-based packet expiration
- Mesh propagation behavior
- Settlement workflow

## Security Considerations

Security is an important part of this prototype.

The application explores the following cryptographic concepts:

| Mechanism | Purpose |
|---|---|
| AES-256-GCM | Authenticated symmetric encryption of payment payloads. |
| RSA-2048/OAEP | Protection of the symmetric encryption key. |
| Idempotency | Reduces duplicate transaction processing. |
| TTL | Limits the lifetime and propagation of packets. |

**Important:** These mechanisms demonstrate security concepts in a prototype. They do not establish production-grade financial security, regulatory compliance, secure device identity, or protection against every real-world attack.

## Current Limitations

The current implementation is a simulation and has the following limitations:

- No integration with official UPI or NPCI infrastructure.
- No real bank account connectivity or actual money transfer.
- Virtual device communication instead of physical Bluetooth or other wireless communication.
- Simulated bridge-node ingestion and settlement.
- No production deployment or financial regulatory certification.

## Future Enhancements

Potential improvements include:

- Implementing real device-to-device communication using Bluetooth Low Energy (BLE).
- Developing stronger device authentication and key management.
- Adding secure transaction synchronization and conflict resolution.
- Improving fault tolerance and network partition handling.
- Expanding automated unit and integration testing.
- Introducing monitoring, logging, and performance metrics.
- Exploring integration with authorized payment infrastructure in a compliant test environment.

## Learning Outcomes

This project provides practical exposure to:

- Building backend applications using Java and Spring Boot.
- Designing REST-based application architectures.
- Understanding symmetric and asymmetric cryptography.
- Exploring gossip protocols and distributed systems concepts.
- Handling duplicate requests through idempotency.
- Understanding concurrent processing in backend services.
- Managing application data using Spring Data JPA.
- Building and testing applications with Maven.

## Contributing

Contributions, suggestions, and improvements are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Implement your changes.
4. Run the available tests.
5. Submit a pull request with a clear description of your changes.

## License

See the [LICENSE](LICENSE) file for licensing information. Ensure that the license and redistribution terms are consistent with the permissions applicable to all reused and modified project components.

## Author

**Umang Gupta**

- GitHub: [@thecoderSky](https://github.com/thecoderSky)
- Project Repository: [UPI Offline Mesh](https://github.com/thecoderSky/UpiOfflineMesh)

---

<p align="center">
  <b>Exploring resilient digital payment systems through distributed computing and secure communication.</b>
</p>
