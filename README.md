# 2asy - AI-Powered Economic News Website

Welcome to 2asy, a website designed to provide daily economic news that is summarized and generated using AI. This project leverages Ghost as the content management system and LangGraph for news summarization and content generation.

## Features

- Automated content creation and publishing via scheduled tasks running inside Docker containers for seamless operation.
- Local execution of language models using vLLM, llama.cpp, and LiteLLM to process and summarize news articles efficiently.
- Backup readiness with an OpenRouter endpoint to handle LLM server issues ensuring service reliability.
- Custom summarizer agent built with structured output (dictionary format) to minimize overhead compared to conventional tools like GPT-Researcher.
- Additional content reviewing node to maintain clarity, neutrality, and ease of understanding in summaries.
- Fully local pipeline for news processing, drastically cutting down monthly operational costs (roughly 1/10th to 1/20th) compared to cloud or commercial LLM API use, saving costs to about just electricity bills.

## Architecture

- Two main websites: [2asy.ai](https://2asy.ai) for English content uploaded 10 times daily for a global audience.
- [2asy.net](https://2asy.net) for Korean content optimized to upload during Korean commuting hours.
- All news articles are automatically fetched, summarized, and published through an orchestrated pipeline running on local servers.
- Future development plans include a monitoring dashboard built with Streamlit and Slack notification bot for event alerts.

## Technologies

- Ghost CMS
- LangGraph for AI summarization and content generation
- Docker for containerized workflows and automation
- Local LLM servers running vLLM, llama.cpp, LiteLLM
- OpenRouter fallback for LLM serving
- Scheduler for timed publishing
- Streamlit (planned) for monitoring UI
- Slack API (planned) for notifications

## Why 2asy?

By running the entire stack locally with LLM models, 2asy achieves efficient, low-cost AI-driven news summarization without reliance on expensive cloud services. This project is an example of leveraging open-source AI tools and containerized pipelines to create a scalable, cost-efficient news platform.

---

Feel free to visit [2asy.ai](https://2asy.ai) and [2asy.net](https://2asy.net) to explore the live websites and their AI-generated content.

For questions or collaboration, please reach out!

