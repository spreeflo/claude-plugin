---
name: build-segment
description: Use when the user wants to find, count, group or target contacts in their Spreeflo workspace by attributes, tags, email or form activity, tracked events, CRM fields or website behaviour, and save the group as a segment, or wants to see who an existing segment contains or change its rules.
---

# Build a segment

A segment is a saved, always up-to-date group of contacts in one audience. Creating one sends nothing: a campaign or journey uses it only once a person points one at it in the Spreeflo app. Explicit instructions from the user take priority over this skill.

## Input

Who the user wants, in their words. If a word could mean several rules ("engaged", "inactive", "VIP"), propose a concrete definition, such as "opened an email in the last 30 days", and confirm it before creating anything.

## Steps

1. **Audience.** `list_audiences`. Ask which one if there are several and the request does not say.
2. **Look for one that exists.** `list_segments` with the audience's `contactListId`. If one already matches, preview it (step 7) instead of making a duplicate.
3. **A simple count may not need a segment.** For one tag, a lifecycle stage, an owner or a score range, `list_contacts` with those filters returns the matching total. Offer to save it as a segment only if the user wants it kept.
4. **Read the format.** `read_format_doc` with `segment-json-format` and with `segment-builder`, once in the conversation, before writing a definition.
5. **Resolve every id the rules need**; never guess one:
   - tags: `list_tags`
   - attributes: `list_contact_attributes`
   - emails and campaigns: `list_email_templates`, `list_campaigns`
   - forms: `list_forms`
   - tracked events and their properties: `list_custom_events`, `list_custom_event_properties`
6. **Create.** `create_segment` with `audienceId`, a clear `name` and the `definition`. If it is rejected, nothing was saved: fix what the reasons name and call it again.
7. **Preview.** `get_segment_preview` with the new `segmentId`. Report the member count and a few sample contacts, and restate the rules in plain words.

## Changing an existing segment

Read it with `get_segment_definition`. Before `update_segment`, tell the user that the new rules change who is in it, and that active journeys triggered by joining or leaving it can then email the contacts who move. Go ahead only on a yes.

## Rules

- Website-activity rules depend on the workspace's plan. If the tool answers that they are not available, tell the user and offer the closest rules built from tags, attributes, email activity or form activity instead.
- Do not describe a segment as sent to, or used by, a campaign. That happens in the app.
