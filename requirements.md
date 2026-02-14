Project Requirements: Velir AI
Bridging the Agricultural "Protection Gap" with Agentic Intelligence

1. Project Overview
Team Name: Velir AI

Team Leader: Tharunika K

Vision: To build a "Digital Krishi Officer" that moves beyond passive weather information to proactive financial protection and agronomic action for Indian smallholder farmers.

2. Problem Statement
The "Protection Gap"

Scale: Over 120 million Indian smallholder farmers face annual losses exceeding $10B due to climate shocks.

Limitations of Current Solutions:

Weather Apps: Act as "Vitamins" (informational only). They require high literacy to interpret data and do not trigger financial safety nets.

Traditional Insurance: Bogged down by manual field inspections, paperwork, and payout delays of 6-12 months.

Literacy Barrier: Complex text-based interfaces exclude the most vulnerable users.

3. Solution Concept
The Shift: Reactive Information → Proactive Action A voice-driven autonomous agent powered by Amazon Bedrock AgentCore that acts as a 24/7 climate-insurance officer.

Core Logic: Agentic Reasoning
The system follows an Observation-Reasoning-Action loop:

Observation: "Forecast predicts 40mm rainfall in 24 hours."

Reasoning: "High risk of pesticide runoff; soil moisture levels are already at 75%."

Action:

Voice Alert: "Do not spray pesticide today."

Auto-Task: "Drafting a 'Prevented Sowing' claim in the PMFBY portal based on this anomaly."

4. Key Differentiators & USP
Feature

Traditional Apps

Velir AI

Primary Function

Data Display (Information)

API Execution (Action)

Insurance Model

Indemnity (Manual Surveys)

Parametric (Data-Triggered)

Interface

Text/Menus

Voice-to-Voice (Dialect)

Tech Enabler

Basic APIs

Amazon Nova Sonic + AgentCore

5. Functional Requirements (Core Features)
5.1 "Vani" Voice Agent
Description: A conversational interface supporting high-fidelity speech-to-speech interaction.

Requirement: Must support 12+ Indic dialects (Bhojpuri, Marathi, Malayalam, etc.) with latency under 2 seconds.

Tech: Amazon Nova Sonic.

5.2 Shield-Trigger (The Action Agent)
Description: An autonomous background agent that monitors hyper-local weather sensors.

Requirement: Automatically trigger insurance claim drafts when weather parameters (rainfall, temp) cross defined policy thresholds.

5.3 Kisan-Vision
Description: Multimodal diagnostics tool.

Requirement: Users upload a photo of a leaf; the agent must identify pests/disease and prescribe immediate biological or chemical remedies.

Tech: Amazon Nova Pro (Vision).

5.4 Smart-Market Bridge
Description: Market intelligence agent.

Requirement: correlate harvest timing with real-time price surges in local Mandis to suggest the optimal "Harvest-Now" window.

6. Process Flow (Happy Path)
Input: Farmer sends voice note: "Rain is coming, what about my insurance?"

Intent Recognition: Amazon Bedrock AgentCore identifies intent (Query: Insurance Status + Context: Weather Risk).

Orchestration:

Agent retrieves location-specific climate data (Weather API).

Agent queries Knowledge Base for policy eligibility.

Resolution: Agent responds via voice: "I've checked your policy; you are covered. I've initiated the claim draft. Don't worry about the rain."

7. User Experience Strategy
Philosophy: Minimalist "Single-Button" Design.

UI Modules
Dashboard: Large central microphone button for "Voice-First" interaction. No complex nav bars.

Status Ring: A visual green ring indicating "Shield Active" (Insurance protection status).

Vision Mode: Camera viewfinder with real-time overlay highlighting infected leaf areas.

8. Technical Architecture
8.1 Front-End
Mobile Application (Flutter/React Native).

Audio Processing: Amazon Transcribe (STT) and Polly (TTS).

Image Processing: Amazon Rekognition / Nova Pro.

8.2 The Brain (Backend)
Orchestrator: Amazon Bedrock AgentCore.

Reasoning Model: Amazon Nova Pro (Multimodal).

Memory: AgentCore Memory Retention (stores crop cycle history & farmer preferences).

8.3 Integrations (Lambda)
Identity: AgriStack / Aadhaar API.

Climate Data: OpenWeatherMap / IMD API.

Insurance Portal: PMFBY Mock API.

9. Technology Stack (AWS)
Foundation Models: Amazon Nova Pro (Vision/Reasoning), Amazon Nova Sonic (Audio).

Orchestration: Amazon Bedrock AgentCore.

Knowledge: Knowledge Bases for Bedrock (RAG on agricultural datasets).

Observability: Amazon CloudWatch (Latency & Accuracy tracking).

Compute: AWS Lambda (Serverless).

10. Economics & Scalability
Architecture: 100% Serverless (Pay-per-use).

Cost Estimate: ~₹0.80 per comprehensive interaction.

Connectivity: Optimized for 2G/3G networks using compressed audio streams.

11. Safety & Guardrails
Amazon Bedrock Guardrails:

Financial Safety: Prevent the AI from promising payouts not covered by policy.

Medical Safety: Ensure pest remedies are safe for human handling.

PII Protection: Redact Aadhaar/Phone numbers from logs.