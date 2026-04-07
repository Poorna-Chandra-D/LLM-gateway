# Resilient LLM Gateway

**Developer:** Poorna Chandra D | Full Stack Developer & Project Lead

## Overview


A production-grade, unified REST API middleware designed to sit in front of multiple Large Language Models (LLMs) such as OpenAI, Google Gemini, Anthropic Claude, and more. The gateway provides resilient infrastructure for applications by handling automatic failover, semantic caching via Redis to reduce costs, and granular token usage tracking in PostgreSQL. This project focuses on backend engineering challenges like smart routing and reliability, ensuring seamless model switching without client-side code changes.

## Key Features

- 🔄 **Multi-Provider Support** - Seamlessly switch between OpenAI, Google Gemini, Anthropic Claude, and more
- 🛡️ **Automatic Failover** - Intelligent routing with fallback mechanisms for provider outages
- ⚡ **Semantic Caching** - Redis-based smart caching to reduce API costs and improve response times
- 📊 **Token Tracking** - Granular request logging and token usage analytics in PostgreSQL
- 🔐 **API Key Management** - Secure authentication and rate limiting per API key
- 🎯 **Smart Routing** - Route requests based on prompt complexity, provider health, and cost optimization
- 📈 **Observability** - Real-time dashboard with health indicators and request monitoring
- 🔌 **RESTful API** - Standard HTTP interface compatible with LLM client libraries
- 📝 **Privacy & Compliance** - Built-in privacy policy and terms of service pages

## Project Pages

- 🏠 [Landing Page](http://localhost:8000/) - Home and overview
- ⭐ [Features](http://localhost:8000/features) - Detailed feature showcase
- 🤖 [Providers](http://localhost:8000/providers) - Supported LLM providers
- 📚 [Resources](http://localhost:8000/resources) - Learning materials and documentation
- 📖 [API Docs](http://localhost:8000/api-docs) - Complete API reference
- 📊 [Status](http://localhost:8000/status) - System health monitoring
- 💬 [Contact](http://localhost:8000/contact) - Support and contact information
- 🔒 [Privacy](http://localhost:8000/privacy) - Privacy policy
- ⚖️ [Terms](http://localhost:8000/terms) - Terms of service

## System Status

| Component | Status | Uptime (1d) |
|-----------|--------|-------------|
| API Server | 🟢 Operational | 99.9% |
| Database (PostgreSQL) | 🟢 Operational | 99.9% |
| Cache (Redis) | 🟢 Operational | 99.9% |
| Provider APIs | 🟢 Operational | 99.7% |
| Monitoring | 🟢 Operational | 99.9% |
| Security & Auth | 🟢 Operational | 99.9% |

## Tech Stack

<p align="left">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" title="Python" alt="Python" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/fastapi/fastapi-original.svg" title="FastAPI" alt="FastAPI" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" title="PostgreSQL" alt="PostgreSQL" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/redis/redis-original.svg" title="Redis" alt="Redis" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" title="Docker" alt="Docker" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" title="GitHub" alt="GitHub" width="60" height="60"/>&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sqlalchemy/sqlalchemy-original.svg" title="SQLAlchemy" alt="SQLAlchemy" width="60" height="60"/>&nbsp;
</p>

**Core Technologies:**
- **Backend:** FastAPI (Python 3.11+)
- **Database:** PostgreSQL 13+
- **Cache:** Redis 6+
- **Deployment:** Docker & Docker Compose
- **ORM:** SQLAlchemy
- **Migrations:** Alembic
- **Frontend:** HTML5, CSS3, JavaScript

## Quick Start


### Clone & Setup

```bash
git clone https://github.com/Poorna-Chandra-D/LLM-Gateway.git
cd LLM-Gateway
```

### Docker Deployment

```bash
docker-compose build
docker-compose up -d
```

The application will be available at `http://localhost:8000`

### First API Request

```bash
curl -X POST http://localhost:8000/api/chat \
  -H "Content-Type: application/json" \
  -H "X-API-Key: your-api-key" \
  -d '{
    "provider": "openai",
    "model": "gpt-3.5-turbo",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

## Project Design

Our implementation follows a modular middleware architecture using an Adapter Pattern for different LLM providers. Requests are authenticated via API keys, checked against rate limits in Redis, and then routed based on prompt complexity or provider health.

### Architecture

- **API Layer** - FastAPI application with route handlers
- **Authentication** - API key validation and rate limiting
- **Provider Adapters** - Abstraction layer for different LLM APIs
- **Caching Layer** - Redis-based semantic cache for responses
- **Data Layer** - PostgreSQL for request tracking and analytics
- **Monitoring** - Real-time health checks and observability

## Contact & Support

**Email:** [poornacd24@gmail.com](mailto:poornacd24@gmail.com)  
**GitHub:** [@Poorna-Chandra-D](https://github.com/Poorna-Chandra-D)  
**Repository:** [Poorna-Chandra-D/LLM-Gateway](https://github.com/Poorna-Chandra-D/LLM-Gateway)

**Quick Links:**
- 💬 [Discussions](https://github.com/Poorna-Chandra-D/LLM-Gateway/discussions)
- 🐛 [Issues](https://github.com/Poorna-Chandra-D/LLM-Gateway/issues)
- 📋 [Pull Requests](https://github.com/Poorna-Chandra-D/LLM-Gateway/pulls)

## Product Personas

### Backend Engineer
Focus on robustness, scalability, and API performance. Interested in failover mechanisms, load distribution, and system reliability metrics.

### Engineering Manager
Concerned with cost optimization, team productivity, and deployment efficiency. Values clear documentation and easy integration.

### AI Product Engineer
Leveraging LLM APIs for product features. Needs seamless provider switching, caching for cost reduction, and comprehensive API docs.

---

**Last Updated:** April 5, 2026  
**Version:** 1.0.0  
**License:** MIT
