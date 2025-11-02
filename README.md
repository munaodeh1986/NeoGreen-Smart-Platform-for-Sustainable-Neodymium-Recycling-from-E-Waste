# 🌱 NeoGreen E-Waste Recycling Platform

A modern, interactive web application for managing electronic waste recycling, tracking neodymium extraction, and rewarding contributors through a comprehensive IoT-integrated system.

![NeoGreen Platform](https://img.shields.io/badge/React-18.x-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

## 📋 Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Components Overview](#components-overview)
- [API Integration](#api-integration)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### 🎯 Core Functionality

- **Dashboard Overview**
  - Real-time statistics on devices, neodymium collection, and CO₂ savings
  - Recent device tracking with status updates
  - Top contributors leaderboard
  - Live IoT status monitoring

- **Device Management**
  - Comprehensive device tracking system
  - Real-time search and filtering
  - Status-based categorization (Delivered, Processed, Analyzing, Processing)
  - Device registration and QR code scanning

- **User Management**
  - Multi-role user system (Admin, Citizen, University, Business)
  - User activity tracking
  - Points and rewards management
  - Interactive user table with CRUD operations

- **IoT Integration**
  - MQTT broker connectivity
  - Arduino integration support
  - Real-time sensor data monitoring
  - Live message tracking from IoT devices

- **Rewards System**
  - Points-based incentive program
  - Token distribution system
  - Configurable reward settings
  - Interactive leaderboard rankings

- **Reports & Analytics**
  - Monthly summaries and trends
  - Device type distribution analysis
  - CO₂ savings calculations
  - Export functionality (CSV/PDF)

### 🎨 UI/UX Features

- **Responsive Design**: Fully optimized for mobile, tablet, and desktop
- **Modern Gradients**: Eye-catching color schemes throughout
- **Smooth Animations**: Fade-in effects and hover transitions
- **Interactive Elements**: Cards, buttons, and navigation with feedback
- **Collapsible Sidebar**: Space-efficient navigation system
- **Search Functionality**: Real-time filtering across devices
- **Custom SVG Icons**: Beautiful, scalable vector graphics
- **Notification System**: Alert badges for important updates

## 🎥 Demo

### Dashboard
- View real-time statistics and metrics
- Monitor IoT device connectivity
- Track top contributors

### Device Management
- Search and filter devices by type, brand, or owner
- View detailed device information
- Track neodymium extraction amounts

### User & Rewards
- Manage user accounts and roles
- View points and token balances
- Track leaderboard rankings

## 🛠 Technologies Used

### Frontend
- **React 18.x** - UI framework
- **Lucide React** - Icon library
- **Tailwind CSS** - Utility-first styling
- **JavaScript ES6+** - Modern JavaScript

### State Management
- **React Hooks** - useState, useEffect for local state

### Planned Backend Integration
- **MQTT** - IoT device communication
- **REST API** - Backend services
- **Arduino** - Hardware integration

## 📦 Installation

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager
- Git

### Step-by-Step Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/neogreen-platform.git
   cd neogreen-platform
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Install required packages**
   ```bash
   npm install lucide-react
   # or
   yarn add lucide-react
   ```

4. **Start the development server**
   ```bash
   npm start
   # or
   yarn start
   ```

5. **Open your browser**
   ```
   Navigate to http://localhost:3000
   ```

## 🚀 Usage

### Running the Application

```bash
# Development mode
npm start

# Production build
npm run build

# Run tests
npm test
```

### Default Login
- **Email**: admin@neogreen.com
- **Role**: Administrator
- **Access**: Full system access

## 📁 Project Structure

```
neogreen-platform/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── App.jsx                 # Main application component
│   ├── index.js                # Application entry point
│   ├── components/
│   │   ├── DeviceCard.jsx      # Device display component
│   │   ├── StatCard.jsx        # Statistics card component
│   │   └── RecycleIcon.jsx     # Custom SVG icon
│   ├── styles/
│   │   └── tailwind.css        # Tailwind configurations
│   └── utils/
│       └── helpers.js          # Utility functions
├── package.json
├── tailwind.config.js
└── README.md
```

## 🧩 Components Overview

### Main Components

#### **App Component**
- Root component managing all application state
- Handles navigation and routing between tabs
- Manages sidebar visibility and responsiveness

#### **DeviceCard Component**
- Displays individual device information
- Shows neodymium content, owner, and status
- Includes interactive "View Details" button

#### **StatCard Component**
- Renders gradient statistics cards
- Displays metrics with icons and trend indicators
- Responsive hover effects

#### **RecycleIcon Component**
- Custom SVG icon for branding
- Used in sidebar and various UI elements

### Key Features by Tab

| Tab | Features |
|-----|----------|
| Dashboard | Stats, Recent Devices, IoT Status, Top Contributors |
| Devices | Search, Filter, Device Cards, Registration |
| Users | User Table, Role Management, CRUD Operations |
| IoT | MQTT Configuration, Arduino Code, Live Messages |
| Rewards | User Rewards, Settings, Leaderboard |
| Reports | Monthly Summary, Charts, Export Options |

## 🔌 API Integration

### Expected API Endpoints

```javascript
// Device Management
GET    /api/devices          // Fetch all devices
POST   /api/devices          // Register new device
PUT    /api/devices/:id      // Update device
DELETE /api/devices/:id      // Remove device

// User Management
GET    /api/users            // Fetch all users
POST   /api/users            // Create new user
PUT    /api/users/:id        // Update user
DELETE /api/users/:id        // Delete user

// IoT Integration
POST   /api/iot/mqtt/connect // Connect to MQTT broker
GET    /api/iot/messages     // Fetch recent messages

// Rewards
GET    /api/rewards          // Fetch user rewards
PUT    /api/rewards/settings // Update reward settings

// Reports
GET    /api/reports/monthly  // Monthly statistics
GET    /api/reports/export   // Export data
```

### MQTT Topics

```
neogreen/devices/+           // Subscribe to all devices
neogreen/devices/DEV001      // Specific device updates
neogreen/sensors/hall        // Hall effect sensor data
neogreen/sensors/temp        // Temperature readings
```

## 🎨 Customization

### Color Schemes

Modify gradients in `App.jsx`:

```javascript
// Example: Change stat card gradient
gradient="from-blue-500 via-blue-600 to-blue-700"
```

### Adding New Device Types

Update the devices array in `useEffect`:

```javascript
{ 
  id: 'DEV006', 
  type: 'Tablet', 
  brand: 'Apple', 
  // ... other properties
}
```

### Configuring Rewards

Adjust reward calculations in the Rewards section:

```javascript
// Points per gram of Neodymium
const pointsPerGram = 10;

// Minimum payout threshold
const minThreshold = 100;
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m "feat: add amazing feature"
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Coding Standards

- Follow React best practices
- Use functional components with hooks
- Maintain Tailwind CSS utility-first approach
- Write descriptive commit messages
- Add comments for complex logic
- Test responsive design on multiple devices

## 🐛 Known Issues

- Chart visualizations are placeholders (pending charting library integration)
- Export functionality requires backend implementation
- MQTT connection needs actual broker configuration
- Real-time updates need WebSocket integration

## 🗺 Roadmap

- [ ] Integrate Chart.js for data visualization
- [ ] Add authentication and authorization
- [ ] Implement real-time WebSocket updates
- [ ] Connect to actual MQTT broker
- [ ] Add dark mode support
- [ ] Implement CSV/PDF export functionality
- [ ] Add multi-language support (i18n)
- [ ] Create mobile app version
- [ ] Add notification system
- [ ] Implement data persistence

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Your Name** - *Initial work* - [YourGitHub](https://github.com/yourusername)

## 🙏 Acknowledgments

- Icons provided by [Lucide React](https://lucide.dev/)
- Inspired by modern sustainability initiatives
- Built with ❤️ for a greener future

## 📞 Support

For support, email support@neogreen.com or open an issue on GitHub.

---

**Made with 🌍 for environmental sustainability**

⭐ **Star this repo if you found it helpful!** ⭐
