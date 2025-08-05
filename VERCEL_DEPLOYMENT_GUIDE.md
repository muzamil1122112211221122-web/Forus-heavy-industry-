# Vercel Deployment Guide for Forus Heavy API

## Prerequisites

1. **GitHub Account** - Your code needs to be in a GitHub repository
2. **Vercel Account** - Sign up at [vercel.com](https://vercel.com)
3. **OpenRouter API Keys** - Your AI service credentials

## Step-by-Step Deployment

### 1. Prepare Your Repository

**Option A: Create New GitHub Repository**
1. Go to [github.com](https://github.com) and create a new repository
2. Clone it locally: `git clone https://github.com/yourusername/forus-heavy-api`
3. Copy all your project files into the cloned folder
4. Commit and push:
   ```bash
   git add .
   git commit -m "Initial commit: Forus Heavy API"
   git push origin main
   ```

**Option B: Use Replit GitHub Integration**
1. In Replit, go to Version Control tab
2. Connect to GitHub and push your code
3. Your repository will be created automatically

### 2. Configure Package.json Scripts

Make sure your `package.json` has these scripts:
```json
{
  "scripts": {
    "dev": "NODE_ENV=development tsx server/index.ts",
    "build": "vite build && esbuild server/index.ts --platform=node --packages=external --bundle --format=esm --outdir=dist",
    "start": "NODE_ENV=production node dist/index.js",
    "vercel-build": "npm run build"
  }
}
```

### 3. Deploy to Vercel

1. **Go to Vercel Dashboard**
   - Visit [vercel.com/dashboard](https://vercel.com/dashboard)
   - Sign in with GitHub

2. **Import Your Repository**
   - Click "New Project"
   - Select your GitHub repository
   - Click "Import"

3. **Configure Build Settings**
   - Framework Preset: "Other"
   - Root Directory: `.` (leave blank)
   - Build Command: `npm run vercel-build`
   - Output Directory: `dist/public`
   - Install Command: `npm install`

4. **Set Environment Variables**
   - Click "Environment Variables"
   - Add these variables:
     ```
     OPENROUTER_API_KEY_1=your_primary_api_key_here
     OPENROUTER_API_KEY_2=your_secondary_api_key_here
     NODE_ENV=production
     SITE_URL=https://your-app-name.vercel.app
     ```

5. **Deploy**
   - Click "Deploy"
   - Wait for build to complete (2-3 minutes)
   - Your app will be live at `https://your-app-name.vercel.app`

### 4. Configure Custom Domain (Optional)

1. **In Vercel Dashboard**
   - Go to your project settings
   - Click "Domains"
   - Add your custom domain
   - Follow DNS configuration instructions

### 5. Enable Automatic Deployments

- Every push to your main branch will automatically deploy
- Pull requests create preview deployments
- Rollback available with one click

## Important Notes

### WebSocket Limitations
- Vercel serverless functions have limitations with persistent WebSocket connections
- Consider using Vercel's Edge Runtime or alternative hosting for real-time features

### Alternative Deployment Options

**If WebSocket issues occur on Vercel:**

1. **Railway** (Recommended for full-stack apps)
   - Better WebSocket support
   - Deploy from GitHub
   - Free tier available

2. **Render**
   - Full Node.js environment
   - Persistent WebSocket connections
   - Easy database integration

3. **Netlify**
   - Good for React frontends
   - Serverless functions for API

## Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Ensure all dependencies are in package.json
- Verify TypeScript compilation

### API Not Working
- Check environment variables are set correctly
- Verify OpenRouter API keys are valid
- Check function logs in Vercel dashboard

### WebSocket Issues
- Use polling fallback for real-time features
- Consider Railway or Render for better WebSocket support

## Success Checklist

- [ ] Repository pushed to GitHub
- [ ] Vercel project created and configured
- [ ] Environment variables set
- [ ] Build completes successfully
- [ ] App loads at Vercel URL
- [ ] API endpoints respond correctly
- [ ] AI chat functionality works

Your Forus Heavy API will be live and accessible worldwide once deployed!