# 📚 Tunwase Library Portal (TLP)

A lightweight, high-performance, fully offline management system engineered to deliver smooth, modern library automation on legacy hardware targets (optimized for systems with down to **2GB of RAM**).

---

## 🛠️ The Problem & Real-World Constraints
Most modern school library software requires heavy server background setups (like Koha) or constant internet connectivity. Tunwase High School required a digital transition that could run on local workstation terminals with the following strict limits:
1. **Network Isolation:** 100% offline execution. No external CDNs, API hooks, or cloud dependencies.
2. **Hardware Restrictions:** Must maintain a minimal memory footprint to run smoothly alongside host processes on a 2GB RAM budget.
3. **Firewall/Port Blocks:** Overcame rigid network security policies by completely eliminating the Node.js production runtime requirement and utilizing a single-port architecture.

---

## 🚀 Key Engineering Solutions Built

### ⚡ Single-Port Production Architecture
Instead of running a separate frontend Node/Vite server and a backend Python server, the React frontend is compiled into ultra-lean static assets (`npm run build`). These assets are mounted and served directly from the FastAPI backend at the root path:
``python
app.mount("/", StaticFiles(directory="../frontend/dist", html=True), name="static")``

Impact: Reduced production RAM overhead by roughly 150MB and dropped the requirement for Node.js on the production machine entirely.

🔍 Dynamic Port Auto-Discovery
To bypass rigid firewall blocks and port collisions on the school PC, the application runner uses a native Python socket scan starting at port 8085. It dynamically binds to the first open, available local port and instantly launches the host browser using webbrowser.open().

📦 Network-Isolated Deployment Automation
install_dependencies.bat: An automated script that leverages a local directory of pre-downloaded wheel files (.whl) on a flash drive to install the complete Python ecosystem (FastAPI, SQLAlchemy, Uvicorn) entirely offline using:
pip install --no-index --find-links=./wheels -r requirements.txt

create_shortcut.bat: A script that programmatically detects the installation path on the host PC and places a working native application shortcut directly onto the librarian's Windows Desktop.

🧮 Tech Stack & Systems Architecture
Frontend: React.js, Tailwind CSS (Custom Dark IDE Theme Matrix using Wine Red #722F37 and Amber #D97706 premium accents).

Charts & Metrics: Built using native HTML5 Canvas / Inline SVGs to enforce a 0MB JS library footprint on the UI dashboard.

Backend: FastAPI (Python 3.11+), Uvicorn.

Database: SQLite (Configured with custom SQLAlchemy event connection listeners to strictly enforce PRAGMA foreign_keys = ON; relational integrity).

📝 Future Roadmap / Active Issues

[x] Phase 1-4: Core Backend Plumbing, Single-Port Serving, and Dynamic Port Routing.

[x] Phase 5: Testing local batch script shortcut compilation across diverse Windows builds.

[x] Phase 6: Final Polish on the Premium Dark Dashboard micro-animations.
(completed as at 18/06/2026)

**Developed by the Coding Club of Tunwase High School.**

`Led by Jeffrey Feyisetan, _The President_`
