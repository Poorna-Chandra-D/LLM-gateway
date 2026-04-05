# Render.com Deployment Guide

## Quick Setup (10 minutes)

### Step 1: Create Render Account
1. Go to [render.com](https://render.com)
2. Sign up with GitHub

### Step 2: Deploy API Service via Blueprint
1. Click **New +** → **Blueprint**
2. Paste repo: `https://github.com/Poorna-Chandra-D/LLM-gateway`
3. Select branch: `main`
4. Click **Create Blueprint** (only deploys Docker service)
5. Wait for deployment to complete

### Step 3: Create PostgreSQL Database
After blueprint deployment, create the database:
1. In Render dashboard, click **+ New** → **PostgreSQL**
2. Set:
   - Name: `llm-gateway-db`
   - Database: `llm_gateway`
   - User: `postgres`
   - Plan: **Free**
3. Click **Create Database**
4. Note the connection string (looks like: `postgresql://postgres:...@...`)

### Step 4: Create Redis Cache
1. Click **+ New** → **Redis**
2. Set:
   - Name: `llm-gateway-cache`
   - Plan: **Free**
   - IP Allowlist: Leave blank (allows all IPs, needed for Docker service)
3. Click **Create Redis**
4. Note the connection string

### Step 5: Connect Database & Redis to API
1. Go to **llm-gateway-api** service
2. Click **Environment** tab
3. Add these environment variables:
   ```
   DATABASE_URL=postgresql://postgres:PASSWORD@HOST:5432/llm_gateway
   REDIS_URL=redis://default:PASSWORD@HOST:6379
   OPENAI_API_KEY=sk-xxxx...
   GEMINI_API_KEY=AIzaSy...
   ```
   (Replace PASSWORD and HOST from Steps 3 & 4)
4. Click **Save** (auto-redeploys)

### What Gets Created
- ✅ **FastAPI server** (Docker) - hosted on free tier
- ✅ **PostgreSQL 15** (free tier, 100MB)
- ✅ **Redis 7** (free tier, 256MB)

### Access Your App
Once all services are live:
```
API: https://llm-gateway-api.onrender.com
Health: https://llm-gateway-api.onrender.com/health
Dashboard: https://llm-gateway-api.onrender.com/dashboard
```

### Free Tier Limits
- 100 MB PostgreSQL storage (plenty for api_keys & requests tables)
- 256MB Redis memory
- Spins down after 15 min of inactivity (cold start ~30s)
- ~500 requests/day

### First-Time Setup
When the API first starts, it will:
1. Run database migrations (Alembic)
2. Create tables automatically
3. Be ready to accept requests

### Troubleshooting

**"Cannot connect to database"**
- Check DATABASE_URL is correct and includes password
- Verify PostgreSQL service says "Available"

**"Cannot connect to Redis"**
- Check REDIS_URL is correct
- Verify Redis service says "Available"

**Cold start (app sleeps after 15 min)**
- First request after sleep takes ~30s (normal)
- This is expected on free tier

**API keys not working**
- Make sure you added OPENAI_API_KEY and GEMINI_API_KEY to Environment
- Render auto-detects changes and redeploys

### Need Help?
Check Render dashboard logs for any errors

