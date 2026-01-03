# Bedbug Detector - AI-Powered Detection System

A modern web application for detecting bedbugs using machine learning. Built with React + TypeScript for the frontend and FastAPI + TensorFlow for the backend.

## 🎯 Features

- **AI-Powered Detection**: Binary classification model to identify bedbugs in images
- **Real-Time Predictions**: Instant analysis with confidence scoring
- **Responsive Design**: Works on desktop and mobile devices
- **Professional UI**: Clinical precision design with medical authority aesthetic
- **Prediction History**: Track and view previous predictions
- **REST API**: Complete FastAPI backend with documentation
- **Database Storage**: SQLite database for prediction records

## 📋 Table of Contents

- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Technologies](#technologies)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Project Details](#project-details)

## 📁 Project Structure

```
bedbug_detector/
├── client/                          # React + TypeScript Frontend
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.tsx            # Main landing page
│   │   │   ├── Info.tsx            # Bedbugs information page
│   │   │   ├── Detector.tsx        # Image upload & prediction page
│   │   │   └── NotFound.tsx        # 404 page
│   │   ├── components/
│   │   │   └── Navigation.tsx      # Navigation bar
│   │   ├── App.tsx                 # Main router
│   │   ├── main.tsx                # React entry point
│   │   └── index.css               # Global styles (clinical precision palette)
│   ├── public/
│   │   └── images/                 # Hero images
│   ├── index.html                  # HTML template
│   └── package.json
│
├── backend/                         # FastAPI Backend
│   ├── app.py                      # Main FastAPI application
│   ├── Database.py                 # SQLAlchemy models
│   ├── testing.py                  # Smart prediction logic
│   ├── requirements.txt            # Python dependencies
│   ├── model/                      # Place your ML model here
│   │   └── cimex_binary_RGB_V4.keras
│   ├── venv/                       # Python virtual environment (created by install)
│   └── predictions.db              # SQLite database (created at runtime)
│
├── run.bat                         # Master batch file (Windows)
├── MANUAL_COMMANDS.md              # Manual command instructions
├── DEPLOYMENT_GUIDE.md             # Detailed deployment guide
├── WINDOWS_SETUP.md                # Windows setup guide
└── README.md                       # This file
```

## 🔧 Prerequisites

### System Requirements

- **Windows 10/11** (or macOS/Linux with similar commands)
- **Disk Space**: ~2GB for dependencies
- **RAM**: 4GB minimum, 8GB recommended

### Software Requirements

1. **Python 3.9+**
   - Download: https://www.python.org/downloads/
   - ✓ Check "Add Python to PATH" during installation
   - Verify: `python --version`

2. **Node.js 18+**
   - Download: https://nodejs.org/
   - Verify: `node --version`

3. **Trained ML Model**
   - File: `cimex_binary_RGB_V4.keras`
   - Size: ~50-100MB
   - Location: `backend/model/cimex_binary_RGB_V4.keras`

## 📦 Installation

### Step 1: Clone or Download the Project

```bash
git clone <repository-url>
cd bedbug_detector
```

### Step 2: Install Backend Dependencies

Open Command Prompt and run:

```cmd
cd backend
python -m venv venv
call venv\Scripts\activate.bat
pip install --upgrade pip
pip install -r requirements.txt
```

**Note**: Installation may take 5-10 minutes due to TensorFlow.

### Step 3: Install Frontend Dependencies

Open a new Command Prompt and run:

```cmd
cd bedbug_detector
npm install --legacy-peer-deps
```

**Note**: Use `--legacy-peer-deps` to resolve dependency conflicts.

### Step 4: Add Your Model File

1. Create directory: `backend/model/`
2. Copy your model file: `cimex_binary_RGB_V4.keras`
3. Verify path: `backend/model/cimex_binary_RGB_V4.keras`

## 🚀 Running the Application

### Option 1: Automated (Windows Batch File)

Simply double-click:
```
run.bat
```

This will:
- ✓ Install all dependencies (if not already installed)
- ✓ Start backend server (port 8000)
- ✓ Start frontend server (port 3000)
- ✓ Open browser to http://localhost:3000

### Option 2: Manual Commands

**Terminal 1 - Backend:**
```cmd
cd backend
call venv\Scripts\activate.bat
python app.py
```

**Terminal 2 - Frontend:**
```cmd
npm run dev
```

**Then open browser:**
```
http://localhost:3000
```

### Option 3: Production Build

```cmd
npm run build
npm run preview
```

## 📡 API Documentation

### Backend Server

- **URL**: http://localhost:8000
- **Interactive Docs**: http://localhost:8000/docs (Swagger UI)
- **ReDoc**: http://localhost:8000/redoc

### API Endpoints

#### Health Check
```
GET /health
```
Returns server status and model availability.

#### Predict
```
POST /predict
Content-Type: multipart/form-data

Body:
- image: (file) JPG or PNG image
```

Response:
```json
{
  "label": "Cimex",
  "probability": 0.85,
  "confidence": 0.92
}
```

#### Save Prediction
```
POST /save
Content-Type: application/json

Body:
{
  "label": "Cimex",
  "confidence": 0.92,
  "probability": 0.85,
  "image_name": "sample.jpg"
}
```

#### Get History
```
GET /history?limit=100
```

Returns list of recent predictions.

#### Get Statistics
```
GET /stats
```

Returns prediction statistics.

## 🛠 Technologies

### Frontend
- **React 19** - UI framework
- **TypeScript** - Type safety
- **Vite** - Build tool
- **TailwindCSS 4** - Styling
- **Wouter** - Routing
- **shadcn/ui** - Component library
- **Lucide React** - Icons

### Backend
- **FastAPI** - Web framework
- **TensorFlow 2.13** - ML framework
- **Keras** - Neural network API
- **SQLAlchemy** - ORM
- **SQLite** - Database
- **Uvicorn** - ASGI server
- **Pillow** - Image processing

### Design
- **Color Palette**: Teal (#0D7377) + Warm Gray
- **Typography**: Playfair Display (headings) + Source Sans Pro (body)
- **Aesthetic**: Clinical Precision Medical Design

## ⚙️ Configuration

### Environment Variables

Create `backend/.env` file (optional):

```env
MODEL_PATH=model/cimex_binary_RGB_V4.keras
DATABASE_URL=sqlite:///./predictions.db
API_HOST=0.0.0.0
API_PORT=8000
```

### API Configuration

Edit `backend/app.py` to change CORS settings:

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://yourdomain.com"],  # Restrict to specific domains
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### Frontend Configuration

Edit `client/src/pages/Detector.tsx` to change API URL:

```typescript
const API_URL = import.meta.env.VITE_API_URL || "http://localhost:8000";
```

Or set environment variable:
```
VITE_API_URL=https://api.yourdomain.com
```

## 🐛 Troubleshooting

### Python Issues

**"Python is not installed"**
- Download from https://www.python.org/
- Make sure to check "Add Python to PATH"
- Restart Command Prompt after installation

**"Module not found" error**
- Ensure virtual environment is activated (should see `(venv)` in prompt)
- Run: `pip install -r requirements.txt` again

**"TensorFlow installation fails"**
- Use Python 3.9 (more stable than 3.13)
- Ensure you have 2GB+ free disk space
- Try: `pip install --upgrade pip` first

### Node.js Issues

**"npm not found"**
- Install Node.js from https://nodejs.org/
- Restart Command Prompt after installation

**"Dependency conflict" error**
- Use: `npm install --legacy-peer-deps`

**"vite not recognized"**
- Run: `npm install --legacy-peer-deps` again
- Delete `node_modules` and reinstall if persistent

### Port Issues

**"Port 3000 already in use"**
```cmd
npm run dev -- --port 3001
```

**"Port 8000 already in use"**
- Edit `backend/app.py` or run:
```cmd
python -m uvicorn app:app --port 8001
```

### Model File Issues

**"Model file not found"**
- Verify path: `backend/model/cimex_binary_RGB_V4.keras`
- Check file exists and is readable
- Restart backend server

**"Model loading fails"**
- Ensure model is compatible with TensorFlow 2.13
- Check model file is not corrupted
- Try with a different model version

### Database Issues

**"Database locked"**
- Close all instances of the application
- Delete `backend/predictions.db` and restart

**"Permission denied"**
- Run Command Prompt as Administrator
- Check folder permissions

## 📊 Project Details

### Frontend Pages

1. **Home Page** (`/`)
   - Hero section with call-to-action
   - Feature cards highlighting system benefits
   - CTA section to detector
   - Footer with links

2. **Info Page** (`/info`)
   - Comprehensive bedbugs information
   - Identification guide
   - Prevention tips
   - Treatment options
   - Health effects information

3. **Detector Page** (`/detector`)
   - Image upload interface (drag & drop)
   - Real-time prediction display
   - Confidence scoring visualization
   - Prediction history
   - Tips for best results

### Backend Features

- **Smart Prediction**: Handles image rotation for uncertain predictions
- **Confidence Scoring**: Provides confidence metrics for results
- **Database Storage**: Stores all predictions for history
- **Error Handling**: Comprehensive error messages
- **CORS Support**: Ready for frontend integration
- **Health Checks**: Monitor server status

### Design Philosophy

The application uses a **Clinical Precision** design aesthetic:
- **Medical Authority**: Teal color palette conveys trust
- **Clarity First**: Generous whitespace and clear typography
- **Professional**: High-contrast, readable fonts
- **Accessible**: WCAG compliant color choices

## 🚢 Deployment

### Docker Deployment

**Backend Dockerfile:**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Frontend Dockerfile:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json .
RUN npm install --legacy-peer-deps
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "preview"]
```

### Cloud Deployment

- **Vercel**: For frontend (React)
- **Railway/Render**: For backend (FastAPI)
- **AWS/GCP/Azure**: For production scale

See `DEPLOYMENT_GUIDE.md` for detailed instructions.

## 📝 Database Schema

### predictions table

| Column | Type | Description |
|--------|------|-------------|
| id | Integer | Primary key |
| label | String | Prediction result (Cimex, Non-Cimex, uncertain) |
| confidence | Float | Confidence score (0-1) |
| probability | Float | Raw probability (0-1) |
| image_name | String | Original image filename |
| created_at | DateTime | Timestamp of prediction |

## 🔐 Security Considerations

1. **CORS**: Restrict to known domains in production
2. **Input Validation**: Images validated for type and size
3. **Rate Limiting**: Add in production
4. **HTTPS**: Use in production
5. **Database**: Use strong credentials for PostgreSQL
6. **Secrets**: Never commit API keys or credentials

## 📈 Performance Tips

- Use GPU acceleration if available (install `tensorflow-gpu`)
- Implement caching for frequent predictions
- Monitor database size and clean old records
- Use CDN for static assets
- Implement request rate limiting

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

## 👨‍💻 Author

Created for bedbugs detection using AI/ML technology.

## 🆘 Support

For issues and questions:
1. Check `TROUBLESHOOTING.md`
2. Review `MANUAL_COMMANDS.md` for setup help
3. Check backend logs: `backend/logs/`
4. Open an issue on GitHub

## 🗺️ Roadmap

- [ ] Mobile app (React Native)
- [ ] Multi-language support
- [ ] Advanced analytics dashboard
- [ ] User authentication
- [ ] Image gallery management
- [ ] Email notifications
- [ ] API rate limiting
- [ ] Advanced prediction filters

## 📚 Additional Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Documentation](https://react.dev/)
- [TensorFlow Documentation](https://www.tensorflow.org/)
- [Vite Documentation](https://vitejs.dev/)
- [TailwindCSS Documentation](https://tailwindcss.com/)

## 🎓 Learning Resources

- Machine Learning: https://www.tensorflow.org/learn
- Web Development: https://developer.mozilla.org/
- Python: https://docs.python.org/3/
- JavaScript/React: https://javascript.info/

---

**Last Updated**: December 2024
**Version**: 1.0.0
**Status**: Production Ready
