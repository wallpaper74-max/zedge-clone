# Zedge Clone - System Architecture

## 🏗️ High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      Mobile Client Layer                         │
│                  (React Native - iOS & Android)                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ UI Components | Navigation | State Management | Services │  │
│  └───────────────────────────────────────────────────────────┘  │
└──────────────────────────┬──────────────────────────────────────┘
                           │ REST API / Firebase SDK
┌──────────────────────────▼──────────────────────────────────────┐
│                      API Layer                                   │
│              (Node.js + Express Backend)                        │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ Routes | Controllers | Middleware | Business Logic       │  │
│  └───────────────────────────────────────────────────────────┘  │
└──────────────────────────┬──────────────────────────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
┌───────▼────────┐ ┌──────▼────────┐ ┌──────▼────────┐
│  Firebase DB   │ │ Firebase Auth │ │ Firebase      │
│  (Firestore)   │ │               │ │ Storage       │
└────────────────┘ └───────────────┘ └───────────────┘
```

---

## 🔵 Frontend Architecture (React Native)

### Directory Structure
```
frontend/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── common/          # Common components (Button, Input, etc.)
│   │   ├── wallpaper/       # Wallpaper-related components
│   │   ├── ringtone/        # Ringtone-related components
│   │   ├── social/          # Social features components
│   │   └── profile/         # Profile-related components
│   │
│   ├── screens/             # Application screens
│   │   ├── auth/
│   │   │   ├── LoginScreen.js
│   │   │   └── RegisterScreen.js
│   │   ├── main/
│   │   │   ├── HomeScreen.js
│   │   │   ├── ExploreScreen.js
│   │   │   ├── DownloadsScreen.js
│   │   │   └── ProfileScreen.js
│   │   ├── wallpaper/
│   │   │   ├── WallpaperListScreen.js
│   │   │   ├── WallpaperDetailScreen.js
│   │   │   └── WallpaperUploadScreen.js
│   │   ├── ringtone/
│   │   │   ├── RingtoneListScreen.js
│   │   │   ├── RingtoneDetailScreen.js
│   │   │   └── RingtoneUploadScreen.js
│   │   └── social/
│   │       ├── FavoritesScreen.js
│   │       ├── CollectionsScreen.js
│   │       ├── UserProfileScreen.js
│   │       └── FollowersScreen.js
│   │
│   ├── navigation/          # Navigation configuration
│   │   ├── RootNavigator.js
│   │   ├── AuthNavigator.js
│   │   ├── MainNavigator.js
│   │   └── LinkingConfiguration.js
│   │
│   ├── services/            # API & Firebase services
│   │   ├── api.js           # API client setup
│   │   ├── authService.js   # Authentication service
│   │   ├── wallpaperService.js
│   │   ├── ringtoneService.js
│   │   ├── userService.js
│   │   ├── downloadService.js
│   │   └── shareService.js
│   │
│   ├── redux/               # State management
│   │   ├── store.js
│   │   ├── slices/
│   │   │   ├── authSlice.js
│   │   │   ├── wallpaperSlice.js
│   │   │   ├── ringtoneSlice.js
│   │   │   ├── userSlice.js
│   │   │   ├── downloadSlice.js
│   │   │   └── uiSlice.js
│   │   └── middleware/
│   │       └── logger.js
│   │
│   ├── utils/               # Utility functions
│   │   ├── constants.js
│   │   ├── validators.js
│   │   ├── formatters.js
│   │   ├── permissions.js
│   │   └── helpers.js
│   │
│   ├── styles/              # Global styles
│   │   ├── colors.js
│   │   ├── typography.js
│   │   └── spacing.js
│   │
│   ├── hooks/               # Custom React hooks
│   │   ├── useAuth.js
│   │   ├── useWallpapers.js
│   │   ├── useDownload.js
│   │   └── useFavorites.js
│   │
│   ├── config/              # Configuration
│   │   ├── firebase.js
│   │   └── apiConfig.js
│   │
│   └── App.js               # Root component
│
├── android/                 # Android-specific code
├── ios/                     # iOS-specific code
├── app.json                 # App configuration
└── package.json
```

### Technology Stack

#### Core Libraries
- **react-native**: Cross-platform mobile framework
- **@react-native-async-storage/async-storage**: Local storage
- **@react-native-camera-roll/camera-roll**: Camera roll access
- **react-native-image-picker**: Image selection
- **react-native-share**: Social sharing

#### Navigation
- **@react-navigation/native**: Navigation container
- **@react-navigation/bottom-tabs**: Tab navigation
- **@react-navigation/native-stack**: Stack navigation
- **@react-navigation/drawer**: Drawer navigation

#### State Management
- **@reduxjs/toolkit**: Redux state management
- **react-redux**: React-Redux bindings
- **redux-persist**: Redux persistence

#### Firebase
- **@react-native-firebase/app**: Firebase core
- **@react-native-firebase/auth**: Authentication
- **@react-native-firebase/firestore**: Database
- **@react-native-firebase/storage**: File storage

#### HTTP Client
- **axios**: HTTP client for API calls
- **react-query**: Server state management

#### UI & UX
- **react-native-ui-lib**: UI components library
- **react-native-svg**: SVG support
- **react-native-fast-image**: Optimized image loading
- **react-native-skeleton-placeholder**: Skeleton loaders

### State Management Flow

```
User Action
    ↓
Dispatch Redux Action
    ↓
Middleware (API Call / Firebase Call)
    ↓
Update Redux State
    ↓
Component Re-render
    ↓
Update UI
```

### Redux Store Structure

```
{
  auth: {
    isLoading: boolean,
    isSignout: boolean,
    userToken: string,
    user: {
      uid, email, username, profileImage, ...
    }
  },
  wallpapers: {
    items: [],
    selectedWallpaper: null,
    isLoading: boolean,
    error: null,
    pagination: { page, totalPages }
  },
  ringtones: {
    items: [],
    selectedRingtone: null,
    isLoading: boolean,
    error: null,
    pagination: { page, totalPages }
  },
  downloads: {
    activeDownloads: [],
    downloadHistory: [],
    isLoading: boolean
  },
  favorites: {
    wallpapers: [],
    ringtones: [],
    collections: []
  },
  ui: {
    theme: 'light' | 'dark',
    bottomTabBarVisible: boolean,
    notifications: []
  }
}
```

---

## 🟢 Backend Architecture (Node.js + Express)

### Directory Structure
```
backend/
├── src/
│   ├── routes/              # API endpoints
│   │   ├── auth.routes.js
│   │   ├── wallpaper.routes.js
│   │   ├── ringtone.routes.js
│   │   ├── user.routes.js
│   │   ├── download.routes.js
│   │   ├── favorite.routes.js
│   │   ├── search.routes.js
│   │   └── index.js
│   │
│   ├── controllers/         # Request handlers
│   │   ├── authController.js
│   │   ├── wallpaperController.js
│   │   ├── ringtoneController.js
│   │   ├── userController.js
│   │   ├── downloadController.js
│   │   ├── favoriteController.js
│   │   └── searchController.js
│   │
│   ├── models/              # Data models & validation
│   │   ├── User.model.js
│   │   ├── Wallpaper.model.js
│   │   ├── Ringtone.model.js
│   │   ├── Download.model.js
│   │   └── Favorite.model.js
│   │
│   ├── services/            # Business logic
│   │   ├── authService.js
│   │   ├── wallpaperService.js
│   │   ├── ringtoneService.js
│   │   ├── userService.js
│   │   ├── fileService.js
│   │   ├── searchService.js
│   │   ├── emailService.js
│   │   └── storageService.js
│   │
│   ├── middleware/          # Custom middleware
│   │   ├── auth.middleware.js
│   │   ├── errorHandler.middleware.js
│   │   ├── validation.middleware.js
│   │   ├── requestLogger.middleware.js
│   │   ├── rateLimiter.middleware.js
│   │   └── cors.middleware.js
│   │
│   ├── utils/               # Utility functions
│   │   ├── validators.js
│   │   ├── formatters.js
│   │   ├── constants.js
│   │   ├── errorHandler.js
│   │   └── logger.js
│   │
│   ├── config/              # Configuration
│   │   ├── firebase.config.js
│   │   ├── database.config.js
│   │   └── env.config.js
│   │
│   └── server.js            # Express server setup
│
├── tests/                   # Test files
├── .env                     # Environment variables
├── .env.example             # Example env file
└── package.json
```

### Technology Stack

#### Core
- **express**: Web framework
- **express-cors**: CORS middleware
- **dotenv**: Environment variables
- **helmet**: Security headers

#### Authentication
- **firebase-admin**: Firebase Admin SDK
- **jsonwebtoken**: JWT tokens
- **bcryptjs**: Password hashing

#### Database
- **firebase-admin/firestore**: Firestore database

#### File Handling
- **multer**: File upload handling
- **sharp**: Image processing
- **ffmpeg**: Audio processing

#### Validation
- **joi**: Schema validation
- **express-validator**: Request validation

#### Utilities
- **axios**: HTTP requests
- **nodemailer**: Email sending
- **uuid**: UUID generation
- **moment**: Date/time handling

#### Development
- **nodemon**: Auto-reload
- **jest**: Testing framework
- **supertest**: API testing

### API Request/Response Flow

```
HTTP Request
    ↓
CORS Middleware
    ↓
Request Logger Middleware
    ↓
Rate Limiter Middleware
    ↓
Route Handler
    ↓
Authentication Middleware (if needed)
    ↓
Request Validation
    ↓
Controller
    ↓
Service Layer (Business Logic)
    ↓
Database Operations (Firestore)
    ↓
Response Formatting
    ↓
Error Handling (if errors)
    ↓
HTTP Response
```

---

## 🔵 Firebase Architecture

### Firebase Services Used

#### 1. **Authentication (Firebase Auth)**
```
User Registration/Login
    ↓
Firebase Auth
    ↓
Generate Auth Token
    ↓
Store Session
```

#### 2. **Database (Firestore)**

**Collections:**
```
firestore/
├── users/
│   └── {userId}/
│       ├── email: string
│       ├── username: string
│       ├── profileImage: string
│       ├── bio: string
│       ├── createdAt: timestamp
│       ├── followers: [userId]
│       ├── following: [userId]
│       └── settings: {theme, notifications, ...}
│
├── wallpapers/
│   └── {wallpaperId}/
│       ├── title: string
│       ├── description: string
│       ├── imageUrl: string
│       ├── thumbnailUrl: string
│       ├── category: string
│       ├── artist: string
│       ├── uploader: userId
│       ├── downloads: number
│       ├── favorites: number
│       ├── rating: number
│       ├── createdAt: timestamp
│       └── tags: [string]
│
├── ringtones/
│   └── {ringtoneId}/
│       ├── title: string
│       ├── artist: string
│       ├── duration: number
│       ├── audioUrl: string
│       ├── category: string
│       ├── uploader: userId
│       ├── downloads: number
│       ├── favorites: number
│       ├── rating: number
│       ├── createdAt: timestamp
│       └── tags: [string]
│
├── downloads/
│   └── {userId}/
│       └── {contentId}/
│           ├── contentType: 'wallpaper' | 'ringtone'
│           ├── downloadedAt: timestamp
│           ├── fileSize: number
│           └── expiresAt: timestamp
│
├── favorites/
│   └── {userId}/
│       └── {contentId}/
│           ├── contentType: 'wallpaper' | 'ringtone'
│           ├── savedAt: timestamp
│           └── collectionId: string
│
└── collections/
    └── {collectionId}/
        ├── name: string
        ├── description: string
        ├── owner: userId
        ├── items: [contentId]
        ├── isPublic: boolean
        ├── collaborators: [userId]
        └── createdAt: timestamp
```

#### 3. **Storage (Firebase Storage)**

**Folder Structure:**
```
storage/
├── wallpapers/
│   ├── originals/
│   │   └── {userId}/{wallpaperId}.jpg
│   ├── thumbnails/
│   │   └── {userId}/{wallpaperId}_thumb.jpg
│   └── optimized/
│       └── {userId}/{wallpaperId}_optimized.jpg
│
└── ringtones/
    ├── originals/
    │   └── {userId}/{ringtoneId}.mp3
    └── optimized/
        └── {userId}/{ringtoneId}_optimized.mp3
```

#### 4. **Cloud Functions (Firebase)**
```
Functions to implement:
├── onUserCreated()          # Initialize user data
├── onContentUploaded()      # Process & moderate content
├── onContentReported()      # Handle content reports
├── cleanupExpiredContent()  # Scheduled cleanup
├── generateRecommendations() # Generate recommendations
└── sendNotifications()      # Send push notifications
```

---

## 🔄 Data Flow Examples

### Example 1: User Downloads a Wallpaper

```
1. User clicks "Download" button in React Native app
   ↓
2. Redux dispatch DOWNLOAD_WALLPAPER action
   ↓
3. Download service calls API: POST /api/wallpapers/{id}/download
   ↓
4. Backend controller processes download
   ↓
5. Firebase increments download counter in Firestore
   ↓
6. Backend stores download record for user analytics
   ↓
7. Return download URL and metadata
   ↓
8. Frontend downloads file using native file system
   ↓
9. Update Redux download state
   ↓
10. UI updates to show download progress
```

### Example 2: User Uploads Wallpaper

```
1. User selects image & fills form in React Native
   ↓
2. Redux dispatch UPLOAD_WALLPAPER action
   ↓
3. Upload service:
   - Compress image
   - Generate thumbnail
   - Call API: POST /api/wallpapers/upload
   ↓
4. Backend receives upload:
   - Validate file
   - Store in Firebase Storage
   - Create Firestore document
   - Queue for moderation
   ↓
5. Firebase Cloud Function triggered:
   - Content scanning (profanity, NSFW, etc.)
   - Auto-approve/reject
   - Send notification to user
   ↓
6. Update user dashboard
   ↓
7. Content visible to community (if approved)
```

### Example 3: Search & Filter

```
1. User enters search query + filters in React Native
   ↓
2. Redux dispatch SEARCH action
   ↓
3. Search service calls: GET /api/search?q=query&filters=...
   ↓
4. Backend search service:
   - Parse query and filters
   - Query Firestore with filters
   - Apply sorting
   - Paginate results
   ↓
5. Return paginated results with metadata
   ↓
6. Redux updates search results state
   ↓
7. UI displays results with pagination
```

---

## 🔒 Security Architecture

### Authentication Flow
```
User Credentials
    ↓
Firebase Auth Validation
    ↓
Generate JWT Token
    ↓
Return Token to Client
    ↓
Store in Secure Storage
    ↓
Include in Request Headers
    ↓
Backend Validates Token
    ↓
Grant/Deny Access
```

### Authorization
- Role-based access control (RBAC)
- User can only modify own content
- Moderators can moderate content
- Admins have full access

### Data Security
- HTTPS for all communications
- Firebase security rules for Firestore
- Firebase Storage security rules
- Input validation on both frontend and backend
- Rate limiting on API endpoints
- JWT token expiration

---

## 📊 Database Indexes

### Firestore Indexes
```
wallpapers:
- category + createdAt (descending)
- artist + downloads (descending)
- uploader + createdAt
- rating + downloads

ringtones:
- category + createdAt (descending)
- artist + downloads (descending)
- uploader + createdAt
- duration + rating

downloads:
- userId + downloadedAt (descending)
- contentId + downloadedAt

favorites:
- userId + savedAt (descending)
- contentType + userId
```

---

## 🚀 Deployment Architecture

### Frontend Deployment
- **iOS**: App Store
- **Android**: Google Play Store
- **Staging**: TestFlight (iOS), Google Play Beta (Android)

### Backend Deployment
- **Options**: Firebase Cloud Functions, Heroku, AWS, or DigitalOcean
- **Database**: Firestore (managed by Firebase)
- **Storage**: Firebase Storage (managed by Firebase)

### CI/CD Pipeline
```
Code Push to GitHub
    ↓
Run Tests
    ↓
Build & Lint
    ↓
Deploy to Staging
    ↓
Run Integration Tests
    ↓
Manual Approval
    ↓
Deploy to Production
```

---

**Last Updated**: 2026-01-08