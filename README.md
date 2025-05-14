🤖How to Build an AI WhatsApp Agent Using n8n

This professional guide will walk you through building a WhatsApp chatbot using n8n, Evolution API, and OpenAI. You'll learn how to:

- Set up a VPS
- Install and configure n8n, Redis, PostgreSQL, and Evolution API
- Create a webhook-based chatbot
- Integrate LLMs for intelligent message handling

🟡 This version focuses exclusively on the chatbot logic, excluding scheduling features.

🚀 Features
- WhatsApp integration with webhook via Evolution API
- Message classification using LLM (OpenAI GPT-4)
- Smart responses using a knowledge base
- Audio message transcription using Whisper API
- Text/Audio differentiation and processing
- Redis-based memory for contextual interaction

1. 🖥️ VPS Setup with DigitalOcean + EasyPanel

✅ Create a VPS

- Use DigitalOcean for quick deployment:
Sign up here on [DigitalOcean](https://www.digitalocean.com/?refcode=66e3dacc4b8c&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) for $200 credit.
- Create a new project and droplet
- Plan: Basic ($4 or $6)
- Select region close to you
- Enable password or SSH login

✅ Install EasyPanel

- Once the droplet is ready:
- Just click on "Get Started" to access EasyPanel 
- Create a user and login.

2. ⚙️ Set Up Services (PostgreSQL, Redis, n8n, Evolution)

✅ PostgreSQL Setup

In EasyPanel:
- Create a service → PostgreSQL
- Name: n8n-postgres
- Save the internal credentials

✅ Redis Setup

In EasyPanel:
- Create a service → Redis
- Name: n8n-redis
- Save the external host, port, and password

✅ n8n Installation

 In EasyPanel:
- Add service → Search for n8n

✅ Evolution API Installation

- Go to https://github.com/EvolutionAPI/evolution-api
- Copy the latest Docker image version from the Releases page
- In EasyPanel, create a Docker app:
- Name: evolution
- Docker image: ghcr.io/evolutionapi/evolution-api:<version>
- Copy environment variables from .env.example in the repo
- Set POSTGRES/REDIS credentials using EasyPanel’s connection strings
- Set a strong API_KEY
- Expose port 8080, and use /manager to access the dashboard
- Pair your WhatsApp via QR code

3. 📲 Creating the n8n Chatbot Workflow

✅ Import Community Node for Evolution API

In n8n:
- Go to Settings → Community Nodes
- Add: n8n-nodes-evolution
- Restart n8n

✅ Import Chatbot Template

You will need a base chatbot template.
Paste or import it via the n8n interface:
<LINK DE DONWLOAD TEMPLATE>
