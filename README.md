# Lead Capture HubSpot

An n8n workflow that receives lead submissions, enriches them with AI, saves them to Supabase, and creates or updates a HubSpot contact.

<img width="600" height="270" alt="leadcapture3 6" src="https://github.com/user-attachments/assets/3db070b7-3344-4593-ae75-1b6d01610cd3" />



## How it works

1. Receives a `POST` request through an n8n Webhook.
2. Maps the submitted lead fields and checks the email.
3. Uses an AI step to create a lead summary, outreach hook, and score.
4. Saves the enriched lead in the Supabase `enriched_leads` table.
5. Creates or updates the contact in HubSpot.

## Tech stack

n8n, OpenRouter, Supabase, HubSpot

## Expected request

Send JSON with these fields:

```json
{
  "name": "Test Lead",
  "email": "you@example.com",
  "company": "Example Company",
  "message": "Interested in your services",
  "industry": "Technology"
}
```
