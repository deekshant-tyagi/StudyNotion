# ✅ StudyNotion Deployment Checklist
## Netlify + Render Deployment

Print this out and check off each step as you complete it!

## 🔧 Pre-Deployment Setup

### Create Accounts (5 minutes each)
- [ ] GitHub account created
- [ ] MongoDB Atlas account created  
- [ ] Cloudinary account created
- [ ] Razorpay account created
- [ ] Gmail App Password generated
- [ ] Netlify account created
- [ ] Render account created

### Get Your Credentials
- [ ] MongoDB connection string copied
- [ ] Cloudinary: Cloud Name, API Key, API Secret copied
- [ ] Razorpay: Key ID, Key Secret copied
- [ ] Gmail App Password copied

## 📁 Project Configuration

### Environment Files
- [ ] Copied `server/.env.example` to `server/.env`
- [ ] Filled in all values in `server/.env`
- [ ] Copied `.env.example` to `.env` 
- [ ] Will fill in frontend `.env` after backend deployment

### Upload to GitHub
- [ ] Created new GitHub repository
- [ ] Uploaded all project files
- [ ] Repository is public

## 🖥️ Backend Deployment (Render)

### Deploy Backend
- [ ] Connected Render to GitHub
- [ ] Selected repository
- [ ] Set root directory to `server`
- [ ] Set build command: `npm install`
- [ ] Set start command: `npm start`
- [ ] Added ALL environment variables from `server/.env`
- [ ] Clicked "Create Web Service"
- [ ] Waited for deployment (5-10 minutes)
- [ ] Copied backend URL (e.g., `https://studynotion-backend.onrender.com`)

## 🌐 Frontend Deployment (Netlify)

### Deploy Frontend
- [ ] Connected Netlify to GitHub
- [ ] Selected repository
- [ ] Set build command: `npm run build`
- [ ] Set publish directory: `build`
- [ ] Added environment variable: `REACT_APP_BASE_URL` = `https://your-backend-url.onrender.com/api/v1`
- [ ] Clicked "Deploy site"
- [ ] Waited for deployment (5-10 minutes)
- [ ] Copied frontend URL (e.g., `https://amazing-app-123.netlify.app`)

## 🔄 Final Configuration

### Update CORS
- [ ] Updated `FRONTEND_URL` in `server/.env` with Netlify URL
- [ ] Committed and pushed changes to GitHub
- [ ] Render automatically redeployed

## ✅ Testing

### Test All Features
- [ ] Website loads correctly
- [ ] User registration works (OTP email sent)
- [ ] User login works
- [ ] Course creation works (file upload)
- [ ] Payment flow works
- [ ] All pages load without errors

## 🎉 Success!

### Your Live URLs
- **Frontend**: ________________________________
- **Backend**: _________________________________

### Share Your Success!
- [ ] Added custom domain (optional)
- [ ] Shared with friends and family
- [ ] Added to portfolio/resume

## 🆘 If Something Goes Wrong

### Check These First:
1. **CORS Error**: Make sure `FRONTEND_URL` matches Netlify URL exactly
2. **Database Error**: Verify MongoDB connection string
3. **Payment Error**: Check Razorpay credentials
4. **Email Error**: Verify Gmail App Password
5. **Build Error**: Check Render/Netlify logs

### Get Help:
- Check `EASY_DEPLOYMENT_GUIDE.md` for detailed troubleshooting
- Look at deployment logs in Render/Netlify dashboards
- Verify all environment variables are set correctly

---

**You've got this! 🚀 Follow each step and you'll have your StudyNotion platform live in about 30 minutes!**
