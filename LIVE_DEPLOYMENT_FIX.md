# 🔧 Fix Live Deployment Issues

## 🚨 **Current Problem**
Your project works locally but fails when deployed live. This is because:

1. **Frontend** is trying to connect to `localhost:4000` (which doesn't exist in production)
2. **Backend** CORS is only allowing `localhost:3000` (not your live frontend URL)
3. **Environment variables** are not properly configured for production

## ✅ **Solution Steps**

### Step 1: Update Netlify Environment Variables

1. Go to your **Netlify Dashboard**
2. Click on your **StudyNotion site**
3. Go to **Site settings** → **Environment variables**
4. Add this variable:
   - **Key**: `REACT_APP_BASE_URL`
   - **Value**: `https://studynotion-backend-jw85.onrender.com/api/v1`
5. Click **Save**

### Step 2: Update Render Environment Variables

1. Go to your **Render Dashboard**
2. Click on your **StudyNotion backend service**
3. Go to **Environment**
4. Update/Add these variables:
   - **FRONTEND_URL**: `https://studyn.netlify.app` (your exact Netlify URL)
   - **PORT**: `4000`
   - **DATABASE_URL**: `mongodb+srv://deekshanttyagii:Kn78AyJUNoOb839Q@cluster0.llq7g.mongodb.net/studyNotionProject`
   - **JWT_SECRET**: `sherrr`
   - **CLOUD_NAME**: `dymekpdmp`
   - **API_KEY**: `541389431611983`
   - **API_SECRET**: `Lz4hIYn2I7yGfHVGYIUHKzFfB1E`
   - **MAIL_HOST**: `smtp.gmail.com`
   - **MAIL_USER**: `deekshanttyagii@gmail.com`
   - **MAIL_PASS**: `mvyvyamknilzbuul`
   - **FOLDER_NAME**: `CodeHelp`
   - **RAZORPAY_KEY**: `rzp_test_R8Ljduj5koYUyK`
   - **RAZORPAY_SECRET**: `hNRwXA6SsPNADye2P4fUmhFx`

### Step 3: Redeploy Both Services

1. **Render**: Your backend will automatically redeploy when you save environment variables
2. **Netlify**: Go to **Deploys** → **Trigger deploy** → **Deploy site**

### Step 4: Test the Connection

1. Wait 5-10 minutes for both deployments to complete
2. Visit your Netlify site
3. Open browser **Developer Tools** (F12)
4. Go to **Network** tab
5. Try to sign up or login
6. Check if API calls are going to your Render backend URL

## 🔍 **How to Debug Issues**

### Check Frontend API Calls:
1. Open your live site
2. Press **F12** → **Network** tab
3. Try to register/login
4. Look for API calls - they should go to `https://studynotion-backend-jw85.onrender.com/api/v1/...`
5. If they go to `localhost`, the environment variable isn't set correctly

### Check Backend CORS:
1. If you see CORS errors in browser console
2. Make sure `FRONTEND_URL` in Render exactly matches your Netlify URL
3. No trailing slashes: `https://studyn.netlify.app` (not `https://studyn.netlify.app/`)

### Check Backend Logs:
1. Go to Render Dashboard → Your service → **Logs**
2. Look for errors when frontend tries to connect
3. Check if database connection is successful

## 🚨 **Common Issues & Fixes**

### Issue 1: "Network Error" or "Failed to fetch"
**Cause**: Frontend can't reach backend
**Fix**: Check `REACT_APP_BASE_URL` in Netlify environment variables

### Issue 2: "CORS Error"
**Cause**: Backend rejecting frontend requests
**Fix**: Update `FRONTEND_URL` in Render to match your exact Netlify URL

### Issue 3: "500 Internal Server Error"
**Cause**: Backend environment variables missing
**Fix**: Add all environment variables to Render dashboard

### Issue 4: "Database connection failed"
**Cause**: MongoDB connection string issue
**Fix**: Check `DATABASE_URL` in Render environment variables

## 📋 **Quick Checklist**

- [ ] Netlify has `REACT_APP_BASE_URL` environment variable
- [ ] Render has `FRONTEND_URL` environment variable (exact Netlify URL)
- [ ] Render has all other environment variables
- [ ] Both services redeployed after environment variable changes
- [ ] No trailing slashes in URLs
- [ ] URLs use `https://` not `http://`

## 🎯 **Expected URLs**

- **Frontend**: `https://studyn.netlify.app`
- **Backend**: `https://studynotion-backend-jw85.onrender.com`
- **API Base**: `https://studynotion-backend-jw85.onrender.com/api/v1`

## 🆘 **Still Not Working?**

1. Check browser console for specific error messages
2. Check Render logs for backend errors
3. Verify all URLs are correct and accessible
4. Make sure both services are running (not sleeping)

Your StudyNotion should work perfectly after these fixes! 🚀
