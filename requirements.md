# Requirements Document

## 1. Introduction


OASIS is a GenAI-powered skills enhancement and career coaching platform designed to guide users from career selection to interview readiness through personalized learning, practice, and AI-driven feedback.


## 2. Goals & Objectives


- Provide personalized career roadmaps

-Enable hands-on skill learning

-Simulate real interview experiences

-Analyze technical and soft skills

-Track learning progress over time

## 3. User Roles


- User (Learner) – accesses learning, practice, and interviews
- System (GenAI Engine) – generates content, analysis, and feedback


## 4. Functional Requirements

### 4.1 Authentication & User Access
- **FR-1**: The system shall allow users to log in using secure authentication.
- **FR-2**: The system shall create and maintain a user profile for each user.
- **FR-3**: The system shall allow users to access the dashboard after successful login.

### 4.2 Dashboard
- **FR-4**: The system shall display the user's overall learning progress on the dashboard.
- **FR-5**: The system shall show active career paths and skills being learned.
- **FR-6**: The system shall allow users to navigate to new career path selection.
- **FR-7**: The system shall allow users to navigate to single skill learning.

### 4.3 Career Path Selection
- **FR-8**: The system shall allow users to select a new career path.
- **FR-9**: The system shall collect user inputs such as current skill level and goals.
- **FR-10**: The system shall generate a personalized career roadmap using GenAI.
- **FR-11**: The system shall display the roadmap in a structured, milestone-based format.

### 4.4 Roadmap Management
- **FR-12**: The system shall divide the career roadmap into individual skills.
- **FR-13**: The system shall track completion status for each roadmap milestone.
- **FR-14**: The system shall allow users to resume progress from the last completed milestone.

### 4.5 Learn Module
- **FR-15**: The system shall provide learning content for each skill in the roadmap.
- **FR-16**: The system shall support hands-on learning through tasks or exercises.
- **FR-17**: The system shall update learning progress upon skill completion.
- **FR-18**: The system shall recommend next skills based on progress.

### 4.6 Most Asked Questions Module
- **FR-19**: The system shall generate commonly asked interview questions for the selected career or skill.
- **FR-20**: The system shall allow users to practice answering interview questions.
- **FR-21**: The system shall analyze user responses using GenAI.
- **FR-22**: The system shall identify knowledge gaps from user responses.
- **FR-23**: The system shall provide feedback and improvement suggestions.

### 4.7 Live Interview Practice
- **FR-24**: The system shall conduct AI-driven live interview sessions.
- **FR-25**: The system shall ask adaptive interview questions based on the chosen career path.
- **FR-26**: The system shall capture user responses during the interview.
- **FR-27**: The system shall transcribe interview responses for analysis.

### 4.8 Skill Analysis & Reporting
- **FR-28**: The system shall analyze technical skills from interview responses.
- **FR-29**: The system shall analyze soft skills such as communication and confidence.
- **FR-30**: The system shall generate a detailed performance report.
- **FR-31**: The system shall highlight strengths and areas for improvement.
- **FR-32**: The system shall assign a readiness or confidence score.

### 4.9 Single Skill Learning Mode
- **FR-33**: The system shall allow users to select a single skill independently.
- **FR-34**: The system shall provide learning and practice options for the selected skill.
- **FR-35**: The system shall generate interview questions specific to the single skill.
- **FR-36**: The system shall track progress for the single skill separately.

### 4.10 Progress Tracking & History
- **FR-37**: The system shall store user learning progress.
- **FR-38**: The system shall display historical performance data.
- **FR-39**: The system shall update progress metrics after each activity.
- **FR-40**: The system shall provide visual indicators of improvement over time.

### 4.11 Feedback & Recommendations
- **FR-41**: The system shall recommend skills to focus on based on analysis.
- **FR-42**: The system shall adapt future questions based on user weaknesses.
- **FR-43**: The system shall personalize learning paths dynamically.

### 4.12 System Notifications (Optional for MVP)
- **FR-44**: The system shall notify users upon milestone completion.
- **FR-45**: The system shall notify users when they are ready for interview practice.

### API Requirements
- RESTful API endpoints for all user interactions
- JSON data format for request/response payloads
- JWT-based authentication for secure API access
- Rate limiting to prevent abuse

### Data Requirements
- User profiles with learning preferences and history
- Career path templates and skill taxonomies
- Interview question banks organized by skill/career
- Progress tracking with timestamps and completion metrics
- AI-generated content storage and versioning

## 5. Non-Functional Requirements

### Performance
- **Response Time**: The system should respond within acceptable time limits
  - Web page loads: < 3 seconds
  - API responses: < 2 seconds
  - AI-generated content: < 10 seconds
- **Throughput**: The system should scale for multiple users
  - Support minimum 100 concurrent users
  - Handle peak loads during high usage periods
- **Scalability**: The system should accommodate growth in user base and data volume

### Security
- **Authentication**: Secure user login with password encryption and session management
- **Authorization**: Role-based access control for different user types
- **Data Protection**: The system should ensure data privacy
  - Encrypt sensitive user data at rest and in transit
  - Comply with GDPR and data protection regulations
  - Secure storage of personal learning data and interview recordings
- **Compliance**: Adhere to educational data privacy standards

### Reliability
- **Availability**: The system should provide high availability
  - Target 99.5% uptime
  - Minimal planned downtime for maintenance
- **Error Handling**: Graceful error handling with user-friendly messages
- **Backup & Recovery**: Regular data backups with disaster recovery procedures

### Usability
- **User Experience**: The UI should be intuitive and beginner-friendly
  - Clear navigation and workflow guidance
  - Consistent design patterns across all modules
- **Accessibility**: Support for users with disabilities (WCAG 2.1 AA compliance)
- **Browser Support**: Compatible with modern browsers (Chrome, Firefox, Safari, Edge)
- **Mobile Compatibility**: Responsive design for mobile and tablet devices

### Maintainability
- **Code Quality**: Clean, well-documented code following industry standards
- **Documentation**: Comprehensive technical and user documentation
- **Testing**: Automated testing with minimum 80% code coverage

## 6. Assumptions & Constraints

### Assumptions
- **Internet connectivity is required** for all system functionality
- Users have access to modern web browsers with microphone capabilities
- **Interview practice may be simulated for MVP** rather than live human interviews
- Users are willing to provide voice input for interview practice sessions
- **Speech analysis accuracy depends on audio quality** from user devices

### Technical Constraints
- **Technology Stack**: Web-based platform with GenAI integration
- **Platform Limitations**: Requires microphone access for speech analysis
- **Integration Requirements**: Integration with GenAI services and speech-to-text APIs
- **External Dependencies**: **Third-party APIs may have rate limits** affecting system performance
- **Audio Processing**: Speech recognition quality varies with device microphone and environment

### Business Constraints
- **Budget**: Development within allocated budget for GenAI API usage
- **Timeline**: MVP delivery timeline may limit advanced features
- **Resources**: Development team size and AI/ML expertise availability
- **Regulatory**: Compliance with educational data privacy and AI ethics guidelines

## 7. Out of Scope

### Explicitly Excluded Features
- **Real human mentor interaction** - The system will rely on AI-driven coaching only
- **Certified course completion** - No formal certification or accreditation will be provided
- **Job placement guarantees** - The platform focuses on skill development, not job placement services
- Live video conferencing with human instructors
- Integration with external job boards or recruitment platforms
- Payment processing for premium features (MVP will be free)

### Future Considerations
- Human mentor integration in future versions
- Partnership with educational institutions for certification
- Job matching and placement services
- Advanced AI features like emotion recognition during interviews
- Mobile native applications for iOS and Android
- Offline learning capabilities

---

