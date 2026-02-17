# TerraOS – Multi-Agent Soil Intelligence Platform

## Design Document

---

## Table of Contents

- Executive Summary
- Problem Statement
- What Makes TerraOS Unique
- User Impact & Success Metrics
- Alignment with National Priorities
- 1. System Overview
- 2. Design Principles
- 3. High-Level Architecture
- 4. User Journey
- 5. Multi-Agent Design
- 6. Orchestration Design
- 7. Data Flow
- 8. Data Storage Design
- 9. Security & Privacy Design
- 10. Scalability & Performance
- 11. Failure Scenarios & Resilience
- 12. Observability & Monitoring
- 13. Cost Optimization
- 14. Non-Goals & Explicit Exclusions
- 15. Future Extensibility
- Appendix: Technology Stack Summary
- Appendix: Key Design Decisions

---

## Executive Summary

TerraOS helps Indian farmers understand their soil health and improve it using AI, without expensive sensors or satellite imagery. A farmer enters basic soil test results (NPK values, pH) into a mobile app, and within 60 seconds receives personalized recommendations in simple language—what to plant, how to improve soil naturally using regenerative practices, and suggestions on how to earn income from carbon credits. 

The platform uses five specialized AI agents that work together to analyze soil data, identify patterns, and generate actionable advice. Each recommendation comes with clear explanations so farmers understand why it matters. Built entirely on AWS serverless technology, TerraOS will be  affordable to scale to millions of smallholder farmers across India.

Unlike existing solutions that require expensive IoT sensors or satellite data, TerraOS works with the soil test reports farmers already have access to through government labs and Krishi Vigyan Kendras or other labs.

---

## Problem Statement

### Current State
India has 146 million farmers, most of whom are smallholders with less than 2 hectares of land. Government soil testing labs and Krishi Vigyan Kendras provide free or low-cost soil testing, generating millions of soil test reports annually. However, these reports contain raw data (NPK values, pH levels) that farmers struggle to interpret and act upon.

### The Challenge
- **Low Comprehension**: Farmers receive soil test reports but don't understand what the numbers mean for their specific crops
- **Generic Advice**: Recommendations are often generic and not tailored to local conditions, crop types, or farmer resources
- **Chemical Dependency**: Most advice focuses on chemical fertilizers, perpetuating soil degradation and high input costs
- **No Historical Context**: Farmers can't track soil health trends over time or understand if their interventions are working
- **Missed Opportunities**: Farmers are unaware of regenerative practices or carbon credit income potential

### Impact of Inaction
- Poor crop yields due to nutrient imbalances
- Excessive fertilizer use (30-40% over-application is common), increasing costs
- Progressive soil degradation and loss of organic matter
- Missed income opportunities from carbon sequestration programs
- Environmental damage from chemical runoff

### The Opportunity
With AI, we can transform raw soil data into actionable intelligence that:
- Explains soil health in farmer-friendly language
- Provides crop-specific, location-aware recommendations
- Promotes regenerative practices for long-term soil health
- Estimates carbon sequestration potential and income opportunities
- Tracks soil health trends over time to measure intervention effectiveness

TerraOS bridges the gap between data and action, empowering farmers to make informed decisions that improve yields, reduce costs, and restore soil health.

---

## What Makes TerraOS Unique

### Our Competitive Advantages

**1. Explainable Multi-Agent AI Architecture**
Unlike black-box AI solutions, TerraOS uses five specialized agents that each focus on a specific aspect of soil intelligence. Every recommendation includes a detailed reasoning chain explaining why it was made, which data was used, and what impact is expected. This transparency builds farmer trust and enables learning.

**2. No Dependency on Expensive Infrastructure**
- **No Satellite Imagery**: Most agri-tech solutions require satellite data (Sentinel, Landsat) which adds cost, complexity, and fails during monsoon cloud cover
- **No IoT Sensors**: We don't require farmers to purchase soil sensors (₹5,000-50,000 per device) that need maintenance and connectivity
- **Works with Existing Data**: TerraOS uses soil test reports farmers already have access to through labs

**3. Regenerative Agriculture Focus**
Rather than perpetuating chemical dependency, TerraOS prioritizes regenerative practices:
- Cover cropping and green manures
- Composting and organic amendments
- Crop rotation strategies
- Microbial inoculants
- Minimal tillage practices

This approach improves soil health long-term while reducing input costs.

**4. Carbon Sequestration Integration**
TerraOS is the first soil intelligence platform to estimate carbon sequestration potential and assess eligibility for carbon credit programs. This creates a new income stream for farmers (₹500-2,000 per acre annually) while contributing to climate goals.

**5. Affordable at Scale**
- Cost per report will be economical 
- Serverless architecture scales automatically from 1 to 100,000+ concurrent users
- No infrastructure management overhead
- Pay-per-use model aligned with rural affordability

**6. Graceful Degradation & Partial Intelligence**
If one AI agent is down, the system still delivers results from successful agents. Farmers always get some value, even if the full analysis is temporarily unavailable.But if first agent is down then try again option will be there or we show a message please try again later

**7. Rural-First Design**
- Phone-based authentication (no email required)
- Optimized for low-bandwidth environments
- Multi-lingual support (Hindi in prototype, 6+ languages in production)
- Voice interface roadmap for low-literacy users

**8. Data Ownership & Privacy**
Farmers own their soil data. Explicit consent required for any data sharing. Right to delete all data at any time. All data stored in Indian regions with no cross-border transfers.

---

## User Impact & Success Metrics

### Target Outcomes (In First 6 Months)

**Expected Farmer Reach**
- 10,000 farmers onboarded
- 50,000 soil reports generated
- 500 villages across 5 states (Maharashtra, Punjab, Karnataka, Uttar Pradesh, Tamil Nadu)

**Expected Agricultural Impact**
- 15-20% average crop yield improvement through optimized nutrient management
- 30% reduction in chemical fertilizer costs through regenerative practices
- 25% improvement in soil organic matter over 2 years
- 2-5 tons CO2 per hectare per year sequestration potential

**Expected Economic Impact**
- ₹15,000-25,000 additional annual income per farmer (yield improvement + cost reduction)
- ₹500-2,000 per acre annual income from carbon credits (for eligible farmers)
- 40% reduction in time spent seeking agronomic advice

**Expected Environmental Impact**
- 50,000 hectares under regenerative management
- 100,000-250,000 tons CO2 sequestered annually
- 30% reduction in chemical runoff and groundwater contamination

**Expected User Engagement**
- 80% report completion rate (farmers who start, finish the process)
- 70% return rate (farmers who generate multiple reports over time)
- 4.5+ star average rating on mobile app
- 60% recommendation rate (farmers who refer others)

### Key Performance Indicators (KPIs)

**Technical KPIs**
- Report generation latency: < 60 seconds (95th percentile)
- Agent success rate: > 95%
- System uptime: > 99.5%

**User Experience KPIs**
- Time to first report: < 5 minutes (from signup to report)
- Recommendation comprehension rate: > 80% (farmers understand advice)
- Implementation rate: > 60% (farmers act on recommendations)
- Satisfaction score: > 4.0/5.0

**Business KPIs**
- Customer acquisition cost: < ₹50 per farmer
- Monthly active users: 5,000+ by month 6
- Report generation growth: 20% month-over-month

### Measurement Approach
- In-app surveys after report generation
- Soil test comparison (before/after interventions)
- Farmer testimonials and case studies

---

## Alignment with National Priorities

### India AI Mission
TerraOS directly supports the India AI Mission's goal of democratizing AI for societal benefit:
- **Accessible AI**: Brings advanced AI capabilities to rural farmers who traditionally lack access to technology
- **Domain-Specific Models**: Uses specialized agents for agricultural reasoning, not generic chatbots 
- **Responsible AI**: Explainable recommendations, data privacy, farmer data ownership
- **Scalable Impact**: Serverless architecture can scale to millions of farmers nationwide

### Digital India Initiative
- **Rural Digital Inclusion**: Mobile-first platform designed for low-bandwidth, low-literacy users
- **Government Integration**: Can integrate with existing government soil testing infrastructure (Krishi Vigyan Kendras)
- **Digital Literacy**: Educates farmers on interpreting data and making informed decisions
- **Bridging the Digital Divide**: No expensive hardware required, works with basic smartphones

### Sustainable Agriculture & Climate Goals
- **Regenerative Practices**: Promotes soil health restoration and organic matter improvement
- **Carbon Sequestration**: Contributes to India's net-zero 2070 commitment through agricultural carbon capture
- **Reduced Chemical Use**: Decreases dependency on synthetic fertilizers, reducing emissions and pollution
- **Water Conservation**: Recommendations include practices that improve water retention

### Doubling Farmer Income
- **Yield Improvement**: 15-20% yield increase through optimized nutrient management
- **Cost Reduction**: 30% savings on fertilizer costs through regenerative practices
- **New Income Streams**: Carbon credit eligibility (₹500-2,000 per acre annually)
- **Risk Reduction**: Better soil health reduces crop failure risk

### Atmanirbhar Bharat (Self-Reliant India)
- **Reduced Import Dependency**: Less reliance on imported chemical fertilizers
- **Indian Innovation**: Built by Indian developers for Indian farmers using Indian data
- **Data Sovereignty**: All data stored in India, no foreign data transfers

---

## 1. System Overview

### Purpose of TerraOS

TerraOS is a serverless, AWS-native multi-agent AI platform designed to transform basic soil test data into actionable soil intelligence for smallholder farmers in India. The platform processes farmer-provided inputs—NPK values, pH levels, crop type,Location, historical soil reports, and contextual information—to generate comprehensive recommendations for soil health improvement, regenerative practices, and carbon sequestration strategy suggestions.

### High-Level Design Philosophy

TerraOS is built on three core pillars:

1. **Intelligence from Data, Not Sensors**: All insights are derived from farmer-provided data, historical soil reports, and public agronomic research. No satellite imagery, remote sensing, or IoT sensors are used.
2. **Explainable AI**: Every recommendation includes detailed reasoning chains to build farmer trust and transparency.
3. **Rural-First Design**: Optimized for low-bandwidth environments, cost-efficient operation at scale.

### Multi-Lingual & Voice-First Accessibility

**Prototype Phase**:
- **English**: Full support (UI + AI responses)
- **Hindi**: UI strings translated, AI responses in English with Hindi glossary for technical terms
- **Text-to-Speech**: Basic TTS for reading recommendations aloud (Android native TTS)

**Production Phase 1 (Months 1-3)**:
- **Hindi**: Full AI response generation in Hindi
- **Regional Languages**: UI support for Tamil, Telugu, Kannada, Marathi, Bengali, Gujarati
- **Improved TTS**: Natural-sounding voice synthesis for all supported languages

**Production Phase 2 (Months 4-6)**:
- **Voice Input**: Farmers can speak soil test values instead of typing
- **Voice Navigation**: Complete voice-driven app navigation for low-literacy users
- **Conversational Interface**: Ask follow-up questions about recommendations
- **Regional Language AI**: Full AI response generation in 6+ Indian languages

**Accessibility Features**:
- Large, high-contrast UI elements for outdoor visibility
- Icon-based navigation for low-literacy users
- Audio explanations for all recommendations

**Language Selection Flow**:
1. On first launch, app detects phone language
2. Offers language selection: English, हिंदी (Hindi), தமிழ் (Tamil), తెలుగు (Telugu), etc.
3. Farmer selects preferred language
4. All UI, notifications, and reports rendered in selected language
5. Can switch language anytime in settings

**Technical Implementation**:
- UI strings: JSON localization files
- AI responses: Language-specific prompts to Bedrock models
- Voice: Amazon Polly for TTS, Amazon Transcribe for voice input (Phase 2)

This multi-lingual, voice-first approach ensures TerraOS is accessible to farmers across India's linguistic diversity, including those with limited literacy.

### Why Multi-Agent Architecture

A single monolithic AI model cannot effectively handle the diverse reasoning required for soil intelligence:

- **Domain Specialization**: Each agent focuses on a specific aspect (nutrient interpretation, ecosystem reasoning, historical patterns, regenerative strategies, carbon sequestration).
- **Explainability**: Modular agents produce traceable reasoning chains for each recommendation.
- **Failure Isolation**: If one agent fails, others can still provide partial intelligence with can be based on historical data.
- **Iterative Improvement**: Individual agents can be updated or replaced without system-wide changes.

---

## 2. Design Principles

### Serverless-First


All compute, orchestration, and storage components are serverless. No EC2 instances, no Kubernetes clusters. This ensures:
- Zero infrastructure management overhead
- Automatic scaling from 1 to 100,000+ concurrent users
- Pay-per-use cost model aligned with rural affordability

### Cost Efficiency for Rural Scale

Target cost: ₹30(approx) per soil report. Can be achieved through:
- Bedrock on-demand pricing (no model hosting costs)
- Lambda memory tuning (128-512 MB per function)
- Step Functions Express workflows (high-throughput, low-cost)
- DynamoDB on-demand billing
- S3 Intelligent-Tiering for historical data

### Explainability and Trust

Every AI-generated recommendation includes:
- Reasoning chain (why this recommendation was made)
- Data sources used (which historical reports, which research papers)
- Transparent explanation of the analysis process

### Failure Tolerance and Graceful Degradation

- If an agent fails, the system delivers partial results from successful agents
- If network fails during submission, retry option will be there.

### No Satellite or Remote Sensing Dependency

**Explicit Design Constraint**: TerraOS does NOT use:
- Satellite imagery (Sentinel, Landsat, MODIS)
- NDVI or vegetation indices
- Remote sensing data of any kind
- Real-time IoT soil sensors

All intelligence is derived from farmer-provided data and historical soil reports and the AI intelligence.

---

## 3. High-Level Architecture



### Architecture Diagram

The system architecture consists of the following layers:
- **Mobile App**: Flutter (Prototype: Android only, online-only | Production: iOS + Android,)
- Amazon API Gateway (REST) with AWS WAF for rate limiting
- Lambda functions for input validation and processing
- AWS Step Functions (Express) for multi-agent orchestration
- Five specialized agents (Nutrient Interpreter, Ecosystem Reasoning, Historical Pattern Analyzer, Regenerative Strategy Advisor, Carbon Sequestration Estimator)
- Amazon Bedrock for AI/ML capabilities
- Data layer with DynamoDB and S3
- Amazon Cognito for authentication

### Component Interaction Flow

1. **Mobile App** submits soil data via API Gateway
2. **Input Validator Lambda** validates schema, normalizes units, stores raw input in DynamoDB
3. **Step Functions** orchestrates multi-agent workflow
4. **Each Agent Lambda** invokes Bedrock with domain-specific prompts
5. **Bedrock** returns structured JSON responses with reasoning
6. **Step Functions** aggregates results from all agents
7. **Output Generator Lambda** formats final report, stores in DynamoDB and S3
8. **API Gateway** returns report ID to mobile app
9. **Mobile App** polls for completion or receives webhook notification

### Entry Points

- **Primary (Prototype)**: Mobile app (Flutter, Android) via REST API
- **Primary (Production)**: Mobile app (Flutter, Android + iOS) via REST API
- **Phase 2**: Web dashboards for historical conditions

### Visual Architecture Diagrams

#### System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         FARMER (Mobile App)                     │
│                    English + Hindi Interface                    │
└────────────────────────────┬────────────────────────────────────┘
                             │ HTTPS/TLS 1.3
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Amazon API Gateway (REST)                    │
│                    + AWS WAF (Rate Limiting)                    │
│                    + Cognito Authorizer                         │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│              Lambda: Input Validator & Normalizer               │
│              (Schema validation, unit conversion using scripts) │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│           AWS Step Functions (Express Workflow)                 │
│                  Multi-Agent Orchestration                      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  PARALLEL EXECUTION                                      │   │
│  │  ┌─────────────────────┐  ┌─────────────────────┐        │   │
│  │  │ Agent 1: Nutrient   │  │ Agent 2: Ecosystem  │        │   │
│  │  │ Interpreter         │  │ Reasoning           │        │   │
│  │  └──────────┬──────────┘  └──────────┬──────────┘        │   │
│  └─────────────┼──────────────────────────┼─────────────────┘   │
│                └──────────────┬───────────┘                     │
│                               ▼                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  SEQUENTIAL EXECUTION                                    │   │
│  │  ┌─────────────────────────────────────────────┐         │   │
│  │  │ Agent 3: Historical Pattern Analyzer        │         │   │
│  │  └──────────────────┬──────────────────────────┘         │   │
│  │                     ▼                                    │   │
│  │  ┌─────────────────────────────────────────────┐         │   │
│  │  │ Agent 4: Regenerative Strategy Advisor      │         │   │
│  │  └──────────────────┬──────────────────────────┘         │   │
│  │                     ▼                                    │   │
│  │  ┌─────────────────────────────────────────────┐         │   │
│  │  │ Agent 5: Carbon Sequestration Estimator     │         │   │
│  │  └──────────────────┬──────────────────────────┘         │   │
│  └─────────────────────┼────────────────────────────────────┘   │
└────────────────────────┼────────────────────────────────────────┘
                         ▼
        ┌────────────────────────────────┐
        │    Amazon Bedrock (Claude)     │
        │  AI Model Inference Service    │
        └────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────────┐
│              Lambda: Output Generator & Aggregator              │
│         (Combine results, format report, compute confidence)    │
│          By writing logics and triggered using Lambda           │
└────────────────────────────┬────────────────────────────────────┘
                             │
                ┌────────────┴────────────┐
                ▼                         ▼
    ┌───────────────────┐     ┌───────────────────┐
    │  Amazon DynamoDB  │     │   Amazon S3       │
    │  (Metadata, Fast  │     │  (Full Reports,   │
    │   Retrieval)      │     │   Archival)       │
    └───────────────────┘     └───────────────────┘
                │
                ▼
    ┌───────────────────────────────────┐
    │  CloudWatch + X-Ray               │
    │  (Monitoring, Logging, Tracing)   │
    └───────────────────────────────────┘
```

#### Multi-Agent Workflow Diagram

```
START
  │
  ▼
[Input Validation]
  │
  ├─────────────────────┐
  │                     │
  ▼                     ▼
[Agent 1]           [Agent 2]
Nutrient            Ecosystem
Interpreter         Reasoning
  │                     │
  └─────────┬───────────┘
            ▼
      [Agent 3]
      Historical
      Pattern
      Analyzer
            │
            ▼
      [Agent 4]
      Regenerative
      Strategy
      Advisor
            │
            ▼
      [Agent 5]
      Carbon
      Sequestration
      Estimator
            │
            ▼
    [Aggregate Results]
            │
            ▼
    [Generate Report]
            │
            ▼
         [END]
```


***OR**

## Parallel Execution: Agent 2 & Agent 3

```
START
  │
  ▼
[Input Validation]
  │
  ▼
[Agent 1]
Nutrient
Interpreter
  │
  ├─────────────────────┐
  │                     │
  ▼                     ▼
[Agent 2]           [Agent 3]
Ecosystem           Historical
Reasoning           Pattern
                    Analyzer
  │                     │
  └─────────┬───────────┘
            ▼
      [Agent 4]
      Regenerative
      Strategy
      Advisor
            │
            ▼
      [Agent 5]
      Carbon
      Sequestration
      Estimator
            │
            ▼
    [Aggregate Results]
            │
            ▼
    [Generate Report]
            │
            ▼
         [END]
```



### Prototype vs Production Comparison

| Aspect | Prototype  | Production (6-8 Months) |
|--------|---------------------|--------------------------|
| **AI Models** | Claude  | Mixed: Haiku + Sonnet (optimized) |
| **Response Time** | < 60 seconds (95th percentile) | < 30 seconds (95th percentile) |
| **Input Method** | Manual entry  | Manual + OCR (Textract) |
| **Mobile Platform** | Android only, online-only | Android + iOS, offline-first |
| **Languages** | English + Hindi (UI only) | Multi-lingual (6+ languages, full AI) |
| **Voice Support** | Text-to-Speech only | Voice input + TTS + navigation |
| **Batch Processing** | No (single reports only) | Yes (Phase 2) |
| **Implementation Support** | Basic recommendations |  directory, guides, community |
| **Regions** | Single region only | Multi-region (Mumbai + Hyderabad) |

---

## 4. User Journey

### Farmer's Experience (Step-by-Step)

**Step 1: Onboarding (2 minutes)**
1. Farmer downloads TerraOS mobile app from Google Play Store
2. Signs up using phone number (receives OTP for verification)
3. Selects preferred language (English or Hindi in prototype)
4. Creates farm profile: farm name, location (state/district), farm size

**Step 2: Soil Data Entry (3 minutes)**
1. Farmer navigates to "New Soil Report" screen
2. Enters soil test values from government lab report:
   - Nitrogen (N): 180 kg/ha
   - Phosphorus (P): 12 kg/ha
   - Potassium (K): 240 kg/ha
   - pH: 6.8
3. Selects current crop type (e.g., Rice)
4. Optionally adds:
   - Last fertilizer application date
   - Crop rotation history
5. Taps "Generate Report" button

**Step 3: Processing (30-60 seconds)**
1. App shows progress indicator with friendly messages:
   - "Analyzing your soil nutrients..."
   - "Understanding your farm ecosystem..."
   - "Comparing with historical patterns..."
   - "Generating personalized recommendations..."
2. Farmer sees which agents are working (visual progress)

**Step 4: Report Review (10-15 minutes)**
1. App displays comprehensive soil intelligence report with sections:
   - **Soil Health Summary**: Overall status with color-coded indicators (Red/Yellow/Green)
   - **What This Means**: Simple explanation of soil condition in farmer's language
   - **Key Issues**: Top 3 problems identified (e.g., "Low phosphorus affecting root growth")
   - **Priority Actions**: Top 5 recommendations ranked by impact and feasibility
   - **Carbon Income Potential**: Suggestions on carbon credits
   - **Historical Trends**: Comparison with previous reports (if available)
2. Each recommendation includes:
   - Why it's important (reasoning)
   - How to implement (step-by-step)
   - Expected cost and timeline
   - Expected impact on yield

**Step 5: Implementation Support**
1. Farmer saves report
2. Sets reminders for implementation milestones
3. Accesses implementation guides with photos
5. Tracks progress and marks completed actions

**Step 6: Follow-Up (3-6 months later)**
1. Farmer conducts new soil test after implementing recommendations
2. Enters new soil data into app
3. System compares with previous report and shows:
   - Improvements achieved
   - Effectiveness of interventions
   - Adjusted recommendations based on progress

### Visual User Journey Diagram

```
[Farmer] → [Download App] → [Phone OTP Login] → [Create Farm Profile]
    ↓
[Enter Soil Data] → [Select Crop] → [Add Context] → [Submit]
    ↓
[API Gateway] → [Input Validation] → [Step Functions Orchestration]
    ↓
[5 AI Agents Process in Parallel/Sequential]
    ↓
[Report Generation] → [Store in DB/S3] → [Return to App]
    ↓
[Farmer Views Report] → [Understands Issues] → [Gets Recommendations]
    ↓
[Implements Practices] → [Tracks Progress] → [Generates New Report]
    ↓
[Sees Improvement] → [Shares with Others] → [Cycle Repeats]
```

### Example Farmer Scenario

**Rajesh Kumar - Rice Farmer, Uttar Pradesh**

**Background**: Rajesh owns 2 acres and grows rice. His yields have been declining (3.5 tons/acre vs 4.5 tons district average). He received a soil test report from the local Krishi Vigyan Kendra but didn't understand the numbers.

**Using TerraOS**:
1. Rajesh's son downloads the app and helps him enter the soil data
2. Within 60 seconds, they receive a report in Hindi explaining:
   - Nitrogen is adequate, but phosphorus is very low (12 kg/ha vs 25 kg/ha needed)
   - pH is slightly acidic (6.8), which reduces phosphorus availability
   - Soil organic matter is low, affecting water retention
3. Top recommendations:
   - Apply rock phosphate (₹800/acre) instead of DAP fertilizer
   - Add lime (₹400/acre) to raise pH to 7.0
   - Start composting farm waste to build organic matter
   - Plant dhaincha (green manure) after rice harvest
4. Expected impact: 20% yield increase (0.7 tons/acre more = ₹14,000 additional income)
5. Carbon potential: ₹1,200/year from composting and green manure

**Outcome (6 months later)**:
- Rajesh implements all recommendations
- Next soil test shows phosphorus improved to 22 kg/ha, pH at 7.1
- Rice yield increases to 4.2 tons/acre
- Fertilizer costs reduced by ₹2,500
- Total benefit: ₹16,500 in first season
- Rajesh refers 5 neighboring farmers to TerraOS

---

## 5. Multi-Agent Design



### Agent 1: Nutrient Interpreter

**Responsibility**: Translate raw NPK and pH values into human-readable soil health status.

**Inputs**:
- NPK values (kg/ha or ppm)
- pH level
- Crop type
- Farm size
- Region/state

**Outputs**:
- Nutrient status for nitrogen, phosphorus, potassium, and pH (deficient/adequate/excess or acidic/neutral/alkaline)
- Severity scores for each nutrient (0-1 scale)
- Reasoning explanation

---

### Agent 2: Ecosystem Reasoning

**Responsibility**: Analyze soil health in the context of local climate, crop rotation, and agronomic best practices.

**Inputs**:
- Nutrient status (from Agent 1)
- Crop type and rotation history
- Region/state
- Farm size
- Historical soil reports (if available)

**Outputs**:
- Ecosystem insights including soil type inference, water retention capacity, organic matter status, and microbial health indicator
- Crop suitability assessment for current crop
- Alternative crop recommendations
- Reasoning explanation

---

### Agent 3: Historical Pattern Analyzer

**Responsibility**: Identify trends and anomalies by comparing current data with historical soil reports.

**Inputs**:
- Current soil data
- Historical soil reports (last 3-5 years)
- Crop history
- Farmer-reported interventions (fertilizers, amendments)

**Outputs**:
- Trends for nitrogen, phosphorus, potassium, and pH (improving/stable/declining)
- Identified anomalies in soil data
- Intervention effectiveness assessment
- Reasoning explanation
- Data availability indicator (sufficient/limited/insufficient)

---

### Agent 4: Regenerative Strategy Advisor

**Responsibility**: Recommend regenerative agriculture practices tailored to soil health status.

**Inputs**:
- Nutrient status (from Agent 1)
- Ecosystem insights (from Agent 2)
- Historical trends (from Agent 3)
- Farmer resources (manual input: low|medium|high)

**Outputs**:
- List of regenerative practice recommendations with priority levels
- Expected impact for each practice
- Cost estimates
- Implementation steps
- Reasoning explanation

---

### Agent 5: Carbon Sequestration Estimator

**Responsibility**: Estimate carbon sequestration potential based on recommended practices.

**Inputs**:
- Regenerative recommendations (from Agent 4)
- Farm size (if given in profile)
- Current organic matter status
- Crop type

**Outputs**:
- Sequestration potential (annual and 5-year projections)
- Practice contributions to carbon sequestration
- Carbon credit eligibility assessment
- Reasoning explanation

---

## 6. Orchestration Design



### Step Functions Workflow

**Workflow Type**: Express Workflow (synchronous, high-throughput, low-cost)

**Execution Pattern**:

The workflow follows this sequence:
1. Input Validation (Lambda)
2. Parallel Execution: Agent 1 (Nutrient Interpreter) and Agent 2 (Ecosystem Reasoning)
3. Sequential Execution:
   - Agent 3: Historical Pattern Analyzer (depends on Agent 1, 2)
   - Agent 4: Regenerative Strategy Advisor (depends on Agent 1, 2, 3)
   - Agent 5: Carbon Sequestration Estimator (depends on Agent 4)
4. Result Aggregation (Lambda)
5. Output Generation (Lambda)

### Sequential vs Parallel Execution

**Parallel Execution** (Agents 1 & 2):
- No dependencies between agents
- Reduces total execution time by ~40%
- Both agents can fail independently

**Sequential Execution** (Agents 3, 4, 5):
- Agent 3 requires outputs from Agents 1 & 2
- Agent 4 requires outputs from Agents 1, 2, 3
- Agent 5 requires output from Agent 4
- Ensures data consistency and reasoning chain integrity

### Error Handling and Retry Logic

**Per-Agent Error Handling**:

**Retry Policy**:
- Step Functions configured with Retry block
- Max attempts: 3
- Exponential backoff enabled


**Failure Handling Strategy**:
1. **Transient Failures**: Retry up to 3 times with exponential backoff
2. **Permanent Failures**: Mark agent as failed, continue with remaining agents
3. **Critical Failures** (Agent 1 fails): Abort workflow, return error to user
4. **Non-Critical Failures** (Agent 5 fails): Deliver partial results with warning of what is failed to be generated

**Partial Result Delivery**:
- If Agents 1, 2, 3 succeed but Agent 4 fails → Deliver diagnostic report without recommendations
- If Agents 1, 2, 3, 4 succeed but Agent 5 fails → Deliver recommendations without carbon estimate suggestions

### State Persistence Strategy

**DynamoDB State Table (Production)**:

State table structure:
- Primary Key: EXECUTION#{execution_id}
- Sort Key: STATE#{timestamp}
- Attributes: execution_id, user_id, farm_id, status (in_progress/completed/failed), agent_results, created_at, updated_at, ttl (30 days)

**State Updates**:
- After each agent completes, update DynamoDB with partial results
- Enables resume on failure (future enhancement)
- Provides audit trail for debugging

---

## 7. Data Flow



### Input Ingestion

**Manual Entry** (Primary):
- Farmer enters NPK, pH, crop type,location via mobile app
- Data validated client-side (basic range checks)
- Submitted to API Gateway as JSON payload

**OCR-Based Upload** (Phase 1 - Post-Prototype):
- Farmer uploads photo of soil test report
- Lambda invokes Amazon Textract to extract text
- Extracted data validated and normalized
- Farmer reviews and confirms extracted values
- Not included in 4-week prototype

**Input Schema**:

Required fields:
- user_id, farm_id
- soil_data: nitrogen, phosphorus, potassium, pH values with units (kg_per_ha or ppm)
- crop_type (rice, wheat, cotton, etc.)
- farm_size_acres
- region: state and district
- historical_reports: array of report IDs
- farmer_inputs: crop_rotation, last_fertilizer_application, resources (low/medium/high)

### Validation and Normalization

**Input Validator Lambda**:

1. **Schema Validation**:
   - Required fields present
   - Data types correct
   - Enum values valid

2. **Range Validation**:
   - NPK values: 0-1000 kg/ha or 0-500 ppm
   - pH: 3.0-10.0
   - Farm size: 0.1-100 acres

3. **Unit Normalization**:
   - Convert all NPK to kg/ha
   - Standardize crop names (e.g., "paddy" → "rice")
   - Normalize region names

4. **Historical Data Retrieval**:
   - Fetch historical reports from DynamoDB
   - Attach to execution context

**Validation Errors**:
- Return 400 Bad Request with specific error messages
- Log validation failures to CloudWatch

### Context Passing Between Agents

**Step Functions Context Object**:

The context object contains:
- execution_id
- validated input data
- agent_results: status, output, confidence, and execution_time_ms for each agent
- metadata: started_at timestamp and region

**Context Enrichment**:
- Each agent receives full context (input + previous agent results)
- Agents extract only relevant fields for their reasoning
- Agents append their results to context for downstream agents

### Output Generation

**Output Generator Lambda**:

1. **Aggregate Results**: Combine all agent outputs into unified report
2. **Generate Reasoning Chain**: Link agent outputs into coherent narrative
3. **Format for Mobile**: Optimize JSON structure for mobile rendering
4. **Store in DynamoDB and S3**:
   - DynamoDB: Metadata + summary (fast retrieval)
   - S3: Full report JSON (archival)

**Output Schema**:

The output report includes:
- report_id, user_id, farm_id, generated_at timestamp
- soil_health_summary: status, key_issues, priority_actions
- agent_outputs: results from all five agents
- reasoning_chain: narrative explanation

---

## 8. Data Storage Design



### DynamoDB Table Design (Single-Table Strategy)

**Table Name**: `TerraOS-Data`

**Primary Key**:
- Partition Key (PK): `string`
- Sort Key (SK): `string`


**Access Patterns**:

| Access Pattern | PK | SK | GSI |
|----------------|----|----|-----|
| Get user profile | `USER#{user_id}` | `PROFILE` | - |
| Get farm details | `FARM#{farm_id}` | `METADATA` | - |
| Get soil report | `REPORT#{report_id}` | `METADATA` | - |
| List user's farms | `USER#{user_id}` | `FARM#{farm_id}` | - |
| List farm's reports | `FARM#{farm_id}` | `REPORT#{timestamp}` | - |
| Get user's reports | - | - | GSI1: `USER#{user_id}` + `REPORT#{timestamp}` |
| Get execution state | `EXECUTION#{execution_id}` | `STATE#{timestamp}` | - |

**Item Examples**:
PK - Parition Key
SK - Sort Key
User Profile items contain: PK (USER#user_id), SK (PROFILE), user details (name, phone, language), created_at

Farm Metadata items contain: PK (FARM#farm_id), SK (METADATA), farm details (name, size_acres, region), GSI keys for user-based queries

Soil Report items contain: PK (REPORT#report_id), SK (METADATA), report details (user_id, farm_id, generated_at, confidence, summary), S3 key reference, GSI keys for user and farm queries, TTL

**Capacity Mode**: On-Demand (auto-scaling for unpredictable traffic)

**TTL**: 
- Execution states: 30 days
- Reports: No TTL (permanent storage for 5 yrs then auto deletion of old reports)

### S3 Bucket Usage and Lifecycle Policies

**Buckets**:

1. **`terraos-reports-{region}`**:
   - Full soil report JSONs
   - Lifecycle: Transition to S3 Glacier after 5 year
   - Versioning: Enabled
   - Encryption: SSE-S3

2. **`terraos-uploads-{region}`**:
   - OCR-scanned soil test reports (images)
   - Lifecycle: Delete after 90 days
   - Encryption: SSE-S3

3. **`terraos-historical-data-{region}`**:
   - Aggregated historical soil data (CSV exports)
   - Lifecycle: Transition to S3 Glacier Deep Archive after 2 years
   - Encryption: SSE-KMS

**S3 Object Key Structure**:

- Reports: reports/{year}/{month}/report_{report_id}.json
- Uploads: uploads/{user_id}/{upload_id}.jpg
- Historical data: historical/{state}/{district}/{year}.csv

### Data Versioning and Historical Tracking

**Report Versioning**:
- Each report is immutable (no updates)
- New soil tests create new reports
- Historical comparison queries fetch multiple reports by farm_id + timestamp range

**Schema Versioning**:
- All reports include `schema_version` field
- Enables backward-compatible schema evolution
- Lambda functions handle multiple schema versions

**Audit Trail**:
- All API calls logged to CloudWatch Logs
- DynamoDB Streams capture all data changes
- Stream events archived to S3 for compliance
- CloudWatch Logs retention: 5 years
- CloudTrail retention: 5 years
- Archived to S3 Glacier Deep Archive after 1 year

---

## 9. Security & Privacy Design

- All API keys stored in AWS Secrets Manager
- Automatic rotation enabled


### Authentication (Amazon Cognito)

**User Pools**:
- Phone number-based authentication (OTP)
- No email required (rural accessibility)
- MFA mandatory for Admin users
- MFA optional for Farmers (SMS-based)
- Password policy: Minimum 8 characters

**Identity Pools**:
- Federated identities for mobile app
- Temporary AWS credentials for S3 uploads
- Scoped IAM policies per user

**Token Management**:
- Access token: 1 hour expiry
- Refresh token: 30 days expiry
- ID token: Contains user_id, phone, language

### Authorization (RBAC)

**Roles**:

1. **Farmer** (default):
   - Create/read own farms and reports
   - Upload soil test images
   - No access to other users' data

2. **Admin**:
   - Full access to all data
   - User management
   - System configuration

**IAM Policies**:

Farmer role policies allow:
- DynamoDB GetItem and Query operations on TerraOS-Data table
- Scoped to user's own data using Cognito identity in condition
- Resource-level permissions based on USER# prefix

**API Gateway Authorization**:
- All endpoints require Cognito authorizer
- User ID extracted from JWT token
- Lambda functions validate user owns requested resources

**Rate Limiting**:
- API Gateway throttling: 100 requests per minute per user
- WAF rules applied to prevent abuse


### Encryption at Rest and in Transit

**At Rest**:
- DynamoDB: AWS-managed encryption (SSE)
- S3: SSE-S3 for reports, SSE-KMS for sensitive data
- CloudWatch Logs: Encrypted with AWS-managed keys

**In Transit**:
- API Gateway: TLS 1.3 enforced (minimum TLS 1.3)

### Data Ownership and Consent

**Principles**:
- Farmers own their soil data
- Explicit consent required for data sharing
- Right to delete all data (GDPR-style)

**Consent Management**:
- Consent recorded in DynamoDB user profile
- Consent version tracked (for policy updates)
- Withdrawal triggers data deletion workflow

**Data Deletion**:
- User-initiated deletion via mobile app
- 30-day grace period (soft delete)
- Permanent deletion after grace period
- Anonymized aggregates retained for research

**Right to Deletion**:
- Users can request account deletion
- Lambda workflow deletes:
  - DynamoDB records
  - S3 objects
  - Historical execution logs
- Confirmation sent to user

### India-Only Data Residency

**Primary Region**: ap-south-1 (Mumbai)
**Secondary Region**: ap-south-2 (Hyderabad)

Failover Strategy:
- DynamoDB Global Tables enabled
- S3 Cross-Region Replication
- Route53 health checks for automatic failover
- Step Functions deployed in both regions

**Compliance Measures**:
- All data stored in Mumbai region
- No cross-region replication
- Bedrock models invoked in `ap-south-1` only
- CloudWatch Logs in `ap-south-1`

**Data Transfer Restrictions**:
- No data exported outside India without explicit consent
- API Gateway regional endpoint (no global accelerator)
- S3 bucket policies block cross-region access

---

## 10. Scalability & Performance

## Performance Targets

### Prototype Phase
- Total processing time (95th percentile): < 60 seconds
- Agent 1: < 10 sec
- Agents 2 & 3 (parallel): < 15 sec
- Agent 4: < 12 sec
- Agent 5: < 8 sec
- API latency (without agents): < 500 ms

### Production Phase (Post-Hackathon)
- Total processing time (95th percentile): < 30 seconds
- Agent 1: < 5 sec
- Agents 2 & 3 (parallel): < 10 sec
- Agent 4: < 8 sec
- Agent 5: < 5 sec
- API latency (without agents): < 200 ms
- Cached report load time: < 10 sec


### Concurrency Handling

**API Gateway**:
- Default limit: 10,000 requests/second per region
- Burst capacity: 5,000 requests
- Throttling: 429 Too Many Requests with Retry-After header

**Lambda**:
- Reserved concurrency per function: 100 (per agent)
- Total account concurrency: 1,000 (default), can request increase to 10,000+
- Provisioned concurrency: Not used (cost optimization)

**DynamoDB**:
- On-demand capacity mode (auto-scaling)
- Handles 100,000+ requests/second automatically
- No throttling under normal conditions

**Step Functions**:
- Express workflows: 100,000+ executions/second
- No execution history stored (reduces cost)
- Synchronous execution (5-minute timeout)

**Bedrock**:
- On-demand throughput (no provisioned capacity)
- Rate limits: 100 requests/minute per model (default)
- Request increase to 1,000 requests/minute for production

### Parallel Agent Execution

**Agents 1 & 2 in Parallel**:
- Reduces execution time from 3s to 1.5s (50% improvement)
- No shared state between agents
- Independent failure handling

**Concurrency Limits**:
- Each agent Lambda: 100 concurrent executions
- Total system capacity: 100 concurrent soil reports
- Scales to 1,000+ with account limit increase

### Cold Start Mitigation

**Lambda Configuration**:
- Runtime: Python 3.12 (fast cold start)
- Memory: 512 MB (balance between cost and performance)
- Ephemeral storage: 512 MB (default)
- Architecture: arm64 (Graviton2, 20% faster, 20% cheaper)

**Cold Start Optimization**:
- Minimal dependencies (boto3, requests only)
- No heavy ML libraries in Lambda (use Bedrock instead)
- Connection pooling for DynamoDB and Bedrock clients
- Environment variables for configuration (no S3 lookups)

**Expected Cold Start Times**:
- Input Validator: 200-300ms
- Agent Lambdas: 300-500ms
- Output Generator: 200-300ms

**Warm Execution Times**:
- Input Validator: 50-100ms
- Agent Lambdas: 800-1500ms (Bedrock invocation dominates)
- Output Generator: 100-200ms

### Expected Latency Breakdown

**End-to-End Latency** (P50):

| Component | Latency | Notes |
|-----------|---------|-------|
| API Gateway | 50ms | Network + routing |
| Input Validator | 100ms | Validation + DynamoDB write |
| Step Functions Overhead | 100ms | State transitions |
| Agent 1 (parallel) | 1200ms | Bedrock invocation |
| Agent 2 (parallel) | 1500ms | Bedrock invocation |
| Agent 3 | 1300ms | Bedrock invocation |
| Agent 4 | 1400ms | Bedrock invocation |
| Agent 5 | 1100ms | Bedrock invocation |
| Output Generator | 200ms | Aggregation + DynamoDB/S3 write |
| **Total (Sequential)** | **7.0s** | All agents sequential |
| **Total (Optimized)** | **5.8s** | Agents 1 & 2 parallel |

**Prototype Phase**:
- P95 Latency: 50-60 seconds (includes cold starts, unoptimized code)
- Timeout Configuration:
  - Lambda: 30 seconds per function
  - Step Functions: 5 minutes (Express workflow limit)
  - API Gateway: 29 seconds (hard limit)
- Async Pattern: API returns immediately with `execution_id`, mobile app polls for completion

**Production Phase**:
- P95 Latency: 8-10 seconds (optimized)
- Same timeout configuration
- Async pattern with webhook notifications

---

## 11. Failure Scenarios & Resilience



### Agent-Level Failures

**Scenario 1: Agent 1 (Nutrient Interpreter) Fails**

- **Impact**: Critical failure, no downstream agents can execute
- **Response**:
  1. Retry 3 times with exponential backoff
  2. If all retries fail, abort workflow
  3. Return error to user: "Unable to analyze soil data. Please try again."

**Scenario 2: Agent 2 (Ecosystem Reasoning) Fails**

- **Impact**: Moderate failure, Agent 3 can still execute with limited context
- **Response**:
  1. Retry 3 times
  2. If all retries fail, mark Agent 2 as failed
  3. Continue with Agents 3, 4, 5 using only Agent 1 output
  4. Include note in report about limited ecosystem analysis

**Scenario 3: Agent 3 (Historical Pattern) Fails**

- **Impact**: Low failure, recommendations can still be generated
- **Response**:
  1. Retry 3 times
  2. If all retries fail, skip historical analysis
  3. Continue with Agents 4, 5
  4. Mark report as "no historical comparison available"

**Scenario 4: Agent 4 (Regenerative Strategy) Fails**

- **Impact**: High failure, no actionable recommendations
- **Response**:
  1. Retry 3 times
  2. If all retries fail, deliver diagnostic report without recommendations
  3. Notify user that recommendations are temporarily unavailable

**Scenario 5: Agent 5 (Carbon Sequestration) Fails**

- **Impact**: Low failure, optional feature
- **Response**:
  1. Retry 3 times
  2. If all retries fail, omit carbon estimates
  3. Deliver report without carbon section

### Partial Result Delivery

**Delivery Matrix**:

| Agents Succeeded | Delivery | User Notification |
|------------------|----------|-------------------|
| 1, 2, 3, 4, 5 | Full report | Complete analysis available |
| 1, 2, 3, 4 | Report without carbon estimates | Carbon analysis unavailable |
| 1, 2, 3 | Diagnostic report without recommendations | Recommendations unavailable |
| 1, 2 | Basic soil health status | Limited analysis available |
| 1 only | Error, no report | Processing failed |

**User Notification**:
- Full report: "Your soil intelligence report is ready."
- Partial report: "Your report is ready with limited insights due to processing issues."
- Failed report: "We couldn't generate your report. Please try again or contact support."

### Retry Strategy

**Retry Configuration**:

Retry policies:
- Lambda service exceptions: 2s interval, 3 max attempts, 2.0 backoff rate
- Task failures: 1s interval, 2 max attempts, 1.5 backoff rate

**Retry Triggers**:
- Bedrock throttling (429 errors)
- Bedrock service unavailable (503 errors)
- Agent timeout (>25 seconds)
- Invalid AI response (JSON parsing errors)

### User-Facing Error Messaging

**Error Categories**:

1. **Validation Errors** (400):
   - "Invalid NPK values. Please check your soil test report."
   - "Farm size must be between 0.1 and 100 acres.(if provided)"

2. **Authentication Errors** (401):
   - "Your session has expired. Please log in again."

3. **Authorization Errors** (403):
   - "You don't have permission to access this farm."

4. **Processing Errors** (500):
   - "We're having trouble generating your report. Please try again in a few minutes."
   - "Some insights are unavailable due to technical issues. Your report includes available information."

5. **Timeout Errors** (504):
   - "Report generation is taking longer than expected. We'll notify you when it's ready."
   

**Error Logging**:
- All errors logged to CloudWatch with execution_id
- User-facing errors sanitized (no stack traces)
- Support team can trace errors using execution_id

---

## 12. Observability & Monitoring



### CloudWatch Metrics and Logs

**Custom Metrics**:

| Metric | Dimension | Unit | Threshold |
|--------|-----------|------|-----------|
| `ReportGenerationLatency` | Agent | Milliseconds | P95 < 10s |
| `AgentSuccessRate` | Agent | Percent | > 95% |
| `PartialReportRate` | - | Percent | < 10% |
| `BedrockThrottleRate` | Model | Count | < 5/hour |
| `APIErrorRate` | Endpoint | Percent | < 1% |
| `ColdStartRate` | Function | Percent | < 20% |

**Log Groups**:

1. `/aws/lambda/terraos-input-validator`
2. `/aws/lambda/terraos-agent-1-nutrient`
3. `/aws/lambda/terraos-agent-2-ecosystem`
4. `/aws/lambda/terraos-agent-3-historical`
5. `/aws/lambda/terraos-agent-4-regenerative`
6. `/aws/lambda/terraos-agent-5-carbon`
7. `/aws/lambda/terraos-output-generator`
8. `/aws/apigateway/terraos-api`
9. `/aws/stepfunctions/terraos-orchestrator`

**Log Retention**: 30 days (cost optimization)

**Structured Logging**:

Log entries include: timestamp, level, execution_id, user_id, farm_id, agent name, event type, latency_ms, bedrock_model

### Step Functions Execution Tracing

**X-Ray Integration**:
- Enabled for all Lambda functions
- Traces end-to-end execution flow
- Identifies bottlenecks and failures

**Trace Segments**:
- API Gateway → Lambda → Step Functions → Agents → Bedrock
- Visualizes parallel vs sequential execution
- Highlights cold starts and retries

### Alerts for Degraded Intelligence

**CloudWatch Alarms**:

1. **High Agent Failure Rate**:
   - Metric: `AgentSuccessRate < 90%` for 5 minutes
   - Action: SNS notification to engineering team
   - Severity: High

2. **High Partial Report Rate**:
   - Metric: `PartialReportRate > 20%` for 15 minutes
   - Action: SNS notification
   - Severity: Medium

4. **Bedrock Throttling**:
   - Metric: `BedrockThrottleRate > 10` in 5 minutes
   - Action: Auto-scale Bedrock throughput (if provisioned)
   - Severity: High

5. **API Error Rate**:
   - Metric: `APIErrorRate > 5%` for 5 minutes
   - Action: SNS notification + PagerDuty alert
   - Severity: Critical

**Dashboard**:
- Real-time metrics for all agents
- Execution success/failure rates
- Latency percentiles (P50, P95, P99)
- Cost per report (updated hourly)

---

## 13. Cost Optimization



### Bedrock Usage Strategy

**Model Selection**:

**Token Optimization**:
- Prompt engineering: Concise system prompts (<500 tokens)
- Context pruning: Only pass relevant data to each agent
- Output constraints: JSON schema enforcement (reduces verbose responses)
- Caching: Reuse system prompts across invocations (future)


**Optimization Strategy**:
- Use AWS Lambda Power Tuning tool to find optimal memory
- Monitor CPU utilization (target 70-80%)
- Increase memory if CPU-bound, decrease if memory-bound

### Step Functions Express Workflows

**Cost Comparison**:

| Workflow Type |  Use Case |
|---------------|----------|
| Standard | Long-running, audit trail required |
| Express  | High-throughput, short-lived |

**TerraOS Choice**: Express workflows
- 25x cheaper than Standard
- No execution history (reduces storage costs)
- Sufficient for 5-minute timeout


**Cost Optimization Levers**:
1. **Prototype**: Single model (Sonnet) for simplicity
2. **Production Phase 1**: Can use cheaper models (Haiku instead of Sonnet) for Agents 1, 3, 5
3. **Production Phase 1**: Reduce token usage through prompt optimization
4. **Production Phase 1**: Cache frequently used data in Lambda environment
5. **Production Phase 2**: Batch processing for non-urgent reports

---

## 14. Non-Goals & Explicit Exclusions



### No Satellite Imagery or Remote Sensing

**Exclusion**: TerraOS does NOT use satellite imagery, remote sensing data, NDVI indices, or any form of aerial/space-based observation.

**Rationale**:
- Satellite data requires specialized processing infrastructure
- Adds significant cost and complexity
- Cloud cover and resolution issues in monsoon regions
- Farmer-provided data is sufficient for soil intelligence
- Not aligned with core design principle: "Intelligence from Data, Not Sensors"

**Permanent Exclusion**: This is a core design decision, not a future feature. TerraOS will never integrate satellite or remote sensing data.

**Alternatives**:
- Farmer-reported observations (crop health, water retention)
- Historical soil test reports
- Regional agronomic research data

### No Real-Time IoT Soil Sensors

**Exclusion**: TerraOS does NOT integrate with real-time IoT soil sensors (moisture, temperature, EC).

**Rationale**:
- Hardware cost prohibitive for smallholder farmers
- Maintenance and calibration challenges in rural areas
- Connectivity requirements (LoRaWAN, cellular) not feasible
- Platform focuses on periodic soil testing, not continuous monitoring
- Not in scope for prototype or production phases

### No Automated Chemical Input Purchasing

**Exclusion**: TerraOS does NOT facilitate direct purchase of fertilizers, pesticides, or other chemical inputs.

**Rationale**:
- Regulatory complexity (fertilizer licensing, quality control)
- Liability concerns (incorrect application, crop damage)
- Focus on regenerative practices, not chemical dependency
- Avoid conflicts of interest (recommendation vs sales)

**Alternative**: Provide recommendations, farmers purchase from local dealers.

**However, TerraOS DOES Provide Implementation Support**:

1. **Local Vendor Directory** (Phase 2):
   - Curated list of organic input suppliers (compost, bio-fertilizers, rock phosphate)
   - FPO contact information for bulk purchasing
   - Government scheme information (subsidies, free inputs)
   - No direct sales, just information

2. **Step-by-Step Implementation Guides**:
   - Visual guides with photos for each recommended practice
   - Video tutorials in local languages (YouTube integration in future)
   - Seasonal calendars showing when to implement each practice
   - Checklists to track implementation progress

3. **Community Learning** (Phase 2):
   - Farmer-to-farmer forum for sharing experiences
   - Success stories from farmers who implemented recommendations
   - Q&A section moderated by agronomists
   - WhatsApp group integration for peer support

4. **Progress Tracking**:
   - Mark recommendations as "Planned", "In Progress", "Completed"
   - Set reminders for time-sensitive actions (e.g., "Apply compost before monsoon")
   - Photo documentation of implementation
   - Compare before/after soil tests to measure impact

5. **Expert Support** (Phase 2):
   - Connect with local agronomists for complex questions
   - Video consultation booking (₹100-200 per session)
   - Government extension officer directory
   - Emergency helpline for urgent issues

This approach ensures farmers can act on recommendations without TerraOS becoming a marketplace, maintaining focus on education and empowerment.

### No Medical or Health Advice

**Exclusion**: TerraOS does NOT provide medical advice, health recommendations, or nutritional guidance.

**Rationale**:
- Platform is agricultural, not medical
- Liability and regulatory constraints
- Soil health ≠ human health (different domains)

**Boundary**: Carbon sequestration and ecosystem health suggestions are environmental, not medical.

---

## 15. Future Extensibility



### Prototype vs Production Roadmap

#### PROTOTYPE PHASE

**Scope**:
- Manual soil data entry only (no OCR)
- Single report generation (no batch processing)
- Single AI : Claude for all 5 agents
- Basic mobile app (Android only, online-only)
- **Bilingual support: English + Hindi** (UI strings in Hindi, AI responses in English with Hindi glossary)
- Mumbai region (ap-south-1) only

**Features Included**:
- All 5 AI agents (Nutrient, Ecosystem, Historical, Regenerative, Carbon)
- Step Functions orchestration with parallel execution
- DynamoDB storage (single table design for inputs and outputs)
- S3 report storage
- Cognito authentication (phone-based OTP)
- API Gateway REST endpoints
- Basic error handling and retries
- **Hindi UI localization** (buttons, labels, navigation)
- **Text-to-Speech** for reading recommendations aloud

**Features Excluded**:
- OCR-based report upload (Textract)
- Batch processing APIs
- Full multi-language AI responses (only UI translated in prototype)
- Offline-first mobile capabilities
- Voice input
- Multi-region deployment
- Advanced monitoring dashboards
- Community forum

**Success Criteria**:
- Generate complete soil intelligence report with all 5 agent outputs
- End-to-end latency < 60 seconds
- Successfully handle 10 concurrent users
- Hindi UI fully functional
- 80% user comprehension rate (farmers understand recommendations)

---

#### PRODUCTION PHASE (Post-Hackathon - 6-8 Months)

**Phase 1 Enhancements (Months 1-3)**:
- OCR-based soil report upload (Amazon Textract)
- Multi-model optimization (Claude Haiku for Agents 1, 3, 5)
- Response time optimization to < 30 seconds
- iOS app development


**Phase 2 Enhancements (Months 4-6)**:
- Multi-language support (Tamil, Telugu, Kannada, Marathi, Bengali)
- Batch processing API 
- CSV/Excel import for bulk reports
- Advanced monitoring dashboards
- Multi-region deployment (Mumbai + Hyderabad)

**Phase 3 Enhancements (Months 7-8)**:
-  dashboard for aggregated insights feom historical data
- Third-party webhook support
- Carbon credit marketplace integration

---
**Integration Points**:
- Input: Receives full context (input + previous agent results)
- Output: Appends results to context
- Orchestration: Step Functions automatically handles state passing

### Supporting New Crops or Regions (Production)

**Crop Extensibility**:
- Crop-specific thresholds stored in DynamoDB (not hardcoded)
- New crops added via admin API (no code changes)
- Bedrock prompts dynamically include crop-specific context

**Region Extensibility**:
- Regional agronomic data stored in S3 (CSV/JSON)
- Lambda functions load regional data at runtime
- New regions added by uploading data files (no deployment)

**Data Schema**:

Crop and region data includes:
- crop name and region
- nutrient_thresholds: low/adequate/high values for NPK
- ph_range: min and max values
- regenerative_practices: list of recommended practices

**Localization** (Phase 2):
- Multi-language support (Hindi, Tamil, Telugu, Kannada, etc.)
- Translations stored in DynamoDB
- Mobile app selects language, API returns localized content


**Government Soil Testing Labs** (Phase 2):
- Batch upload API for lab-generated reports
- CSV/Excel import with schema validation
- Automatic farmer notification on report availability

**Farmer Producer Organizations (FPOs)** (Phase 3):
- Multi-farm dashboard for FPO managers
- Aggregated insights across member farms
- Bulk report generation for seasonal planning

**Data Sharing**:
- Farmer consent required for data sharing with FPOs/government
- Anonymized aggregates for research (no PII)
- API access with OAuth 2.0 for third-party integrations

**Integration Architecture** (Phase 2):

Government lab integration flow:
1. Government Lab sends HTTPS POST with CSV data
2. API Gateway routes to Lambda function
3. Lambda processes and stores in DynamoDB
4. SNS notification sent to Farmer Mobile App

**Future APIs** (Phase 2-3):
- `POST /api/v1/batch/reports` - Bulk upload
- `GET /api/v1/fpo/{fpo_id}/insights` - Aggregated insights
- `POST /api/v1/integrations/webhook` - Third-party webhooks

---

## Appendix: Technology Stack Summary

### AWS Services Used (Complete List)

**Compute & Orchestration**
- **AWS Lambda**: Serverless compute for all business logic (7 functions)
  - Runtime: Python 3.12 on ARM64 (Graviton2)
  - Memory: 256-512 MB per function
  - Use case: Input validation, agent execution, output generation
- **AWS Step Functions**: Multi-agent workflow orchestration
  - Type: Express Workflows (synchronous, high-throughput)
  - Use case: Coordinate 5 AI agents with parallel and sequential execution

**AI & Machine Learning**
- **Amazon Bedrock**: Managed AI model inference
  - Models: Claude 3.5 Sonnet (prototype), Claude 3 Haiku + Sonnet (production)
  - Use case: All 5 AI agents for soil intelligence reasoning
  - Pricing: Pay-per-token, no model hosting costs

**API & Authentication**
- **Amazon API Gateway**: RESTful API endpoints
  - Type: Regional REST API
  - Features: Cognito authorizer, request validation, throttling
- **Amazon Cognito**: User authentication and authorization
  - User Pools: Phone-based OTP authentication
  - Identity Pools: Temporary AWS credentials for mobile app
  - Use case: Secure farmer authentication without email requirement

**Data Storage**
- **Amazon DynamoDB**: NoSQL database for all application data
  - Design: Single-table design with GSIs
  - Capacity: On-demand (auto-scaling)
  - Use case: User profiles, farm metadata, report metadata, execution state
- **Amazon S3**: Object storage for reports and uploads
  - Buckets: Reports, uploads, historical data
  - Features: Lifecycle policies, versioning, encryption (SSE-S3, SSE-KMS)
  - Use case: Full report JSONs, OCR images (Phase 2), CSV exports

**OCR & Document Processing** (Phase 2)
- **Amazon Textract**: Extract text from soil test report images
  - Use case: Automated data entry from scanned reports

**Voice & Language** (Phase 2)
- **Amazon Polly**: Text-to-speech for reading recommendations
  - Languages: English, Hindi, Tamil, Telugu, Kannada, Marathi, Bengali
- **Amazon Transcribe**: Speech-to-text for voice input
  - Use case: Voice-based soil data entry

**Monitoring & Observability**
- **Amazon CloudWatch**: Logs, metrics, alarms, dashboards
  - Log retention: 30 days
  - Custom metrics: Latency, success rate, cost per report
- **AWS X-Ray**: Distributed tracing for end-to-end request tracking
  - Use case: Identify bottlenecks, visualize agent execution flow

**Security & Compliance**
- **AWS IAM**: Fine-grained access control for all resources
  - Use case: Role-based access control (Farmer, Agronomist, Admin)
- **AWS KMS**: Encryption key management
  - Use case: Encrypt sensitive data in S3
- **AWS WAF**: Web application firewall for API Gateway
  - Use case: Rate limiting, DDoS protection
- **AWS Secrets Manager**: Secure storage for API keys and credentials
  - Use case: Third-party API keys (future integrations)

**Networking & Content Delivery**
- **AWS PrivateLink**: Private connectivity between Lambda and Bedrock
  - Use case: No internet exposure for AI model invocations
- **Amazon Route 53**: DNS and health checks (Phase 2)
  - Use case: Multi-region failover

**Data Transfer & Streaming**
- **Amazon DynamoDB Streams**: Capture data changes for audit trail
  - Use case: Archive all data modifications to S3 for compliance
- **Amazon SNS**: Notifications for alerts and webhooks
  - Use case: Engineering alerts, farmer notifications (Phase 2)

**Cost Management**
- **AWS Cost Explorer**: Track and optimize costs
- **AWS Budgets**: Set cost alerts and limits

### Technology Stack by Layer

| Layer | Technology | Justification |
|-------|------------|---------------|
| **Compute** | AWS Lambda (Python 3.12, arm64) | Serverless, auto-scaling, cost-efficient |
| **Orchestration** | AWS Step Functions (Express) | Multi-agent coordination, failure handling |
| **AI/ML** | Amazon Bedrock (Claude, Llama, Mistral) | Managed LLMs, no model hosting, pay-per-use |
| **API** | Amazon API Gateway (REST) | Managed, scalable, Cognito integration |
| **Authentication** | Amazon Cognito | Phone-based auth, federated identities |
| **Database** | Amazon DynamoDB (On-Demand) | NoSQL, single-table design, auto-scaling |
| **Storage** | Amazon S3 (Standard, Glacier) | Object storage, lifecycle policies |
| **OCR** | Amazon Textract | Managed OCR, no ML model training |
| **Voice** | Amazon Polly + Transcribe | TTS and STT for voice interface |
| **Monitoring** | Amazon CloudWatch + X-Ray | Logs, metrics, traces, alarms |
| **Security** | AWS IAM, KMS, WAF | Fine-grained access control, encryption |
| **Mobile (Prototype)** | Flutter (Android, online-only) | Rapid development, single platform |
| **Mobile (Production)** | Flutter  | Cross-platform, low-bandwidth optimized |
| **Region** | ap-south-1 (Mumbai) | India data residency compliance |

### Why AWS Serverless Architecture?

**1. Zero Infrastructure Management**
- No servers to provision, patch, or maintain
- Focus 100% on application logic, not DevOps
- Ideal for hackathon rapid development

**2. Automatic Scaling**
- Scales from 1 to 100,000+ concurrent users automatically
- No capacity planning required
- Handles traffic spikes during harvest seasons

**3. Pay-Per-Use Cost Model**
- Only pay for actual usage (requests, compute time, storage)
- No idle capacity costs
- Aligned with rural affordability

**4. High Availability & Resilience**
- Multi-AZ deployment by default
- Automatic failover and retry mechanisms
- 99.9%+ uptime SLA

**5. Security by Default**
- Encryption at rest and in transit
- IAM-based access control
- Compliance with Indian data residency requirements

**6. Rapid Development**
- Managed services reduce development time by 60-70%
- Pre-built integrations (Cognito + API Gateway, Lambda + Bedrock)
- Perfect for 4-week hackathon timeline

---

## Appendix: Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Multi-agent vs monolithic AI** | Domain specialization, explainability, failure isolation |
| **Serverless vs containers** | Zero infrastructure management, auto-scaling, pay-per-use |
| **Express vs Standard workflows** | 25x cheaper, sufficient for 5-minute timeout |
| **DynamoDB vs RDS** | NoSQL flexibility, auto-scaling, no server management |
| **On-demand vs provisioned capacity** | Unpredictable traffic, cost optimization |
| **Claude vs GPT-4** | Better reasoning, structured output, India availability |
| **Phone-based vs email auth** | Rural accessibility, no email requirement |
| **No satellite imagery** | Cost, complexity, farmer-provided data sufficient |
| **India-only data residency** | Compliance, data sovereignty, farmer trust |



---


**End of Document**
