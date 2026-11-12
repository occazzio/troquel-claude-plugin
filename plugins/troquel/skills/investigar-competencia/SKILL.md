---
name: investigar-competencia
description: Read the ads a brand is running on Meta, label them and score creatives with Troquel. Use when the user wants to study a competitor's ads, see what a brand has live in the Meta Ad Library, find which creatives a brand keeps running, or score their own ad before publishing.
---

# Competitor ad research

Answer in the user's language. Prices are in credits (1 credit = USD 0.01); `list_models` and
each tool's answer give the current cost.

## 1. Pull the library

`scrape_meta_library` takes a Meta Ad Library link or a page id and returns the ads the brand
has live. It is charged per ads read, so say the cost before a large pull. Libraries already
pulled are in `list_sources`: reuse them instead of paying again.

## 2. Label the ads

`analyze_ads` labels each ad against twelve questions (hook, format, offer, CTA, awareness
level and more). It costs credits: tell the user the total first.

When you report, lead with what repeats: the creatives that have been running longest, the ones
with several active copies, and the formats more than one brand uses. Those are observations
about what the brand keeps paying for, not proof of results. Do not state sales or ROAS
figures; the library does not contain them.

## 3. Score a creative

`score_creative` scores an ad image from 0 to 100 against a fixed rubric. For a file from the
chat, get its URL first with `request_upload` and `get_upload`. Report the score with the
reasons the tool returns, and what to change.

## 4. Turn findings into pieces

To make creatives from what you found, use the `anuncios-producto` skill: real product photo
as reference, price stated before generating.

## Errors

Follow the `next` field of the error. `insufficient_credits`: offer the top-up link the error
returns. `invalid_request`: fix what `error` says and resend.
