# Lead Capture HubSpot

An n8n workflow that receives lead submissions, enriches them with AI, saves them to Supabase, and creates or updates a HubSpot contact.

<img width="1600" height="714" alt="lead capture hubspot 3" src="https://github.com/user-attachments/assets/4f470eb1-a298-4dfe-bbd6-cd726f44f1e9" />


## How it works

1. Receives a `POST` request through an n8n Webhook.
2. Maps the submitted lead fields and checks the email.
3. Uses an AI step to create a lead summary, outreach hook, and score.
4. Saves the enriched lead in the Supabase `enriched_leads` table.
5. Creates or updates the contact in HubSpot.

## Expected request

Send JSON with these fields:

```json
{
  "name": "Test Lead",
  " "email": "you@example.com",
  "company": "Example Company",
  "message": "Interested in your services",
  "industry": "Technology"
}<img width="1600" height="714" alt="lead capture hubspot 3" src="https://github.com/user-attachments/assets/d09bc330-add0-4865-b642-87d7bab82385" />
