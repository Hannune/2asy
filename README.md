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

**Key Achievement:** Reduced operational costs to **1/10-1/20** compared to cloud APIs (from ~$100+/month → ~$5/month electricity)

---

## 🏗️ Built With My LLM Stack

This project is a **real-world deployment** showcasing components from my other repositories:

### From [LLM-Infrastructure](https://github.com/Hannune/LLM-Infrastructure)

**Architecture:**
```
2asy News Pipeline
    ↓
LiteLLM Gateway (Port 4000)  ← Load balancing & fallback to OpenRouter
    ↓
    ├─────────┬─────────┐
    │         │         │
  vLLM    llama.cpp   Ollama  ← Multi-server fleet for reliability
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
1. News Collection (GDELT Collector Component)
   Keywords: ["economy", "market", "finance"]
   Filters: Top sources, English/Korean
   Output: 50-100 articles/day
                    ↓
2. LangGraph Summarization Pipeline (LOCAL LLMs)
   Collector Node → Summarizer Node → Reviewer Node
   Fetch articles   Custom structured   Quality check
                    output (no GPT-R)   & neutrality
                    ↓
3. Content Publishing (Ghost CMS)
   Schedule: 10x daily (2asy.ai), Korean peak hours (2asy.net)
   Format: Structured articles with metadata
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

### 🤖 AI-Powered Content Generation

![Custom Summarizer](https://img.shields.io/badge/✅_Custom_Summarizer-Structured_output_(dictionary_format)-00C7B7?style=for-the-badge)

![Content Reviewer](https://img.shields.io/badge/✅_Content_Reviewer-Clarity,_neutrality_&_readability-4285F4?style=for-the-badge)

![Optimized Speed](https://img.shields.io/badge/⚡_Optimized_Speed-No_GPT--Researcher_overhead-FF6F00?style=for-the-badge)

![Multi-language](https://img.shields.io/badge/🌐_Multi--language-English_&_Korean_generation-76B900?style=for-the-badge)

### 🏭 Production Infrastructure

![Automated Scheduling](https://img.shields.io/badge/🕐_Automated_Scheduling-Docker_24/7-00C7B7?style=for-the-badge)

![Multi-server Fleet](https://img.shields.io/badge/🖥️_Multi--server_Fleet-ollama--fleet--manager-4285F4?style=for-the-badge)

![Automatic Failover](https://img.shields.io/badge/🔄_Automatic_Failover-LiteLLM_→_OpenRouter-9C27B0?style=for-the-badge)

![Real-time Monitoring](https://img.shields.io/badge/📊_Monitoring-Multi--server_dashboard-FF6F00?style=for-the-badge)

![Load Balancing](https://img.shields.io/badge/⚖️_Load_Balancing-vLLM,_llama.cpp,_Ollama-76B900?style=for-the-badge)

### 💰 Cost Efficiency

![Cost Reduction](https://img.shields.io/badge/💰_Cost_Reduction-10--20x_vs_cloud_APIs-00C7B7?style=for-the-badge)

![Monthly Cost](https://img.shields.io/badge/💵_Monthly_Cost-~$5_(electricity)_vs_$200+_(APIs)-4285F4?style=for-the-badge)

![Local Inference](https://img.shields.io/badge/🏠_Local_Inference-100%25_during_normal_operation-76B900?style=for-the-badge)

![Backup Only](https://img.shields.io/badge/🔧_OpenRouter_Backup-Infrastructure_failures_only-9C27B0?style=for-the-badge)

### 📊 Scalability

![Daily Processing](https://img.shields.io/badge/📰_Daily_Processing-3000_articles-00C7B7?style=for-the-badge)

![Publishing](https://img.shields.io/badge/📝_Publishing-10+_summaries_per_site-4285F4?style=for-the-badge)

![Uptime](https://img.shields.io/badge/⏰_Uptime-99.9%25_with_automatic_failover-76B900?style=for-the-badge)

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
| **2asy (Local)** | **~$5-10** | Electricity only |
| OpenAI GPT-4o API | ~$800-850 | Based on ~37M input + 74M output tokens |
| Claude Sonnet 4.5 API | ~$1,200-1,250 | Premium quality, expensive at scale |
| Cohere Command R | ~$100-150 | Mid-tier alternative |

**Savings: 95%+**

---

## 🎯 Why This Matters

### Proof of Concept for Local LLM Infrastructure

2asy demonstrates that **production AI applications** can run entirely on local infrastructure:

![Reliability](https://img.shields.io/badge/✅_Reliability-99.9%25_uptime_with_proper_setup-00C7B7?style=for-the-badge)

![Scalability](https://img.shields.io/badge/✅_Scalability-Handling_1000+_daily_users-4285F4?style=for-the-badge)

![Cost-Effective](https://img.shields.io/badge/✅_Cost--Effective-95%25_cost_reduction_vs_cloud-FF6F00?style=for-the-badge)

![Privacy](https://img.shields.io/badge/✅_Privacy-Complete_data_control-9C27B0?style=for-the-badge)

![Performance](https://img.shields.io/badge/✅_Performance-Fast_enough_for_real--time_publishing-76B900?style=for-the-badge)

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

![Production Ready](https://img.shields.io/badge/✅_Local_LLMs-Production--ready_for_real_applications-00C7B7?style=for-the-badge)

![Infrastructure](https://img.shields.io/badge/🏗️_Infrastructure-Gateways,_monitoring,_failover_crucial-4285F4?style=for-the-badge)

![Reusable Components](https://img.shields.io/badge/🧩_Reusable_Components-Accelerate_development-FF6F00?style=for-the-badge)

![Cost Savings](https://img.shields.io/badge/💰_Cost_Savings-95%25+_vs_cloud_APIs-76B900?style=for-the-badge)

### For Businesses

![No Cloud APIs](https://img.shields.io/badge/🚫_No_Cloud_APIs-Zero_subscription_fees-00C7B7?style=for-the-badge)

![Privacy & Control](https://img.shields.io/badge/🔒_Privacy_&_Control-Achievable_with_local_deployment-4285F4?style=for-the-badge)

![Scalability](https://img.shields.io/badge/📈_Scalability-Possible_with_proper_architecture-9C27B0?style=for-the-badge)

![Immediate ROI](https://img.shields.io/badge/💵_ROI-Immediate_with_cost_reduction-76B900?style=for-the-badge)

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
