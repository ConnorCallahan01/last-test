# Regulatory Tracker - Technical Architecture Documentation

**Source**: repository/technical-specifications/regulatory-tracker-technical-architecture.md
**Type**: Technical Specification
**Upload Date**: 2026-02-09
**Source SHA**: Not provided

## Key Points

- Three-tier cloud-ready architecture with Next.js 14 frontend, FastAPI backend, and SQLite database, featuring asynchronous background processing for AI-powered regulatory analysis
- 7-stage scan orchestration pipeline: Initializing → Retrieving Sources → Detecting Changes → Analyzing (Claude API) → Scoring → Generating Artifacts → Finalizing
- Change detection uses SHA-256 hashing, keyword regex matching, and demo mode; integrates Claude Sonnet 4 API for structured JSON analysis with confidence scoring
- Comprehensive REST API endpoints for scans management, results retrieval, workflow transitions (draft → in_review → verified), and knowledge store exports
- Document artifact generation in two formats: markdown (stored in database) and professional Word documents (.docx) with cover pages, TOC, and styling
- Database schema includes scans, results, and sources tables with workflow status tracking and foreign key relationships; file-based SQLite with mock regulatory source JSON files
- Deployment via Docker Compose with containerized frontend and backend services sharing bridge network; designed for horizontal scaling with PostgreSQL migration and Redis caching for production

## Entities and Topics

- **Next.js 14 & React 19**: Frontend framework using App Router, TypeScript, and Tailwind CSS for component-based UI
- **FastAPI & Python 3.11**: Backend web framework with Pydantic validation and Uvicorn ASGI server
- **ScanOrchestrator Service**: Core service managing seven-stage pipeline with error handling and real-time status updates
- **LLMService**: Integration layer for Claude Sonnet 4 API with prompt engineering, output schema validation, and retry logic
- **ChangeDetectionService**: Identifies material changes via content hashing and keyword detection patterns
- **ArtifactGenerator**: Creates markdown and Word documents with professional formatting and structured content
- **Claude API**: Anthropic's model endpoint (claude-sonnet-4-20250514) for regulatory document analysis
- **Workflow Management**: Status tracking system (draft → in_review → verified → knowledge store)
- **SQLite Database**: File-based relational storage at `data/regulatory_tracker.db` with foreign key constraints
- **Asyncio Task Queue**: Python asyncio-based background processing for asynchronous scan execution
- **Mock Sources Directory**: JSON files simulating FinCEN, OCC, and Federal Reserve regulatory documents
- **Artifacts Directory**: Storage for generated .docx files with 90-day retention policy
- **Docker Compose**: Multi-container orchestration with shared volumes and networking

## Relevance to Project

This technical specification document provides the foundational architecture design for the Regulatory Tracker system, detailing the complete technology stack, data flows, API contracts, and deployment strategy. It serves as the authoritative reference for implementing the system components, integrating with external Claude API services, managing background scan processing, and scaling the application for production use in financial compliance automation.