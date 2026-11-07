# EarlySignal: hosting with a real AI assistant

Structure:
  public/index.html   the site (frontend)
  api/chat.js         server function that holds your API key and calls Claude

## Deploy on Vercel (free tier is enough to start)
1. Create an API key at https://console.anthropic.com (add billing; you pay per message).
2. Put this folder on GitHub (or install the Vercel CLI and run `vercel` inside it).
3. In Vercel: New Project -> import the repo. Framework preset: "Other". Output directory: public.
4. Project Settings -> Environment Variables:
     ANTHROPIC_API_KEY = your key      (required)
     MODEL             = claude-sonnet-5-5   (optional, change to a cheaper model to save money)
5. Deploy. Open the site: the yellow banner should switch to "AI assistant (Claude)".

## Test locally
  npm i -g vercel
  vercel dev          (set ANTHROPIC_API_KEY in a .env file first)

## Before real users
- Set a monthly spend limit in the Anthropic console.
- Replace the in-memory rate limit in api/chat.js with Upstash/Vercel KV (serverless memory resets).
- Add a privacy policy and consent screen: chat messages and lab values are sent to Anthropic.
- Data is stored only in each visitor's browser; there are no accounts or database yet.

## Optional: OpenAI-compatible gateway (e.g. OmniRoute)
Instead of ANTHROPIC_API_KEY set:
  LLM_BASE_URL = https://your-gateway.example.com/v1
  LLM_API_KEY  = key created in the gateway
  LLM_MODEL    = model or combo name configured in the gateway
The gateway must be reachable from the internet over HTTPS (localhost will not work from Vercel).
