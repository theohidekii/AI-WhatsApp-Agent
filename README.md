# 🤖How to Build an AI WhatsApp Agent Using n8n

## This professional guide will walk you through building a WhatsApp chatbot using n8n, Evolution API, and OpenAI. You'll learn how to:

- Set up a VPS
- Install and configure n8n, Redis, PostgreSQL, and Evolution API
- Create a webhook-based chatbot
- Integrate LLMs for intelligent message handling

🔴 This version focuses exclusively on the chatbot logic, excluding scheduling features.

### 🚀 Features
- WhatsApp integration with webhook via Evolution API
- Message classification using LLM (OpenAI GPT-4)
- Smart responses using a knowledge base
- Audio message transcription using Whisper API
- Text/Audio differentiation and processing
- Redis-based memory for contextual interaction

## 1. 🖥️ VPS Setup with DigitalOcean + EasyPanel

### ✅ Create a VPS

- Use DigitalOcean for quick deployment:
Sign up here on [DigitalOcean](https://www.digitalocean.com/?refcode=66e3dacc4b8c&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) for $200 credit.
- Create a new project and droplet
- Plan: Basic ($4 or $6)
- Select region close to you
- Enable password or SSH login

### ✅ Install EasyPanel

- Once the droplet is ready:
- Just click on "Get Started" to access EasyPanel 
- Create a user and login.

## 2. ⚙️ Set Up Services (PostgreSQL, Redis, n8n, Evolution)

### ✅ PostgreSQL Setup

In EasyPanel:
- Create a service → PostgreSQL
- Name: n8n-postgres
- Save the internal credentials

###✅ Redis Setup

In EasyPanel:
- Create a service → Redis
- Name: n8n-redis
- Save the external host, port, and password

### ✅ n8n Installation

 In EasyPanel:
- Add service → Search for n8n

### ✅ Evolution API Installation

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

## 3. 📲 Creating the n8n Chatbot Workflow

###✅ Import Community Node for Evolution API

In n8n:
- Go to Settings → Community Nodes
- Add: n8n-nodes-evolution
- Restart n8n

### ✅ Import Chatbot Template

You will need a base chatbot template.
Paste or import it via the n8n interface:
<LINK DE DONWLOAD TEMPLATE>

## 4. 🧠 Workflow Logic Overview

### 🔹 Webhook Trigger

- Triggers on incoming WhatsApp message
- Filter by correct API Key and eventType = upsert

### 🔹 Message Type Routing

Use a Switch node to check if the message is:
- Text: send directly to AI
- Audio: use Whisper API to transcribe

### 🔹 Whisper Integration (if audio)

- HTTP Request to OpenAI Whisper
- Transcribe base64 audio (check Evolution setting webhookBase64=true)

### 🔹 Intent Classification

- AI Agent 1: Receptionist (classifies message as information or scheduling)
- Prompt Example:

You are a specialist in classifying customer messages into two categories: 'information' or 'scheduling'.

### 🔹 Commercial Assistant Response

- If information, forward to AI Agent 2: Sales Assistant
- Use RAG (Retrieval-Augmented Generation) if needed with file attachments
- Provide product details, FAQs, and encourage visit scheduling

### 🔹 Send Response

Use Evolution API node to send back the AI-generated text

Fill in:

- Session name
- Recipient number
- Message text

## 5. 🧪 Testing Your Bot

- Send a message to your connected WhatsApp number
- Monitor execution in n8n → Executions
- Check logs and message delivery on your device


