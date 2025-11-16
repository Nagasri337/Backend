Lumibyte Assignment Reference Document
Simplified Chat Application
1. Objective
The primary goal of this project is to build a responsive, single-page application (SPA) that mimics a basic conversational interface, like ChatGPT.
Frontend Goal: Create an interactive, two-pane web application (Sidebar + Main Chat View) using React (JavaScript) and Tailwind CSS, featuring light/dark theme toggling and displaying structured (tabular) data responses.
Backend Goal: Develop a simple REST API using Node.js/Express to serve mock, static JSON data that simulates session management, conversation history, and structured answers.
Core Feature: Implement session management where each conversation is linked to a unique ID in the URL, and past sessions are viewable in a sidebar.
2. Technical Requirements
This project requires a fundamental understanding of the following technologies:
Category
Tool/Technology
Description
Frontend
React (with JavaScript/ES6)
Library for building the user interface.
Styling
Tailwind CSS
Utility-first CSS framework for rapid, responsive styling.
Backend
Node.js
JavaScript runtime environment.
Backend
Express.js
Fast, unopinionated, minimalist web framework for Node.js.
Tools
Git & GitHub
Version control and public repository for submission.
Tools
VS Code (Recommended)
Code editor.
Tools
npm or Yarn/pnpm
Package manager for installing dependencies.
Prerequisites
Node.js (LTS version) installed on your machine.
Basic command line/terminal usage.
3. Step-by-Step Instructions
This project is best tackled by separating the Frontend and Backend into two distinct directories.
Phase 1: Backend Setup (Mock API Server)
The backend's only job is to provide static JSON data. It does not require a database.
Step 1.1: Project Initialization
Create a new folder named backend.
mkdir backend
cd backend
npm init -y

​
Install necessary packages: express for the server, and cors to allow your frontend to connect.
npm install express cors

​
Create the main server file: server.js.
Step 1.2: Create Mock Data
Create a new file named mockData.js. This file will hold all your mock JSON objects.
Step 1.3: Define API Endpoints
In server.js, set up Express and define the four required REST endpoints.
Route (Method)
Description
/api/sessions (GET)
Returns a list of all mock session IDs/titles for the sidebar.
/api/new-chat (GET)
Returns a new, unique mock session ID.
/api/session/:id (GET)
Returns the full mock conversation history for a given session ID.
/api/chat/:id (POST)
Accepts a user question and returns a mock structured (tabular) response.
Step 1.4: Start the Server
Add a start script to your package.json (e.g., "start": "node server.js").
Run the server: npm start.
Phase 2: Frontend Setup (React and Styling)
The frontend will handle all UI logic, routing, and API calls.
Step 2.1: Project Initialization
Navigate out of the backend directory and create the frontend project.
cd ..
npx create-react-app frontend --template cra-template-js
cd frontend

​
Install necessary packages: react-router-dom for routing.
npm install react-router-dom

​
Step 2.2: Tailwind CSS Integration
Follow the official documentation to integrate Tailwind CSS into your React project (typically involving npm install -D tailwindcss postcss autoprefixer and configuration files).
Step 2.3: Routing Setup
In src/App.js, use BrowserRouter and Routes to set up two main paths:
/: The Landing Page/New Chat view.
/chat/:sessionId: The main Chat Interface view.
Step 2.4: Build Core Components
Create the main components: Sidebar.js, ChatWindow.js, TableResponse.js, and ThemeToggle.js.
Step 2.5: Implement Theme Toggle
Use React's useState and useEffect hooks to manage a global theme state ('light' or 'dark').
Apply the dark mode class (usually dark) to the highest parent element (e.g., document.documentElement or the main App div).
Phase 3: Integration and Logic
Step 3.1: Session History Retrieval
In Sidebar.js, use fetch to call the backend's /api/sessions on component mount to populate the list of mock sessions.
Step 3.2: New Chat Flow
When the "New Chat" button is clicked:
Call the backend's /api/new-chat to get a new sessionId.
Use useNavigate (from React Router) to redirect the user to /chat/:sessionId.
Step 3.3: Chat Interaction and Structured Data
In ChatWindow.js:
Listen to the URL parameter using useParams() to get the current sessionId.
When the user submits a message, send a POST request to /api/chat/:id with the question.
Receive the response, which should contain both descriptive text and the structured data array.
Render the structured data using the dedicated TableResponse.js component.
4. Project Structure
A clean, modular structure is essential for maintainability.
/chat-app-project
|
├── /backend
|   ├── node_modules/
|   ├── server.js               <-- Express setup and routing
|   ├── mockData.js             <-- All static JSON data
|   ├── package.json
|
└── /frontend
    ├── node_modules/
    ├── package.json
    ├── tailwind.config.js
    └── /src
        ├── /components
        |   ├── Sidebar.js      <-- Collapsible session panel
        |   ├── ThemeToggle.js  <-- Handles Light/Dark switching
        |   ├── ChatInput.js    <-- Component for user text input
        |   ├── TableResponse.js <-- Renders structured data beautifully
        |   └── AnswerFeedback.js <-- Like/Dislike buttons
        ├── App.js              <-- Main component and routing logic
        ├── index.js            <-- Root file
        └── index.css           <-- Base Tailwind CSS imports
