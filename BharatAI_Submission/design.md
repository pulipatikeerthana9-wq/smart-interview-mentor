# BharatAI Coach: System Design & Architecture

## 1. High-Level Architecture

The system follows a modern **Serverless Microservices** architecture on AWS to ensure scalability and cost-efficiency.

```mermaid
graph TD
    Client[React Mobile/Web App] -->|HTTPS/REST| APIGateway[AWS API Gateway]
    Client -->|Upload Resume| S3[Amazon S3 Bucket]
    
    subgraph "Backend Services (AWS Lambda)"
        Auth[Auth Service (Cognito)]
        Parser[Resume/JD Parser]
        Engine[Prediction Engine]
        Coach[Mock Interview Bot]
    end
    
    APIGateway --> Auth
    APIGateway --> Parser
    APIGateway --> Engine
    APIGateway --> Coach
    
    Parser --> Textract[Amazon Textract]
    
    Engine --> Bedrock[Amazon Bedrock (Claude 3 / Titan)]
    Coach --> Bedrock
    
    Engine --> DB[(Amazon DynamoDB)]
    Coach --> DB
```

## 2. Component Details

### Frontend

- **Framework**: React.js with Tailwind CSS (Mobile-responsive).
- **Hosting**: AWS Amplify.
- **Features**: Audio recording API, Resume Upload, Chat Interface.

### Backend (AWS Serverless)

- **API Gateway**: Manages REST endpoints and WebSocket connections for real-time chat.
- **AWS Lambda**: Executes business logic (Python).
- **Amazon Textract**: Extracts text from uploaded PDF resumes.
- **Amazon Bedrock**: The core AI brain.
  - *Model 1 (Analysis)*: Claude 3 Sonnet for deep analysis of Resume vs JD.
  - *Model 2 (Conversation)*: Amazon Titan for fast, interactive interview dialogue.

### Database (Amazon DynamoDB)

- **Table: Users** (`user_id`, email, college, preferred_language)
- **Table: Sessions** (`session_id`, user_id, job_role, timestamps)
- **Table: Interactions** (`interaction_id`, session_id, question, user_audio_url, ai_feedback, score)

## 3. API Specification

### POST `/api/v1/analyze-profile`

- **Input**: `{ resume_s3_key: "...", job_description: "..." }`
- **Process**: identifying skills gap and key focus areas.
- **Output**: `{ skills_match: 85%, critical_topics: ["React Hooks", "System Design"], behavioral_focus: ["Team conflict"] }`

### POST `/api/v1/predict-questions`

- **Input**: `{ session_id: "..." }`
- **Output**: List of 10 predicted questions (3 Technical, 2 Behavioral, 1 HR) prioritized by probability.

### POST `/api/v1/submit-answer`

- **Input**: `{ question_id: "...", user_response_text: "..." }`
- **Output**:
  - `score`: 7/10
  - `feedback`: "Good use of STAR method, but you forgot to mention the Result/Impact."
  - `suggested_improvement`: "Try adding: 'As a result, API latency dropped by 20%'."

## 4. Security & Compliance

- **Data Privacy**: All resumes are processed in-memory or stored with encryption (SSE-S3).
- **Auth**: Amazon Cognito for secure user sign-up/sign-in.
