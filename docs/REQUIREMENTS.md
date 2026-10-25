# Rootly — Requirements

Confirmed v1 requirements. Implementation and legal questions are listed at the end.

## Product

- Rootly has two equally primary loops in v1: caring for your own Plants and discovering other people's Plants. See `docs/adr/0001-care-and-community-both-primary.md`.
- The community side is read-only: Map, Profiles, and Public Plants. No follows, reactions, comments, or direct messages. See `docs/adr/0002-v1-community-read-only.md`.
- Both loops are the product's positioning, but v1 validates the care loop first. Discovery is read-only and may be sparse.
- Anyone can browse the Map and public Profiles without an account. An account is required to own Plants, log care, and publish a Plant.

## Plants

- A user has one flat list of Plants. Rootly has no Collection, Balcony, or Garden entity.
- A Plant has a mandatory personal name. Its Species is optional.
- Plant names need not be unique, can be changed, and are capped at 60 characters.
- Photos are optional.
- A Public Plant without a photo uses a placeholder.
- There is no automatic photo identification in v1. Species is chosen manually from a searchable catalog, with a Custom Species free-text fallback.
- The catalog contains roughly 100 common houseplants, with common and scientific names.
- Catalog care data is curated from reputable public sources and reviewed before release, with source notes.
- A Catalog Species carries curated care guidance; a Custom Species does not.

## Map and privacy

- Every Plant is private by default.
- A Plant has one visibility switch. Making it public shows it on both the Profile and the Map; there is no profile-only state.
- A Plant can be made public by its Owner, one at a time; Map inclusion is opt-in.
- A Public Plant appears as a pin at a neighborhood-level coarse location, never an exact address.
- All of an Owner's Public Plants share one coarse area to prevent triangulation.
- Exact coordinates are never stored or displayed.
- The Coarse Area is a grid cell of roughly 1 km.
- The Owner sets the Coarse Area by panning and tapping the Map; GPS may center it, but only the resulting grid cell is stored.
- The Owner can change the Coarse Area later; all of their Public Plants move with it.
- See `docs/adr/0004-plants-mapped-at-coarse-locations.md` and `docs/adr/0006-plants-private-by-default.md`.

## Platform

- v1 is a cross-platform mobile app built with React Native and Expo for iOS and Android. See `docs/adr/0007-cross-platform-mobile-v1.md`.

## Technology

- Backend: Supabase (Postgres, Auth, Storage, Row-Level Security, PostGIS). See `docs/adr/0009-supabase-backend.md`.
- Maps: MapLibre with a self-hosted PMTiles archive; no map vendor API and no geocoding. Requires an Expo development build. See `docs/adr/0010-maplibre-self-hosted-pmtiles.md`.
- Map tiles: Protomaps planet PMTiles hosted on Cloudflare R2, with OpenStreetMap/Protomaps attribution.
- Offline: last-synced data is readable; writes require network; there is no offline write queue in v1.
- Analytics: first-party events only (activation, care logged, Plant published, discovery viewed), with no PII or precise location and no third-party ad tracking.

## Launch

- v1 is available globally; there is no geographic gating.
- v1 is English-only.
- The Map may be sparse at launch; the global recent feed and the care loop carry v1.
- Empty nearby results point the visitor to the global feed and to publishing their own Plants.

## Identity

- An Owner has a unique Username, a free-form Display Name, and an optional avatar.
- The Username is shown with `@` and used in the Profile URL.
- A real name is never required.
- Sign-in methods: Google, Apple, and email one-time code.
- Username changes are allowed; the old Username is reserved for 30 days and does not redirect. Display Name can change anytime.
- Account recovery uses the same sign-in methods. If all access is lost, support performs manual recovery after verification. There are no security questions.

## Discovery

- A visitor discovers Public Plants within a radius of their device location.
- The nearby radius defaults to 10 km, with 5/10/25/50 km options.
- There is no place search or geocoding.
- If location permission is denied, the Map opens at a default view and can be panned and zoomed manually; radius-based nearby discovery is unavailable.
- A visitor can filter Public Plants by Catalog Species; Custom Species are grouped under "Other".
- A global "recent" feed shows Public Plants ordered by first publish time, with a 30-day window and an all-time fallback when sparse.
- Edits and unpublish/republish do not bump a Plant in the feed.
- The feed shows one card per Public Plant and excludes blocked and reported content.
- Visitor location is used only to filter nearby results and is not stored.

## Photos

- Photos are compressed client-side before upload, with a 10 MB maximum per upload.
- Each Owner has a fair-use cap of 1 GB of photo storage.
- When the cap is reached, new uploads are blocked until the Owner deletes photos.

## Monetization

- v1 is free: no paywall and no ads.
- The photo cap controls infrastructure cost.
- A future version may add free usage limits with a paid unlock; this is not in v1.

## Data controls

- Account deletion is available in-app, behind re-authentication and an explicit confirmation.
- Deletion immediately removes the account, Plants, care logs, Growth Entries, photos, and public content. Backups are purged within 30 days and deletion is not reversible.
- Data export is handled manually through support in v1.

## Eligibility and content

- Owners must be 16 or older, self-attested at sign-up.
- There is no parental-consent flow in v1.
- Prohibited content: harassment, hate, sexual content, illegal activity, and non-plant content.
- Display Names, plant names, and photos must not contain personal contact details.
- Reported content can be removed.

## Safety

- A visitor can report a Public Plant or Profile.
- A visitor can block an Owner; blocked content is hidden for that visitor and the block is not disclosed to the Owner.
- Blocks are stored at the account level so they persist across devices.
- Reports go to a manual admin review queue; content can be removed.
- v1 has no automated moderation or appeals process.

## Public Profiles

- A Profile becomes discoverable only when it has at least one Public Plant.
- A public Profile shows the Owner's Display Name, avatar, approximate area, and Public Plants.
- The approximate area is a small map preview with a shaded 1 km cell labeled "Approximate area"; no neighborhood name is shown.
- A Public Plant shows its personal name, photo, and Species. Without a Species, it shows "Species unknown".
- Care logs, schedules, Measurements, notes, and Growth Entries are never public in v1.

## Plant lifecycle

- A Plant can be archived. Archiving stops its reminders, removes it from the active list, and unpublishes it, while retaining its history.
- A Plant can be permanently deleted with confirmation; deletion removes its care logs and Growth Entries.
- An archived Plant can be restored.
- Archiving automatically unpublishes the Plant.

## Care

- v1 tracks watering and fertilizing only.
- A Catalog Species provides default watering and fertilizing intervals.
- The Owner can override intervals per Plant.
- For a Custom Species, the Owner sets the intervals; the form pre-fills 7 days for watering and 30 days for fertilizing, editable.
- Logging a care action resets that Plant's next due date.
- Care logs record the current time only. A 5-second undo is offered, and logs can be edited or deleted from history; timestamps cannot be backdated.
- v1 has no care-log notes.
- Reminders address the Plant by its personal name.

## Care guide

- A Catalog Species shows a structured Care Card: light, watering, fertilizing, soil, temperature, toxicity, and a short note.
- A Custom Species shows generic care guidance and the Owner's own schedule.
- v1 has no long-form species articles or external care links.

## Reminders

- v1 sends one daily digest at an Owner-chosen local time, defaulting to 9:00 local time, listing due Plants by name and grouped by care action. The time follows the Owner's stored timezone and re-localizes when it changes. See `docs/adr/0008-care-reminders-are-a-daily-digest.md`.
- An in-app due list is always available, even when push permission is denied.
- v1 does not send individual per-action notifications.
- An overdue action stays in every daily digest, labeled overdue by N days, until it is logged or its interval is changed. There is no separate nagging notification.
- Push delivery uses Expo Push. If a push fails, the in-app due list remains authoritative.
- Notification permission is requested after the first Plant and schedule are saved, with an explanation; never at first launch.

## Growth

- A Growth Entry belongs to one Plant and has a date.
- An entry requires at least one of: a photo, a Measurement, a note, or an Event.
- Photos are optional, one or more per entry.
- Measurements are independently optional: height/length, width, and leaf count. Lengths use cm or inches.
- Notes are optional free text.
- Events are optional and chosen from a fixed list: repotted, pruned, flowered, propagated, pest/disease, other.
- Charts are derived over time from numeric Measurements.
- Tasks are not part of Growth Entries; care reminders remain a separate concept.

## Success

- An activated Owner has added at least one Plant and accepted a care schedule.
- Primary metric: the share of activated Owners who log at least one watering or fertilizing action in week 4.
- Leading indicator: activation rate.
- Secondary signals: Public Plant publication rate and discovery engagement.

## Non-goals for v1

- Automatic photo identification.
- Follows, reactions, comments, or direct messages.
- Collections, Balconies, or Gardens as entities.
- Public care logs, schedules, Measurements, notes, or Growth Entries.
- Exact plant or Owner coordinates.
- Web app, non-English UI, or geographic gating.
- Paywall, ads, or paid tiers.
- Automated moderation or appeals.

## Open implementation and legal questions

- Privacy policy, terms of service, and report-response process.
- Admin moderation tooling.
- Map pin clustering and performance at low zoom.
- Legal review of care guidance and toxicity data.
- App store release setup (EAS, store accounts).
