# Complete Step-by-Step Deployment Guide
## Deploy Forus Heavy API to Live Web Application

### PART 1: Prepare Your Code (5 minutes)

#### Step 1: Download Your Project
1. **In Replit**: Click the three dots menu (⋯) next to your project name
2. **Select "Download as zip"**
3. **Save the file** to your computer
4. **Extract the zip file** to a folder (like `forus-heavy-api`)

#### Step 2: Create GitHub Account (if needed)
1. **Go to** [github.com](https://github.com)
2. **Click "Sign up"** if you don't have an account
3. **Follow the registration process**
4. **Verify your email address**

#### Step 3: Create New Repository
1. **Sign in to GitHub**
2. **Click the green "New" button** (or go to github.com/new)
3. **Repository name**: `forus-heavy-api`
4. **Description**: `AI chat application with dual API integration`
5. **Make it Public** (check the Public radio button)
6. **Don't add README, .gitignore, or license** (we have our files)
7. **Click "Create repository"**

#### Step 4: Upload Your Code
1. **On the new repository page**, click "uploading an existing file"
2. **Drag and drop** all files from your extracted folder
3. **Or click "choose your files"** and select all project files
4. **Commit message**: `Initial commit: Forus Heavy API`
5. **Click "Commit changes"**

### PART 2: Deploy to Vercel (10 minutes)

#### Step 5: Create Vercel Account
1. **Go to** [vercel.com](https://vercel.com)
2. **Click "Sign Up"**
3. **Choose "Continue with GitHub"**
4. **Authorize Vercel** to access your GitHub account
5. **Complete your profile setup**

#### Step 6: Import Your Project
1. **In Vercel Dashboard**, click "New Project"
2. **Find your repository** `forus-heavy-api` in the list
3. **Click "Import"** next to it
4. **If asked for permissions**, click "Install" to give Vercel access

#### Step 7: Configure Build Settings
1. **Framework Preset**: Select "Other" from dropdown
2. **Root Directory**: Leave blank (default is correct)
3. **Build Command**: `npm run build`
4. **Output Directory**: `dist/public`
5. **Install Command**: `npm install`
6. **Don't change anything else**

#### Step 8: Add Environment Variables
1. **Click "Environment Variables"** section
2. **Add these three variables**:

   **Variable 1:**
   - Name: `OPENROUTER_API_KEY_1`
   - Value: [Your OpenRouter API key]
   
   **Variable 2:**
   - Name: `OPENROUTER_API_KEY_2`
   - Value: [Your secondary API key or same as first]
   
   **Variable 3:**
   - Name: `NODE_ENV`
   - Value: `production`

3. **Click "Add" for each variable**

#### Step 9: Deploy
1. **Click the blue "Deploy" button**
2. **Wait for build** (2-4 minutes)
3. **Watch the build logs** - you'll see:
   - Installing dependencies
   - Building your app
   - Deploying to Vercel

#### Step 10: Access Your Live App
1. **When build completes**, you'll see "Your project has been deployed"
2. **Click the URL** (like `https://forus-heavy-api-xyz.vercel.app`)
3. **Your app is now live on the internet!**

### PART 3: Test Your Deployed App (5 minutes)

#### Step 11: Verify Everything Works
1. **Open your live URL** in a web browser
2. **Check the interface** loads correctly
3. **Try typing a message** in the chat
4. **Test AI responses** are working
5. **Check file upload** button works
6. **Try theme switching** (light/dark mode)

### PART 4: Share Your App

#### Step 12: Get Your Live URL
Your app is now accessible at: `https://your-project-name.vercel.app`

**Share this URL with anyone** - they can use your AI chat app from any device!

### TROUBLESHOOTING

#### If Build Fails:
1. **Check build logs** in Vercel dashboard
2. **Verify all files** were uploaded to GitHub
3. **Check environment variables** are set correctly

#### If AI Chat Doesn't Work:
1. **Verify OpenRouter API keys** are correct
2. **Check the keys have credits/quota**
3. **Try regenerating the API keys**

#### If Upload Fails to GitHub:
1. **Try smaller batches** of files
2. **Use GitHub Desktop** application instead
3. **Or use git command line** if familiar

### ALTERNATIVE: Railway Deployment (Better WebSocket Support)

If you want better real-time chat features:

1. **Go to** [railway.app](https://railway.app)
2. **Sign in with GitHub**
3. **New Project** → "Deploy from GitHub repo"
4. **Select your repository**
5. **Add same environment variables**
6. **Deploy** - Railway handles full Node.js better

### SUCCESS CHECKLIST

- [ ] Project downloaded from Replit
- [ ] GitHub repository created
- [ ] Code uploaded to GitHub
- [ ] Vercel account created
- [ ] Project imported to Vercel
- [ ] Environment variables added
- [ ] Build completed successfully
- [ ] Live URL works
- [ ] AI chat responds correctly
- [ ] All features working

**Congratulations! Your Forus Heavy API is now live on the internet!**

### Your Live App Features:
- Professional web URL
- AI chat with dual integration
- Voice input and text-to-speech
- File and image uploads
- Theme switching
- Mobile responsive
- Accessible worldwide

### Next Steps:
- **Custom domain**: Add your own domain in Vercel settings
- **Analytics**: Monitor usage in Vercel dashboard
- **Updates**: Push to GitHub to automatically redeploy
- **Scaling**: Upgrade Vercel plan if needed for high traffic