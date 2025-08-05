# Quick Vercel Deployment - Forus Heavy API

## 🚀 Fast Track Deployment (5 minutes)

### Step 1: Get Your Code on GitHub
1. **Create GitHub repo**: Go to github.com → New Repository
2. **Upload your files**: Either:
   - Download your Replit project as ZIP
   - Use Replit's GitHub integration in Version Control tab

### Step 2: Deploy to Vercel
1. **Go to vercel.com** → Sign in with GitHub
2. **Click "New Project"** → Import your repository
3. **Configure settings**:
   - Framework: `Other`
   - Build Command: `npm run build`
   - Output Directory: `dist/public`
   - Root Directory: `.` (leave empty)

### Step 3: Add Environment Variables
In Vercel project settings, add:
```
OPENROUTER_API_KEY_1=your_api_key_here
OPENROUTER_API_KEY_2=your_secondary_key_here
NODE_ENV=production
```

### Step 4: Deploy
- Click **Deploy**
- Wait 2-3 minutes
- Your app will be live at `https://your-project-name.vercel.app`

## ⚠️ Important Note About WebSockets

Vercel has limitations with persistent WebSocket connections. Your chat will work, but real-time features might be limited.

## 🔧 Alternative: Railway (Better for WebSockets)

If you need full WebSocket support:
1. **Go to railway.app** → Sign in with GitHub
2. **New Project** → Deploy from GitHub repo
3. **Add environment variables** (same as above)
4. **Deploy** → Full Node.js environment with WebSocket support

## ✅ What Works After Deployment

- AI chat with dual integration
- File and image uploads
- Voice input and text-to-speech
- Theme switching
- All UI features
- Mobile responsive design

Your Forus Heavy API will run exactly like the Replit preview, but accessible worldwide!

## 🆘 Need Help?

If you encounter issues:
1. Check build logs in Vercel dashboard
2. Verify environment variables are set
3. Ensure your OpenRouter API keys are valid
4. Consider Railway for better WebSocket support