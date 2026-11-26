---
name: peer-benchmark
description: Compare the person's own social account with the accounts they watch and find the content that works for those peers. Use when the person asks how they are doing against competitors, peers or creators they follow, who to learn from, what content works in their niche, what topics they are missing, or to see a given competitor's best posts.
---

# Peer benchmark with Alpine Reach

Goal: tell the person where they stand against the accounts they watch and what to make next, with the posts that prove it. Use stored Alpine Reach data; do not scrape social networks when `alpine_peers` has the data.

## 1. Get the evidence

1. Know the project. If no `projectId` is chosen yet, follow the alpine-reach-setup skill.
2. Call `alpine_peers` with `{ "projectId": "..." }`. Add `platform` when the person names a network, `days` (14, 30 or 90) for the window, and `account` with a handle to see one peer's best posts.
   - `state: "no_watched_accounts"`: the workspace watches no accounts. Tell the person to add the accounts to compare with in the Watchlist in Alpine Reach. Stop there.
   - A platform with `status: "no_owned_account"`: the person's own account on that network is not connected; compare peers with each other only and say so.
   - `status: "too_few_peers"`: not enough active peers to rank; give the numbers without a rank.
   - `state: "no_match"` in account mode: offer handles from `watched`.
3. Check freshness: `lastPostsReadAt` per watched account and `unreadPeers` per network. Say when peers have not been read yet.

## 2. Read it

- **Where I stand**: `engagementRank` ("3rd of 8"), my `engagementRatePercent` against the group median, `typicalViews` or `typicalLikes` against peers of similar size, `postsPerWeek` against theirs, `growth.mePercent` against `growth.peerMedianPercent`.
- **What works for peers**: `bestPosts` sorted by `timesTypical` (how many times the post beat that account's own typical post). Read `caption`, `transcript` and `hookToBorrow` to name the pattern: the opening, the format, the topic.
- **Gaps**: `topicGaps` are topics several peers covered and the person did not.

## 3. Answer

Lead with the verdict in one or two lines, then what to do.

1. **Where you stand**: rank, engagement and reach against the group, one line each, with the numbers.
2. **What to make next**: two or three post ideas, each modeled on a peer post that beat its account's typical post, with the opening line written for the person (never copied) and the link to the original.
3. **Evidence**: the posts used, with handle, date, times typical and link.
4. **Limits**: window, number of peers read, data age.

## Rules

- Every claim carries a number and, for posts, a link.
- Answer in the language the person writes in; numbers in that language's format.
- Use only data the tool returned. Never invent accounts, posts or numbers.
- Never carry a peer's claims about results or income into the person's content.
- Stored data only; for fresher data, the person refreshes in Alpine Reach.
