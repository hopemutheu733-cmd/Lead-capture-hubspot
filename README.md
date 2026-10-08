# AI Lead Enrichment to HubSpot

An n8n workflow that receives a lead, validates the email, enriches the lead with AI, saves it to Supabase, and creates or updates the contact in HubSpot.

<img width="600" height="270" alt="leadcapture3 6" src="https://github.com/user-attachments/assets/588f2a0f-4d7e-452f-aeee-b8efb3bf5126" />


## How it works

1. Receives a `POST` request through an n8n Webhook.
2. Maps the submitted fields and checks that the email is present.
3. If the email is missing, returns a JSON error response.
4. Sends the lead to an LLM via OpenRouter to write a summary, an outreach hook, and a lead score (retry on fail is enabled).
5. A JavaScript Code node parses the AI output into clean fields.
6. Saves the enriched lead to the Supabase `enriched_leads` table.
7. Creates or updates the contact in HubSpot.
8. Returns a JSON response only after processing finishes.

## Tools

n8n, OpenRouter (LLM), Supabase, HubSpot CRM

## Setup

1. Import `ai-lead-enrichment-hubspot.json` into n8n.
2. Add your own credentials for OpenRouter, Supabase, and HubSpot.
3. Create the Supabase table `enriched_leads` with columns: [list your column names].
4. Activate the workflow and copy the production webhook URL.

## Example request

```json
{
  "name": "Test Lead",
  "email": "you@example.com",
  "company": "Example Company",
  "message": "Interested in your services",
  "industry": "Technology"
}
```

Test with curl:

```bash
curl -X POST "YOUR_WEBHOOK_URL" -H "Content-Type: application/json" -d '{"name":"Test Lead","email":"you@example.com","company":"Example Company","message":"Interested in your services","industry":"Technology"}'
```

## Example responses

Success: [paste your real success response]

Missing email: [paste your real error response]

## Notes

- Tested end to end with PowerShell.
- Diagnosed and fixed a duplicate-email error in the Supabase insert: [one line on what you changed].
