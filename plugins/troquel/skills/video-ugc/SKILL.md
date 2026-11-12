---
name: video-ugc
description: Make a finished UGC-style video ad with Troquel's K-Chin Studio, from the link of a product. Use when the user asks for a UGC video, a person talking about the product, a testimonial-format ad, an unboxing, "video UGC", "K-Chin", or several UGC videos at once.
---

# UGC video with K-Chin Studio

K-Chin Studio returns a finished vertical video from the link of a product: script in parts,
scenes, edit and subtitles. Answer in the user's language.

## Flow

1. **Plan.** `plan_ugc` with `product_url` (the product page) or `store_product_id`. Planning
   costs nothing, with a daily cap on scripts per account. It returns a `project_id`, the script
   in parts and the price in credits of the finished video. If the page cannot be read, try the
   direct link of the product.
2. **Show.** Give the user the script and the price. Wait for their yes.
3. **Create.** `create_ugc` only after the yes. That is when credits are charged.
4. **Collect.** `get_ugc` returns the status and the video URL. Check every 30 to 60 seconds;
   do not resubmit.

## Choices in `plan_ugc`

Take the valid values from the tool's own description, not from memory: they change.

- `format`: the kind of video (talking to camera in a car, testimonial, unboxing, problem and
  solution, objection, comparison and others).
- `avatar` or `avatar_id`: who tells it. `persona` adjusts accent, gender, age and traits.
- `seconds`: the presets are 16, 30, 60 and 80.
- `engine`: the video model, which decides how the script is split into parts.
- `quality`: `final` or `draft`.
- `angle` and `angle_type`: optional, if the user already has the angle.

If the user did not choose, use the defaults and say which ones you used.

## Several videos

Plan each one with `plan_ugc`, then `quote_ugc_batch` with the `project_id`s. Show every script
and the total. After approval, `create_ugc_batch` with the exact `quote_key` and
`expected_total_credits` of that quote, up to 4 projects per call. Follow each `project_id` with
`get_ugc`. A batch is not all-or-nothing: report partial results as they are. Never retry a
failed video on your own.

## Changes to a delivered video

`correct_ugc` re-edits the same material from the user's own words ("take out the repeated
line in part 2", "a shorter title"). It does not generate new video and does not charge extra,
but each video has a limited number of corrections. Call it only when the user asked for the
change, and show the result with `get_ugc`.

## What not to do

- Do not present the video as a real customer's review. It is an ad in UGC format.
- Do not promise sales or performance. Say what was made and what it cost.

## Errors

Follow the `next` field of the error. Failed videos refund their credits on their own.
