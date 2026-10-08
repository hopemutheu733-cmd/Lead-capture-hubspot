# AI Lead Enrichment to HubSpot

An n8n workflow that receives a lead through a webhook, validates the email, enriches the lead with AI, saves it to Supabase, and creates or updates the contact in HubSpot.

![AI Lead Enrichment workflow](https://github.com/user-attachments/assets/d09bc330-add0-4865-b642-87d7bab82385)

## How it works

1. Receives a `POST` request through an n8n Webhook.
2. Maps the submitted lead fields and checks that the email is present.
3. If the email is missing, returns a separate JSON error response.
4. Sends the lead to an LLM via OpenRouter, which writes a summary, an outreach hook and a lead score (retry on fail is enabled).
5. A JavaScript Code node parses the AI output into clean fields.
6. Saves the enriched lead to the Supabase `enriched_leads` table.
7. Creates or updates the contact in HubSpot.
8. Returns a JSON response only after all processing has finished.

## Tools

n8n Cloud, OpenRouter (LLM), Supabase, HubSpot CRM

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

## Testing

The workflow was tested end to end with PowerShell:

```powershell
Invoke-RestMethod -Method Post -Uri "YOUR_WEBHOOK_URL" -ContentType "application/json" -Body '{"name":"Test Lead","email":"you@example.com","company":"Example Company","message":"Interested in your services","industry":"Technology"}'
```

Tested paths:
- A valid lead is enriched, saved to Supabase, created or updated in HubSpot, and returns a JSON success response.
- A lead with no email returns a JSON error response and nothing is saved.

## Setup

1. Import the workflow JSON file into n8n.
2. Add your own credentials for OpenRouter, Supabase and HubSpot.
3. Create the Supabase table `enriched_leads` to match the fields the workflow saves.
4. Activate the workflow and send a test request to the production webhook URL.

## Troubleshooting notes

- During testing, sending the same email twice caused a duplicate-email error from the database. Diagnosed by reading the failed execution data in n8n.
- The webhook responds only after processing finishes, so the caller always gets the real result.

## Notes

- Credentials are not included in the exported workflow.
- Portfolio project using test data only.
