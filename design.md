# Design Document - OASIS Platform

## 1. System Overview

OASIS follows a modular, AI-first architecture where user interactions trigger GenAI workflows to generate personalized learning paths, interview questions, and performance analysis. This web-based career coaching platform provides adaptive skill development and interview preparation through intelligent automation and real-time AI-driven feedback.

### Core Components
- **Frontend**: React-based web application with responsive design
- **Backend API**: Node.js/Express RESTful API server
- **GenAI Engine**: Integration with AI services for content generation and analysis
- **Database**: PostgreSQL for structured data, Redis for caching
- **Audio Processing**: Speech-to-text integration for interview practice
- **Authentication**: JWT-based secure authentication system

### Key Features
- Personalized career roadmap generation
- Interactive skill learning modules
- AI-driven interview practice sessions
- Real-time performance analysis and feedback
- Progress tracking and historical data visualization

## 2. Architecture Diagram (Textual)

OASIS follows a modular, AI-first architecture where user interactions trigger GenAI workflows to generate personalized learning paths, interview questions, and performance analysis.

```
┌─────────────────────────────────────────────────────────┐
│                Frontend Dashboard                       │
│           (React SPA - User Interface)                  │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ↓
┌─────────────────────────────────────────────────────────┐
│                Backend API Layer                        │
│         (Node.js/Express - Business Logic)              │
│              [AI Workflow Engine]                       │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ↓
┌─────────────────────────────────────────────────────────┐
│                  GenAI Engine                           │
│        (OpenAI/Anthropic - Content Generation)         │
│    • Learning Path Generation                           │
│    • Interview Question Creation                        │
│    • Response Processing                                │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ↓
┌─────────────────────────────────────────────────────────┐
│            Analysis & Scoring Module                    │
│         (AI-Powered Performance Evaluation)            │
│    • Technical Skill Assessment                         │
│    • Soft Skill Analysis                               │
│    • Progress Tracking                                  │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ↓
┌─────────────────────────────────────────────────────────┐
│                    Database                             │
│              (PostgreSQL + Redis)                      │
│    • User Profiles & Progress                           │
│    • Learning Content & Analytics                       │
│    • Performance Reports & History                      │
└─────────────────────────────────────────────────────────┘
```

## 3. Module Design

### 3.1 Authentication Module
**Purpose**: Secure user access and session management

**Components**:
- User registration and login
- JWT token generation and validation
- Password encryption and security
- Session management

**API Endpoints**:
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update user profile

### 3.2 Dashboard Module
**Purpose**: Central hub for user progress and navigation

**Components**:
- Progress visualization
- Active career paths display
- Quick navigation to modules
- Recent activity feed

**API Endpoints**:
- `GET /api/dashboard/overview` - Dashboard data
- `GET /api/dashboard/progress` - Progress metrics
- `GET /api/dashboard/recent-activity` - Recent user activities

### 3.3 Career Path Generator
**Purpose**: AI-powered career selection and personalized roadmap generation

**Components**:
- Career path selection interface
- User input collection (skills, goals, experience)
- GenAI roadmap generation
- Milestone tracking and personalization

**API Endpoints**:
- `GET /api/careers` - Available career paths
- `POST /api/careers/select` - Select career path
- `POST /api/careers/roadmap` - Generate personalized roadmap
- `GET /api/careers/roadmap/:id` - Get specific roadmap
- `PUT /api/careers/roadmap/:id/progress` - Update progress

### 3.4 Learning Module
**Purpose**: Skill-based learning content delivery and hands-on practice

**Components**:
- Learning content management
- Interactive exercises and tasks
- Progress tracking
- Skill completion validation

**API Endpoints**:
- `GET /api/learning/skills/:skillId` - Get skill content
- `POST /api/learning/skills/:skillId/complete` - Mark skill complete
- `GET /api/learning/exercises/:skillId` - Get exercises
- `POST /api/learning/exercises/:exerciseId/submit` - Submit exercise

### 3.5 Interview Practice Module
**Purpose**: AI-driven interview simulation and adaptive questioning

**Components**:
- AI-powered question generation based on career/skill
- Audio recording and transcription
- Real-time AI analysis
- Adaptive questioning based on responses

**API Endpoints**:
- `POST /api/interviews/start` - Start interview session
- `GET /api/interviews/:sessionId/questions` - Get interview questions
- `POST /api/interviews/:sessionId/response` - Submit response
- `GET /api/interviews/:sessionId/analysis` - Get performance analysis

### 3.6 Analysis & Feedback Module
**Purpose**: AI-powered performance analysis and personalized feedback

**Components**:
- Technical skill analysis
- Soft skill evaluation
- Performance report generation
- AI-driven improvement recommendations

**API Endpoints**:
- `GET /api/analysis/performance/:userId` - User performance data
- `GET /api/analysis/skills/:userId` - Skill analysis
- `GET /api/analysis/reports/:reportId` - Detailed reports
- `POST /api/analysis/generate-report` - Generate new report

### 3.7 Progress Tracking Module
**Purpose**: Comprehensive learning progress monitoring and analytics

**Components**:
- Learning milestone tracking
- Performance metrics collection
- Historical data visualization
- Achievement and goal management

**API Endpoints**:
- `GET /api/progress/:userId` - User progress overview
- `GET /api/progress/:userId/milestones` - Milestone tracking
- `POST /api/progress/update` - Update progress metrics
- `GET /api/progress/:userId/analytics` - Progress analytics

## 4. GenAI Workflow

### 4.1 Career Path & Roadmap Generation
**Trigger**: User selects a new career path and provides background details.

**Workflow**:
1. User inputs career preference, current skill level, and goals.
2. The system constructs a structured prompt using user inputs.
3. The GenAI model generates a personalized career roadmap.
4. The roadmap is broken into skills and milestones.
5. The roadmap is stored and displayed to the user.

**GenAI Output**:
- Skill list
- Learning order
- Estimated milestones

### 4.2 Learning Content Generation
**Trigger**: User enters the Learn module for a skill.

**Workflow**:
1. Selected skill details are sent to the GenAI engine.
2. The GenAI generates concept explanations and hands-on tasks.
3. Content is adapted based on user progress.
4. Learning completion updates the user profile.

**GenAI Output**:
- Skill explanations
- Practical exercises
- Progress recommendations

### 4.3 Most Asked Questions Generation
**Trigger**: User opens the Most Asked Questions section.

**Workflow**:
1. Career path or skill context is passed to GenAI.
2. The GenAI generates frequently asked interview questions.
3. Questions are categorized by difficulty.
4. Questions are presented for user practice.

**GenAI Output**:
- Role-specific interview questions
- Difficulty classification

### 4.4 Interview Answer Evaluation
**Trigger**: User submits answers to practice questions.

**Workflow**:
1. User responses are captured in text or speech format.
2. Speech responses are transcribed using speech-to-text.
3. The transcript is sent to GenAI for evaluation.
4. The GenAI analyzes correctness, clarity, and depth.
5. Feedback and improvement suggestions are generated.

**GenAI Output**:
- Answer quality feedback
- Knowledge gap identification
- Improvement tips

### 4.5 Live Interview Practice
**Trigger**: User starts a live interview session.

**Workflow**:
1. The system initializes an interview prompt based on career path.
2. GenAI dynamically asks interview questions.
3. User responses are captured in real time.
4. The interview adapts based on previous answers.
5. The session ends after a predefined number of questions.

**GenAI Output**:
- Adaptive interview questions
- Context-aware follow-ups

### 4.6 Soft Skill Analysis
**Trigger**: Completion of a live interview session.

**Workflow**:
1. Interview transcript is processed using NLP.
2. GenAI evaluates communication clarity, confidence, and structure.
3. Speech patterns and response flow are analyzed.
4. Soft-skill scores are generated.

**GenAI Output**:
- Communication score
- Confidence indicators
- Soft-skill feedback

### 4.7 Technical Skill Analysis
**Trigger**: Interview transcript and practice responses available.

**Workflow**:
1. Responses are matched against expected technical knowledge.
2. GenAI evaluates problem-solving approach.
3. Skill-wise proficiency levels are determined.
4. Technical strengths and weaknesses are identified.

**GenAI Output**:
- Skill proficiency levels
- Technical strengths
- Areas requiring improvement

### 4.8 Performance Report Generation
**Trigger**: Completion of interview or practice session.

**Workflow**:
1. Technical and soft-skill analyses are aggregated.
2. GenAI generates a structured performance report.
3. Readiness and confidence scores are calculated.
4. Recommendations are personalized for the user.

**GenAI Output**:
- Strengths summary
- Weakness analysis
- Readiness score
- Learning recommendations

### 4.9 Progress Adaptation & Feedback Loop
**Trigger**: User completes learning or interview activities.

**Workflow**:
1. Updated performance data is sent to GenAI.
2. Learning paths are dynamically adjusted.
3. Future interview questions adapt to weak areas.
4. Dashboard metrics are updated.

**GenAI Output**:
- Adaptive learning path
- Personalized next steps

### 4.10 Single Skill Learning Workflow
**Trigger**: User selects a single skill instead of a full career path.

**Workflow**:
1. Skill context is passed to GenAI.
2. Learning content and interview questions are generated.
3. Practice and analysis follow the same evaluation pipeline.
4. Skill-specific progress is tracked independently.

**GenAI Output**:
- Skill-focused roadmap
- Practice feedback
- Skill proficiency report

## 5. Data Flow

### 5.1 Core AI-First Data Flow
```
User Input Captured → Data Sent to Backend → Prompt Sent to GenAI → AI Response Processed → Results Stored → Dashboard Updated
```

### 5.2 User Registration Flow
```
Frontend Form → Validation → API Request → Database Insert → JWT Generation → Response
```

### 5.3 Career Path Selection Flow
```
User Selection → Input Collection → GenAI Request → Roadmap Generation → Database Storage → UI Update
```

### 5.4 Learning Progress Flow
```
Skill Completion → Progress Update → Database Write → Analytics Update → Dashboard Refresh
```

### 5.5 Interview Practice Flow
```
Session Start → Question Generation → Audio Capture → Transcription → AI Analysis → Feedback Display
```

## 6. Tech Stack

### 6.1 Frontend
- **React.js / Next.js** - Used for building a responsive and interactive user interface
- **Tailwind CSS** - Used for fast and consistent UI styling
- **WebRTC / Media APIs** - Used for capturing audio during live interview sessions
- **Chart.js / Recharts** - Used for visualizing learning progress and performance metrics

### 6.2 Backend
- **Node.js (Express) / FastAPI (Python)** - Used to handle API requests, user sessions, and GenAI orchestration
- **REST APIs** - Used for communication between frontend, backend, and AI services
- **WebSockets** - Used for real-time interaction during live interview practice

### 6.3 GenAI & AI Services
- **Large Language Model (LLM)**
  - **Gemini / OpenAI GPT** - Used for roadmap generation, interview questions, evaluation, and feedback
- **Speech-to-Text API**
  - **OpenAI Whisper / Google Speech-to-Text** - Used to transcribe live interview responses
- **Natural Language Processing (NLP)** - Used for soft-skill and technical skill analysis

### 6.4 Database & Storage
- **MongoDB / Firebase Firestore** - Used to store user profiles, progress, and reports
- **Cloud Storage (Optional)** - Used temporarily for interview audio files (not permanently stored)

### 6.5 Analytics & Scoring
- **Custom Scoring Engine** - Used to calculate readiness, confidence, and skill proficiency scores
- **Prompt-based Evaluation Logic** - Used to standardize GenAI assessment responses

### 6.6 Authentication & Security
- **JWT / OAuth 2.0** - Used for secure user authentication
- **HTTPS & Encrypted APIs** - Used for secure data transmission
- **Role-based Access Control (RBAC)** - Used to manage user access (optional for MVP)

### 6.7 Cloud & Deployment
- **Google Cloud Platform (GCP) / AWS** - Used for hosting backend services and AI workloads
- **Docker (Optional)** - Used for containerized deployment
- **Vercel / Netlify** - Used for frontend deployment

### 6.8 Development & Collaboration Tools
- **Kiro** - Used for requirements tracking and design documentation
- **GitHub** - Used for version control and collaboration
- **Postman / Thunder Client** - Used for API testing

### 6.9 Monitoring & Logging (Optional)
- **Cloud Logging / Prometheus** - Used to monitor system performance and errors

## 7. Security & Privacy

### 7.1 Data Handling Principles
- **Client-side data handling where possible** - Minimize server-side data processing
- **Encrypted API communication** - All data transmission secured with TLS 1.3
- **No permanent storage of interview audio** - Audio files deleted immediately after transcription
- **User consent for analysis** - Explicit consent required for AI analysis and feedback

### 7.2 Authentication & Authorization
- **JWT Implementation**: Short-lived access tokens (15 minutes) with refresh tokens
- **Password Security**: bcrypt hashing with salt rounds ≥ 12
- **Session Management**: Secure token storage, automatic logout on inactivity
- **Role-Based Access**: User roles with granular permissions

### 7.3 Data Protection
- **Encryption at Rest**: Database encryption for sensitive data
- **Encryption in Transit**: TLS 1.3 for all API communications
- **Audio Data**: Temporary storage with automatic deletion after processing
- **Personal Data**: GDPR-compliant data handling and user consent

### 7.4 API Security
- **Rate Limiting**: Per-user and per-endpoint rate limits
- **Input Validation**: Comprehensive validation and sanitization
- **CORS Configuration**: Strict origin policies
- **Security Headers**: HSTS, CSP, X-Frame-Options

### 7.5 GenAI Security
- **Prompt Injection Protection**: Input sanitization and validation
- **API Key Management**: Secure storage and rotation of AI service keys
- **Content Filtering**: Inappropriate content detection and filtering
- **Usage Monitoring**: AI service usage tracking and anomaly detection

### 7.6 Privacy Compliance
- **Data Minimization**: Collect only necessary user data
- **Consent Management**: Clear consent for data processing and AI analysis
- **Data Retention**: Automatic deletion of old data per retention policies
- **User Rights**: Data export, deletion, and modification capabilities

### 7.7 Monitoring & Incident Response
- **Security Logging**: Comprehensive audit trails
- **Anomaly Detection**: Unusual activity monitoring
- **Incident Response**: Defined procedures for security incidents
- **Regular Audits**: Periodic security assessments and penetration testing

---

*This design document serves as the technical blueprint for the OASIS platform development. It should be reviewed and updated as requirements evolve during the development process.*