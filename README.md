
# 🌾 WAHA KUN AI - Vision Service

**AI-Powered Irrigation Problem Diagnosis System**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.139.0-green.svg)](https://fastapi.tiangolo.com/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.21.0-orange.svg)](https://www.tensorflow.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue.svg)](https://www.docker.com/)

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
│
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
2. Synchronous Prediction (Success)
bash
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict
Response:

json
{
  "status": "success",
  "problem": "تلف في أنبوب المياه",
  "problem_code": "Pipe_Damage",
  "confidence": "77.39%",
  "severity": "حرجة",
  "recommendation": "يوصى بإيقاف مصدر المياه فوراً...",
  "explanation": "اكتشف نموذج الذكاء الاصطناعي وجود تلف...",
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
3. Refused Response (No Problem Detected)
bash
curl -X POST -F "file=@test_images/no_problem.jpg" http://localhost:8001/api/v1/predict
Response:

json
{
  "status": "refused",
  "message": "لم يتم الكشف عن مشكلة واضحة في الصورة.",
  "confidence": "45.23%",
  "suggestion": "يرجى رفع صورة توضح مكان المشكلة بشكل أفضل.",
  "timestamp": "2026-07-24T10:00:00.000000"
}
📊 Severity Levels
Level (Arabic)	Level (English)	Urgency
حرجة جداً	Very Critical	Within 1 hour
حرجة	Critical	Within 4 hours
عالية جداً	Very High	Within 12 hours
عالية	High	Within 24 hours
متوسطة	Medium	Within 48 hours
منخفضة	Low	Within 1 week
بسيطة	Minor	Next maintenance
بسيطة جداً	Very Minor	Schedule later
غير مؤثرة	Negligible	No action needed
🧪 Testing
bash
# 1. Health Check
curl http://localhost:8001/health

# 2. Synchronous Prediction
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict

# 3. Asynchronous Prediction
curl -X POST -F "file=@test_images/pipe_damage.jpg" http://localhost:8001/api/v1/predict-async

# 4. Swagger UI
# Open in browser: http://localhost:8001/docs
🐳 Docker Deployment
bash
# Build and run
docker-compose -f docker/docker-compose.yml up --build

# Run in background
docker-compose -f docker/docker-compose.yml up -d --build

# Stop containers
docker-compose -f docker/docker-compose.yml down
❌ Troubleshooting
1. ModuleNotFoundError
bash
$env:PYTHONPATH = "D:\Graduation_Project\VisionService"
2. Port 8001 Already in Use
bash
netstat -ano | findstr :8001
taskkill /PID [PID] /F
3. RabbitMQ Connection Refused
bash
docker start rabbitmq
