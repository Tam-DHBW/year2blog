# Software Architecture Document

## 1. Introduction

This Software Architecture Document provides a comprehensive architectural overview of the jAilbreak system. jAilbreak is an interactive web-based game that challenges players to extract hidden passwords from AI systems using various jailbreaking techniques. The document describes the architectural decisions, constraints, and views that shape the system design.

## 2. Architectural Representation

The jAilbreak architecture is represented through multiple views:

- **Use-Case View**
- **Logical View**
- **Process View**
- **Deployment View**
- **Implementation View**

The architecture follows a serverless, cloud-native approach using AWS services with a clear separation between frontend presentation layer and backend business logic.

## 3. Architectural Goals and Constraints

### Goals
- **Cost Efficiency**: Minimize operational costs through serverless architecture
- **Scalability**: Support growth from zero to thousands of concurrent users
- **Performance**: Provide sub-2-second response times for AI interactions, and sub 100ms response times for regular requests.
- **Maintainability**: Enable rapid development and deployment cycles

### Constraints
- **Cloud Provider**: AWS ecosystem for cost optimization
- **Programming Languages**: Rust for backend (performance/safety), JavaScript/React for frontend
- **Authentication**: AWS Cognito for user management
- **AI Models**: AWS Bedrock for LLM integration
- **Budget**: Minimal operational costs during development phase

## 4. Use-Case View

The system supports three primary use cases, which are elaborated on in the [use case overview](./use-cases/):

### AI Gatekeeper Chat
Players interact with AI models that guard passwords, requiring creative prompt engineering to bypass security measures.

### Level Progression
Players unlock new levels by successfully extracting passwords, with increasing difficulty and sophisticated guardrails.

### Level Selection
Authenticated users can select and replay unlocked levels to practice different jailbreaking techniques.

## 5. Logical View

### 5.1 Overview

The system is decomposed into three main layers:
- **Presentation Layer**: React-based web frontend
- **API Layer**: Rust-based Lambda functions
- **Data Layer**: DynamoDB for persistence, Bedrock for AI services

### 5.2 Architecturally Significant Design Packages

#### Frontend (`/frontend`)
- **Components**: Reusable UI components
- **Pages**: Route-specific page components
- **Services**: API communication and local storage management
- **Styles**: Retro terminal aesthetics with mobile responsiveness

#### Backend (`/backend`)
- **jb_api**: Main API handlers for game logic and user interactions
- **jb_authorizer**: JWT token validation for API Gateway
- **jb_common**: Shared utilities and configuration

#### Infrastructure (`/terraform`)
- **API Gateway**: REST API routing
- **Lambda Functions**: Serverless compute for business logic
- **DynamoDB**: Level definition data
- **Cognito**: Moderator authentication and authorization

### 5.3 Use-Case Realizations

#### AI Chat Flow
1. User submits prompt through React frontend
2. API Gateway routes request to Lambda function
3. Lambda enriches prompt with game context and security instructions
4. Bedrock processes prompt through selected LLM
5. Response returned to user

## 6. Process View

The system operates through lightweight, stateless processes:

### Frontend Processes
- **Main UI Thread**: Handles user interactions and DOM updates
- **Audio Manager**: Background music and sound effects
- **API Client**: Asynchronous HTTP requests to backend

### Backend Processes
- **API Lambda**: Concurrent request handling
- **Authorizer Lambda**: Token validation
- **Bedrock Integration**: AI model invocation

Communication occurs through:
- **HTTP REST**: Frontend to API Gateway
- **AWS SDK**: Lambda to AWS services
- **WebSocket**: Potential future real-time bedrock response streaming

## 7. Deployment View
[![Architecture diagram](../assets/architecture-diagram.svg)](../assets/architecture-diagram.svg)

## 8. Implementation View

### 8.1 Overview

The implementation follows a modular, microservices-inspired architecture:
- **Frontend Layer**: Single-page application with component-based architecture
- **API Layer**: Function-as-a-Service with Axum handler function structure
- **Infrastructure Layer**: Infrastructure-as-Code using Terraform

### 8.2 Layers

#### Presentation Layer
- React components with hooks for state management
- Vite for build tooling and development server
- NES.css for consistent retro styling

#### Business Logic Layer
- Rust Lambda functions for high-performance, memory-safe execution
- Axum framework for HTTP handling
- Tokio for asynchronous runtime
[![Class diagram](../assets/backend-class-diagram.svg)](../assets/backend-class-diagram.svg)

#### Data Access Layer
- DynamoDB for NoSQL operations
- Cognito for user management

## 9. Data View
[![Database tables](../assets/database-tables.svg)](../assets/database-tables.svg)

## 10. Size and Performance

### Dimensioning Characteristics
- **Concurrent Users**: 0-1000 simultaneous players
- **Request Volume**: 0-100 requests/second during peak usage
- **Data Storage**: <1GB for level data
- **AI Model Calls**: 10000-100000 daily invocations

### Performance Targets
- **Page Load**: <3 seconds initial load
- **API Response**: <2 seconds for AI interactions, <100 ms for other requests
- **Availability**: 99.99% uptime
- **Scalability**: Zero-cost scaling during low usage

## 11. Quality

### Security
- JWT-based authentication with short-lived tokens
- Input validation and sanitization for all user inputs
- HTTPS encryption for all communications

### Reliability
- Serverless architecture eliminates single points of failure
- Comprehensive error handling and logging
- Type-safe Rust backend reduces runtime errors

### Maintainability
- Standardized backend handler function structure
- Component-based React frontend enables code reuse
- Infrastructure-as-Code ensures reproducible deployments

### Extensibility
- Architecture supports new game levels and features
- Configurable AI model selection and parameters
