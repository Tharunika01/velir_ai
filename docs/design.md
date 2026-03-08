Design Specification: Velir AI
Bridging the Agricultural "Protection Gap" with Agentic Intelligence

1. System Overview
Velir AI is a "Digital Krishi Officer" designed to automate climate risk protection for smallholder farmers. Unlike passive weather apps, it is an Agentic System that observes data, reasons about risk, and executes financial actions (insurance claims) autonomously.

1.1 Design Philosophy
Voice-First: The primary interface is speech, catering to low-literacy users.

Proactive: The system initiates contact (alerts) rather than waiting for user queries.

Action-Oriented: The goal is not just information retrieval, but transaction execution (API calls).

2. High-Level Architecture
The system follows a Serverless, Event-Driven Architecture built on AWS.

graph TD
    User((Farmer)) <-->|Voice/Image| App[Mobile App (Flutter)]
    App <-->|API/WebSocket| Gateway[Amazon API Gateway]
    
    subgraph "Perception Layer"
        Gateway --> Transcribe[Amazon Transcribe\n(STT)]
        Gateway --> Rekognition[Amazon Nova Pro\n(Vision)]
        Transcribe --> Text[Text Input]
    end
    
    subgraph "The Brain (Orchestration)"
        Text --> AgentCore[Amazon Bedrock AgentCore]
        AgentCore -->|Reasoning| Nova[Amazon Nova Sonic/Pro]
        AgentCore <-->|RAG| KB[Knowledge Base\n(Policy Docs)]
        AgentCore <-->|Context| Memory[Session Memory]
    end
    
    subgraph "Action Layer (Tools)"
        AgentCore -->|Invoke| Lambda[AWS Lambda Tools]
        Lambda -->|API| AgriStack[AgriStack Identity]
        Lambda -->|API| Weather[Weather APIs]
        Lambda -->|API| PMFBY[Insurance Portal]
        Lambda -->|API| Mandi[Market Prices]
    end
    
    subgraph "Output Layer"
        AgentCore -->|Response| Polly[Amazon Polly\n(TTS)]
        Polly -->|Audio| App
    end
3. Component Design
3.1 Front-End ("Vani" Interface)
Framework: Flutter (for cross-platform native performance).

Core Modules:

Voice Recorder: Captures audio chunks, compresses using Opus codec for low bandwidth (2G/3G), and streams to backend.

Vision Viewfinder: Camera interface with overlay markers for leaf scanning.

Status Dashboard: Minimalist UI showing the "Shield Ring" (Green = Protected, Red = Risk).

3.2 The Orchestrator (Amazon Bedrock AgentCore)
This is the central logic unit. It does not just "chat"; it manages state and executes multi-step workflows.

Agent Identity: "Digital Krishi Officer."

Instruction Set: "You are an expert agronomist and insurance officer. Your goal is to protect the farmer's livelihood. Always verify policy eligibility before promising payouts."

Action Groups:

CheckEligibility: Verifies user ID against AgriStack.

AssessRisk: Analyzes weather data vs. crop stage.

FileClaim: Submits JSON payload to PMFBY API.

3.3 The "Shield-Trigger" Background Service
An autonomous loop running on AWS EventBridge Scheduler:

Trigger: Runs every 6 hours.

Check: Queries IoT/Satellite weather data for enrolled districts.

Logic: IF Rainfall > 40mm AND Crop_Stage == "Sowing" THEN Risk = High.

Action: Triggers AgentCore to initiate "Prevented Sowing" claim for affected User IDs.

4. Data Architecture
4.1 Knowledge Base (RAG)
Source Data: PMFBY (Pradhan Mantri Fasal Bima Yojana) policy documents (PDFs), Agronomy Handbooks.

Storage: Amazon OpenSearch Serverless (Vector Store).

Usage: Used by the Agent to answer questions like "Is my tomato crop covered for hailstorm?" with citations.

4.2 Transactional Data (DynamoDB)
Table: Users (Profile, AgriStack ID, Geo-coordinates).

Table: Policies (Active coverage details).

Table: Claims (Status logs of automated claims).

5. User Interface (UI) Strategy
View A: The "Single Button" Home
Visual: 80% of the screen is a pulsing Green Microphone button.

Interaction: Tap-to-Speak. No wake word required (simplifies UX).

Feedback: Haptic vibration when listening; Audio chime when processing.

View B: Velir-Vision Overlay
Visual: Live camera feed.

AR Elements: Bounding boxes drawn around detected pests (e.g., "Stem Borer").

Result Card: Slides up from bottom showing: "Disease Detected: 85% Confidence" + "Recommended Spray: Neem Oil".

6. Security & Guardrails
6.1 Amazon Bedrock Guardrails
Financial Guardrail: Blocks the AI from hallucinating fake payout amounts (e.g., "You will get ₹1 Lakh"). It forces the AI to say "Estimated payout subject to verification."

Agri-Safety Guardrail: Filters out banned or dangerous chemical recommendations.

6.2 Data Privacy
PII Redaction: All Aadhaar numbers and Phone numbers are masked in logs using Bedrock's PII filter.

Encryption: Data encrypted at rest (AES-256) in DynamoDB and S3.

7. Scalability & Economics
7.1 Serverless Model
Compute: AWS Lambda scales to zero. Costs are incurred only per-request.

Concurrency: API Gateway configured to handle burst traffic during monsoon alerts (e.g., 10k requests/second).

7.2 Low-Bandwidth Optimization
Edge Caching: Static assets (icons, policy PDFs) cached via CloudFront.

Audio Compression: Voice notes sent as 16kbps mono streams to support rural network speeds.

Document Control

Version: 1.0

Status: Draft for Hackathon Implementation

Author: Pooja Ramachandran