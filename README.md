# Slack AI Assistant

An n8n workflow that responds to Slack app mentions using an OpenAI-powered AI agent. A Date & Time tool lets the agent access date and time information when needed.

## Workflow

1. **Slack Trigger** receives an `app_mention` event in the configured channel.
2. **AI Agent** receives the Slack event as JSON and generates a response.
3. **OpenAI Chat Model** supplies `gpt-5-mini`.
4. **Date & Time** is available as an agent tool.
5. **Send a message** posts the response to the configured Slack channel.

Replies are channel messages; this workflow does not configure threaded replies or conversation memory.

## Setup

1. Download [slack-ai-assistant.json](./slack-ai-assistant.json) and import it into n8n.
2. Connect your Slack credentials in **Slack Trigger** and **Send a message**.
3. Replace `YOUR_SLACK_CHANNEL_ID` in both Slack nodes with your channel ID.
4. Connect your OpenAI API credentials in **OpenAI Chat Model**. API usage requires separate billing.
5. Configure your Slack app's event subscription to use the URL shown by the n8n Slack Trigger. Subscribe to `app_mention` and give the app permission to read mentions and post messages (typically `app_mentions:read` and `chat:write`).
6. Install the Slack app in your workspace and invite it to the configured channel.
7. Test the workflow, then activate/publish it and use the production trigger URL for ongoing use.

Use an n8n version that supports the node versions included in the export. For self-hosting, Slack must be able to reach your n8n webhook over HTTPS, and your n8n service must remain running.

## Quick check

Mention the Slack app in the configured channel with a simple question. Confirm that the workflow executes and posts a response. Ask for the current date to check the Date & Time tool when the agent chooses to use it.

## Files

- `slack-ai-assistant.json` — importable workflow template.
- `README.md` — overview, configuration, and manual checks.

## Export and privacy

The shared export is inactive and contains no credential references, original channel IDs, webhook IDs, or instance metadata. Configure your own credentials after import. The agent prompt sends the incoming Slack event JSON to OpenAI; use a channel whose content you are comfortable processing this way.

## Limitations

This repository contains a workflow export, not a hosted service. It has no persistent chat memory or custom error-handling branch. Live execution requires your own Slack, OpenAI, and n8n configuration; it has not been tested from this repository.
