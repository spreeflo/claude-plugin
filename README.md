# Spreeflo for Claude

Spreeflo is email marketing, automation and a light CRM for marketing and sales. This plugin connects Claude to your own Spreeflo workspace and adds skills that show Claude how to use Spreeflo's tools together, so you can look at results and prepare marketing and sales work in conversation.

## What you can do

- Ask how a campaign or broadcast performed (sends, opens, clicks and bounces) and get a chart of the numbers.
- Find contacts, update their details, tags and notes, or import contacts from a CSV file.
- Build segments from contact attributes, tags and email activity, and preview who is in them.
- Draft email and web push templates, campaigns, journeys and broadcasts.
- Create and edit forms and their embeds, and review form responses and analytics.
- In workspaces with the CRM: set lifecycle stages and owners, manage companies, deals, pipelines and tasks, and save 1:1 email drafts for a team member to review and send.

## What's in the plugin

- **One MCP server:** `https://mcp.spreeflo.com/mcp`, Spreeflo's remote MCP server. It is the same server as the Spreeflo connector in the Claude directory.
- **Five skills:** `get-started`, `campaign-report`, `build-segment`, `design-email` and `crm-follow-up`. Each is a Markdown file of instructions for Claude. They contain no code.

The plugin runs nothing on your computer: no scripts, hooks or local servers.

## Connecting

You need a Spreeflo account. When Claude first uses the server, you sign in with your Spreeflo login and approve the connection on Spreeflo's consent page, where you pick the workspace and can choose read-only access. Claude never sees your password, and the plugin asks for no API key.

What the connection can do follows your role in the workspace (viewers get read-only access) and your workspace's plan. You can revoke the connection at any time from Spreeflo, under Connected AI apps.

## Data the plugin sends

- **To Spreeflo, and only to Spreeflo:** when Claude calls a tool, the call's arguments go to `https://mcp.spreeflo.com/mcp` with your OAuth token. Arguments can include contact details, segment rules, email content or a CSV you ask Claude to import. Results come back from your workspace.
- **What Spreeflo keeps:** each tool call is logged with its input and output, which can contain contact data. The input and output are redacted after 30 days, and the log row is deleted after 180 days.
- **Images by URL:** if you ask Claude to add an image from a web address, Spreeflo downloads that one image and stores a copy in your media library.
- **Nothing else:** the plugin sends no data to any other service and reads nothing from your computer.

Spreeflo's privacy policy: https://spreeflo.com/legal/privacy

## Limitations

Changes apply to your workspace straight away, without a separate review step. Sending or scheduling email, starting or resuming a campaign or journey, publishing a form and deleting anything can only be done by a person in the Spreeflo app, so new campaigns, journeys, broadcasts and forms stay drafts until you start or publish them there. Other changes apply at once: updating contacts, tags, segments or CRM records can set off your active journeys, which email contacts, and editing a template that an active campaign or journey uses changes what it sends from then on.

## Links

- Documentation: https://spreeflo.com/help/mcp-connecting
- Support: https://spreeflo.com/contact-us
- Terms of service: https://spreeflo.com/legal/terms-of-service
