# Task Manager - Full Stack Web Application

A modern, scalable task management application built with React, TypeScript, and Supabase, featuring JWT-based authentication and comprehensive CRUD operations.

## Features

### Authentication
- Email/password authentication with JWT tokens
- Secure signup and login flows
- Protected routes requiring authentication
- Session management with automatic token refresh
- Client-side and server-side validation

### Dashboard
- User profile display
- Task statistics overview
- Real-time task synchronization
- Responsive design for all devices

### Task Management (CRUD Operations)
- Create new tasks with title, description, status, and priority
- Read and display all user tasks
- Update task details and status
- Delete tasks with confirmation
- Filter tasks by status and priority
- Search tasks by title or description
- Task statistics and analytics

## Tech Stack

### Frontend
- **React 18** - Modern UI library
- **TypeScript** - Type-safe development
- **Vite** - Fast build tool and dev server
- **TailwindCSS** - Utility-first CSS framework
- **Lucide React** - Beautiful icon library

### Backend
- **Supabase** - Backend-as-a-Service platform
- **PostgreSQL** - Relational database
- **Edge Functions** - Serverless TypeScript functions
- **Row Level Security (RLS)** - Database-level security

### Security
- JWT token-based authentication
- Password hashing (handled by Supabase Auth)
- Row Level Security policies
- CORS configuration
- Environment variable protection
- Secure API endpoints

## Project Structure

```
├── src/
│   ├── components/          # React components
│   │   ├── Dashboard.tsx    # Main dashboard view
│   │   ├── Login.tsx        # Login form
│   │   ├── Signup.tsx       # Registration form
│   │   ├── Header.tsx       # Navigation header
│   │   ├── FilterBar.tsx    # Task filtering UI
│   │   ├── TaskList.tsx     # Task list container
│   │   ├── TaskCard.tsx     # Individual task card
│   │   └── TaskForm.tsx     # Create/edit task form
│   ├── contexts/
│   │   └── AuthContext.tsx  # Authentication state management
│   ├── lib/
│   │   └── supabase.ts      # Supabase client configuration
│   ├── App.tsx              # Main app component with routing
│   ├── main.tsx             # Application entry point
│   └── index.css            # Global styles
├── supabase/
│   ├── migrations/          # Database migrations
│   └── functions/           # Edge Functions
│       └── tasks/           # Task CRUD API
└── dist/                    # Production build output
```

## Getting Started

### Prerequisites
- Node.js 18+ and npm
- Supabase account (already configured)

### Installation

1. Install dependencies:
```bash
npm install
```

2. Environment variables are already configured in `.env`:
```
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

3. Run development server:
```bash
npm run dev
```

4. Build for production:
```bash
npm run build
```

5. Preview production build:
```bash
npm run preview
```

## Database Schema

### Tasks Table
- `id` (uuid) - Primary key
- `user_id` (uuid) - Foreign key to auth.users
- `title` (text) - Task title (required)
- `description` (text) - Task description
- `status` (text) - Task status (pending, in_progress, completed)
- `priority` (text) - Task priority (low, medium, high)
- `created_at` (timestamptz) - Creation timestamp
- `updated_at` (timestamptz) - Last update timestamp

### Security Policies
- Users can only view their own tasks
- Users can only create tasks for themselves
- Users can only update their own tasks
- Users can only delete their own tasks

## API Endpoints

All API endpoints are implemented as Supabase Edge Functions:

### Tasks API (`/functions/v1/tasks`)

**Authentication Required**: All endpoints require Bearer token in Authorization header

- `GET /tasks` - Get all tasks for authenticated user
  - Query params: `status`, `priority`, `search`

- `GET /tasks/:id` - Get single task by ID

- `POST /tasks` - Create new task
  - Body: `{ title, description?, status?, priority? }`

- `PUT /tasks/:id` - Update task
  - Body: `{ title?, description?, status?, priority? }`

- `DELETE /tasks/:id` - Delete task

## Form Validation

### Client-Side Validation
- Email format validation
- Password length requirements (minimum 6 characters)
- Password confirmation matching
- Required field validation
- Real-time error feedback

### Server-Side Validation
- Authentication token verification
- User authorization checks
- Data type validation
- Database constraint enforcement

## Security Best Practices

1. **Authentication**
   - JWT tokens with automatic refresh
   - Secure password handling via Supabase Auth
   - Session persistence across page reloads

2. **Authorization**
   - Row Level Security (RLS) policies
   - User-scoped data access
   - Server-side permission checks

3. **Data Protection**
   - Environment variables for sensitive data
   - HTTPS-only communication
   - CORS properly configured
   - SQL injection prevention via parameterized queries

4. **API Security**
   - Token validation on all requests
   - Rate limiting (via Supabase)
   - Error message sanitization

## Scalability Considerations

### Current Architecture Benefits
- **Serverless Functions**: Auto-scaling Edge Functions
- **Database**: Managed PostgreSQL with connection pooling
- **CDN**: Static assets served via CDN
- **Caching**: Browser caching and API response caching

### Production Scaling Strategies

1. **Database Optimization**
   - Indexes on frequently queried columns (user_id, status, priority)
   - Query optimization with proper joins
   - Database connection pooling
   - Read replicas for high-traffic scenarios

2. **API Performance**
   - Edge Functions deployed globally
   - Response caching for read-heavy operations
   - Pagination for large datasets
   - GraphQL for complex queries (future enhancement)

3. **Frontend Optimization**
   - Code splitting and lazy loading
   - Asset optimization and compression
   - Service Workers for offline support
   - Progressive Web App (PWA) features

4. **Monitoring & Observability**
   - Error tracking (Sentry integration)
   - Performance monitoring
   - User analytics
   - Server logs and metrics

5. **Infrastructure**
   - Multi-region deployment
   - Load balancing
   - Automated backups
   - Disaster recovery plan

## Development Best Practices

- **Type Safety**: Full TypeScript coverage
- **Code Organization**: Component-based architecture
- **State Management**: React Context for global state
- **Error Handling**: Comprehensive error boundaries
- **Testing**: Unit tests for components and integration tests
- **Documentation**: Inline code comments and README

## Future Enhancements

- Task categories and tags
- Task due dates and reminders
- File attachments
- Task sharing and collaboration
- Email notifications
- Dark mode support
- Mobile app (React Native)
- Real-time updates (WebSocket)
- Task templates
- Advanced analytics and reporting

## Testing

### Manual Testing Checklist

**Authentication:**
- [ ] Sign up with valid email/password
- [ ] Sign up with invalid email (error handling)
- [ ] Sign up with short password (validation)
- [ ] Sign in with correct credentials
- [ ] Sign in with incorrect credentials (error handling)
- [ ] Session persistence after page reload
- [ ] Sign out functionality

**Task Management:**
- [ ] Create new task
- [ ] Edit existing task
- [ ] Delete task (with confirmation)
- [ ] Change task status
- [ ] Filter tasks by status
- [ ] Filter tasks by priority
- [ ] Search tasks by title
- [ ] Search tasks by description

**Security:**
- [ ] Unauthorized users cannot access dashboard
- [ ] Users can only see their own tasks
- [ ] API returns 401 for invalid tokens
- [ ] CORS headers properly configured

**Responsive Design:**
- [ ] Mobile view (< 768px)
- [ ] Tablet view (768px - 1024px)
- [ ] Desktop view (> 1024px)

## Deployment

The application can be deployed to various platforms:

### Vercel (Recommended)
```bash
npm install -g vercel
vercel
```

### Netlify
```bash
npm install -g netlify-cli
netlify deploy
```

### Docker
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 4173
CMD ["npm", "run", "preview"]
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request
