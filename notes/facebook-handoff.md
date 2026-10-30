# Kaya Kreates Facebook: session handoff

Last updated 30 Oct 2026. Read this before doing Graph API work on the Kaya Kreates Page.

## Setup

- Pages: **Kaya Kreates** `194865463713135` (this file) and **Twnda** `1410685179208832` (handled in a separate session).
- App: "Kreates Twnda Manager". System User: "Kaya Klaude". The System User token is injected by the environment proxy for `graph.facebook.com`.
- The token was regenerated on 30 Oct 2026 to add `pages_manage_metadata`. Check `/me/permissions` first.
- Token rules: never print or log any token. Save Page tokens to a `chmod 600` file in the scratchpad and pass them with `curl --data-urlencode "access_token@file"`. Strip `paging` and `access_token` from every response before showing it.
- The proxy overwrites the `Authorization` header with the System User token. Send Page tokens as the `access_token` parameter instead.
- Don't delete or overwrite anything without explicit approval.

## How to post backdated content (works)

- **Photo posts:** upload each photo to `/{page}/photos` with `published=false`. Then `POST /{page}/feed` with `message`, `attached_media[n]={"media_fbid":...}`, `backdated_time` (unix) and `backdated_time_granularity=min`. This makes one real post. Don't post straight to `/photos`, which only creates photo uploads.
- **Times shift on create.** Facebook stores the time shifted by the US Pacific offset (7 h in Oct, 8 h in Nov/Dec). Read `backdated_time` back after creating, then `POST /{post-id}` with the same `backdated_time` + granularity to correct it. The update stores the exact value.
- **Videos:** `POST graph-video.facebook.com/v23.0/{page}/videos` with `source`, `description` and `backdated_post={"backdated_time":...,"backdated_time_granularity":"min"}`. The time is stored exactly. A video can't be both unpublished and backdated.
- **Link posts** (e.g. Spotify): `/feed` with `link=` and a backdated time. They show as music cards.
- **Can't do via the API:** hide or unpublish the Page's own posts (`is_hidden` and `is_published=false` are both refused). Archive in Business Suite instead.
- **Timeline:** backdated posts showed on the Page timeline once the app was published (confirmed by the owner 30 Oct 2026). They never go to followers' home feeds.
- **Style the owner wants:** campaigns of about 15–18 posts per event. Irregular gaps, sometimes two posts a day, a quiet week after the announcement, posters repeated with different angles, photos split across several after-event posts. Days and times come from a seeded random generator, not even spacing.

## Done

- **Ningenjelwanga Experience** (Sat 11 Oct 2025, Umunthu Space, Mzuzu, partner Mzuzu Mafia): 15 posts, 26 Sep to 21 Nov 2025. Credit "📷 Mzuzu Mafia". The source media came from Twnda's page.
- **Afrobeat & HipHop Hangout** (Sat 14 Dec 2024, Le Jardin, Area 43, Lilongwe): 18 posts, 13 Nov to 31 Dec 2024, including 4 guest Spotify playlists and the recap video. Credit "📷 DC28" (day) and "📷 Fatbway Montage" (night). No edition number: Twnda said 2nd, the Drive folder says 3rd.

## Open items

1. **Page info.** Needs `pages_manage_metadata`. Then `POST /{page}` with:
   - `about`: "Creative industrialists. We plan, organise and deliver creative projects. Mzuzu, Malawi."
   - `description`: the About text below.
   - `emails`: `["kayakreates@gmail.com"]`
   - Founded: **leave empty** (owner's decision).
   - Category: Arts & Entertainment + Community Organization, replacing "Digital creator". This probably needs Business Suite.
   - Address: Kaya Business Park, Jowelo Rd Block, Mzuzu, Malawi.
   - Username: @KayaKreates.
   - Never describe Kaya as a studio or an events company.

   About text:

   > Kaya Kreates is a Malawi-based venture platform that develops and administers projects across different areas of work. We bring together ideas, people, resources and partnerships to move initiatives from concept to execution.
   >
   > We don't replace creatives. We bring them together, give the work a plan, a standard and a structure, and make sure everyone who made it gets credit.
   >
   > We turn creative ideas into workable projects, from planning and coordination to partnerships, resource management and execution.
   >
   > Creativity is non-linear.

2. ~~The 4 original Ningenjelwanga posts~~: deleted on 30 Oct 2026 with the owner's approval (marked "ninge v1" below).
3. **Next events, one at a time.** Ask the owner for posters, photos, credits and dates:
   - Valentine's at Kwithu (14 Feb 2026, Kwithu Kitchen)
   - First Sunday Market: ed. 1 Sun 3 May 2026, ed. 2 Sun 7 Jun, ed. 3 Sun 5 Jul, ed. 4 Sun 9 Aug (postponed from 2 Aug). Mood Café & Garden. Confirm Sep/Oct.
   - Words Build Worlds (Liza Mawu): Twnda's posts say Sat 25 Jul 2026, 2–5pm, Kwithu Rooftop Kitchen. The pack says 27 Apr 2026. Confirm.
   - Liza Mawu street cleaning (around 4 Jun 2026)
   - Twnda & The Kaya Band Live and Unplugged, Kuwala Gardens (6 Jul 2024). Already on the Page from 24 Aug 2024.
   - End of Year Mixer, Camp Fire Soul, Ghetto Youth Festival: dates unknown.
4. The profile picture (Kaya K mark) and an orange cover ("Creativity is non-linear.") need image files from the owner.

## Posts created via the API (30 Oct 2026)

| Campaign | Backdated to (UTC) | ID |
|---|---|---|
| hangout (recap video) | 2024-12-23T12:00 | video 1914908372676858 |
| hangout | 2024-11-13T10:46 | 194865463713135_122301621992164388 |
| hangout | 2024-11-23T05:04 | 194865463713135_122301622136164388 |
| hangout | 2024-12-03T09:57 | 194865463713135_122301622196164388 |
| hangout | 2024-12-04T08:38 | 194865463713135_122301622310164388 |
| hangout | 2024-12-04T11:46 | 194865463713135_122301622418164388 |
| hangout | 2024-12-07T05:51 | 194865463713135_122301622496164388 |
| hangout | 2024-12-07T08:23 | 194865463713135_122301622562164388 |
| hangout | 2024-12-10T06:04 | 194865463713135_122301622790164388 |
| hangout | 2024-12-10T12:51 | 194865463713135_122301622928164388 |
| hangout | 2024-12-13T05:17 | 194865463713135_122301623120164388 |
| hangout | 2024-12-14T09:57 | 194865463713135_122301623294164388 |
| hangout | 2024-12-15T09:46 | 194865463713135_122301624344164388 |
| hangout | 2024-12-16T05:46 | 194865463713135_122301626168164388 |
| hangout | 2024-12-18T08:32 | 194865463713135_122301627392164388 |
| hangout | 2024-12-19T07:17 | 194865463713135_122301628232164388 |
| hangout | 2024-12-31T10:38 | 194865463713135_122301628556164388 |
| hangout | 2024-12-31T14:17 | 194865463713135_122301628748164388 |
| ningenjelwanga v2 | 2025-09-26T09:03 | 194865463713135_122301630686164388 |
| ningenjelwanga v2 | 2025-10-01T09:58 | 194865463713135_122301630764164388 |
| ningenjelwanga v2 | 2025-10-01T15:41 | 194865463713135_122301630884164388 |
| ningenjelwanga v2 | 2025-10-03T11:09 | 194865463713135_122301630986164388 |
| ningenjelwanga v2 | 2025-10-03T17:36 | 194865463713135_122301631286164388 |
| ningenjelwanga v2 | 2025-10-07T06:48 | 194865463713135_122301631496164388 |
| ningenjelwanga v2 | 2025-10-07T09:03 | 194865463713135_122301631886164388 |
| ningenjelwanga v2 | 2025-10-10T07:27 | video 1417072066757324 |
| ningenjelwanga v2 | 2025-10-10T10:53 | 194865463713135_122301632378164388 |
| ningenjelwanga v2 | 2025-10-11T05:48 | 194865463713135_122301632678164388 |
| ningenjelwanga v2 | 2025-10-15T09:03 | 194865463713135_122301632942164388 |
| ningenjelwanga v2 | 2025-10-16T07:36 | video 937722309214447 |
| ningenjelwanga v2 | 2025-10-19T08:27 | 194865463713135_122301633296164388 |
| ningenjelwanga v2 | 2025-11-02T05:03 | video 1585427216245053 |
| ningenjelwanga v2 | 2025-11-21T08:36 | video 986096237885791 |
| ninge v1 (DELETED 30 Oct 2026) | 2025-10-05T12:00 | 194865463713135_122301608324164388 |
| ninge v1 (DELETED 30 Oct 2026) | 2025-10-10T12:00 | 194865463713135_122301609524164388 |
| ninge v1 (DELETED 30 Oct 2026) | 2025-10-13T12:00 | 194865463713135_122301610124164388 |
| ninge v1 (DELETED 30 Oct 2026) | 2025-10-19T12:00 | 194865463713135_122301610454164388 |
