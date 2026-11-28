---
name: analyze-a-post
description: Analyze a pasted Instagram, TikTok, YouTube or LinkedIn post or profile link with Alpine Reach - how the post did against its account's normal, why it worked, what it says (caption, opening line, transcript) and what to borrow. Use whenever the person pastes a social post or profile link and asks how it did, why it went viral, what the video says, what the hook is, or how to make something like it.
---

# Analyze a post or profile link

Goal: tell the person, in a few lines, whether this post beat its own account's normal and by how much, why it likely did, and how to make one like it for their own account. Use the stored data in Alpine Reach; do not open or scrape the link when `alpine_analyze_link` has it.

## 1. Get the evidence

1. Know the project. If no `projectId` is chosen yet, follow the alpine-reach-setup skill.
2. Call `alpine_analyze_link` with `{ "projectId": "...", "url": "<the link as pasted>" }`.
   - `state: "unsupported_link"` with `reason: "short_link"`: ask for the full address the short link opens. Other reasons: say which links work (public Instagram, TikTok, YouTube or LinkedIn post or profile).
   - `state: "not_in_workspace"`: Alpine Reach has no stored posts for that account in this workspace. Tell the person to add the account to the Watchlist in Alpine Reach; its posts arrive with the first read. Stop there; do not guess numbers.
3. For a post, `post` holds its numbers and text. For a profile, `post` is null and `account` plus `bestPosts` carry the answer.

## 2. Read it

- **Did it work?** `timesTypicalInteractions` compares the post with its own account's typical post (median of the last 90 days). 3 times or more is a clear outlier; around 1 is a normal post; under 0.5 underperformed. Use `timesTypicalViews` on video. Add `rankInWindow` ("2nd of 41 posts in 90 days").
- **Too early or unreadable**: `stillGathering` (under three days old) or `metricsHidden` (likes hidden) means no multiple. Say so and give the raw numbers only.
- **Why**: read `openingLine`, `transcriptOpening` and the caption. Name the mechanism (question, bold claim with a number, pain, story, proof, list, contrarian take, trend audio) and the format (`contentType`). Compare with the account's other `bestPosts`: a pattern shared by several of them is stronger than one post.
- **What it says**: summarize `transcript` in 2 to 4 lines when it exists (`transcriptAvailable`). Quote at most one or two short lines.
- **Account context**: `account.followers`, `typicalViews`, `engagementRatePercent`, `postsPerWeek`. `relation` is `own` for the person's own account.

## 3. Answer

1. **Verdict** in one line: "This post reached 6.2x the account's typical post (1st of 38 in 90 days)."
2. **Why it worked**: 2 or 3 reasons, each tied to something in the post (its opening line, format, topic, length of the caption).
3. **What it says**: the short transcript or caption summary.
4. **Make one like it**: 2 or 3 opening lines and a structure written for the person's own account and offer, modeled on the mechanism, never copied.
5. **Limits**: data age (`lastPostsReadAt` when given), that likes and views are public counts, and that the numbers say nothing about sales.

## Rules

- Every claim carries its number with its base ("6.2x its typical post", "38 posts in 90 days") and the post link.
- Never carry the creator's income claims, results or promises into the person's content. Model the structure, not the claims.
- Answer in the language the person writes in. Write numbers the way that language does (for Brazilian Portuguese: 1.234 e 6,2x).
- Use only data the tool returned. Do not invent numbers, posts or quotes.
- Do not reveal internal ids or fields; use handles, numbers and links.
- This skill reads stored data only and never starts a paid collection.
