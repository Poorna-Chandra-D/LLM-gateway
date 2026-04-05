# Render.com Deployment Guide

## Quick Setup (5 minutes)

### Step 1: Create Render Account
1. Go to [render.com](https://render.com)
2. Sign up with GitHub (easiest option)

### Step 2: Deploy from GitHub
1. In Render dashboard, click **New +** → **Blueprint**
2. Connect your GitHub repository
3. Select branch: `main`
4. Render auto-detects `render.yaml` and creates all services

### Step 3: Configure API Keys
After deployment, add your secrets to Render:

1. Go to **Render Dashboard** → **llm-gateway-api** service
2. Click **Environment** tab
3. Add these variables:
   - **OPENAI_API_KEY**: Your OpenAI API key
   - **GEMINI_API_KEY**: Your Gemini API key
4. Click **Save** (triggers redeploy)

### What Gets Created
- ✅ **PostgreSQL 15** (free tier, 100MB)
- ✅ **Redis 7** (free tier)
- ✅ **FastAPI server** (free tier Docker)

### Access Your App
Once deployed, your API will be at:
```
https://llm-gateway-api.onrender.com
```

Test it:
```bash
curl https://llm-gateway-api.onrender.com/health
```

### First-Time Setup
When the API first starts, it will:
1. Run database migrations (Alembic)
2. Create tables
3. Be ready to accept requests

### Free Tier Limits
- 100 MB PostgreSQL storage (plenty for api_keys & requests tables)
- 256MB Redis memory
- Spins down after 15 min of inactivity (cold start ~30s)
- ~500 requests/day per service (plenty for portfolio)

### Environment Variables Needed
```
OPENAI_API_KEY=sk-...
GEMINI_API_KEY=AIzaSy...
```

### Dashboard Access
Your dashboard will be at:
```
https://llm-gateway-api.onrender.com/dashboard
```

### Logs & Monitoring
In Render dashboard:
- **Logs** tab: Real-time logs (same as Docker Compose locally)
- **Metrics** tab: CPU, memory, requests
- **Events** tab: Deployment history

### Troubleshooting

**Cold start (app sleeps after 15 min):**
- First request after sleep takes ~30s (normal)
- Keep-alive requests can prevent sleep (optional)

**Database not connecting:**
- Check that DATABASE_URL env var is set automatically ✓
- Render auto-generates from PostgreSQL service

**Redis not connecting:**
- Check that REDIS_URL env var is set automatically ✓
- Render auto-generates from Redis service

**API keys not working:**
- Make sure you added OPENAI_API_KEY and GEMINI_API_KEY to Environment
- Render auto-detects changes and redeploys

### Need Help?
- Render logs show everything: Render dashboard → Logs tab
- test_gemini.py and test_health.py scripts validate endpoints locally first
- All container commands are identical to local Docker setup

---

**That's it!** Your LLM Gateway is now production-ready. 🚀
