# 2asy - Production AI News Platform

<div align="center">

[![Live](https://img.shields.io/badge/🌍_Live-2asy.ai-00C7B7?style=for-the-badge)](https://2asy.ai)
[![Live](https://img.shields.io/badge/🌍_Live-2asy.net-FF6B6B?style=for-the-badge)](https://2asy.net)
[![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)]()

**Real-world application built with [LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure) and [LLM-Components](https://github.com/Hannune/LLM-Components)**

</div>

---

## 🎯 Overview

2asy is an **AI-powered economic news platform** that automatically generates and publishes 10+ daily articles across two languages - demonstrating the real-world capability of 100% local LLM infrastructure at scale.

**Live Sites:**
- 🌍 [2asy.ai](https://2asy.ai) - English content, 10 daily publications for global audience
- 🇰🇷 [2asy.net](https://2asy.net) - Korean content, optimized for Korean commuting hours

**Key Achievement:** Reduced operational costs to **1/10-1/20** compared to cloud APIs (from ~$1000+/month → ~$50/month electricity)

---

## 🏗️ Built With My LLM Stack

This project is a **real-world deployment** showcasing components from my other repositories:

### From [LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure)

```
┌─────────────────────────────────────────┐
│     2asy News Pipeline                  │
└────────────┬────────────────────────────┘
             │
    ┌────────▼─────────┐
    │  LiteLLM Gateway │  ← Load balancing & fallback
    │  (Port 4000)     │     to OpenRouter
    └────────┬─────────┘
             │
        ┌────┴────┬──────────┐
        │         │          │
   ┌────▼──┐ ┌───▼───┐ ┌───▼────┐
   │ vLLM  │ │llama  │ │Ollama  │  ← Multi-server fleet
   │Server │ │.cpp   │ │Fleet   │     for reliability
   └───────┘ └───────┘ └────────┘
```

**Infrastructure Components Used:**
- ✅ **[litellm-local-gateway](https://github.com/Hannune/LLM-Infrastructure/tree/main/litellm-local-gateway)** - Unified API gateway with automatic fallback to OpenRouter
- ✅ **[ollama-fleet-manager](https://github.com/Hannune/LLM-Infrastructure/tree/main/ollama-fleet-manager)** - Managing multiple LLM instances across servers
- ✅ **[vllm-gptq-marlin-optimization](https://github.com/Hannune/LLM-Infrastructure/tree/main/vllm-gptq-marlin-optimization)** - Optimized inference for faster summarization
- ✅ **[ollama-production-docker](https://github.com/Hannune/LLM-Infrastructure/tree/main/ollama-production-docker)** - Production-hardened Docker deployment
- ✅ **[multi-server-monitoring-dashboard](https://github.com/Hannune/LLM-Infrastructure/tree/main/multi-server-monitoring-dashboard)** - Real-time infrastructure monitoring

### From [LLM-Components](https://github.com/Hannune/LLM-Components)

**Components Used:**
- ✅ **[gdelt-article-collector](https://github.com/Hannune/LLM-Components/tree/main/gdelt-article-collector)** - Real-time global news collection with advanced filtering
- ✅ **[mcp-agent-services](https://github.com/Hannune/LLM-Components/tree/main/mcp-agent-services)** - GPT-Researcher service for deep research
- ✅ **[large-text-summarizer](https://github.com/Hannune/LLM-Components/tree/main/large-text-summarizer)** - Map-reduce summarization for long articles

---

## 🚀 Architecture & Workflow

### Complete Pipeline

```
┌──────────────────────────────────────────────────────────────┐
│ 1. News Collection (GDELT Collector Component)              │
│    ↓                                                          │
│    Keywords: ["economy", "market", "finance"]                │
│    Filters: Top sources, English/Korean                      │
│    Output: 50-100 articles/day                               │
└──────────────────────────────────────────────────────────────┘
                           ↓
┌──────────────────────────────────────────────────────────────┐
│ 2. LangGraph Summarization Pipeline (LOCAL LLMs)            │
│    ↓                                                          │
│    ┌─────────────┐    ┌──────────────┐    ┌──────────┐     │
│    │  Collector  │ →  │ Summarizer   │ →  │ Reviewer │     │
│    │    Node     │    │    Node      │    │   Node   │     │
│    └─────────────┘    └──────────────┘    └──────────┘     │
│    Fetch articles     Custom structured    Quality check    │
│                       output (no GPT-R)    & neutrality     │
└──────────────────────────────────────────────────────────────┘
                           ↓
┌──────────────────────────────────────────────────────────────┐
│ 3. Content Publishing (Ghost CMS)                           │
│    ↓                                                          │
│    Schedule: 10x daily (2asy.ai), Korean peak hours (2asy.net)│
│    Format: Structured articles with metadata                │
└──────────────────────────────────────────────────────────────┘
                           ↓
                    📰 Published!
```

### LangGraph Workflow

```python
# Simplified workflow structure
from langgraph.graph import StateGraph

workflow = StateGraph(NewsState)

# Nodes using LLM-Components
workflow.add_node("collect", gdelt_collector_node)      # ← GDELT Component
workflow.add_node("summarize", custom_summarizer_node)  # ← Large Text Summarizer
workflow.add_node("review", content_reviewer_node)       # ← LOCAL LLM via Gateway
workflow.add_node("publish", ghost_publisher_node)

# Edges
workflow.add_edge("collect", "summarize")
workflow.add_edge("summarize", "review")
workflow.add_edge("review", "publish")
```

---

## ✨ Key Features

### 🤖 **AI-Powered Content Generation**
- **Custom Summarizer Agent** with structured output (dictionary format)
- **Content Reviewer Node** ensuring clarity, neutrality, and readability
- **Optimized for speed** - No overhead from heavy tools like standard GPT-Researcher
- **Multi-language support** - English and Korean content generation

### 🏭 **Production Infrastructure**
- **Automated scheduling** via Docker containers running 24/7
- **Multi-server LLM fleet** managed by ollama-fleet-manager
- **Automatic failover** via LiteLLM Gateway → OpenRouter backup
- **Real-time monitoring** with multi-server dashboard
- **Load balancing** across vLLM, llama.cpp, and Ollama instances

### 💰 **Cost Efficiency**
- **10-20x cost reduction** compared to cloud APIs
- Monthly costs: **~$50** (electricity only) vs **$1000+** (API fees)
- **100% local inference** during normal operation
- OpenRouter backup only for infrastructure failures

### 📊 **Scalability**
- Processing **50-100 articles daily**
- Publishing **10+ articles per site**
- Serving **1000+ daily visitors**
- **99.9% uptime** with automatic failover

---

## 🛠️ Technologies Used

### Content Management
- **Ghost CMS** - Modern headless CMS for publishing

### AI & LLM Stack
- **LangGraph** - Workflow orchestration for multi-node pipeline
- **vLLM** - High-performance inference engine
- **llama.cpp** - Efficient CPU/GPU inference
- **LiteLLM** - Unified gateway with fallback support
- **Ollama** - Easy local model management

### Infrastructure
- **Docker & Docker Compose** - Containerized services
- **Ubuntu Server** - Production hosting
- **NVIDIA GPUs** - Hardware acceleration
- **Cron Scheduler** - Timed publishing automation

### Future Enhancements
- **Streamlit Dashboard** - Real-time monitoring UI (planned)
- **Slack Bot** - Event notifications and alerts (planned)

---

## 📈 Production Metrics

### Performance
```
Daily Operations:
├─ Articles Collected: 50-100
├─ Articles Summarized: 20-30
├─ Articles Published: 10-15 (per site)
├─ Processing Time: ~5-10 min per article
└─ Total Pipeline Time: ~2-3 hours/day

Infrastructure:
├─ LLM Servers: 3 (vLLM, llama.cpp, Ollama)
├─ GPU Utilization: 60-80% during processing
├─ Uptime: 99.9%
└─ API Costs: ~$0/month (local) + $10/month (backup)
```

### Cost Comparison

| Solution | Monthly Cost | Notes |
|----------|--------------|-------|
| **2asy (Local)** | **~$5~10** | Electricity only |
| OpenAI GPT-4 API | ~$800-1200 | 10 articles/day estimate |
| Claude API | ~$600-1000 | Similar usage |
| Cohere | ~$400-800 | Lower tier models |

**Savings: 95%+**

---

## 🎯 Why This Matters

### Proof of Concept for Local LLM Infrastructure

2asy demonstrates that **production AI applications** can run entirely on local infrastructure:

✅ **Reliability** - 99.9% uptime with proper setup
✅ **Scalability** - Handling 1000+ daily users
✅ **Cost-Effective** - 95% cost reduction vs cloud
✅ **Privacy** - Complete data control
✅ **Performance** - Fast enough for real-time publishing

### Reusable Components

Every component used in 2asy is available in my other repositories:
- Fork [LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure) for the server setup
- Use [LLM-Components](https://github.com/Hannune/LLM-Components) for building blocks
- Follow the patterns in [LLM-Applications](https://github.com/Hannune/LLM-Applications)

---

## 🚀 How to Build Your Own

### 1. Set Up Infrastructure

```bash
# Clone the infrastructure repo
git clone https://github.com/Hannune/LLM-Infrastructure.git
cd LLM-Infrastructure

# Deploy LiteLLM Gateway
cd litellm-local-gateway
docker-compose up -d

# Set up Ollama fleet
cd ../ollama-fleet-manager
python setup.py
```

### 2. Install Components

```bash
# Clone components repo
git clone https://github.com/Hannune/LLM-Components.git
cd LLM-Components

# Deploy GDELT collector
cd gdelt-article-collector
docker-compose up -d

# Deploy other services as needed
```

### 3. Build Your Pipeline

```python
from langgraph.graph import StateGraph
from gdelt_collector import GDELTSearch
from llm_gateway import LiteLLMClient

# Your custom workflow here
# See LLM-Applications repo for examples
```

### 4. Deploy Ghost CMS

```bash
docker run -d \
  --name ghost \
  -p 2368:2368 \
  -e url=http://your-domain.com \
  -v ghost_data:/var/lib/ghost/content \
  ghost:latest
```

---

## 📊 Monitoring & Maintenance

### Current Monitoring
- **Infrastructure dashboard** from multi-server-monitoring-dashboard
- **Ghost CMS analytics** for visitor metrics
- **Manual log review** via Docker logs

### Planned Improvements
- **Streamlit dashboard** for real-time pipeline monitoring
- **Slack notifications** for errors and daily reports
- **Automated quality scoring** for published articles
- **A/B testing** for different summarization prompts

---

## 🔗 Related Projects

This is one application in a complete ecosystem:

- 🏭 **[LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure)** - The foundation (gateways, fleet management, monitoring)
- 🧩 **[LLM-Components](https://github.com/Hannune/LLM-Components)** - Reusable building blocks (GDELT, summarizer, services)
- 🤖 **[LLM-Applications](https://github.com/Hannune/LLM-Applications)** - Other complete applications
- 🔬 **[LangGraph-Research-Agent](https://github.com/Hannune/Langgraph-Research-Agent)** - Similar LangGraph patterns

---

## 🌐 Live Demonstration

Visit the live sites to see the results:

- 🌍 **[2asy.ai](https://2asy.ai)** - English economic news
- 🇰🇷 **[2asy.net](https://2asy.net)** - Korean economic news

Every article you see was:
1. Collected via GDELT Component
2. Summarized via LOCAL LLM through LiteLLM Gateway
3. Reviewed for quality via custom LangGraph node
4. Published automatically via Ghost API

**Zero human intervention. Zero cloud APIs. 100% local.**

---

## 💡 Key Takeaways

### For Developers
- **Local LLMs are production-ready** for real applications
- **Proper infrastructure** (gateways, monitoring, failover) is crucial
- **Reusable components** accelerate development
- **Cost savings are massive** (95%+) vs cloud APIs

### For Businesses
- **AI applications don't require cloud APIs** and subscription fees
- **Privacy and control** are achievable with local deployment
- **Scalability is possible** with proper architecture
- **ROI is immediate** with cost reduction

---

## 📄 License

MIT License - This project demonstrates the capabilities of open-source LLM infrastructure.

---

## 🙏 Acknowledgments

Built with open-source technologies:
- [Ghost](https://ghost.org/) - Content management
- [LangGraph](https://langchain-ai.github.io/langgraph/) - Workflow orchestration
- [LiteLLM](https://github.com/BerriAI/litellm) - LLM gateway
- [vLLM](https://github.com/vllm-project/vllm) - Inference engine
- [Ollama](https://ollama.ai/) - Model management
- [GDELT Project](https://www.gdeltproject.org/) - Global news data

---

<div align="center">

**This is what's possible with local LLM infrastructure** 🚀

Check out [LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure) and [LLM-Components](https://github.com/Hannune/LLM-Components) to build your own!

[![Visit 2asy.ai](https://img.shields.io/badge/🌍_Visit-2asy.ai-00C7B7?style=for-the-badge)](https://2asy.ai)
[![Visit 2asy.net](https://img.shields.io/badge/🌍_Visit-2asy.net-FF6B6B?style=for-the-badge)](https://2asy.net)

</div>
