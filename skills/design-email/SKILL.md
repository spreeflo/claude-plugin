---
name: design-email
description: Use when the user wants to draft, write, redesign or fix an email template in Spreeflo, such as a newsletter, announcement, welcome, transactional or double opt-in email, including one modelled on an existing template or on email HTML they paste. Builds the template, reads Spreeflo's style checks and fixes what they flag.
---

# Design an email template

Creating a template sends nothing: it is emailed only when a campaign or journey that uses it is started, which a person does in the Spreeflo app. Changing a template that an active campaign or journey already uses changes what it sends from then on. Explicit instructions from the user take priority over this skill.

## Input

- What the email is for, who receives it, and the facts it must state (offer, dates, links). Ask for facts that are missing; never invent prices, discounts, dates or claims.
- Optionally, a reference: an existing template's name, or email HTML the user pastes.

## Steps

1. **Audience and type.** `list_audiences`, then pick the type: `CAMPAIGN` for marketing email, `TRANSACTION` for receipts and account email, `OPT_IN` for a double opt-in confirmation.
2. **Read the format.** `read_format_doc` with `email-json-format`, once in the conversation. It covers sections and blocks, personalisation variables and how to work from a reference.
3. **Voice.** `get_business_profile` for the tone and words the business uses.
4. **Starting point.**
   - A variation of an existing template: `duplicate_email_template`, then edit the copy.
   - Modelled on one: `list_email_templates`, then `get_email_template_structure` to see its sections.
   - From pasted HTML: rebuild it section by section in the builder format. Images in someone else's email belong to them; use the user's own.
5. **Images.** `list_media` for images already in the library. For an image the user has online and the right to use, `upload_media_from_url`. Use the `imageUrl` either returns as the image block's `src`.
6. **Create.** `create_email_template`. A `CAMPAIGN` template needs the unsubscribe link and an `OPT_IN` template the opt-in link, as the format doc shows.
7. **Fix the checks.** The result lists style checks (each naming a `blockId`) and variable warnings. Call `get_email_template_structure`, then `update_email_template` with the full sections, keeping the ids of blocks that stay. Repeat until no check is left or the user accepts the rest.
8. **See it as a recipient would.** `get_email_template_html` returns the subject, preview, plain text and the checks, rendered with `sampleValues` or as one contact (`contactId`). Ask for the HTML (`include` with `html`) only when the user wants the code itself.
9. **Report** the template's name, the subject and preview, any check left, and that it sends nothing until a campaign or journey using it is started in the app.

## Rules

- `update_email_template` replaces the current version, and active campaigns and journeys that use the template send the new version from then on. Before changing a template that may be in use, say so and get a yes, or offer to work on a copy.
- Personalise with the variables the format doc describes, with a default for when a contact has no value.
