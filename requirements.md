# BharatAI Coach: Requirements Specification

## 1. Problem Statement

**The "Bharat" Employability Gap**: India has millions of talented students in Tier-2 and Tier-3 colleges who possess technical skills but fail placement interviews due to a lack of soft skills and structured preparation.

- **Current State**: Students rely on generic YouTube videos or static "Top 100 HTML Questions" lists that are not tailored to their specific profile or the job they are applying for.
- **The Void**: Non-urban students lack access to experienced mentors who can conduct mock interviews and provide personalized feedback.

## 2. Proposed Solution

**BharatAI Coach** is an AI-powered interview preparation platform designed to democratize access to high-quality career mentorship. It uses Large Language Models (LLMs) on AWS to:

1. **Predict** the specific questions a recruiter is likely to ask based on the candidate's Resume and the Job Description (JD).
2. **Coach** the student on *how* to structure their answers using frameworks like the STAR method (Situation, Task, Action, Result).
3. **Simulate** realistic, adaptive mock interviews with vernacular support (Hinglish).

## 3. User Personas

- **Rohan (The Student)**: A final-year B.Tech student from a Tier-3 city. Good at coding but nervous about speaking English and doesn't know what to expect in an HR round.
- **Priya (The Job Seeker)**: Applying for a specific "React Developer" role. Needs to know what tricky React questions might come up based on her specific project experience.

## 4. User Stories

### Core Features

- **[US-01] Resume & JD Analysis**
  - As a student, I want to upload my Resume (PDF) and paste a Job Description so that the AI can understand my profile and the target role.
- **[US-02] Predictive Question Generation**
  - As a student, I want to receive a curated list of "Most Likely Questions" (Technical, Behavioral, HR) so that I can focus my preparation on what matters.
- **[US-03] Answer Strategy Coaching**
  - As a student, I want the AI to teach me *how* to answer a behavioral question using the STAR method, providing a sample structure before I attempt it.
- **[US-04] Adaptive Mock Interview**
  - As a student, I want to simulate a real interview where the AI asks follow-up questions based on my previous answers, just like a real human would.
- **[US-05] Vernacular Support**
  - As a student, I want to receive feedback in "Hinglish" or my native language if I struggle to understand complex English feedback.

## 5. Functional Requirements

- **FR-01**: System must parse PDF/Docx resumes to extract skills and project details.
- **FR-02**: System must use AWS Bedrock (Claude / Titan) to generate context-aware questions.
- **FR-03**: System must support real-time Speech-to-Text (STT) for oral interview practice.
- **FR-04**: System must provide a "Confidence Score" and granular feedback (Grammar, Relevance, Sentiment) after each answer.

## 6. Non-Functional Requirements

- **Scalability**: Must handle thousands of concurrent users during placement season (Serverless Architecture).
- **Latency**: AI responses should appear within 3 seconds to maintain flow.
- **Accessibility**: Mobile-first design for students without laptops.
