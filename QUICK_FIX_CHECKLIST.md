# ⚡ Quick Fix for Live Deployment

## 🎯 **The Problem**
Your local project works but live deployment doesn't because:
- Frontend is looking for backend at `localhost:4000` (doesn't exist in production)
- Backend is only allowing `localhost:3000` (not your live frontend)

## 🔧 **5-Minute Fix**

### 1. Fix Netlify (Frontend)
1. Go to [Netlify Dashboard](https://app.netlify.com)
2. Click your **StudyNotion site**
3. **Site settings** → **Environment variables**
4. **Add variable**:
   - **Key**: `REACT_APP_BASE_URL`
   - **Value**: `https://studynotion-backend-jw85.onrender.com/api/v1`
5. **Save**

### 2. Fix Render (Backend)
1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click your **StudyNotion backend**
3. **Environment** tab
4. **Add/Update**:
   - **FRONTEND_URL**: `https://studyn.netlify.app`
5. **Save Changes**

### 3. Redeploy
1. **Netlify**: Deploys → **Trigger deploy**
2. **Render**: Will auto-redeploy when you save environment variables

### 4. Wait & Test
1. Wait **5-10 minutes**
2. Visit your live site
3. Try signing up/logging in

## ✅ **How to Verify It's Fixed**

1. Open your live site
2. Press **F12** (Developer Tools)
3. Go to **Network** tab
4. Try to register
5. You should see API calls going to `https://studynotion-backend-jw85.onrender.com/api/v1/...`

## 🚨 **If Still Not Working**

Check `LIVE_DEPLOYMENT_FIX.md` for detailed troubleshooting.

## 📱 **Your Live URLs**
- **Frontend**: https://studyn.netlify.app
- **Backend**: https://studynotion-backend-jw85.onrender.com
- **API**: https://studynotion-backend-jw85.onrender.com/api/v1

That's it! Your StudyNotion should work live now! 🚀
