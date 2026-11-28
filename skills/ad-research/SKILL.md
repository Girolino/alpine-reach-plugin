---
name: ad-research
description: Recommend which ads to make for a product, offer or launch from what competitors and peers actually keep running on Meta (Facebook and Instagram). Use when the person asks what ad, ad format, hook, creative or ad copy to make, what competitors advertise, which ads work at a given price, whether to send ads to a sales page or straight to checkout, or how a competitor tests ads.
---

# Ad research with Alpine Reach

Goal: a ready recipe ("make these three ads, sending people here") backed by ads that real advertisers keep paying for. Use the stored data in Alpine Reach; do not scrape the Ad Library or browse when `alpine_ads` has the data.

## 1. Get the evidence

1. Know the project. If no `projectId` is chosen yet, follow the alpine-reach-setup skill.
2. Note what the person is selling: product type, price, audience. Ask only for what is missing and changes the answer (usually the price).
3. Call `alpine_ads` with `{ "projectId": "...", "advertisers": 10, "longestRunning": 8 }`.
   - To study one competitor, pass `advertiser` with its name or Instagram handle.
   - `state: "no_tracked_advertisers"`: the workspace tracks no advertisers. Tell the person to add the competitors to the Watchlist in Alpine Reach and confirm their Facebook pages (or add them in Ads). The first read arrives with the next daily refresh. Stop there; do not guess.
   - `state: "no_match"`: offer the names in `otherAdvertisers`.
4. Check freshness: `dataAgeHours` per advertiser. Say so when the latest read is more than 3 days old.

## 2. Read it the way a media buyer would

- **Proof that an ad works** is time running. An ad running 30 days or more (`daysRunning`, `runningOver30Days`) is the strongest public signal; the Ad Library shows no sales or spend. Never call an ad "validated" or "converting"; say "has run for N days".
- **Format**: compare the format mix of all sampled ads with the formats of the longest running ads. The format to start with is the one that dominates among ads past 30 days, not the most common one overall.
- **Hook**: read `openingLine` of the longest running ads. Name the patterns (question, promise with a number, pain, proof, direct offer) and quote two or three real opening lines with their advertiser and days running.
- **Price bands**: group the ads by the prices in `prices` (each with its ad count) and `priceMentions` (for example under 100, 100 to 200, 200 to 1,000, above 1,000 in the person's currency). If no tracked advertiser advertises a price in the person's band, say that plainly in the first lines and say which neighbouring bands the recipe is inferred from.
- **Destination and temperature**: `destinations` tells sales page vs checkout vs WhatsApp. Keep two groups apart: ads that send people to a sales page with the price visible (made to reach new people), and low-price ads that go straight to checkout (usually impulse offers or retargeting of people who already know the seller). Do not mix their numbers into one recipe. The Ad Library shows no audience, so a retargeting reading comes only from the ad copy: call it retargeting when the copy speaks to people who already showed interest ("you joined but have not secured your spot"), quote that line, and say "likely" otherwise. To read the checkout group alone, call `alpine_ads` again with `"destination": "checkout"`.
- **Tests**: in `recentTests`, a test with most ads stopped and one or two still running shows which variant the advertiser kept. Use `survivorExamples` as the strongest per-advertiser evidence. Proof level `early` or `low` is weak; say so.
- **Cadence**: `launchedLast7` and `stoppedLast7` show how fast advertisers rotate creatives; use it to suggest how many new ads per week.

## 3. Answer

Lead with the recipe, then the evidence. Keep it short.

1. **Start with**: format, destination and call to action, one line each, with the reason in a few words.
2. **The first three ads**: for each, the format, an opening line written for the person's product (modeled on a real pattern, never copied), the body structure, the call to action and where it sends people.
3. **Evidence**: 3 to 5 ads with advertiser name, days running, format and the Ad Library link (`adLibraryUrl`).
4. **Limits**: data age, how much was read (`aggregateBasis`: `full_read` counts every ad of the latest read, `sample` only `sampledAds`; give `adsInLatestRead` of `activeAdsKnown`; say when `readBudgetReached` or `trimmedToFit` is true), and that time running is a proxy, not sales.

## Rules

- Every claim carries its evidence: a count with its base ("13 of 174 ads go straight to checkout", "7 ads at R$ 49 or R$ 97", "ran 63 days") taken from the call that returned it, and at least one Ad Library link (`adLibraryUrl`). This holds most for the destination and the price the recipe rests on: never state those without their counts.
- The tool returns ad text, opening line, format and destination, not what happens inside a video (who is on camera, captions, when the price or call to action is spoken). Say so when the person asks about video structure; do not guess it.
- An amount followed by "mil", "milhão" or "milhões" ("R$ 100 mil em vendas") is a result claim, not a price. Never read it as a price band.
- Never carry advertisers' income claims, results or promises into the person's ads. Model the structure, not the claims; write copy the person can prove.
- Answer in the language the person writes in. Write numbers and prices the way that language and the workspace's country do (for Brazilian Portuguese: R$ 1.234,56).
- Use only data the tool returned. Do not invent advertisers, ads, numbers or links.
- Do not reveal tracking ids or internal fields; use names, numbers and Ad Library links.
- This skill reads stored data only. If the person wants fresher data, tell them the daily refresh in Alpine Reach updates it; do not start paid reads from here.
