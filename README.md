# Zedge Clone - Mobile Wallpaper & Ringtone Discovery App

A feature-rich mobile application for discovering, browsing, and managing wallpapers and ringtones. Built with modern technologies to provide a seamless user experience across iOS and Android platforms.

## 🎨 Overview

Zedge Clone is a comprehensive mobile wallpaper and ringtone discovery platform that allows users to explore, download, share, and manage their favorite media content. The app combines a powerful React Native frontend with a robust Node.js backend, all powered by Firebase for authentication and data management.

## 🏗️ Architecture

### Frontend
- **Framework**: React Native
- **Type**: Mobile application (iOS & Android)
- **Features**: Cross-platform compatibility, native performance

### Backend
- **Runtime**: Node.js
- **Database & Services**: Firebase
  - Firestore for data storage
  - Firebase Authentication for user management
  - Firebase Storage for media files
  - Firebase Cloud Functions for serverless operations

## ✨ Key Features

### 1. **Wallpaper Browsing & Discovery**
- Browse through an extensive library of wallpapers
- Categorized wallpaper collections
- Trending and popular wallpapers section
- New releases and featured content
- High-resolution image preview
- Multiple wallpaper formats and dimensions

### 2. **Ringtone Library**
- Extensive collection of ringtones and notification sounds
- Music-based ringtones
- Sound effect categories
- Audio preview functionality
- Customizable audio quality options

### 3. **User Uploads**
- Upload custom wallpapers to the platform
- Upload personal ringtones and sounds
- Media validation and processing
- User content management dashboard
- Upload history tracking

### 4. **Social Features**
- **Sharing Capabilities**
  - Share wallpapers and ringtones with friends via social media
  - Direct sharing through messaging apps
  - Share to social platforms (Instagram, Twitter, etc.)
  - Generate shareable links
  
- **Favorites Management**
  - Save favorite wallpapers and ringtones
  - Create personal collections
  - Organize favorites by categories
  - Sync favorites across devices

### 5. **Search & Filtering**
- Advanced search functionality
- Filter by category, color, artist, duration
- Search suggestions and autocomplete
- Sort by popularity, date added, ratings
- Advanced filters for specific use cases

### 6. **Download Management**
- Download wallpapers and ringtones for offline access
- Batch download capabilities
- Download progress tracking
- Queue management
- Download history
- Storage optimization
- Auto-cleanup of old downloads

## 📱 User Capabilities

- **User Registration & Authentication**: Secure sign-up and login via Firebase
- **Profile Management**: User profiles with custom preferences
- **Personalization**: Custom recommendations based on user preferences
- **Offline Access**: Downloaded content available without internet
- **Sync Across Devices**: Seamless experience across multiple devices
- **Notifications**: Updates on new content and social interactions

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- React Native development environment
- Firebase project setup
- iOS/Android development environment (Xcode/Android Studio)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/wallpaper74-max/zedge-clone.git
   cd zedge-clone
   ```

2. **Install dependencies**
   ```bash
   # Frontend dependencies
   cd frontend
   npm install
   
   # Backend dependencies
   cd ../backend
   npm install
   ```

3. **Configure Firebase**
   - Create a Firebase project on [Firebase Console](https://console.firebase.google.com)
   - Download the configuration files
   - Add Firebase credentials to your frontend and backend configuration

4. **Setup environment variables**
   ```bash
   # Backend .env
   FIREBASE_PROJECT_ID=your_project_id
   FIREBASE_PRIVATE_KEY=your_private_key
   FIREBASE_CLIENT_EMAIL=your_client_email
   NODE_ENV=development
   ```

5. **Start the development servers**
   ```bash
   # Terminal 1: Backend
   cd backend
   npm start
   
   # Terminal 2: Frontend
   cd frontend
   npm start
   ```

## 📁 Project Structure

```
zedge-clone/
├── frontend/                  # React Native frontend
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── screens/          # App screens/pages
│   │   ├── navigation/       # Navigation configuration
│   │   ├── services/         # API and Firebase services
│   │   ├── redux/            # State management
│   │   ├── utils/            # Utility functions
│   │   └── App.js            # Root component
│   └── package.json
│
├── backend/                   # Node.js backend
│   ├── routes/               # API endpoints
│   ├── controllers/          # Business logic
│   ├── models/               # Data models
│   ├── middleware/           # Custom middleware
│   ├── services/             # External services
│   ├── config/               # Configuration files
│   ├── server.js             # Express server setup
│   └── package.json
│
└── README.md                  # This file
```

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/profile` - Get user profile

### Wallpapers
- `GET /api/wallpapers` - Get wallpapers (with pagination)
- `GET /api/wallpapers/:id` - Get wallpaper details
- `GET /api/wallpapers/category/:category` - Get wallpapers by category
- `POST /api/wallpapers` - Upload new wallpaper
- `POST /api/wallpapers/:id/download` - Track wallpaper download
- `POST /api/wallpapers/:id/favorite` - Add to favorites

### Ringtones
- `GET /api/ringtones` - Get ringtones (with pagination)
- `GET /api/ringtones/:id` - Get ringtone details
- `GET /api/ringtones/category/:category` - Get ringtones by category
- `POST /api/ringtones` - Upload new ringtone
- `POST /api/ringtones/:id/download` - Track ringtone download
- `POST /api/ringtones/:id/favorite` - Add to favorites

### Search & Discovery
- `GET /api/search` - Search wallpapers and ringtones
- `GET /api/trending` - Get trending content
- `GET /api/featured` - Get featured content
- `GET /api/recommendations` - Get personalized recommendations

### User Content
- `GET /api/user/uploads` - Get user's uploaded content
- `GET /api/user/downloads` - Get user's download history
- `GET /api/user/favorites` - Get user's favorite items
- `DELETE /api/user/uploads/:id` - Delete user's upload

## 🔐 Security Features

- Firebase Authentication with email/password and social login options
- Secure API endpoints with authentication middleware
- Input validation and sanitization
- CORS configuration for secure cross-origin requests
- Rate limiting to prevent abuse
- Secure file upload validation
- HTTPS encryption for all communications

## 📊 Database Schema

### Firestore Collections

**Users**
```
{
  uid: string,
  email: string,
  username: string,
  profileImage: string,
  bio: string,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

**Wallpapers**
```
{
  id: string,
  title: string,
  description: string,
  imageUrl: string,
  thumbnailUrl: string,
  category: string,
  colors: array,
  artist: string,
  uploader: string (uid),
  downloads: number,
  favorites: number,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

**Ringtones**
```
{
  id: string,
  title: string,
  artist: string,
  duration: number,
  audioUrl: string,
  category: string,
  uploader: string (uid),
  downloads: number,
  favorites: number,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

**User Favorites**
```
{
  userId: string,
  contentType: string (wallpaper/ringtone),
  contentId: string,
  savedAt: timestamp
}
```

## 🧪 Testing

### Frontend Tests
```bash
cd frontend
npm test
```

### Backend Tests
```bash
cd backend
npm test
```

## 📦 Dependencies

### Frontend (React Native)
- react-native
- @react-navigation/native
- @react-navigation/bottom-tabs
- firebase
- redux & react-redux
- axios
- react-native-image-picker
- react-native-share

### Backend (Node.js)
- express
- firebase-admin
- cors
- dotenv
- axios
- multer (for file uploads)
- express-validator (for input validation)

## 🚢 Deployment

### Frontend Deployment
- Build for iOS: `react-native run-ios --configuration Release`
- Build for Android: `react-native run-android --configuration Release`
- Deploy to App Store and Google Play Store

### Backend Deployment
- Deploy to Firebase Cloud Functions or Heroku
- Configure environment variables on the hosting platform
- Set up CI/CD pipeline for automated deployments

## 📈 Performance Optimization

- Image compression and optimization
- Lazy loading of content
- Pagination for large datasets
- Caching strategies for frequently accessed data
- Code splitting in React Native
- Database query optimization

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🐛 Bug Reports & Feature Requests

Found a bug or have a feature request? Please open an issue on GitHub with:
- Clear description of the issue
- Steps to reproduce (for bugs)
- Expected behavior
- Screenshots or logs if applicable

## 📞 Support

For support, questions, or inquiries, please reach out to the development team or open an issue in the repository.

## 🙏 Acknowledgments

- Firebase for providing backend infrastructure
- React Native community for excellent documentation
- All contributors and users of the application

## 📄 Version History

### v1.0.0 (Current)
- Initial release with core features
- Wallpaper browsing and discovery
- Ringtone library
- User uploads functionality
- Social sharing and favorites
- Search and filtering capabilities
- Download management system

---

**Last Updated**: 2026-01-08

**Repository**: [zedge-clone](https://github.com/wallpaper74-max/zedge-clone)

**Author**: wallpaper74-max
