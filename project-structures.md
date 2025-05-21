# Project Structure Guide

This file explains how the folders and files in this project are organized.  
It helps developers understand where to find things and where to add new code.

## Who Should Read This

- All developers working in the codebase
- Anyone adding new features or organizing files

## Purpose

This guide helps you:

- Understand how the project is organized
- Add new code in the correct place
- Keep the structure clean and easy to use


## Core Directory Structure
project-root/
├── src/                    # Source code (language-specific)
│   ├── js/                 # JavaScript/TypeScript (Node.js, Vite)
│   │   ├── assets/         # Static assets
│   │   ├── components/     # Reusable UI components
│   │   ├── routes/         # API or frontend routes
│   │   ├── services/       # Business logic, API calls
│   │   ├── lib/            # Shared utilities
│   │   ├── config/         # JS/TS cloud-agnostic configs
│   │   ├── logging/        # Logging configurations
│   │   ├── security/       # Security configurations (e.g., auth policies)
│   │   ├── Dockerfile      # Cloud-agnostic Docker config for JS/TS
│   │   └── index.ts        # Entry point
│   ├── go/                 # Go source code
│   │   ├── cmd/            # Application entry points
│   │   ├── pkg/            # Shared packages
│   │   ├── internal/       # Internal packages
│   │   ├── config/         # Go cloud-agnostic configs
│   │   ├── logging/        # Logging configurations
│   │   ├── security/       # Security configurations
│   │   └── Dockerfile      # Cloud-agnostic Docker config for Go
│   ├── rust/               # Rust source code
│   │   ├── src/            # Rust modules
│   │   ├── config/         # Rust cloud-agnostic configs
│   │   ├── logging/        # Logging configurations
│   │   ├── security/       # Security configurations
│   │   ├── Dockerfile      # Cloud-agnostic Docker config for Rust
│   │   └── Cargo.toml      # Rust dependencies
│   └── wasm/               # WebAssembly modules
│       ├── src/            # WASM source
│       ├── build/          # WASM build outputs
│       ├── config/         # WASM cloud-agnostic configs
│       ├── logging/        # Logging configurations
│       ├── security/       # Security configurations
│       └── Dockerfile      # Cloud-agnostic Docker config for WASM
├── tests/                  # Tests (language-specific)
│   ├── js/                 # JS/TS tests
│   │   ├── unit/           # Unit tests
│   │   ├── integration/    # Integration tests
│   │   └── e2e/            # End-to-end tests
│   ├── go/                 # Go tests
│   └── rust/               # Rust tests
├── docs/                   # Documentation
│   ├── compliance/         # NIST/FedRAMP compliance artifacts
│   │   ├── boundary/       # Authorization boundary diagrams, data flows
│   │   └── ssp/            # System Security Plan, CIS, etc.
│   ├── portability/        # Lock-in avoidance and portability guides
│   └── docker/             # Docker setup and usage
├── scripts/                # Automation scripts (Docker, Node.js, shell)
│   ├── docker/             # Cloud-agnostic Docker scripts
│   ├── build/              # Build scripts (Vite, WASM)
│   └── monitoring/         # Monitoring scripts for compliance
├── cloud-config/           # Optional cloud-specific configs (isolated)
│   ├── aws/                # AWS-specific files (e.g., ECS tasks)
│   ├── gcp/                # GCP-specific files
│   └── azure/              # Azure-specific files
├── .dockerignore           # Docker ignore file
├── .gitignore              # Git ignore file
├── .env                    # Cloud-agnostic environment variables
├── README.md               # Project overview
├── LICENSE                 # License file
├── package.json            # Node.js/Vite dependencies
├── tsconfig.json           # TypeScript configuration
├── biome.json              # Biome configuration
├── Dockerfile              # Root cloud-agnostic Dockerfile (if single-container)
├── docker-compose.yml      # Cloud-agnostic Docker Compose for local dev
├── go.mod                  # Go module file
└── Cargo.toml              # Rust project manifest (root, if Rust primary)


## Directory Details, DOs, DON’Ts, PROs, and CONs

### 1. src/
**Purpose**: Root for source code, split by language, with cloud-agnostic Docker configs for NIST/FedRAMP traceability.

- **DO**:
  - Use language-specific subdirs (`js/`, `go/`, `rust/`, `wasm/`) with `Dockerfile`s.
  - Ensure `Dockerfile`s use standard base images (e.g., `node:alpine`, `golang:alpine`) and multi-stage builds.
  - Document each component’s role in `docs/compliance/` for FedRAMP boundary definition.
- **DON’T**:
  - Include cloud-specific settings in `Dockerfile`s or `config/` (use `cloud-config/`).
  - Mix languages in one dir, as it complicates auditing.
  - Skip documentation of components for compliance.
- **PROs**:
  - Clear component inventory supports NIST CM-8 and FedRAMP boundary clarity.
  - Cloud-agnostic `Dockerfile`s ensure portability and compliance.
  - Modular design simplifies FedRAMP assessments.
- **CONs**:
  - Multiple `Dockerfile`s require rigorous version control (CM-3).
  - Team must maintain compliance documentation.

### 2. src/js/
**Purpose**: JS/TS code (Vite/Node.js) with cloud-agnostic Dockerization for compliance.

- **DO**:
  - Use a `Dockerfile` with `node:alpine` and multi-stage builds.
  - Store cloud-agnostic configs in `config/` and security policies in `security/`.
  - Use `.env` for runtime settings (e.g., API URLs, ports).
- **DON’T**:
  - Embed cloud-specific SDKs or settings in `config/` or `security/`.
  - Hardcode cloud provider endpoints in `Dockerfile`.
  - Mix frontend/backend without separation.
- **PROs**:
  - Portable containers meet NIST CM-7 and FedRAMP requirements.
  - `.env` and `security/` support AC-3 and SC-28.
  - Vite/Node.js aligns with open standards.
- **CONs**:
  - Node.js image size needs optimization.
  - Requires discipline to avoid cloud SDKs.

### 3. src/js/assets/
**Purpose**: Static assets, optimized for cloud-agnostic Docker builds.

- **DO**:
  - Subdivide by type (e.g., `assets/images/`) for Vite.
  - Optimize assets in `Dockerfile` (e.g., image compression).
  - Include assets in Docker image for portability.
- **DON’T**:
  - Assume cloud storage (e.g., S3) in asset structure.
  - Include unoptimized assets.
  - Scatter assets outside `assets/`.
- **PROs**:
  - Self-contained assets avoid cloud storage lock-in, supporting SC-28.
  - Vite optimization aids CM-7 (least functionality).
  - Simplifies FedRAMP audits.
- **CONs**:
  - Large assets increase image size.
  - Requires build-time optimization.

### 4. src/js/components/
**Purpose**: Reusable UI components, containerized without lock-in.

- **DO**:
  - Group by component (e.g., `components/Button/`) for modular builds.
  - Ensure components are cloud-agnostic and secure (e.g., no cloud-specific APIs).
  - Use TypeScript for type safety.
- **DON’T**:
  - Embed cloud-specific logic (e.g., AWS Amplify).
  - Create cloud-dependent components.
  - Mix backend logic with UI.
- **PROs**:
  - Portable components meet SA-8 and FedRAMP security requirements.
  - TypeScript supports SA-11 (secure development).
  - Modular structure avoids lock-in.
- **CONs**:
  - Many components increase build time.
  - Requires Vite config for compliance.

### 5. src/js/routes/
**Purpose**: Frontend/API routes, Dockerized and cloud-agnostic.

- **DO**:
  - Organize by resource (e.g., `routes/api/users.ts`).
  - Use `.env` for endpoint URLs to avoid hardcoding.
  - Keep routes thin, delegating to `services/`.
- **DON’T**:
  - Hardcode cloud-specific endpoints (e.g., AWS API Gateway).
  - Embed cloud service logic in routes.
  - Mix client/server routes without subdirs.
- **PROs**:
  - Portable routes support NIST AC-4 and FedRAMP.
  - `.env` ensures vendor-neutral routing.
  - Aligns with REST/SPA standards.
- **CONs**:
  - Many routes complicate container setup.
  - Requires separation of concerns.

### 6. src/js/services/
**Purpose**: Business logic and integrations, Dockerized without lock-in.

- **DO**:
  - Group by domain (e.g., `services/auth.ts`).
  - Use `.env` for vendor-neutral API/service configs.
  - Support WASM/external APIs with standard protocols (e.g., HTTP).
- **DON’T**:
  - Embed cloud-specific SDKs (e.g., AWS SDK).
  - Hardcode cloud service endpoints.
  - Create monolithic services.
- **PROs**:
  - Portable services meet NIST SC-7 and FedRAMP.
  - `.env` avoids lock-in for integrations.
  - TypeScript supports SA-11.
- **CONs**:
  - Complex integrations increase complexity.
  - Requires careful `.env` management.

### 7. src/js/lib/
**Purpose**: Shared JS/TS utilities, included in cloud-agnostic Docker images.

- **DO**:
  - Include stateless, vendor-neutral utilities (e.g., `dateUtils.ts`).
  - Ensure utilities work in Docker without cloud dependencies.
  - Use TypeScript for type safety.
- **DON’T**:
  - Include cloud-specific logic (e.g., AWS S3 utilities).
  - Create large utility files.
  - Duplicate utilities across projects.
- **PROs**:
  - Portable utilities support CM-7 and FedRAMP.
  - Reduces duplication without lock-in.
  - TypeScript ensures reliability.
- **CONs**:
  - Can become a “misc” dump if unorganized.
  - Adds to container size if overused.

### 8. src/js/config/
**Purpose**: Cloud-agnostic JS/TS configs for Dockerized environments.

- **DO**:
  - Include `.env` parsing (e.g., `env.ts`) for vendor-neutral settings.
  - Store Vite/Node.js configs (e.g., `vite.config.ts`).
  - Use `.env` for ports, URLs, avoiding cloud specifics.
- **DON’T**:
  - Embed cloud-specific configs (e.g., AWS region).
  - Scatter configs across `src/`.
  - Commit sensitive data.
- **PROs**:
  - Vendor-neutral configs support CM-6 and FedRAMP.
  - `.env` enables dynamic settings.
  - TypeScript reduces errors.
- **CONs**:
  - Complex configs add overhead.
  - Requires secure `.env` handling.

### 9. src/js/logging/
**Purpose**: Logging configurations for NIST AU-2 and FedRAMP compliance.

- **DO**:
  - Store logging configs (e.g., `log-config.ts`) for audit trails.
  - Ensure logs are cloud-agnostic (e.g., standard formats like JSON).
  - Integrate with `services/` for log collection.
- **DON’T**:
  - Embed cloud-specific logging (e.g., AWS CloudWatch).
  - Skip logging configs.
  - Store logs in `src/`.
- **PROs**:
  - Supports NIST AU-2/AU-6 and FedRAMP monitoring.
  - Portable logging configs work on any cloud.
  - Simplifies audit compliance.
- **CONs**:
  - Adds configuration overhead.
  - Requires log management (not structural).

### 10. src/js/security/
**Purpose**: Security configurations for NIST AC-4/SC-13 and FedRAMP.

- **DO**:
  - Store security policies (e.g., `auth-policy.ts`, encryption settings).
  - Ensure configs are cloud-agnostic (e.g., standard JWT, not AWS IAM).
  - Document policies in `docs/compliance/`.
- **DON’T**:
  - Embed cloud-specific security (e.g., AWS KMS).
  - Mix security with other configs.
  - Skip security documentation.
- **PROs**:
  - Supports NIST AC-4/SC-13 and FedRAMP security controls.
  - Portable configs reduce lock-in.
  - Enhances auditability.
- **CONs**:
  - Adds configuration complexity.
  - Requires team expertise in security.

### 11. src/go/, src/rust/, src/wasm/
**Purpose**: Go, Rust, and WASM code with cloud-agnostic Dockerization and compliance support.

- **DO**:
  - Use standard base images (`golang:alpine`, `rust:alpine`) in `Dockerfile`s.
  - Store vendor-neutral configs in `config/`, logging in `logging/`, security in `security/`.
  - Follow language standards (e.g., Go’s `cmd/`, Rust’s Cargo).
- **DON’T**:
  - Embed cloud-specific settings in `Dockerfile`, `config/`, or `security/`.
  - Mix languages or skip logging/security configs.
  - Place tests in `src/` (use `tests/`).
- **PROs**:
  - Portable containers meet NIST CM-7 and FedRAMP.
  - Logging/security configs support AU-2/AC-4.
  - Aligns with language standards, avoiding lock-in.
- **CONs**:
  - Long build times (Rust) slow Docker builds.
  - Requires language-specific Docker expertise.

### 12. tests/
**Purpose**: Tests for all languages, supporting NIST SA-11 and FedRAMP secure development.

- **DO**:
  - Mirror `src/` structure (e.g., `tests/js/unit/`).
  - Support Dockerized tests with vendor-neutral images.
  - Split by language and type (`js/`, `go/`, `rust/`, `unit/`, `e2e/`).
- **DON’T**:
  - Place tests in `src/`.
  - Use cloud-specific test frameworks.
  - Mix language-specific tests.
- **PROs**:
  - Dockerized tests ensure consistent environments (CA-2).
  - Clear organization supports SA-11.
  - Portable across clouds.
- **CONs**:
  - Test setup adds overhead.
  - Requires alignment with `src/`.

### 13. docs/
**Purpose**: Documentation for NIST RA-3, FedRAMP SSP, and lock-in avoidance.

- **DO**:
  - Include `docs/compliance/` for SSP, CIS, boundary diagrams.
  - Use `docs/portability/` for lock-in avoidance strategies.
  - Document Docker setup in `docs/docker/`.
- **DON’T**:
  - Store code or configs in `docs/`.
  - Document cloud-specific processes (use `cloud-config/`).
  - Skip compliance or boundary docs.
- **PROs**:
  - Centralizes NIST/FedRAMP artifacts, easing audits.
  - Portability focus reduces lock-in.
  - Supports 3PAO assessments.
- **CONs**:
  - Needs regular updates (CA-7).
  - Can be ignored without enforcement.

### 14. scripts/
**Purpose**: Cloud-agnostic automation scripts for Docker, builds, and monitoring.

- **DO**:
  - Use `scripts/docker/` for vendor-neutral Docker scripts (e.g., `build-js.sh`).
  - Use `scripts/build/` for Vite/WASM builds; `scripts/monitoring/` for compliance monitoring.
  - Avoid cloud-specific tools (e.g., no AWS CLI).
- **DON’T**:
  - Store scripts in `src/`.
  - Include cloud-specific commands (e.g., `gcloud`).
  - Duplicate CI/CD logic (see `ci-cd.md`).
- **PROs**:
  - Simplifies automation without lock-in.
  - Monitoring scripts support CA-7.
  - Portable across clouds.
- **CONs**:
  - Script sprawl possible.
  - Requires maintenance.

### 15. cloud-config/
**Purpose**: Isolates optional cloud-specific configs to avoid lock-in.

- **DO**:
  - Store cloud-specific files in subdirs (e.g., `cloud-config/aws/ecs-task.json`).
  - Keep optional and separate from `src/*/config/`.
  - Document usage in `docs/portability/`.
- **DON’T**:
  - Embed cloud-specific configs in `src/` or `Dockerfile`s.
  - Commit sensitive cloud credentials.
  - Rely on `cloud-config/` for core functionality.
- **PROs**:
  - Isolates cloud configs, supporting RA-2 and FedRAMP.
  - Enables multi-cloud without core changes.
  - Reduces lock-in risk.
- **CONs**:
  - May remain unused.
  - Requires discipline to keep isolated.

### 16. Root Files
**Purpose**: Essential files for cloud-agnostic portability and compliance.

- **DO**:
  - Include `.dockerignore` to exclude vendor-specific files.
  - Use `.env` for cloud-agnostic settings (e.g., no AWS region).
  - Add vendor-neutral `Dockerfile`, `docker-compose.yml`, `package.json`, `tsconfig.json`, `biome.json`, `go.mod`, `Cargo.toml`.
- **DON’T**:
  - Commit `.env` or sensitive files.
  - Include cloud-specific settings in `Dockerfile` or `docker-compose.yml`.
  - Clutter root with vendor-specific files.
- **PROs**:
  - `.dockerignore` and `.env` ensure lean, compliant images (CM-2).
  - `docker-compose.yml` supports vendor-neutral dev (CA-2).
  - Supports NIST/FedRAMP without lock-in.
- **CONs**:
  - Crowded root with configs.
  - Requires team alignment.

## Notes
- **NIST/FedRAMP Compliance**: `docs/compliance/`, `src/*/logging/`, and `src/*/security/` support key controls (PL-2, AU-2, AC-4). `cloud-config/` isolates cloud-specific files, ensuring portability.
- **Lock-In Avoidance**: `cloud-config/` and vendor-neutral `Dockerfile`s/`docker-compose.yml` minimize dependency on specific clouds, aligning with SA-8.
- **Containerization**: Standard images (e.g., `node:alpine`) and multi-stage builds ensure consistent, auditable deployments (CM-7).
- **Documentation**: `docs/compliance/boundary/` and `docs/portability/` guide auditors and developers, supporting RA-3 and FedRAMP’s SSP requirements.
- **Consistency**: Use this structure unless justified, ensuring compliance and portability.
- **Review**: Align on structure during project kickoff to enforce NIST/FedRAMP and lock-in avoidance.

For feedback or updates, submit a pull request or contact the project lead.

## Who Maintains This File

The **Platform Team** maintains this file.  
Review happens every three months or after major refactors.
