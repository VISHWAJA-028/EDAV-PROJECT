# Student Academic Manager

A full-stack web application for students to manage their academic workload effectively.

## Features

- 📋 **Task Management** - Organize and manage assignments and tasks
- ⏱️ **Time Tracking** - Track study time across different subjects
- 📊 **Progress Monitoring** - Monitor academic performance
- 🔔 **Reminders** - Get notified about deadlines and exams
- 🎯 **Goal Setting** - Set and track academic goals

## Tech Stack

### Backend
- Node.js with Express
- TypeScript
- MongoDB with Mongoose ODM
- JWT Authentication
- CORS enabled

### Frontend
- React 18
- TypeScript
- React Router v6
- Axios for API calls

## Prerequisites

Before you begin, ensure you have installed:
- Node.js (v14 or higher)
- npm or yarn
- MongoDB Community Server or MongoDB Atlas account

## Installation & Setup

### 1. MongoDB Setup

#### Option A: Local MongoDB Installation
```bash
# On Windows, download from https://www.mongodb.com/try/download/community
# Or use Chocolatey:
choco install mongodb-community

# Start MongoDB service
net start MongoDB
```

#### Option B: MongoDB Atlas (Cloud)
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account
3. Create a cluster
4. Get your connection string
5. Update `MONGODB_URI` in `.env` file

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# Edit .env with your MongoDB URI
# Example for local MongoDB:
# MONGODB_URI=mongodb://localhost:27017/student-manager

# Build TypeScript
npm run build

# Start development server
npm run dev
```

The backend will be available at `http://localhost:5000`

### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# Start development server
npm start
```

The frontend will be available at `http://localhost:3000`

## Project Structure

```
student/
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   └── database.ts          # Database connection
│   │   ├── models/
│   │   │   ├── User.ts             # User schema
│   │   │   ├── Task.ts             # Task schema
│   │   │   ├── Goal.ts             # Goal schema
│   │   │   ├── TimeEntry.ts        # Time tracking schema
│   │   │   └── Reminder.ts         # Reminder schema
│   │   ├── routes/                 # API routes
│   │   ├── controllers/            # Request handlers
│   │   ├── middleware/             # Custom middleware
│   │   ├── utils/                  # Utility functions
│   │   └── server.ts               # Server entry point
│   ├── .env.example
│   ├── .eslintrc.json
│   ├── tsconfig.json
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/             # React components
│   │   ├── pages/                  # Page components
│   │   ├── hooks/                  # Custom React hooks
│   │   ├── context/                # React context
│   │   ├── styles/                 # CSS files
│   │   ├── App.tsx
│   │   └── index.tsx
│   ├── public/
│   ├── .env.example
│   ├── .eslintrc.json
│   ├── tsconfig.json
│   └── package.json
└── README.md
```

## Database Schema

### User
- `username` (String, unique)
- `email` (String, unique)
- `password` (String, hashed)
- `fullName` (String)

### Task
- `userId` (Reference to User)
- `title` (String)
- `description` (String)
- `subject` (String)
- `dueDate` (Date)
- `priority` (low | medium | high)
- `status` (pending | in-progress | completed)
- `estimatedHours` (Number)
- `actualHours` (Number)

### Goal
- `userId` (Reference to User)
- `title` (String)
- `description` (String)
- `subject` (String)
- `targetValue` (Number)
- `currentValue` (Number)
- `unit` (String, default: %)
- `dueDate` (Date)
- `status` (not-started | in-progress | completed)

### TimeEntry
- `userId` (Reference to User)
- `taskId` (Reference to Task, optional)
- `subject` (String)
- `duration` (Number, in minutes)
- `date` (Date)
- `notes` (String)

### Reminder
- `userId` (Reference to User)
- `taskId` (Reference to Task, optional)
- `title` (String)
- `message` (String)
- `reminderDate` (Date)
- `type` (deadline | exam | study | custom)
- `isActive` (Boolean)
- `isSent` (Boolean)

## Available Scripts

### Backend
```bash
npm run dev     # Start development server with hot reload
npm run build   # Build TypeScript to JavaScript
npm start       # Start production server
npm test        # Run tests
npm run lint    # Run ESLint
```

### Frontend
```bash
npm start       # Start development server
npm run build   # Create production build
npm test        # Run tests
npm run lint    # Run ESLint
```

## Environment Variables

### Backend (.env)
```
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/student-manager
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d
CORS_ORIGIN=http://localhost:3000
```

### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

## MongoDB Connection Verification

To verify your MongoDB connection is working:

1. **Check if MongoDB is running:**
   - Windows: `tasklist | findstr mongod`
   - Mac/Linux: `ps aux | grep mongod`

2. **Connect using MongoDB Shell:**
   ```bash
   mongosh
   # or older version
   mongo
   ```

3. **View databases:**
   ```
   show dbs
   use student-manager
   show collections
   ```

4. **Check API health:**
   ```bash
   curl http://localhost:5000/api/health
   ```

## Troubleshooting

### MongoDB Connection Error
- Ensure MongoDB service is running
- Check `MONGODB_URI` in `.env` file
- For Atlas, whitelist your IP address
- Verify network connectivity

### Port Already in Use
```bash
# Windows - Kill process on port 5000
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Mac/Linux
lsof -ti:5000 | xargs kill -9
```

### Missing Dependencies
```bash
# Reinstall node_modules
rm -rf node_modules package-lock.json
npm install
```

## Future Enhancements

- [ ] User authentication & authorization
- [ ] Email notifications for reminders
- [ ] Advanced analytics dashboard
- [ ] Collaborative study groups
- [ ] Mobile app version
- [ ] AI-powered study recommendations

## License

MIT License - feel free to use this project for your own purposes

## Support

For issues and questions, please create an issue in the repository.
