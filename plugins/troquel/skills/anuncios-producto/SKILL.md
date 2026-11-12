---
name: anuncios-producto
description: Make ad images and short ad videos of a real product with Troquel. Use when the user wants ad creatives, product photos, static ads, a product video or variations for Meta, TikTok or their store, or says "anuncio", "creativo", "foto de producto", "video del producto", "ad creative".
---

# Ad creatives from a real product

Troquel generates images, video and voice with the user's own credits (1 credit = USD 0.01).
Answer in the user's language. Text that appears inside the piece goes in the language of the ad.

## 1. Get the real product, never a description

Troquel does not receive files attached to the chat. If the user attached or mentions a product
photo, logo or face:

1. `request_upload` gives the user a place to drop the original files.
2. `get_upload` returns the URLs once they are uploaded.

Saved brand photos come from `list_brands`. Earlier generations come from `list_generations`.
Do not send a downscaled base64 image and do not describe the product in words instead of
passing it: the model invents what it cannot see.

## 2. Pick the model and say the price first

`list_models` returns every model with its variants, limits and price in credits. Choose from
that list, not from memory. Before anything that costs more than a few credits, or any batch,
call the generation tool with `dry_run: true` and tell the user the total. Generate only after
they agree. If credits are short, `balance` shows what is left; offer a cheaper variant or the
top-up link the error returns.

## 3. Write the whole prompt

The prompt reaches the model as written. Troquel does not translate or complete it.

- Describe subject, setting, light, framing and format.
- If the image carries text, write the exact words. A sign with no stated text comes out illegible.
- Name references by their role: "the product in reference 1".
- In video, pass `references` with a `role` (`first_frame`, `last_frame`, `product`, `character`,
  `subject`, `style`). `list_models` says which roles each model accepts.

## 4. Generate and wait once

- Several images: `n` in `generate_image`, or several calls.
- Collect every `job_id` and wait with a single `get_jobs` call. Do not poll one by one.
- If the client can time out or retry, pass `idempotency_key`.

## 5. Finish the piece

On a finished image (by `image_url` or `job_id`): `remove_background`, `upscale_image`,
`expand_image` to reframe to another ratio without cropping.

## Errors

Follow the `next` field of the error.

- `insufficient_credits`: offer the cheaper option or the top-up link.
- `too_many_in_flight`: `get_jobs` with the jobs in flight, then resend.
- `provider_unavailable`: use one of the `alternatives`.
- `invalid_request`: fix what `error` says.
- `content_policy`: change the prompt or the reference before trying again.

Failed jobs refund their credits on their own. Troquel already retries random provider failures
once: if the answer says `retrying`, wait for it and do not resubmit.

## What not to promise

Say what the tool makes and what it costs. Do not promise sales, ROAS or that a creative will
perform.
