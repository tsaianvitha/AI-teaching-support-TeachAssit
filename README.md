# TeachAssit - AI-Powered Teacher's Assistant 

**TeachAssit** is a real-time conversational web application designed to support school teachers in Indian classrooms. By leveraging state-of-the-art Generative AI (LLaMA 3.1) and custom pedagogical templates, the application provides adaptive guidance, custom MCQ quizzes, classroom management strategies, and voice synthesis support in regional Indian languages.

---

##  Key Features

*   **Adaptive AI Mentor:** Chat assistant that customizes its advice and pedagogical tone based on the teacher's profile (Grade, Subject, Years of Experience, Location, and specific Classroom Challenges).
*   **Context-Aware Dialogues:** Utilizes localized query-history buffers to recall previous interactions and prevent repetitive suggestions.
*   **MCQ Quiz Generator:** Generates custom, grade-appropriate multiple-choice tests on any topic, complete with answer keys and printable templates.
*   **Classroom Behaviour Coach:** Offers tailored, structured 3-step action plans (including a verbatim script of what to say) to resolve specific classroom management and student counseling issues.
*   **Saved Resources Library:** Enables teachers to save generated lesson plans, worksheets, and quizzes for future retrieval, searching, filtering, and printing.
*   **Multilingual Speech Integration:** Hybrid Text-to-Speech (TTS) engine speaking in English and regional Indian languages (Hindi, Tamil, Telugu, Kannada, Malayalam).

---

##  Tech Stack

### Frontend
*   **Framework:** React.js (Vite)
*   **Styling:** Custom CSS
*   **HTTP Client:** Axios (configured with automated JWT authorization headers)

### Backend
*   **Framework:** Python Flask (REST API)
*   **ORM:** Flask-SQLAlchemy
*   **Database Driver:** PyMySQL
*   **Security & Authentication:** Flask-JWT-Extended & Werkzeug (Password hashing)
*   **AI Engine:** Groq API SDK (targeting LLaMA-3.1-8b-instant)

### Database
*   **RDBMS:** MySQL

---

## 📂 Project Structure

```text
├── backend/
│   ├── app.py             # REST API endpoints & server setup
│   ├── models.py          # SQLAlchemy Database Schema
│   ├── service.py         # Groq LLM connectors & JSON cleansing logic
│   ├── requirements.txt   # Python dependency list
│   └── .env.example       # Backend environmental variables template
├── frontend/
│   ├── src/
│   │   ├── components/    # Reusable UI elements (Navbar, Buttons, etc.)
│   │   ├── pages/         # Page components (Landing, Assistant, Coach, Library)
│   │   ├── services/      # Axios API connector & Speech utilities
│   │   └── styles/        # CSS stylesheets
│   ├── package.json       # Node dependency list
│   └── vite.config.js     # Vite configuration
└── README.md              # Documentation
```

---

## ⚙️ Installation & Setup

### Prerequisites
*   [Node.js](https://nodejs.org/) (v16+ recommended)
*   [Python](https://www.python.org/) (v3.9+ recommended)
*   [MySQL Server](https://www.mysql.com/)

---

### 1. Backend Configuration

1. Navigate to the `backend` folder:
   ```bash
   cd backend
   ```

2. Create a virtual environment and activate it:
   ```bash
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the `backend/` directory:
   ```env
   PORT=5001
   DATABASE_URL=mysql+pymysql://<DB_USER>:<DB_PASSWORD>@localhost:3306/teacher_Ai
   JWT_SECRET_KEY=your-jwt-super-secret-key
   GROQ_API_KEY=your-groq-cloud-api-key
   ```

5. Initialize the database schema and launch the Flask server:
   ```bash
   python app.py
   ```
   *The server runs by default on `http://localhost:5001`*

---

### 2. Frontend Configuration

1. Navigate to the `frontend` folder:
   ```bash
   cd ../frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the `frontend/` directory:
   ```env
   VITE_API_URL=http://localhost:5001
   ```

4. Run the Vite development server:
   ```bash
   npm run dev
   ```
   *The client runs by default on `http://localhost:5173`*

---

## 📡 REST API Reference

| Endpoint | Method | Authentication | Description |
| :--- | :--- | :--- | :--- |
| `/signup` | `POST` | Public | Register a new teacher account |
| `/login` | `POST` | Public | Authenticate credentials and get JWT token |
| `/chats` | `POST` | JWT Required | Create a new conversational session |
| `/chats` | `GET` | JWT Required | List all conversational sessions for the user |
| `/ask` | `POST` | JWT Required | Submit query to context-aware LLaMA 3.1 assistant |
| `/quiz` | `POST` | JWT Required | Generate topic-specific MCQ quizzes in JSON format |
| `/behaviour-coach` | `POST` | JWT Required | Request classroom behavior action plans |
| `/resources` | `POST` | JWT Required | Save lesson plans, quizzes, or behavior coach responses |
| `/resources` | `GET` | JWT Required | Query, filter, and search saved resources |
| `/stats/ratings` | `GET` | JWT Required | Retrieve weekly satisfaction rating statistics |
| `/tts` | `POST` | Public | Synthesize text to base64-encoded MP3 audio |
