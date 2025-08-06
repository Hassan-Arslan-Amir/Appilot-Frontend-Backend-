# AppPilot - Multi-Platform Automation Suite

AppPilot is a comprehensive automation platform that enables users to create, schedule, and manage automation tasks across multiple social media platforms and applications. The system consists of three integrated components working together to provide a seamless automation experience.

## 🏗️ Project Structure

```
AppPilot/
├── appilot-master/         # Android App (Java)
│   ├── app/               # Main Android application
│   ├── build.gradle       # Android build configuration
│   └── ...               # Android project files
├── backend/               # FastAPI Backend (Python)
│   ├── routes/           # API endpoints
│   ├── models/           # Database models
│   ├── Bot/              # Discord bot integration
│   ├── config/           # Database configuration
│   ├── utils/            # Utility functions
│   ├── main.py           # FastAPI application entry point
│   ├── requirements.txt  # Python dependencies
│   └── deploy.sh         # Deployment script
├── frontend/              # React Frontend (JavaScript)
│   ├── src/              # Source code
│   │   ├── Components/   # React components
│   │   ├── Utils/        # Frontend utilities
│   │   └── assets/       # Static assets
│   ├── public/           # Public assets
│   ├── package.json      # Node.js dependencies
│   └── vite.config.js    # Vite configuration
├── .gitignore            # Git ignore rules
└── README.md             # This file
```

## 🚀 Components

### 1. Android App (`appilot-master/`)

- **Technology**: Java, Android SDK, Accessibility Service
- **Purpose**: Mobile automation client that runs on Android devices
- **Key Features**:
  - Accessibility service for UI automation
  - Real-time communication with backend via WebSocket
  - Support for multiple automation bots
  - Task execution and progress reporting
  - Device registration and status monitoring

### 2. Backend (`backend/`)

- **Technology**: FastAPI, Python 3.x, MongoDB, Redis, APScheduler
- **Purpose**: Central API server, task management, and coordination hub
- **Key Features**:
  - RESTful API for task and device management
  - Real-time WebSocket communication with Android devices
  - Task scheduling with timezone support
  - Discord bot integration for notifications
  - Device connection registry with Redis
  - User authentication and authorization
  - Comprehensive logging and monitoring

### 3. Frontend (`frontend/`)

- **Technology**: React 18, Vite, Tailwind CSS, React Router
- **Purpose**: Web dashboard for managing automation tasks and monitoring devices
- **Key Features**:
  - Intuitive task creation and configuration
  - Real-time device monitoring and status
  - Task scheduling with multiple time options
  - Bot configuration with dynamic inputs
  - Responsive design for desktop and mobile
  - User-friendly interface for automation management

## 🛠️ Setup Instructions

### Prerequisites

- **Python 3.8+** for backend
- **Node.js 16+** and npm for frontend
- **Android Studio** for Android app development
- **MongoDB** database
- **Redis** server (optional, for production)

### Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create .env file with your configuration
cp .env.example .env  # Edit with your settings

# Run the development server
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### Android App Setup

1. Open `appilot-master/` in Android Studio
2. Sync project with Gradle files
3. Build and run the application on your device
4. Enable accessibility permissions in device settings
5. Grant necessary permissions for automation

## 🔧 Configuration

### Backend Environment Variables

Create a `.env` file in the `backend/` directory:

```env
# Database Configuration
MONGODB_URL=mongodb+srv://username:password@cluster.mongodb.net/database_name
DATABASE_NAME=Appilot

# Redis Configuration (Optional)
REDIS_URL=redis://localhost:6379

# Discord Bot Integration
DISCORD_BOT_TOKEN=your_discord_bot_token_here

# JWT Secret for Authentication
JWT_SECRET_KEY=your_jwt_secret_key_here

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000

# Timezone Settings
DEFAULT_TIMEZONE=UTC
```

### Frontend Configuration

Update API endpoints in `frontend/src/Utils/utils.jsx` if needed:

```javascript
const API_BASE_URL = "https://server.appilot.app"; // Production
// const API_BASE_URL = "http://localhost:8000"; // Development
```

### Android App Configuration

- Update server URLs in the Android app configuration
- Ensure proper permissions are granted for accessibility service
- Configure device registration settings

## 📱 Supported Automation Bots

| Bot Name                       | Platform       | Features                                             |
| ------------------------------ | -------------- | ---------------------------------------------------- |
| **Instagram Followers Bot**    | Instagram      | Follow users, like posts, automated engagement       |
| **Instagram Mother Slave Bot** | Instagram      | Advanced Instagram automation with multiple accounts |
| **X (formerly Twitter) Bot**   | Twitter/X      | Tweet automation, following, engagement              |
| **Reddit Karma Bot**           | Reddit         | Post automation, comment engagement                  |
| **LinkedIn Bot**               | LinkedIn       | Professional networking automation                   |
| **Facebook Bot**               | Facebook       | Social media automation and posting                  |
| **TikTok Bot**                 | TikTok         | Video engagement and following                       |
| **Gmail Bot**                  | Gmail          | Email automation and management                      |
| **Snapchat Bot**               | Snapchat       | Social media automation                              |
| **Bumble Bot**                 | Bumble         | Dating app automation                                |
| **Spotify Bot**                | Spotify        | Music streaming automation                           |
| **Chrome Bot**                 | Chrome Browser | Web browsing automation                              |

### Bot Features

- **Dynamic Input Configuration**: Each bot supports custom inputs and parameters
- **Scheduling Options**: Exact time, time windows, and recurring schedules
- **Multi-Device Support**: Bots can run on multiple devices simultaneously
- **Progress Monitoring**: Real-time updates and notifications via Discord
- **Error Handling**: Comprehensive error reporting and recovery

## 🚀 Deployment

### Production Backend Deployment

The backend includes a deployment script for Linux servers:

```bash
cd backend

# Make deployment script executable
chmod +x deploy.sh

# Run deployment (requires sudo for systemd services)
sudo ./deploy.sh
```

The deployment script handles:

- Git repository updates
- Python dependency installation
- SystemD service restart
- Nginx configuration reload

### Manual Backend Deployment

```bash
# Install Gunicorn for production
pip install gunicorn

# Run with Gunicorn
gunicorn main:app -w 3 -k uvicorn.workers.UvicornWorker -b 127.0.0.1:8000
```

### Frontend Deployment

The frontend can be deployed to various platforms:

**Vercel (Recommended):**

```bash
npm run build
# Deploy the dist/ folder to Vercel
```

**Netlify:**

```bash
npm run build
# Deploy the dist/ folder to Netlify
```

**Self-hosted:**

```bash
npm run build
# Serve the dist/ folder with any web server (nginx, apache, etc.)
```

### Android App Distribution

- Build APK/AAB using Android Studio
- Distribute via Google Play Store or direct APK installation
- Ensure proper code signing for production releases

## 📊 Monitoring & Debugging

### Backend Monitoring

```bash
# View FastAPI service logs
sudo journalctl -u fastapi.service -f

# Check service status
sudo systemctl status fastapi.service

# View application logs
tail -f backend/logs/app.log
```

### Android App Debugging

```bash
# View device logs (replace with actual process ID)
adb logcat --pid=<process_id>

# View all logs related to your app
adb logcat | grep "com.yourpackage.appilot"

# Screenshots and UI inspection
# Use 'weditor' tool for UI element inspection
```

### Development Tools

- **Backend**: FastAPI automatic documentation at `/docs`
- **Frontend**: React DevTools browser extension
- **Android**: Android Studio debugger and logcat
- **Database**: MongoDB Compass for database inspection
- **API Testing**: Use Postman or similar tools

## 🏃‍♂️ Quick Start

1. **Clone the repository**:

   ```bash
   git clone https://github.com/Hassan-Arslan-Amir/Appilot.git
   cd Appilot
   ```

2. **Setup Backend**:

   ```bash
   cd backend
   python -m venv venv
   venv\Scripts\activate  # Windows
   pip install -r requirements.txt
   python -m uvicorn main:app --reload
   ```

3. **Setup Frontend**:

   ```bash
   cd frontend
   npm install
   npm run dev
   ```

4. **Open Android App** in Android Studio and run on your device

5. **Access the web dashboard** at `http://localhost:5173`

## 🔗 API Endpoints

### Authentication

- `POST /login` - User authentication
- `POST /register` - User registration

### Tasks

- `GET /get-all-tasks` - Retrieve all tasks
- `POST /create-task` - Create new automation task
- `PUT /update-task` - Update existing task
- `DELETE /delete-tasks` - Delete tasks

### Devices

- `POST /register_device` - Register new device
- `GET /device_status/{device_id}` - Check device status
- `WebSocket /ws/{device_id}` - Real-time device communication

### Bots

- `GET /get-all-bots` - Retrieve available bots
- `POST /send_command` - Send commands to devices

## 🤝 Contributing

We welcome contributions to AppPilot! Here's how you can help:

### Development Process

1. **Fork the repository** on GitHub
2. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** following the coding standards
4. **Test your changes** thoroughly
5. **Commit your changes** with clear commit messages:
   ```bash
   git commit -m "Add: new feature description"
   ```
6. **Push to your fork** and submit a pull request

### Code Standards

- **Backend**: Follow PEP 8 for Python code
- **Frontend**: Use ESLint and Prettier configurations
- **Android**: Follow Android coding guidelines
- **Documentation**: Update README and add inline comments

### Issues and Bug Reports

- Use GitHub Issues to report bugs
- Provide detailed reproduction steps
- Include environment information (OS, versions, etc.)

### Feature Requests

- Open a GitHub Issue with the "enhancement" label
- Describe the feature and its use case
- Discuss implementation approach before coding

## � Project Status

### Current Version: v1.0.0

**Features:**

- ✅ Multi-platform automation support
- ✅ Real-time device communication
- ✅ Task scheduling and management
- ✅ Discord integration for notifications
- ✅ Web dashboard for task management
- ✅ Android accessibility service automation

**Upcoming Features:**

- 🔄 Enhanced error handling and recovery
- 🔄 Advanced scheduling options
- 🔄 Performance monitoring dashboard
- 🔄 Multi-user support improvements
- 🔄 Additional bot integrations

## ⚖️ License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### Third-Party Licenses

- FastAPI: MIT License
- React: MIT License
- Android SDK: Android Software Development Kit License

## 📞 Support

- **GitHub Issues**: For bug reports and feature requests
- **Documentation**: Comprehensive setup and usage guides
- **Discord**: Join our community for real-time support

## 🙏 Acknowledgments

- Thanks to all contributors who have helped improve AppPilot
- Special thanks to the open-source community for the amazing tools and libraries
- Inspired by automation enthusiasts and developers worldwide

---

**AppPilot** - Streamlining automation across platforms 🚀
