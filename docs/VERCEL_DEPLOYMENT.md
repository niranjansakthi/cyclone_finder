# Deploying CycloSense_Ai to Vercel

Since your project consists of a separate frontend (React + Vite) and backend, **Vercel is the perfect choice for hosting your frontend**, while your backend can be hosted on a service like Render (which you already have configured via `render.yaml`).

Here is a step-by-step guide to deploying your frontend to Vercel.

## Option 1: Deploy via Vercel Dashboard (Recommended & Easiest)

1. **Push your code to GitHub:** 
   (We just completed this step! Your code is ready at `https://github.com/niranjansakthi/cyclone_finder`)
2. **Log into Vercel:** Go to [vercel.com](https://vercel.com/) and sign in with your GitHub account.
3. **Import the Project:**
   - Click on the **Add New** button and select **Project**.
   - Find `cyclone_finder` in your list of GitHub repositories and click **Import**.
4. **Configure Project Settings:**
   - **Project Name:** `cyclosense-ai` (or whatever you prefer)
   - **Framework Preset:** Vercel should automatically detect **Vite**.
   - **Root Directory:** Click "Edit" and select `frontend` (since your React app is inside the `frontend` folder).
   - **Build and Output Settings:** Leave as default. (Build Command: `npm run build` or `npm run build`, Output Directory: `dist`)
5. **Set Environment Variables:**
   - Expand the **Environment Variables** section.
   - You need to connect your frontend to your deployed backend API.
   - Add a new variable:
     - **Name:** `VITE_API_URL`
     - **Value:** `https://your-backend-url.onrender.com` *(Replace this with your actual Render/deployed backend URL)*
6. **Deploy:** Click the **Deploy** button. Vercel will build and deploy your frontend in less than a minute!

## Option 2: Deploy via Vercel CLI

If you prefer using the terminal, you can deploy using the Vercel CLI:

1. Open your terminal and install Vercel CLI globally:
   ```bash
   npm i -g vercel
   ```
2. Navigate to your frontend directory:
   ```bash
   cd frontend
   ```
3. Run the Vercel command and log in:
   ```bash
   vercel
   ```
4. Follow the prompts:
   - *Set up and deploy?* **Y**
   - *Which scope do you want to deploy to?* **(Your account)**
   - *Link to existing project?* **N**
   - *What's your project's name?* **cyclosense-frontend**
   - *In which directory is your code located?* **./**
   - *Auto-detected Project Settings (Vite)?* **Y**
5. **Set Environment Variable:** To point the deployed site to your backend API, deploy for production with environment variables:
   ```bash
   vercel --prod --build-env VITE_API_URL=https://your-backend-url.onrender.com
   ```

## Next Steps
Once your Vercel deployment is successful, Vercel will give you a live URL (e.g., `https://cyclosense-frontend.vercel.app`).

**Don't forget:** 
Make sure your backend API is configured to accept **CORS** requests from your new Vercel URL, or your frontend won't be able to fetch data! In your FastAPI backend, add your Vercel URL to the allowed origins.
