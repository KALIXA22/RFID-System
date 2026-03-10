KALIZ III – Automated Asset Vault System






KALIZ III is a secure, real-time asset management platform designed to monitor, track, and manage high-value items. It features a modern dashboard, role-based access, and integrated transaction tracking.

🚀 Features

Current Exhibits Overview: Card-based visual display of assets with their values.

Acquisition Summary: Shows total asset value dynamically.

Role-Based Access: Officer, operator, technician, researcher, and admin.

Real-Time Updates: Live updates via Socket.IO and MQTT.

System Status Monitoring: Online/offline system status indicators.

Polished UI: Responsive dark theme with intuitive layout for quick insights.

🗂 Project Structure
Payment/
├─ backend/
│  ├─ app.py                # Flask app, routes, Socket.IO & MQTT integration
│  ├─ instance/
│  │  └─ kaliz.db           # SQLite database for assets & transactions
│  └─ templates/
│     ├─ dashboard.html     # Agent/Sales dashboard
│     ├─ admin.html         # Admin data view
│     ├─ login.html         # Main login selector
│     ├─ agent_login.html   # Agent login page
│     └─ sales_login.html   # Sales login page
└─ ESP_RFID/
   └─ ESP_RFID.ino          # ESP8266 + MFRC522 firmware for card scans
⚙ Backend Behavior

Host / Port: 0.0.0.0:9243 (LAN access via http://<your-ip>:9243)

Database: SQLite via Flask-SQLAlchemy (instance/kaliz.db)

Automatic Table Creation: Tables auto-create at startup if missing

Reset Data: Delete instance/kaliz.db to reset assets and transactions

MQTT Broker: broker.benax.rw for real-time RFID card events

🌐 Routes
Method	Route	Description
GET	/	Landing page
GET	/login/agent	Agent login page
POST	/login/agent	Agent authentication
GET	/topup-dashboard	Agent dashboard (top-up flow)
GET	/login/sales	Sales login page
POST	/login/sales	Sales authentication
GET	/payment-dashboard	Sales dashboard (payment flow)
GET	/admin	Admin interface
POST	/asset/add	Add a new asset
POST	/asset/update	Update asset information
POST	/asset/remove	Remove an asset
🖥 Local Setup
# Navigate to backend
cd Payment/backend

# Create & activate virtual environment
python3 -m venv .venv
.venv\Scripts\activate
source .venv/bin/activate

# Install dependencies
pip install -U pip
pip install flask flask-sqlalchemy flask-cors flask-socketio paho-mqtt

# Run backend server
python app.py

Dashboards:

Agent: http://127.0.0.1:9243/topup-dashboard

Sales: http://127.0.0.1:9243/payment-dashboard

🔌 Hardware Integration (Optional)

Open ESP_RFID.ino in Arduino IDE.

Install libraries: ESP8266WiFi, PubSubClient, MFRC522, ArduinoJson.

Configure Wi-Fi & team ID, then flash ESP8266 for live RFID scanning.

🛠 Tech Stack

Backend: Flask, Flask-SocketIO, Flask-SQLAlchemy

Frontend: HTML, Tailwind CSS, JavaScript

Database: SQLite

Messaging: MQTT (real-time card events)

Hardware: ESP8266 + MFRC522 for RFID scanning

⚡ Quick Start

Clone & run in one line:

git clone https://github.com/KALIXA22/KALIZ-III.git && cd KALIZ-III/Payment/backend && python -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt && python app.py

Open dashboards at http://127.0.0.1:9243/topup-dashboard (Agent) or http://127.0.0.1:9243/payment-dashboard (Sales)