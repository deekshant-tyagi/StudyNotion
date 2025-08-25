# 🚀 Complete MERN Stack Deployment Guide

## Deploy Any MERN Project to Production (Netlify + Render)

This guide will help you deploy any MERN stack project with separate frontend and backend folders to production using Netlify (frontend) and Render (backend).

## 📁 Project Structure Requirements

Your project should have this structure:

```
your-project/
├── src/              (React frontend files)
├── public/           (Frontend assets)
├── server/           (Node.js backend files)
├── package.json      (Frontend dependencies)
└── server/package.json (Backend dependencies)
```

## 🔧 Prerequisites & Setup

### 1. Required Accounts (All Free)

- [GitHub](https://github.com) - Code repository
- [MongoDB Atlas](https://www.mongodb.com/atlas) - Database
- [Cloudinary](https://cloudinary.com) - File storage (if needed)
- [Netlify](https://netlify.com) - Frontend hosting
- [Render](https://render.com) - Backend hosting
- Gmail App Password - For email services

### 2. Get Service Credentials

#### MongoDB Atlas:

1. Create cluster → Connect → Get connection string
2. Format: `mongodb+srv://username:password@cluster.mongodb.net/dbname`

#### Cloudinary (if using file uploads):

1. Dashboard → Copy: Cloud Name, API Key, API Secret

#### Gmail App Password:

1. Enable 2FA on Gmail
2. Generate App Password for your application

## 📝 Configuration Files Setup

### 1. Frontend Environment Configuration

Create `.env` in project root:

```env
# For local development
REACT_APP_BASE_URL=http://localhost:4000/api/v1

# For production (comment out local, uncomment production)
# REACT_APP_BASE_URL=https://your-backend-name.onrender.com/api/v1
```

Create `.env.example` in project root:

```env
# Backend API URL
REACT_APP_BASE_URL=https://your-backend-name.onrender.com/api/v1
```

### 2. Backend Environment Configuration

Create `server/.env`:

```env
# Server
PORT=4000

# Database
DATABASE_URL=your_mongodb_connection_string

# JWT
JWT_SECRET=your_super_secret_jwt_key

# Cloudinary (if using file uploads)
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=your_folder_name

# Email (if using email services)
MAIL_HOST=smtp.gmail.com
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_gmail_app_password

# Payment (if using Razorpay)
RAZORPAY_KEY=your_razorpay_key
RAZORPAY_SECRET=your_razorpay_secret

# CORS - Frontend URL
FRONTEND_URL=http://localhost:3000
```

Create `server/.env.example`:

```env
DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/dbname
JWT_SECRET=your_jwt_secret
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=your_folder_name
MAIL_HOST=smtp.gmail.com
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_gmail_app_password
RAZORPAY_KEY=your_razorpay_key
RAZORPAY_SECRET=your_razorpay_secret
PORT=4000
FRONTEND_URL=https://your-app-name.netlify.app
```

### 3. Frontend API Configuration

Ensure your `src/services/apis.js` (or similar) uses environment variables:

```javascript
const BASE_URL =
  process.env.REACT_APP_BASE_URL || "http://localhost:4000/api/v1";
```

### 4. Backend CORS Configuration

Ensure your `server/index.js` has proper CORS setup:

```javascript
const allowedOrigins = [
  "http://localhost:3000", // Local development
  process.env.FRONTEND_URL, // Production frontend URL
].filter(Boolean);

app.use(
  cors({
    origin: function (origin, callback) {
      if (!origin) return callback(null, true);
      if (allowedOrigins.indexOf(origin) !== -1) {
        callback(null, true);
      } else {
        callback(new Error("Not allowed by CORS"));
      }
    },
    credentials: true,
  })
);
```

### 5. Build Configuration

Update `package.json` scripts to handle build warnings:

```json
{
  "scripts": {
    "build": "set CI=false && react-scripts build",
    "build:unix": "CI=false react-scripts build"
  }
}
```

### 6. Netlify Configuration

Create `netlify.toml` in project root:

```toml
[build]
  base = "."
  publish = "build"
  command = "npm run build"

[build.environment]
  NODE_VERSION = "18"
  CI = "false"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"

[[headers]]
  for = "/static/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

## 🚀 Deployment Steps

### Step 1: Upload to GitHub

1. Create new repository on GitHub
2. Upload all your project files
3. Make repository public
4. Note your repository URL

### Step 2: Deploy Backend (Render)

1. Go to [Render Dashboard](https://dashboard.render.com)
2. Sign up with GitHub
3. **New** → **Web Service**
4. Connect your GitHub repository
5. Configure:
   - **Name**: `your-project-backend`
   - **Root Directory**: `server`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
6. **Advanced** → Add ALL environment variables from `server/.env`
7. **Create Web Service**
8. Wait 5-10 minutes for deployment
9. **Copy your backend URL**: `https://your-project-backend.onrender.com`

### Step 3: Deploy Frontend (Netlify)

1. Go to [Netlify Dashboard](https://app.netlify.com)
2. Sign up with GitHub
3. **New site from Git**
4. Choose your GitHub repository
5. Configure:
   - **Build command**: `npm run build`
   - **Publish directory**: `build`
6. **Advanced build settings** → **Environment variables**:
   - **Key**: `REACT_APP_BASE_URL`
   - **Value**: `https://your-project-backend.onrender.com/api/v1`
7. **Deploy site**
8. Wait 5-10 minutes
9. **Copy your frontend URL**: `https://amazing-app-123.netlify.app`

### Step 4: Update CORS Configuration

1. Go back to **Render Dashboard** → Your backend service
2. **Environment** tab
3. Update `FRONTEND_URL` with your Netlify URL (exact URL, no trailing slash)
4. **Save Changes** (auto-redeploys)

### Step 5: Test Deployment

1. Wait 5-10 minutes for all deployments to complete
2. Visit your Netlify frontend URL
3. Test all functionality:
   - User registration/login
   - API calls
   - File uploads (if applicable)
   - Payment flow (if applicable)

## 🔍 Troubleshooting Common Issues

### Issue 1: CORS Errors

**Error**: "blocked by CORS policy"
**Solution**:

- Check `FRONTEND_URL` in Render matches your Netlify URL exactly
- No trailing slashes in URLs
- Redeploy backend after changes

### Issue 2: Environment Variables Not Working

**Error**: API calls going to wrong URL or undefined
**Solution**:

- Check Netlify environment variables
- Ensure `REACT_APP_BASE_URL` is set correctly
- Redeploy frontend after changes

### Issue 3: Backend Not Responding

**Error**: Network timeouts, 500 errors
**Solution**:

- Check Render logs for errors
- Verify all environment variables are set
- Visit backend URL to wake it up (free tier sleeps)

### Issue 4: Build Failures

**Error**: ESLint warnings causing build to fail
**Solution**:

- Use `CI=false` in build script
- Check `netlify.toml` configuration
- Review build logs for specific errors

### Issue 5: Database Connection Issues

**Error**: "Database connection failed"
**Solution**:

- Verify MongoDB connection string
- Check database user permissions
- Ensure IP whitelist includes 0.0.0.0/0

## 📋 Pre-Deployment Checklist

### Code Preparation:

- [ ] Frontend uses environment variables for API URL
- [ ] Backend has proper CORS configuration
- [ ] All sensitive data in environment variables
- [ ] Build script handles warnings properly
- [ ] Database connection string is correct

### Service Setup:

- [ ] GitHub repository created and uploaded
- [ ] MongoDB Atlas cluster created
- [ ] Cloudinary account setup (if needed)
- [ ] Gmail App Password generated (if needed)
- [ ] Payment service setup (if needed)

### Deployment:

- [ ] Backend deployed to Render with all environment variables
- [ ] Frontend deployed to Netlify with API URL
- [ ] CORS updated with frontend URL
- [ ] All services tested and working

## 🎯 Success Indicators

Your deployment is successful when:

- ✅ Frontend loads without errors
- ✅ API calls reach backend successfully
- ✅ No CORS errors in browser console
- ✅ Database operations work
- ✅ File uploads work (if applicable)
- ✅ Email services work (if applicable)
- ✅ Payment flow works (if applicable)

## 💡 Pro Tips

1. **Free Tier Limitations**: Render free tier sleeps after 15 minutes of inactivity
2. **Environment Variables**: Always use environment variables for sensitive data
3. **HTTPS**: Both Netlify and Render provide free HTTPS
4. **Custom Domains**: You can add custom domains in both services
5. **Monitoring**: Check service logs regularly for issues
6. **Backup**: Keep environment variables backed up securely

## 🔄 Updating Your Deployment

### Code Changes:

1. Push changes to GitHub
2. Netlify auto-deploys on push
3. Render auto-deploys on push

### Environment Variable Changes:

1. Update in respective service dashboard
2. Services will auto-redeploy
3. Wait 5-10 minutes for changes to take effect

---

## 📞 Support

If you encounter issues:

1. Check service logs (Render/Netlify dashboards)
2. Verify all environment variables
3. Test each service independently
4. Check network requests in browser dev tools

**Your MERN stack application should now be live and accessible worldwide!** 🎉
