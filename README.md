# FACULTY CONNECT
> **Tagline:** Making Academic Communication Smarter, Faster and More Organised.  
> **Course:** INT335 Design Thinking Group Innovation Project  
> **Institution:** Lovely Professional University (LPU)  
> **Project ID:** P09  
> **Official Project Title:** Heard in Class, Lost After  
> **Project Domain:** Faculty–Student Academic Communication Outside Lectures  

---

## 1. Project Overview & Problem Solved

Students at Lovely Professional University (LPU) frequently face significant hurdles when seeking academic assistance outside regular lecture hours:
- **Unpredictable Faculty Availability:** Students often visit faculty cabins without knowing consultation schedules.
- **Scattered Communication Channels:** Messages distributed across WhatsApp groups, UMS announcements, and physical cabin visits lead to lost doubts.
- **Repetitive Questions:** Faculty members receive dozens of identical or slightly reworded academic questions from students across multiple sections.
- **Delayed Doubt Resolution:** Questions go unanswered for days, causing bottlenecks ahead of continuous assessments (CAs) and end-term exams.

**Faculty Connect** provides a centralized, intelligent academic assistance platform that:
1. **Intelligently detects duplicate doubts** scoped by section, subject, unit, and topic using semantic similarity.
2. **Features a "+1 – I Have the Same Doubt" mechanism**, allowing classmates to endorse existing doubts and receive answer notifications without flooding faculty queues.
3. **Implements a reliable 3-hour server-side AI fallback mechanism** that provides preliminary syllabus-grounded academic answers if a professor is temporarily unavailable.
4. **Organizes faculty availability and cabin consultation bookings** with conflict prevention and capacity control.
5. **Provides empirical, section-wise confusion analytics** derived directly from database records.
6. **Delivers 3 unified experiences:** Laptop-optimized SaaS desktop, mobile-first responsive web, and an installable Progressive Web Application (PWA) for Chrome.

---

## 2. Design System & Fixed Color Palette

The entire user interface strictly follows the designated color palette without unauthorized neons or gradients:

| Token | Hex Value | Usage |
|---|---|---|
| **Primary Navigation Green** | `#15370D` | Navbar, primary action buttons, active navigation states, headers |
| **Background Cream** | `#FCF9EA` | Application background, subtle card surface, modal backdrops |
| **Orange Accent** | `#F2842F` | Active indicators, notification badges, duplicate highlights, action sparks |
| **Primary Text & Dark Lines** | `#000000` | Headings, body typography, borders, high-contrast markers |

---

## 3. Verified Syllabus Source of Truth

The academic syllabus was extracted directly from the official PDF documents located in the workspace folder `All subjects syllabus`:

1. **INT335: Design Thinking** (2 Credits, `L:2 T:0 P:0`)
   - Unit I: Foundations of Learning, Creativity and Design Thinking
   - Unit II: Empathy, Observation and Problem Identification (AEIOU, User Personas)
   - Unit III: Ideation and Creative Problem Solving (SCAMPER, Divergent/Convergent)
   - Unit IV: Product Design and Prototyping (Wireframing, MVP)
   - Unit V: Testing, Validation and Customer Experience
   - Unit VI: Innovation Project, Re-Design and Product Presentation
2. **CSE316: Operating Systems** (3 Credits, `L:3 T:0 P:0`)
   - Unit I: OS Structures & Process Management
   - Unit II: CPU Scheduling (Round Robin, FCFS, SJF, Priority, Multilevel Feedback)
   - Unit III: Process Synchronization & Threads (Semaphores, Dining Philosophers)
   - Unit IV: Deadlock & Protection (Coffman conditions, Banker's Algorithm)
   - Unit V: Memory Management (Paging, Segmentation, Virtual Memory)
   - Unit VI: File & Device Management, IPC (Pipes, Shared Memory, Message Queues)
3. **CSM228: Data Structures** (4 Credits, `L:3 T:0 P:2`)
   - Stacks, Queues, HashTables, HashMaps, HashSets, BSTs, Priority Queues, Heaps, Graphs (Dijkstra)
4. **CSM229: Programming in Java** (4 Credits, `L:3 T:0 P:2`)
   - Java Core, Control Structures, OOP, Inheritance/Polymorphism, Collections, Stream API, JDBC
5. **MTH401: Discrete Mathematics** (4 Credits, `L:3 T:1 P:0`)
   - Logic & Proofs, Recurrence Relations, Counting Principles, Graph Theory, Number Theory (Euclidean & Bezout)
6. **CSE325: Operating Systems Laboratory** (1 Credit, `L:0 T:0 P:2`)
   - Linux Shell Scripting, System Calls (`fork`, `exec`), POSIX Threads, Semaphores, IPC
7. **CSM216: Python Project** (2 Credits, `L:0 T:0 P:3`)
   - Algorithmic Thinking, Tkinter GUI, Pygame Foundations, Data Science Stack

---

## 4. Architecture & Technical Stack

```
   ┌─────────────────────────────────────────────────────────┐
   │                  CLIENT EXPERIENCES                     │
   │  Laptop Desktop (SaaS) • Mobile-First PWA • Chrome App  │
   │      (React 19, TypeScript, Tailwind CSS, Vite)         │
   └───────────────────────────┬─────────────────────────────┘
                               │ HTTP / REST / JSON
                               ▼
   ┌─────────────────────────────────────────────────────────┐
   │                     FLASK BACKEND                       │
   │  • RESTful API (Flask + CORS)                           │
   │  • Smart Doubt Engine (Academic Semantic Similarity)    │
   │  • 3-Hour AI Timer Scheduler (Server Daemon Thread)     │
   │  • Session & Role-Based Access Control                  │
   └───────────────┬─────────────────────────┬───────────────┘
                   │                         │
                   ▼                         ▼
   ┌──────────────────────────────┐  ┌─────────────────────────┐
   │     SQL DATABASE ENGINE      │  │     ACADEMIC AI CORE    │
   │  • SQLite (Default Out-of-   │  │  • Syllabus Synthesizer │
   │    the-box Zero-Config)      │  │  • Gemini 1.5 Flash API │
   │  • MySQL / PyMySQL Supported │  │    (Configurable)       │
   └──────────────────────────────┘  └─────────────────────────┘
```

---

## 5. Step-by-Step Installation & Setup

### Prerequisites
- **Python 3.10+** (Python 3.11 recommended)
- **Node.js 18+** and **npm**

### 1. Install Backend Dependencies
```bash
pip install flask flask-cors sqlalchemy werkzeug python-dotenv requests
```

### 2. Configure Environment Variables
Copy `backend/.env.example` to `backend/.env` (pre-configured with sensible defaults):
```bash
cd backend
cp .env.example .env
```
Key configuration parameters:
- `PORT=5000`
- `DATABASE_URL=sqlite:///faculty_connect.db` *(or `mysql+pymysql://user:pwd@localhost:3306/faculty_connect`)*
- `AI_ANSWER_DELAY_HOURS=3.0` *(Default 3 hours for the automatic AI response)*
- `DUPLICATE_SIMILARITY_THRESHOLD=0.60`
- `GEMINI_API_KEY=` *(Optional: leave blank to run syllabus-grounded synthesizer)*

### 3. Initialize & Seed Database
Run the seed script to import official syllabus structures and realistic sample demonstration records:
```bash
cd backend
python seed_data.py
```

### 4. Install Frontend Dependencies & Build
```bash
cd frontend
npm install
npm run build
```

### 5. Running the Application

#### Option A: Unified Server (Recommended)
Flask serves both the REST API and the compiled React production application simultaneously:
```bash
cd backend
python app.py
```
Open **`http://localhost:5000`** in Google Chrome.

#### Option B: Independent Vite Hot-Reloading Development Server
In Terminal 1 (Backend):
```bash
cd backend
python app.py
```
In Terminal 2 (Frontend):
```bash
cd frontend
npm run dev
```
Open **`http://localhost:3000`** in your browser.

---

## 6. Accessing Student & Faculty Portals

### Student Portal Access
1. Open the landing screen.
2. Select **1. STUDENT PANEL**.
3. Enter student name and choose your section:
   - **Aman Choudhary** (Section `K22DF`)
   - **Priya Sharma** (Section `K22DF`)
   - **Rohan Patel** (Section `K22GF`)
4. Click **Enter Student Portal**.

### Teacher Console Access (Secure Hashed Credentials)
1. Open the landing screen.
2. Select **2. TEACHER PANEL**.
3. Use pre-configured faculty accounts (default password: `faculty123`):
   - **Dr. Rajesh Sharma** (INT335 Design Thinking Lead)  
     Email: `dr.rajesh@lpu.co.in` | Pwd: `faculty123` | Cabin: Block 34-601
   - **Dr. Harpreet Kaur** (CSE316 Operating Systems)  
     Email: `dr.harpreet@lpu.co.in` | Pwd: `faculty123` | Cabin: Block 38-402
   - **Prof. Amit Verma** (CSM228 Data Structures & Java)  
     Email: `prof.verma@lpu.co.in` | Pwd: `faculty123` | Cabin: Block 34-405
   - **Dr. Neha Gupta** (MTH401 Discrete Mathematics)  
     Email: `dr.neha@lpu.co.in` | Pwd: `faculty123` | Cabin: Block 36-201
   - **Prof. Gurpreet Singh** (CSM216 Python Project)  
     Email: `prof.singh@lpu.co.in` | Pwd: `faculty123` | Cabin: Block 34-312

*Tip:* Use the floating **INT335 Demo Bar** on the bottom-right of the screen for instant 1-click account switching during evaluation!

---

## 7. Installing Faculty Connect as a Chrome PWA

Faculty Connect includes a Web App Manifest (`manifest.json`), service worker (`sw.js`), and SVG application icons:
1. Open `http://localhost:5000` (or `http://localhost:3000`) in **Google Chrome**.
2. Click the **"Install App"** button in the top navigation bar, or click the **Install icon (⊕)** on the right side of the Chrome address bar.
3. Click **Install**.
4. Faculty Connect will launch as a standalone desktop/mobile app window without browser URL bars, complete with offline shell caching.

---

## 8. Verifying Core Evaluator Workflows

### Workflow 1: Smart Duplicate Question Detection & "+1"
1. Log in as student **Priya Sharma** (Section `K22DF`).
2. Click **Ask a Doubt**.
3. Choose:
   - Subject: `CSE316: Operating Systems`
   - Unit: `Unit II: CPU Scheduling`
   - Topic: `CPU Scheduling Principles & Algorithms`
   - Date: Select today's date
4. Type: *"What is the purpose of time quantum in Round Robin scheduling?"*
5. Click **Next: Check & Submit**.
6. **Smart Doubt Engine Triggers:** The screen displays:  
   *"A similar doubt has already been submitted!"*  
   Shows classmate Aman Choudhary's question and the existing faculty answer.
7. Click **OPTION 1: +1 – I HAVE THE SAME DOUBT**.  
   The supporter count increments, linking Priya to the question without creating duplicate notification clutter.

### Workflow 2: 3-Hour Automatic AI Response Mechanism
1. Log in as student **Rohan Patel** (Section `K22GF`).
2. Ask a new query on `CSM229: Programming in Java` -> Unit IV -> `Inheritance and Polymorphism`.
3. Question enters faculty queue with a 3-hour timer deadline.
4. Open the floating **INT335 Demo Bar** on the bottom right and click **Trigger 3-Hour AI Check** (simulates the 3-hour timer expiration).
5. Open **My Questions**: The doubt is now marked **`AI Answered`** with a preliminary syllabus-grounded academic response.
6. Switch to faculty **Prof. Amit Verma**: The question remains in the faculty queue for official review and quality evaluation (`Correct`, `Needs Correction`, etc.).

### Workflow 3: Faculty Consultation Slot Booking
1. As student, navigate to **Faculty Availability**.
2. Find **Dr. Rajesh Sharma (Block 34, Cabin 601)** and click **Book Slot**.
3. Select an upcoming date, write a consultation reason, and click **Confirm Booking**.
4. Switch to **Dr. Rajesh Sharma** in the teacher console -> **Appointments**.
5. Click **Accept Slot** and add a note (*"Bring your wireframe sketches"*).
6. Student receives an in-app notification confirming the accepted booking.

### Workflow 4: Advanced Empirical Analytics
1. As faculty, open **Advanced Analytics**.
2. Review **Section-Wise Breakdown** (`K22DF` vs `K22GF` vs `K22SE`), **Course Query Distribution**, **Topic-Wise Confusion Impact Ranking**, and **Response-Time Metrics**.
3. Click **Export Analytics CSV** to download `FacultyConnect_Academic_Doubts_Report.csv`.

---

## 9. Resetting Demonstration Data
To restore the platform to its pristine demonstration state at any time:
- In the UI: Click **Reset Demonstration Data** in the floating INT335 Demo Bar.
- Via CLI: Run `python backend/seed_data.py`.
- Via API: Send a POST request to `/api/demo/reset`.

---

## 10. Group Innovation Credentials & Team Members
- **Course & Project:** INT335 Design Thinking Group Innovation Project (ID: P09)
- **Official Domain:** Faculty–Student Academic Communication Outside Lectures
- **Institution:** Lovely Professional University (LPU), Punjab
- **Academic Year:** 2026–2027

### Project Team Members:
1. **Aryan Singh** — Registration Number: `12516621`
2. **Kaya Hamir Reddy** — Registration Number: `12516680`
3. **Aditya Tiwari** — Registration Number: `12516873`
4. **Susmit Choudhury** — Registration Number: `12517025`

---

## 11. Cloud Deployment Guide (Free & Instant)
This application is fully production-ready with zero hardcoded URLs. It can be deployed in under 2 minutes on **Render**, **Railway**, or **Fly.io** with free automatic HTTPS (enabling the Chrome PWA "Install App" button):

### Deploying to Render.com (Recommended Free Hosting):
1. Sign in to [Render.com](https://render.com) using your GitHub account.
2. Click **New +** -> **Web Service**.
3. Select this repository: `SusmitChoudhury/FACULTY-CONNECT`.
4. Configure service details:
   - **Name:** `faculty-connect`
   - **Environment:** `Python 3`
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn --chdir backend app:app --bind 0.0.0.0:$PORT`
5. Click **Create Web Service**.
6. Render builds and deploys your application on a free HTTPS URL (e.g. `https://faculty-connect.onrender.com`).
7. Open the URL in Google Chrome -> Click the **Install** button in the address bar to install the Progressive Web Application (PWA)!
