# 🗓️ Day 1 — Data Engineering Environment Setup

**Date:** November 4, 2025**  
**Apprenticeship:** Data Engineering (SQL | Python | PySpark | Azure | Power BI | PostgreSQL)

---

## 🎯 Objective
Set up a complete local data engineering environment with Python, PostgreSQL, Git, and VS Code.  
Learn why each tool and command matters, and confirm Python ↔ PostgreSQL connectivity.

---

## 🧰 Tools Installed
| Tool | Purpose |
|------|----------|
| **Python 3.13.9 (64-bit)** | Core programming language for data engineering |
| **VS Code 1.105.1** | IDE for Python, SQL, and Markdown |
| **Git 2.51.2** | Version control for managing project versions |
| **PostgreSQL 16 + pgAdmin 4** | SQL database for analytics and ETL practice |
| **Power BI Desktop** | Reporting & dashboarding |
| **Azure Free Account** | Future cloud integration |
| **Python Libraries:** pandas, psycopg2-binary, SQLAlchemy, Jupyter | Core Python ecosystem for ETL and database operations |

---

## 📁 Project Structure
**Folder Path:** `C:\Users\Madhu\Documents\retailx-analytics`

retailx-analytics/
┣ data/
┣ notebooks/
┣ sql/
┣ src/
┣ docs/
┗ README.md

yaml
Copy code

**Why:**  
This structure separates raw data, notebooks, SQL scripts, source code, and documentation — mirroring professional data engineering projects.

---

## ⚙️ Commands Used and Why

### 🐍 Python Version Check
```powershell
python --version
✅ Confirms Python is installed and accessible globally.

💻 Git Initialization
powershell
Copy code
git init
git add .
git commit -m "Initial project structure"
Why:

git init starts tracking your project.

git add . stages all files.

git commit records a snapshot (checkpoint) in history.

🧾 Git Identity Setup
powershell
Copy code
git config --global user.name "Madhu Gundoji"
git config --global user.email "madhu.datadev@gmail.com"
✅ Ensures every commit is labeled with your name and email for version tracking.

🙈 .gitignore File
powershell
Copy code
echo venv/ > .gitignore
echo __pycache__/ >> .gitignore
echo data/ >> .gitignore
Why: Keeps unnecessary or sensitive files (like data, venv) out of Git commits.

☁️ Connecting to GitHub
powershell
Copy code
git remote add origin https://github.com/<yourusername>/retailx-analytics.git
git branch -M main
git push -u origin main
✅ Backs up your work to GitHub and enables collaboration.

🧩 Virtual Environment Setup
powershell
Copy code
python -m venv venv
Why: Creates an isolated Python environment just for this project.
Prevents dependency conflicts between projects.

⚡ Activating the Environment (PowerShell)
powershell
Copy code
.\venv\Scripts\Activate
If PowerShell blocks it:

powershell
Copy code
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
Why: PowerShell requires .\ to explicitly run local scripts for security reasons.

📦 Installing Core Packages
powershell
Copy code
pip install pandas psycopg2-binary sqlalchemy jupyter
Why Each Library:

pandas → handle dataframes & CSVs

psycopg2-binary → connect Python to PostgreSQL

SQLAlchemy → manage database operations

Jupyter → run notebooks interactively

🐘 PostgreSQL Connection Test
File: src/test_connection.py

python
Copy code
import psycopg2

try:
    conn = psycopg2.connect(
        dbname="postgres",
        user="postgres",
        password="Admin@123",  # replace with your password
        host="localhost",
        port="5432"
    )
    print("✅ Connection successful!")
    conn.close()
except Exception as e:
    print("❌ Connection failed:")
    print(e)
Output:

pgsql
Copy code
✅ Connection successful!
✅ Confirms your Python → PostgreSQL connection works perfectly.