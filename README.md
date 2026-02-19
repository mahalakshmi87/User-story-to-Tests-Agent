# User-story-to-Tests-Agent

A comprehensive full-stack application that automatically generates test cases from Jira user stories using AI (Groq LLM), with export capabilities and defect tracking integration.

## 🎯 Project Overview

This application bridges the gap between product requirements (Jira user stories) and QA testing by automatically generating comprehensive test cases using advanced AI models. It provides a seamless workflow for:

1. **Jira Integration** - Fetch user stories directly from your Jira instance
2. **AI-Powered Test Generation** - Leverage Groq's advanced LLM (qwen/qwen3-32b) to generate test cases
3. **Test Export** - Export generated tests to Excel format for easy distribution
4. **Defect Logging** - Log and track defects directly within the application

## 🏗️ Architecture

### Backend Stack
- **Framework**: FastAPI (Python)
- **Server**: Uvicorn 0.24.0
- **LLM Integration**: Groq API (qwen/qwen3-32b model)
- **Data Validation**: Pydantic 2.5.0
- **HTTP Client**: aiohttp (async), requests
- **CORS**: Starlette middleware

### Frontend Stack
- **Framework**: React 18.2.0 with TypeScript
- **Build Tool**: Vite 7.3.1
- **HTTP Client**: Axios 1.4.0
- **Styling**: Tailwind CSS
- **Package Manager**: npm

## 📁 Project Structure

```
├── backend/                        # FastAPI application
│   ├── llm/
│   │   └── groq_client.py         # Groq LLM client for test generation
│   ├── routers/
│   │   ├── generate.py             # Test generation endpoint
│   │   └── jira.py                 # Jira API endpoints
│   ├── services/
│   │   └── jira_service.py         # Jira integration service
│   ├── middleware/
│   │   └── session_middleware.py   # Session management
│   ├── schemas.py                  # Pydantic data models
│   ├── main.py                     # FastAPI application entry
│   ├── .env                        # Environment configuration
│   └── venv/                       # Python virtual environment
│
├── frontend/                       # React application
│   ├── src/
│   │   ├── components/             # React components
│   │   ├── api.ts                  # API client configuration
│   │   ├── App.tsx                 # Main application component
│   │   └── main.tsx                # Application entry point
│   ├── vite.config.ts              # Vite configuration
│   └── package.json                # npm dependencies
│
├── README.md                       # This file
└── .gitignore                      # Git exclusions
```

## 🚀 Getting Started

### Prerequisites
- Python 3.12+
- Node.js 16+ (npm or yarn)
- Jira instance with API access
- Groq API key (get free credits at https://console.groq.com)

### Backend Setup

1. **Navigate to backend directory**
   ```bash
   cd backend
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your settings:
   # - groq_API_KEY: Your Groq API key
   # - JIRA_URL: Your Jira instance URL
   # - JIRA_USERNAME: Jira username
   # - JIRA_API_TOKEN: Jira API token
   ```

5. **Run the server**
   ```bash
   uvicorn main:app --reload --host 127.0.0.1 --port 3001
   ```
   The API will be available at `http://localhost:3001`

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure API endpoint**
   - Update `src/api.ts` with your backend URL (default: `http://localhost:3001`)

4. **Run development server**
   ```bash
   npm run dev
   ```
   The application will be available at `http://localhost:5173`

## 📋 Key Features

### 1. User Story Fetching
- Connect to your Jira instance
- Fetch user stories from specified projects
- Filter stories by status and assignee
- Display comprehensive story details

### 2. AI-Powered Test Generation
- **Model**: Groq's qwen/qwen3-32b (high performance)
- **Generation**: Automatic test case creation from user stories
- **Quality**: Validates test structure and completeness
- **Performance**: Async processing for quick generation

### 3. Test Export
- Export generated tests to Excel format
- Preserve test structure and formatting
- Include test IDs, titles, steps, and expected results
- Batch export multiple test cases

### 4. Defect Logging
- Log defects directly from test results
- Track defect status and severity
- Link defects to specific test cases
- Export defect reports

## 🔧 API Endpoints

### Generate Tests
```
POST /api/generate-tests
Content-Type: application/json

{
  "user_story": "As a user, I want to login with email",
  "story_id": "JIRA-123",
  "project_key": "TEST"
}

Response:
{
  "test_cases": [
    {
      "id": "TC-1",
      "title": "Verify login with valid email",
      "steps": [...],
      "expected_results": [...]
    }
  ]
}
```

### Fetch Jira Stories
```
GET /api/jira/issues?project=TEST&status=Open

Response:
{
  "issues": [
    {
      "key": "JIRA-123",
      "summary": "User story title",
      "description": "Story description",
      "status": "Open"
    }
  ]
}
```

## 🛠️ Development

### Backend Development
- Framework: FastAPI with async/await support
- Code organization: Router-based architecture
- Services: Business logic layer for Jira and LLM operations
- Middleware: Session and CORS handling

### Frontend Development
- Component-based architecture with React Hooks
- Axios for HTTP requests
- TypeScript for type safety
- Tailwind CSS for styling

### Testing
```bash
# Backend tests
cd backend
pytest

# Frontend tests
cd frontend
npm run test
```

## 🔐 Security

- **API Keys**: All sensitive keys stored in `.env` file (never committed)
- **CORS**: Configured to allow frontend communication
- **Session**: Middleware-based session management
- **Best Practices**: Environment-based configuration

### Environment Configuration
Create a `.env` file based on `.env.example`:
```env
HOST=127.0.0.1
PORT=3001
CORS_ORIGIN=http://localhost:5173
groq_API_KEY=your_groq_api_key_here
groq_API_BASE=https://api.groq.com/openai/v1
groq_MODEL=qwen/qwen3-32b
SESSION_SECRET=your-secret-key-change-in-production
JIRA_URL=https://your-jira-instance.atlassian.net
JIRA_USERNAME=your_email@example.com
JIRA_API_TOKEN=your_jira_api_token
```

## 📦 Dependencies

### Backend
- fastapi: Web framework
- uvicorn: ASGI server
- pydantic: Data validation
- aiohttp: Async HTTP client
- requests: HTTP library
- python-dotenv: Environment configuration

### Frontend
- react: UI framework
- axios: HTTP client
- vite: Build tool
- typescript: Type safety
- tailwind: CSS framework

## 🤝 Contributing

1. Clone the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Troubleshooting

### Backend Issues
- **Port 3001 already in use**: Change port in `.env` or kill existing process
- **Groq API errors**: Verify API key in `.env` and check Groq console for quota
- **Jira connection fails**: Verify Jira credentials and network connectivity

### Frontend Issues
- **CORS errors**: Ensure backend CORS_ORIGIN matches frontend URL
- **API connection fails**: Check backend is running and API endpoint in `src/api.ts` is correct
- **Build errors**: Clear node_modules and run `npm install` again

## 📞 Support

For issues, questions, or feature requests, please create an issue on the GitHub repository.

---

**Last Updated**: 2024
**Maintainer**: Mahalakshmi
