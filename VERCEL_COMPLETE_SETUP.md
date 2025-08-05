# Complete Vercel Upload Files - Fixed Configuration

## Upload These Files to Your GitHub Repository

### 1. Updated vercel.json (CRITICAL)
The main configuration file has been fixed. Upload this updated version to your repository.

### 2. Required Project Structure
Make sure your GitHub repository has this exact structure:
```
forus-heavy-api/
├── server/
│   ├── index.ts           ← Main server file
│   ├── routes.ts
│   ├── storage.ts
│   ├── vite.ts
│   └── services/
│       └── ai-service.ts
├── client/
│   ├── index.html         ← Entry point HTML
│   └── src/
│       ├── main.tsx       ← React entry
│       ├── App.tsx
│       ├── index.css
│       ├── components/
│       ├── hooks/
│       ├── lib/
│       └── pages/
├── shared/
│   └── schema.ts
├── package.json           ← Dependencies
├── vite.config.ts         ← Build config
├── vercel.json           ← UPDATED - Upload this
├── tailwind.config.ts
├── tsconfig.json
├── components.json
├── postcss.config.js
└── drizzle.config.ts
```

## Vercel Deployment Steps

### Step 1: Update Repository
1. **Go to your GitHub repository**
2. **Upload the updated `vercel.json` file** (replace the old one)
3. **Verify all other files are present**

### Step 2: Vercel Project Settings
1. **In Vercel dashboard** → Go to your project settings
2. **Build & Development Settings:**
   - Framework Preset: **Other**
   - Build Command: `npm run build`
   - Output Directory: `dist/public`
   - Install Command: `npm install`
   - Node.js Version: **18.x**

### Step 3: Environment Variables
**Add these in Vercel Environment Variables section:**
- `OPENROUTER_API_KEY_1` = your primary API key
- `OPENROUTER_API_KEY_2` = your secondary API key  
- `NODE_ENV` = production

### Step 4: Deploy
1. **Click "Redeploy"** in Vercel dashboard
2. **Wait for build to complete** (3-5 minutes)
3. **Check build logs** for any errors
4. **Visit your live URL**

## Key Changes Made

### Fixed vercel.json Configuration:
- **Proper build source**: Uses `package.json` for static build
- **Correct routing**: API routes go to server, everything else to HTML
- **Build output**: Points to correct `dist/public` directory
- **Function timeout**: Set to 30 seconds for AI responses

### Build Process:
1. **Frontend**: Vite builds React app to `dist/public/`
2. **Backend**: ESBuild bundles server to `dist/index.js`
3. **Vercel**: Serves frontend files and routes API calls

## Troubleshooting

### If Build Fails:
- Check Node.js version is 18.x
- Verify all dependencies in package.json
- Check build logs for specific errors

### If 404 Still Occurs:
- Verify `dist/public/index.html` exists after build
- Check routing configuration in vercel.json
- Ensure environment variables are set

### If API Doesn't Work:
- Verify API keys are correctly set
- Check server function logs in Vercel
- Test API endpoints individually

The updated configuration should resolve the deployment issues. Upload the corrected vercel.json and redeploy.