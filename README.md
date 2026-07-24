Here is a comprehensive README file that covers everything about your project, including all commands and API examples.

📄 README.md
markdown
# 🌾 WAHA KUN AI - Vision Service

**AI-Powered Irrigation Problem Diagnosis System**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.139.0-green.svg)](https://fastapi.tiangolo.com/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.21.0-orange.svg)](https://www.tensorflow.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 **Table of Contents**

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Installation & Setup](#installation--setup)
- [Run Commands](#run-commands)
- [API Endpoints](#api-endpoints)
- [API Response Examples](#api-response-examples)
- [Severity Levels](#severity-levels)
- [Testing](#testing)
- [Docker Deployment](#docker-deployment)
- [Troubleshooting](#troubleshooting)
- [Contributors](#contributors)
- [License](#license)

---

## 🎯 **Project Overview**

**WAHA KUN AI Vision Service** is a Computer Vision system that analyzes images of irrigation systems and provides a complete diagnosis in Arabic.

### **What It Does:**

| Input | Process | Output |
|-------|---------|--------|
| 📸 Image of irrigation system | AI Model (EfficientNet) analyzes the image | Complete diagnosis in Arabic |

### **Diagnosis Includes:**

| Field | Description | Example |
|-------|-------------|---------|
| **Problem** | Problem name in Arabic | "تلف في أنبوب المياه" |
| **Problem Code** | Problem code in English | `Pipe_Damage` |
| **Confidence** | AI confidence percentage | "77.39%" |
| **Severity** | Urgency level | "حرجة" (Critical) |
| **Recommendation** | What to do | "يوصى بإيقاف مصدر المياه فوراً" |
| **Explanation** | Why AI made this diagnosis | "اكتشف النموذج وجود تلف..." |
| **Repair Steps** | Step-by-step guide | 7 step repair process |

---

## ✨ **Key Features**

| Feature | Description |
|---------|-------------|
| **🖼️ Image Analysis** | Analyzes images of irrigation systems |
| **🤖 AI Model** | Uses EfficientNet deep learning model |
| **📊 Confidence Scoring** | Shows AI confidence percentage (0-100%) |
| **⚠️ Severity Assessment** | 5 levels from Critical to Minor |
| **📝 Repair Steps** | Step-by-step repair instructions |
| **🔍 Quality Check** | Validates image quality automatically |
| **✨ Image Enhancement** | Auto-enhances poor quality images |
| **⚡ Async Processing** | RabbitMQ for background processing |
| **🐳 Docker Support** | Easy deployment with Docker |
| **🌐 Arabic Output** | All responses in Arabic |
| **🚫 No Problem Detection** | Refuses images with no clear problem |

---

## 🏗️ **System Architecture**
┌─────────────────────────────────────────────────────────────────────────┐
│ WAHA KUN AI Vision Service │
├─────────────────────────────────────────────────────────────────────────┤
│ │
│ ┌─────────────────────────────────────────────────────────────────┐ │
│ │ API Layer (FastAPI) │ │
│ │ • POST /api/v1/predict → Synchronous prediction │ │
│ │ • POST /api/v1/predict-async → Asynchronous prediction │ │
│ │ • GET /health → Health check │ │
│ │ • GET / → Service info │ │
│ │ • GET /docs → Swagger documentation │ │
│ └─────────────────────────────────────────────────────────────────┘ │
│ │ │
│ ▼ │
│ ┌─────────────────────────────────────────────────────────────────┐ │
│ │ Core Layer (Business Logic) │ │
│ │ • model.py → AI Model (EfficientNet) │ │
│ │ • severity.py → Basic severity calculation │ │
│ │ • severity_enhanced.py → Enhanced severity (7 factors) │ │
│ │ • problem_info.py → Knowledge base │ │
│ │ • knowledge_base.py → RAG system │ │
│ └─────────────────────────────────────────────────────────────────┘ │
│ │ │
│ ▼ │
│ ┌─────────────────────────────────────────────────────────────────┐ │
│ │ Infrastructure Layer │ │
│ │ • config.py → Configuration management │ │
│ │ • logger.py → Logging setup │ │
│ │ • queue_broker.py → RabbitMQ connection │ │
│ │ • utils.py → Image processing utilities │ │
│ │ • validators.py → File validation │ │
│ └─────────────────────────────────────────────────────────────────┘ │
│ │ │
│ ▼ │
│ ┌─────────────────────────────────────────────────────────────────┐ │
│ │ Worker Layer (Background) │ │
│ │ • worker.py → Background task processing │ │
│ │ • RabbitMQ → Message queue for async processing │ │
│ └─────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘

text

---

## 📂 **Project Structure**
GRADUATION_PROJECT/
└── VisionService/
├── docker/ # Docker files
│ ├── Dockerfile
│ └── docker-compose.yml
│
├── models/ # AI Model
│ └── efficientnet_waha_kun.keras
│
├── test_images/ # Test images
├── uploads/ # Temporary uploads
├── logs/ # Log files
│
└── VisionService/ # Main Python package
├── API/ # API Layer (FastAPI)
│ ├── init.py
│ ├── app.py # Main entry point
│ ├── routes.py # API endpoints
│ ├── schemas.py # Data models
│ ├── dependencies.py # Dependency injection
│ └── middleware.py # CORS middleware
│
├── Core/ # Core Business Logic
│ ├── init.py
│ ├── model.py # AI Model loading & prediction
│ ├── severity.py # Basic severity calculation
│ ├── severity_enhanced.py # Enhanced severity (7 factors)
│ ├── problem_info.py # Knowledge database
│ ├── knowledge_base.py # RAG system
│ └── interfaces.py # Interfaces for testing
│
├── Infrastructure/ # External Dependencies
│ ├── init.py
│ ├── config.py # Configuration
│ ├── logger.py # Logging setup
│ ├── queue_broker.py # RabbitMQ connection
│ ├── utils.py # Image processing utilities
│ └── validators.py # File validation
│
├── Shared/ # Shared Constants
│ ├── init.py
│ ├── constants.py # Shared constants
│ ├── enums.py # Enumerations
│ └── exceptions.py # Custom exceptions
│
├── Worker/ # Background Worker
│ ├── init.py
│ └── worker.py # Async task processor
│
├── knowledge_docs/ # RAG Knowledge Documents
│ ├── pipe_damage.txt
│ ├── overflow.txt
│ ├── blockage.txt
│ └── expert_advice.txt
│
├── .env # Environment variables
├── .env.example # Environment template
├── .gitignore # Git ignore
└── requirements.txt # Python dependencies

text

---

## 🛠️ **Technologies Used**

| Category | Technology | Version |
|----------|------------|---------|
| **Language** | Python | 3.10+ |
| **Web Framework** | FastAPI | 0.139.0 |
| **AI/ML** | TensorFlow | 2.21.0 |
| **AI Model** | EfficientNet | Pre-trained |
| **Image Processing** | Pillow | 12.3.0 |
| **Numerical Computing** | NumPy | 2.4.6 |
| **Message Queue** | RabbitMQ | 3.x |
| **Async Communication** | Pika | 1.3.2 |
| **Containerization** | Docker | Latest |
| **Logging** | Python Logging | Built-in |

---

## 🚀 **Installation & Setup**

### **Prerequisites**

- ✅ Python 3.10 or higher
- ✅ Docker Desktop (for RabbitMQ)
- ✅ Git

### **Step 1: Clone the Repository**

```bash
git clone https://github.com/malak-wq/vision-service.git
cd vision-service
Step 2: Create and Activate Virtual Environment
bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
Step 3: Install Dependencies
bash
pip install -r requirements.txt
Step 4: Set Up Environment Variables
bash
# Copy the example environment file
cp .env.example .env

# Edit .env if needed (defaults are fine)
Step 5: Start RabbitMQ
bash
# Start RabbitMQ container
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management
▶️ Run Commands
Option 1: Run with Docker (Recommended)
bash
# Navigate to project
cd D:\Graduation_Project\VisionService

# Build and run everything
docker-compose -f docker/docker-compose.yml up --build

# Run in background
docker-compose -f docker/docker-compose.yml up -d --build

# Stop everything
docker-compose -f docker/docker-compose.yml down
Option 2: Run Locally
Terminal 1: Run API
bash
# Navigate to project
cd D:\Graduation_Project\VisionService

# Activate virtual environment
venv\Scripts\activate

# Set PYTHONPATH
$env:PYTHONPATH = "D:\Graduation_Project\VisionService"

# Run the API
uvicorn VisionService.API.app:app --host 127.0.0.1 --port 8001
Terminal 2: Run Worker
bash
# Navigate to project
cd D:\Graduation_Project\VisionService

# Activate virtual environment
venv\Scripts\activate

# Set PYTHONPATH
$env:PYTHONPATH = "D:\Graduation_Project\VisionService"

# Run the worker
python -m VisionService.Worker.worker
📡 API Endpoints
Method	Endpoint	Description
GET	/health	Service health check
GET	/	Service information
POST	/api/v1/predict	Synchronous prediction (1-3s)
POST	/api/v1/predict-async	Asynchronous prediction (RabbitMQ)
GET	/docs	Swagger API documentation
📊 API Response Examples
1. Health Check
bash
curl http://localhost:8001/health
Response:

json
{
  "status": "healthy",
  "service": "vision-service",
  "version": "1.0.0",
  "model_loaded": true,
  "rabbitmq": "connected",
  "timestamp": "2026-07-24T10:00:00.000000"
}
2. Service Info
bash
curl http://localhost:8001/
Response:

json
{
  "service": "vision-service",
  "version": "1.0.0",
  "description": "Computer Vision for irrigation problem diagnosis",
  "endpoints": {
    "/api/v1/predict": "POST - Synchronous prediction (1-3s)",
    "/api/v1/predict-async": "POST - Asynchronous prediction (RabbitMQ)",
    "/health": "GET - Service health check",
    "/docs": "GET - API documentation"
  },
  "rabbitmq": {
    "host": "localhost",
    "port": 5672,
    "queues": {
      "requests": "vision.prediction.requests",
      "results": "vision.prediction.results"
    }
  },
  "timestamp": "2026-07-24T10:00:00.000000"
}
3. Synchronous Prediction (Success)
bash
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict
Response (Success):

json
{
  "status": "success",
  "problem": "تلف في أنبوب المياه",
  "problem_code": "Pipe_Damage",
  "confidence": "77.39%",
  "severity": "حرجة",
  "recommendation": "يوصى بإيقاف مصدر المياه فوراً ثم إصلاح أو استبدال الجزء التالف من الأنبوب.",
  "explanation": "اكتشف نموذج الذكاء الاصطناعي وجود تلف في أحد أنابيب شبكة الري بعد تحليل الصورة. استند القرار إلى خصائص بصرية مشابهة للصور التي تدرب عليها النموذج، مثل وجود تشققات أو كسور أو آثار تسرب للمياه. قد يؤدي هذا العطل إلى فقدان كميات كبيرة من المياه وانخفاض كفاءة الري إذا لم يتم إصلاحه بسرعة.",
  "repair_steps": [
    "إيقاف مصدر المياه.",
    "تحديد مكان التلف.",
    "فحص الأنبوب بالكامل.",
    "استبدال أو إصلاح الجزء التالف.",
    "إعادة تشغيل المياه.",
    "اختبار شبكة الري.",
    "التأكد من عدم وجود أي تسرب."
  ],
  "timestamp": "2026-07-24T10:00:00.000000"
}
4. Synchronous Prediction (Refused - No Problem)
bash
curl -X POST -F "file=@test_images/no_problem.jpg" http://localhost:8001/api/v1/predict
Response (Refused):

json
{
  "status": "refused",
  "message": "لم يتم الكشف عن مشكلة واضحة في الصورة.",
  "confidence": "45.23%",
  "suggestion": "يرجى رفع صورة توضح مكان المشكلة بشكل أفضل.",
  "timestamp": "2026-07-24T10:00:00.000000"
}
5. Synchronous Prediction (Uncertain)
bash
curl -X POST -F "file=@test_images/unclear.jpg" http://localhost:8001/api/v1/predict
Response (Uncertain):

json
{
  "status": "uncertain",
  "message": "الصورة غير واضحة أو لا تظهر مشكلة محددة بوضوح.",
  "confidence": "58.00%",
  "suggestion": "يرجى رفع صورة أوضح أو التأكد من وجود مشكلة.",
  "timestamp": "2026-07-24T10:00:00.000000"
}
6. Asynchronous Prediction
bash
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict-async
Response (Accepted):

json
{
  "status": "accepted",
  "request_id": "abc12345",
  "message": "Request accepted for processing. Result will be delivered asynchronously via RabbitMQ.",
  "queue": "vision.prediction.results",
  "timestamp": "2026-07-24T10:00:00.000000"
}
Result delivered later via RabbitMQ:

json
{
  "request_id": "abc12345",
  "success": true,
  "result": {
    "problem": "تلف في أنبوب المياه",
    "problem_code": "Pipe_Damage",
    "confidence": 77.39,
    "severity": "حرجة",
    "recommendation": "...",
    "explanation": "...",
    "repair_steps": [...]
  },
  "processing_time": 2.3,
  "timestamp": "..."
}
📊 Severity Levels
Level (Arabic)	Level (English)	Score Range	Urgency	Recommended Action
حرجة جداً	Very Critical	95-100	Within 1 hour	Call emergency team IMMEDIATELY
حرجة	Critical	80-94	Within 4 hours	Call repair team within 4 hours
عالية جداً	Very High	70-79	Within 12 hours	Schedule emergency repair
عالية	High	60-69	Within 24 hours	Schedule repair within 24 hours
متوسطة	Medium	45-59	Within 48 hours	Plan repair within 48 hours
منخفضة	Low	30-44	Within 1 week	Monitor and repair within 1 week
بسيطة	Minor	20-29	Next maintenance	Include in next maintenance
بسيطة جداً	Very Minor	10-19	Schedule later	Schedule when convenient
غير مؤثرة	Negligible	0-9	No action	No action needed
🧪 Testing
Test Commands
bash
# 1. Health Check
curl http://localhost:8001/health

# 2. Service Info
curl http://localhost:8001/

# 3. Synchronous Prediction (with problem)
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict

# 4. Synchronous Prediction (no problem)
curl -X POST -F "file=@test_images/no_problem.jpg" http://localhost:8001/api/v1/predict

# 5. Asynchronous Prediction
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict-async

# 6. Swagger UI
# Open in browser: http://localhost:8001/docs

# 7. RabbitMQ UI
# Open in browser: http://localhost:15672
# Login: guest / guest
Test Images
Place test images in the test_images/ folder:

text
test_images/
├── pipe_damage.jpg      # Image with pipe damage
├── overflow.jpg         # Image with overflow
├── blockage.jpg         # Image with blockage
├── no_problem.jpg       # Image with no problem
├── unclear.jpg          # Blurry or unclear image
└── dark.jpg             # Dark image
🐳 Docker Deployment
Docker Compose Commands
bash
# Navigate to project
cd D:\Graduation_Project\VisionService

# Build and run
docker-compose -f docker/docker-compose.yml up --build

# Run in background
docker-compose -f docker/docker-compose.yml up -d --build

# View logs
docker-compose -f docker/docker-compose.yml logs -f

# Stop containers
docker-compose -f docker/docker-compose.yml down

# Stop and remove volumes
docker-compose -f docker/docker-compose.yml down -v
Docker Commands
bash
# Build image
docker build -f docker/Dockerfile -t vision-service .

# Run container
docker run -p 8001:8001 vision-service

# Check running containers
docker ps

# Stop container
docker stop vision-service
❌ Troubleshooting
1. ModuleNotFoundError
bash
# Set PYTHONPATH
$env:PYTHONPATH = "D:\Graduation_Project\VisionService"

# Or run with Python module
python -m uvicorn VisionService.API.app:app --host 127.0.0.1 --port 8001
2. Port 8001 Already in Use
bash
# Find and kill process
netstat -ano | findstr :8001
taskkill /PID [PID] /F

# Or use different port
uvicorn VisionService.API.app:app --host 127.0.0.1 --port 8002
3. RabbitMQ Connection Refused
bash
# Check if RabbitMQ is running
docker ps | findstr rabbitmq

# Start RabbitMQ
docker start rabbitmq

# Or restart
docker rm -f rabbitmq
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management
4. Model File Not Found
bash
# Check if model exists
ls models\efficientnet_waha_kun.keras

# If not, place your model in the models folder
5. Dependency Installation Fails
bash
# Upgrade pip
python -m pip install --upgrade pip

# Install with no cache
pip install --no-cache-dir -r requirements.txt

# Install one by one
pip install fastapi uvicorn tensorflow numpy pillow pika
📋 Environment Variables
Variable	Default	Description
SERVICE_NAME	vision-service	Service name
SERVICE_VERSION	1.0.0	Service version
HOST	0.0.0.0	Host address
PORT	8001	Port number
DEBUG	true	Debug mode
MODEL_PATH	./models/efficientnet_waha_kun.keras	Model file path
CONFIDENCE_THRESHOLD	50.0	Minimum confidence
UPLOAD_FOLDER	./uploads	Upload folder
MAX_FILE_SIZE	10485760	Max file size (10 MB)
RABBITMQ_HOST	localhost	RabbitMQ host
RABBITMQ_PORT	5672	RabbitMQ port
RABBITMQ_USER	guest	RabbitMQ username
RABBITMQ_PASSWORD	guest	RabbitMQ password
👥 Contributors
Name	Role	GitHub
Malak Ragab	Developer	@malak-wq
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🙏 Acknowledgments
TensorFlow for the deep learning framework

FastAPI for the web framework

RabbitMQ for message queuing

EfficientNet for the pre-trained model

📞 Contact
GitHub: @malak-wq

Email: ragabmalak581@gmail.com

⭐ Star the Project
If you found this project useful, please give it a ⭐ on GitHub!

Made with ❤️ by Malak Ragab

text

---

## 🚀 **How to Add README to GitHub**

### **Step 1: Create README.md**

```bash
# Navigate to project
cd D:\Graduation_Project\VisionService

# Create README file
notepad README.md
Copy the entire content above into the file and save.

Step 2: Add and Commit
bash
# Add README
git add README.md

# Commit
git commit -m "Add comprehensive README.md with project documentation"

# Push to GitHub
git push
Step 3: Verify
Visit your GitHub repository:

text
https://github.com/malak-wq/vision-service
You should see the README displayed beautifully on the main page.

✅ Summary
Section	Content
Project Overview	What the project does
Key Features	All features listed
Architecture	System architecture diagram
Structure	Complete project structure
Technologies	Technologies used
Installation	Step-by-step setup
Run Commands	All run commands
API Endpoints	All endpoints with examples
Response Examples	All response types
Severity Levels	All severity levels
Testing	Test commands
Docker	Docker commands
Troubleshooting	Common issues and solutions
