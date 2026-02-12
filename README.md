#  AI-Powered Dental Imaging System

An advanced dental diagnostic platform that leverages artificial intelligence to analyze DICOM X-ray images, detect dental conditions, and generate comprehensive diagnostic reports automatically.

##  Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [Configuration](#configuration)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [License](#license)

##  Overview

This application streamlines the dental diagnostic workflow by:
- Processing DICOM medical imaging files
- Using AI-powered object detection to identify dental conditions
- Generating professional diagnostic reports with LLM assistance
- Providing an intuitive interface for dental professionals

## ✨ Features

### Core Functionality
- **DICOM File Processing**: Upload and convert DICOM files to viewable images
- **AI-Powered Detection**: Automatic detection of dental conditions using Roboflow's trained models
- **Smart Annotation**: Visual bounding boxes highlighting detected conditions
- **Report Generation**: AI-generated diagnostic reports using GPT-3.5-turbo
- **PDF Export**: Download professional reports in PDF format

### User Interface
- **Modern Design**: Clean, professional interface with light/dark theme support
- **Welcome Screen**: Intuitive onboarding experience
- **Patient Management**: Input and track patient information (name, age, gender)
- **Real-time Processing**: Live feedback during image analysis
- **Responsive Layout**: Works seamlessly across different screen sizes

##  Tech Stack

### Backend
- **Framework**: FastAPI
- **Image Processing**: OpenCV, pydicom, numpy
- **AI/ML**: Roboflow (object detection), OpenRouter API (LLM)
- **API Communication**: requests, inference_sdk

### Frontend
- **Framework**: React 19.1.0
- **Styling**: Custom CSS with theme support
- **PDF Generation**: html2pdf.js
- **HTTP Client**: Axios
- **Routing**: React Router DOM

##  Prerequisites

Before you begin, ensure you have the following installed:

- **Python**: 3.8 or higher
- **Node.js**: 14.x or higher
- **npm**: 6.x or higher
- **pip**: Latest version

### API Keys Required

You'll need to obtain the following API keys:

1. **Roboflow API Key**: [Get it here](https://roboflow.com/)
2. **OpenRouter API Key**: [Get it here](https://openrouter.ai/)

##  Project Structure
```
dental-ai-project/
├── backend/
│   ├── main.py                 # FastAPI application
│   ├── requirements.txt        # Python dependencies
│   └── uploads/                # Temporary file storage
│
├── frontend/
│   ├── public/
│   │   ├── index.html         # HTML template
│   │   ├── manifest.json      # PWA manifest
│   │   └── robots.txt         # SEO robots file
│   │
│   ├── src/
│   │   ├── App.js             # Main application component
│   │   ├── App.css            # Application styles
│   │   ├── WelcomeScreen.js   # Welcome screen component
│   │   ├── WelcomeScreen.css  # Welcome screen styles
│   │   ├── index.js           # React entry point
│   │   ├── index.css          # Global styles
│   │   └── logo.png           # Application logo
│   │
│   └── package.json           # Node dependencies
│
└── README.md                  # This file
```

##  Setup Instructions

### Backend Setup

1. **Clone the repository**
```bash
git clone <https://github.com/Gaurika29062004/Dental-Xray-ai>
cd dental-ai-project
```

2. **Navigate to backend directory**
```bash
cd backend
```

3. **Create a virtual environment**
```bash
python -m venv venv

# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

4. **Install dependencies**
```bash
pip install -r requirements.txt
```

5. **Configure environment variables** (see [Configuration](#configuration))

6. **Run the backend server**
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend will be available at `http://localhost:8000`

### Frontend Setup

1. **Navigate to frontend directory**
```bash
cd frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Start the development server**
```bash
npm start
```

The frontend will be available at `http://localhost:3000`

## Configuration

### Backend Configuration

Update the API keys in `backend/main.py`:
```python
# Roboflow Configuration
roboflow_client = InferenceHTTPClient(
    api_url="https://serverless.roboflow.com",
    api_key="YOUR_ROBOFLOW_API_KEY"
)

# OpenRouter Configuration
OPENROUTER_API_KEY = "YOUR_OPENROUTER_API_KEY"
```

**Important**: For production, use environment variables instead of hardcoding API keys:
```python
import os
from dotenv import load_dotenv

load_dotenv()

ROBOFLOW_API_KEY = os.getenv("ROBOFLOW_API_KEY")
OPENROUTER_API_KEY = os.getenv("OPENROUTER_API_KEY")
```

Create a `.env` file in the backend directory:
```env
ROBOFLOW_API_KEY=your_roboflow_api_key_here
OPENROUTER_API_KEY=your_openrouter_api_key_here
```

### Frontend Configuration

Update the backend URL in `frontend/src/App.js` if your backend runs on a different host/port:
```javascript
const response = await fetch("http://127.0.0.1:8000/upload", {
    method: "POST",
    body: formData,
});
```

##  Usage

### Step-by-Step Guide

1. **Launch the Application**
   - Start both backend and frontend servers
   - Navigate to `http://localhost:3000`

2. **Welcome Screen**
   - Click "Launch App" to proceed to the main interface

3. **Enter Patient Information**
   - Fill in patient name
   - Enter patient age
   - Select gender from dropdown

4. **Upload DICOM File**
   - Click "Choose File" and select a `.dcm` file
   - Ensure the file is a valid DICOM dental X-ray

5. **Generate Report**
   - Click "Generate Report" button
   - Wait for processing (usually 5-15 seconds)

6. **Review Results**
   - View annotated X-ray image with detected conditions
   - Read the AI-generated diagnostic report

7. **Export Report**
   - Click "Download Report as PDF" to save the report
   - PDF includes patient info, annotated image, and findings

### Tips
- Use high-quality DICOM files for best results
- Ensure patient information is complete before generation
- Toggle between light/dark themes using the theme switcher


##  Screenshots
<img width="1280" height="692" alt="image" src="https://github.com/user-attachments/assets/42a8c4f1-524d-4c18-a8e6-d49b141e3240" />
<img width="1280" height="723" alt="image" src="https://github.com/user-attachments/assets/ea8fb8f1-1e96-4ed7-aa26-6d991f203ade" />
<img width="1280" height="723" alt="image" src="https://github.com/user-attachments/assets/fc2ed4a3-59d8-4a44-96c3-06e797c656b2" />

### Welcome Screen
Modern landing page with feature overview and app launch button.

### Main Interface
- Patient information input panel
- DICOM file upload section
- Theme toggle (light/dark mode)

### Results Display
- Annotated X-ray image with bounding boxes
- Detailed diagnostic report
- PDF download functionality


##  Deployment

### Backend Deployment

**Using Docker:**

Create `Dockerfile` in backend directory:
```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Build and run:
```bash
docker build -t dental-ai-backend .
docker run -p 8000:8000 --env-file .env dental-ai-backend
```

### Frontend Deployment

Build the production version:
```bash
cd frontend
npm run build
```

Deploy the `build` folder to your hosting service (Netlify, Vercel, AWS S3, etc.)

##  Performance Optimization

- **Image Processing**: Large DICOM files may take longer to process
- **API Rate Limits**: Be aware of Roboflow and OpenRouter rate limits
- **Caching**: Consider implementing Redis for caching results
- **CDN**: Use a CDN for static assets in production

##  Future Enhancements

- [ ] Multi-language support
- [ ] User authentication and authorization
- [ ] Patient history tracking
- [ ] Batch processing of multiple DICOM files
- [ ] Advanced report customization
- [ ] Integration with electronic health record (EHR) systems
- [ ] Mobile application
- [ ] Cloud storage integration

##  License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

- Gaurika Gupta,Final year student at NSUT 

##  Acknowledgments

- [Roboflow](https://roboflow.com/) for object detection capabilities
- [OpenRouter](https://openrouter.ai/) for LLM API access
- [FastAPI](https://fastapi.tiangolo.com/) framework
- [React](https://reactjs.org/) library
- Open source community



---

Made with ❤️ for better dental healthcare
