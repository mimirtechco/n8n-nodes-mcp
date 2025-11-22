# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
