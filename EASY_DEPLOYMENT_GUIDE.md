# 🚀 Super Easy StudyNotion Deployment Guide
## Netlify (Frontend) + Render (Backend)

Follow these steps exactly - no technical knowledge required! 

## 📋 What You'll Need (5 minutes setup)

### 1. Create Free Accounts
- [GitHub](https://github.com) - to store your code
- [MongoDB Atlas](https://www.mongodb.com/atlas) - for database
- [Cloudinary](https://cloudinary.com) - for file uploads
- [Razorpay](https://razorpay.com) - for payments
- [Netlify](https://netlify.com) - for frontend
- [Render](https://render.com) - for backend

### 2. Get Gmail App Password
1. Go to your Gmail settings
2. Enable 2-factor authentication
3. Generate an "App Password" for StudyNotion
4. Save this password - you'll need it later

## 🗄️ Step 1: Setup Database (MongoDB Atlas)

1. Go to [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Click "Try Free" and create account
3. Create a new cluster (choose FREE tier)
4. Click "Connect" → "Connect your application"
5. Copy the connection string (looks like: `mongodb+srv://username:password@cluster...`)
6. Replace `<password>` with your actual password
7. Save this connection string

## 📁 Step 2: Setup File Storage (Cloudinary)

1. Go to [Cloudinary](https://cloudinary.com)
2. Sign up for free account
3. Go to Dashboard
4. Copy these 3 values:
   - Cloud Name
   - API Key  
   - API Secret
5. Save these values

## 💳 Step 3: Setup Payments (Razorpay)

1. Go to [Razorpay](https://razorpay.com)
2. Create account
3. Go to Settings → API Keys
4. Copy:
   - Key ID
   - Key Secret
5. Save these values

## 🔧 Step 4: Configure Your Project

### 4.1 Create Backend Environment File
1. In your project, go to `server` folder
2. Copy `.env.example` to `.env`
3. Open `.env` and fill in:

```env
DATABASE_URL=your_mongodb_connection_string_from_step1
JWT_SECRET=make_up_a_long_random_password_here
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=studynotion
RAZORPAY_KEY=your_razorpay_key_id
RAZORPAY_SECRET=your_razorpay_secret
MAIL_HOST=smtp.gmail.com
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_gmail_app_password
PORT=4000
FRONTEND_URL=https://your-app-name.netlify.app
```

### 4.2 Create Frontend Environment File
1. In your project root, copy `.env.example` to `.env`
2. Fill in:

```env
REACT_APP_BASE_URL=https://your-backend-name.onrender.com/api/v1
```

## 📤 Step 5: Upload to GitHub

1. Go to [GitHub](https://github.com)
2. Click "New repository"
3. Name it "studynotion" 
4. Make it public
5. Upload all your project files (drag and drop works!)

## 🖥️ Step 6: Deploy Backend (Render)

1. Go to [Render](https://render.com)
2. Sign up with GitHub
3. Click "New" → "Web Service"
4. Connect your GitHub repository
5. Choose the `server` folder as root directory
6. Fill in:
   - **Name**: studynotion-backend
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
7. Click "Advanced" and add ALL environment variables from your `server/.env` file
8. Click "Create Web Service"
9. Wait 5-10 minutes for deployment
10. Copy your backend URL (like: `https://studynotion-backend.onrender.com`)

## 🌐 Step 7: Deploy Frontend (Netlify)

1. Go to [Netlify](https://netlify.com)
2. Sign up with GitHub
3. Click "New site from Git"
4. Choose your GitHub repository
5. Fill in:
   - **Build command**: `npm run build`
   - **Publish directory**: `build`
6. Click "Advanced build settings"
7. Add environment variable:
   - **Key**: `REACT_APP_BASE_URL`
   - **Value**: `https://your-backend-url.onrender.com/api/v1`
8. Click "Deploy site"
9. Wait 5-10 minutes
10. Your site is live!

## 🔄 Step 8: Update CORS (Important!)

1. Go back to your `server/.env` file
2. Update `FRONTEND_URL` with your Netlify URL
3. Commit and push changes to GitHub
4. Render will automatically redeploy

## ✅ Step 9: Test Everything

1. Visit your Netlify site
2. Try signing up (should send OTP email)
3. Try logging in
4. Test course creation
5. Test payment flow

## 🎉 You're Live!

Your StudyNotion platform is now live on the internet!

- **Frontend**: Your Netlify URL
- **Backend**: Your Render URL
- **Database**: MongoDB Atlas
- **Files**: Cloudinary
- **Payments**: Razorpay

## 🆘 Having Issues?

### Common Problems:

**"CORS Error"**
- Make sure `FRONTEND_URL` in backend matches your Netlify URL exactly

**"Database connection failed"**
- Check your MongoDB connection string
- Make sure you replaced `<password>` with actual password

**"Payment not working"**
- Verify Razorpay keys are correct
- Make sure you're using test mode initially

**"Files not uploading"**
- Check Cloudinary credentials
- Verify all 3 values (cloud name, API key, secret)

**"Emails not sending"**
- Make sure you're using Gmail App Password, not regular password
- Check 2-factor authentication is enabled

## 💡 Pro Tips

1. **Custom Domain**: You can add your own domain in Netlify settings
2. **HTTPS**: Both Netlify and Render provide free HTTPS
3. **Monitoring**: Check Render logs if backend has issues
4. **Updates**: Push to GitHub to automatically update both sites

That's it! Your StudyNotion platform is now live and ready for users! 🚀
