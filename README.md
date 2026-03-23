# Java Quiz Application (AI Integrated)

An **AI-powered Quiz Platform** built in **Java (Swing GUI)** that can generate fresh quiz questions using **Google Gemini AI**, while also supporting local quiz logic, user profiles, and result tracking.

---

## Project Structure (Architecture Overview)

> Main code lives inside:  
`Quiz_Platform/quiz_java_ai/main-application/`

```
Java_Quiz_Application_with_AI_Integrated/
└── Quiz_Platform/
    └── quiz_java_ai/
        └── main-application/
            ├── QuizApplication.java
            ├── Login.java
            ├── Quiz.java
            ├── Rules.java
            ├── Question.java
            ├── QuestionBank.java
            ├── QuizResult.java
            ├── UserProfile.java
            ├── Config.java
            ├── GeminiSetup.java
            ├── GeminiQuestionGenerator.java
            ├── SimpleJsonParser.java
            ├── TestGeminiIntegration.java
            ├── config.properties
            ├── compile_and_run.bat
            └── profiles/
                └── *.dat
```

---

## High-Level Architecture

This project is a **desktop GUI application** with a **single-JVM layered structure**:

### 1) UI Layer (Swing Screens)
Responsible for user interaction and navigation.

- **`Login.java`**
  - Entry UI for user login/profile selection.
  - Typically routes user to the quiz flow.

- **`Quiz.java`**
  - Main quiz UI/logic controller.
  - Displays questions, handles options selection, scoring, timers, etc.

- **`Rules.java`**
  - UI for showing rules/instructions and user guidance before quiz.

### 2) Domain / Model Layer (Core Entities)
Plain Java objects representing the quiz data.

- **`Question.java`**
  - Represents one quiz question (prompt, options, correct answer, etc.)

- **`QuizResult.java`**
  - Stores quiz outcome (score, correct answers, summary details)

- **`UserProfile.java`**
  - Represents user data and progress.
  - Persisted to disk in the `profiles/` directory.

### 3) Data + Question Source Layer
Responsible for getting questions either from AI or fallback/local logic.

- **`QuestionBank.java`**
  - Acts like a “repository/service” for questions.
  - Also contains Gemini connectivity testing (used during startup checks).
  - Provides questions to the quiz flow.

### 4) AI Integration Layer (Gemini)
Responsible for generating questions dynamically using Gemini APIs.

- **`GeminiSetup.java`**
  - Configuration/initial setup utility to store Gemini API key.
  - Designed to be run before launching if the key is missing.

- **`GeminiQuestionGenerator.java`**
  - Core Gemini client wrapper that:
    - Sends prompt requests
    - Receives AI responses
    - Converts into usable quiz questions

- **`SimpleJsonParser.java`**
  - Lightweight JSON parsing helper to interpret AI responses safely.

- **`TestGeminiIntegration.java`**
  - A test/debug utility to validate Gemini integration independently.

### 5) Configuration + Persistence Layer
Handles configuration files and user data storage.

- **`Config.java`**
  - Loads/validates config settings (like API key availability).
  - Reads from `config.properties`.

- **`config.properties`**
  - Stores application configuration (including AI configuration).

- **`profiles/`**
  - Local persistence folder.
  - Contains user profile data files like `Vaibhav.dat`.

---

## Application Execution Flow

### Entry Point
✅ **`QuizApplication.java`** is the main launcher.

It performs:

1. Sets Swing Look & Feel (system UI style)
2. Prints a welcome banner
3. Runs startup checks:
   - Loads configuration (`Config`)
   - Checks whether Gemini API key is configured
   - Tests Gemini connectivity via `QuestionBank.testGeminiConnection()`
   - Ensures `profiles/` directory exists (creates it if missing)
   - Checks write permissions for profile/config saving
4. Launches the UI with:
   - `Login loginScreen = new Login();`

---

## Setup & Run

### 1) Configure Gemini API Key (Recommended)
If not configured, the app may run with limited AI features.

Run setup:

```bash
java GeminiSetup
```

### 2) Run Application
```bash
java QuizApplication
```

### Windows shortcut
You can also use:

- `compile_and_run.bat`

---

## Key Features

- Swing-based Desktop UI
- AI question generation using Google Gemini
- Startup validation for:
  - API key presence
  - Internet / Gemini connectivity
  - profile folder persistence
- User profiles saved locally (`profiles/*.dat`)
- Quiz scoring + result tracking

---

## Notes / Improvements (Suggested)

If you want to make the project more “standard Java project structure”, consider:
- Moving code into `src/main/java/...`
- Introducing packages like:
  - `ui/`
  - `model/`
  - `service/`
  - `ai/`
  - `config/`
- Adding a build tool (Maven/Gradle) for easier dependency management.

---

## Author

GitHub: **Divyansh-132006**
