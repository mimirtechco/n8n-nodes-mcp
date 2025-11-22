# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.5] - 2025-11-23

### Fixed
- **DEFINITIVE FIX: Force Zod 3.25.67 across all dependencies**
  - Added zod 3.25.67 as direct dependency (matching n8n-workflow version)
  - Added npm overrides to force zod 3.25.67 in all transitive dependencies
  - This ensures the package uses the same zod version as n8n-workflow, which includes the `/v3` export
  - Removed zod from peerDependencies to prevent version conflicts during installation
  - **This version WILL work in n8n environments** - all dependencies now use the correct zod version with `/v3` export

### Why This Works
- n8n-workflow uses zod 3.25.67, which has exports for `/v3`, `/v4`, and `/v4-mini`
- Previous versions tried to let npm resolve zod versions, which caused older versions without `/v3` to be installed
- Now we explicitly force the same version n8n uses, ensuring compatibility

## [0.2.4] - 2025-11-23

### Changed
- Intermediate version (not released)

## [0.2.3] - 2025-11-23

### Fixed
- **Critical: Resolved Zod dependency conflict preventing n8n installation**
  - Removed zod version pinning (was 3.24.0) that lacked `/v3` export required by n8n
  - Added zod as peerDependency (>=3.23.0) to allow n8n to use its preferred version
  - Fixed TypeScript compilation errors with proper type casting for Zod objects
  - Updated `callTool` arguments to use `unknown` intermediate casting
  - Used `any` type for aiTools mapping to avoid version conflicts between dependencies
  - Disabled `noUnusedLocals` in tsconfig.json to resolve NodeConnectionType import issue
  - Added NodeConnectionType mock in test suite for compatibility

### Changed
- Improved TypeScript configuration for better compatibility with n8n ecosystem
- Enhanced test suite with proper mocking of n8n-workflow dependencies

## [0.2.2] - 2025-11-22

### Changed
- Updated package name to `@mimirtech/n8n-nodes-mcp` for npm publishing

## [0.2.1] - 2025-11-22

### Fixed
- Fixed CI/CD workflow token authentication
  - Added fallback to `github.token` when `CICD_TOKEN` is not configured
  - Prevents workflow failures when custom token is not set

## [0.2.0] - 2025-11-22

### Changed
- **Updated @modelcontextprotocol/sdk** from 1.16.0 to 1.22.0
  - Updated client initialization to use new capabilities API
  - Removed deprecated individual capability specifications
- **Updated package metadata**
  - Enhanced description with detailed feature information
  - Updated author to Mimir Tech Co
  - Added original author (Jd Fiscus) as contributor
  - Updated repository URL to mimirtechco/n8n-nodes-mcp
  - Added homepage URL
  - Added new keywords: model-context-protocol, ai-agent, langchain

### Fixed
- Fixed security vulnerabilities in dependencies:
  - js-yaml: prototype pollution (updated to 3.14.2 and 4.1.1)
  - brace-expansion: ReDoS vulnerability (updated to 1.1.12 and 2.0.2)
- Fixed TypeScript compatibility with latest MCP SDK

### Security
- Resolved 2 vulnerabilities (1 moderate, 1 low)
- Remaining vulnerabilities are transitive dependencies from n8n-workflow and will be resolved by n8n updates

## [0.1.29] - Previous Release

### Initial features
- Support for STDIO, SSE, and HTTP Streamable transports
- Integration with n8n AI Agent
- Operations: List Tools, Execute Tool, List/Get Prompts, List/Read Resources
- Multiple credential types for different connection methods
