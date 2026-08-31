# NWR Maintenance Portal

Single-file React SPA (`public/index.html`) for tracking NOAA Weather Radio
transmitter maintenance, deployed to Firebase Hosting (project
`nwr-maintenance-v2`). See the Firebase deploy workflow in
`.github/workflows/deploy.yml`.

## Live Firestore access

Firestore project: **`nwr-maintenance-v2`** (`appId = "nwr-maintenance-v2"`).

- **Credentials:** `GOOGLE_APPLICATION_CREDENTIALS` points at the
  service-account key file under `NWR Resources\secrets` (the local
  `NWR Resources` directory, granted via
  `.claude/settings.local.json` → `permissions.additionalDirectories`). Use it
  for any admin/migration script that reads or writes Firestore.

- **Root (top-level) collections:**
  - `maintenance_log`
  - `parts_tracker`

- **Nested collections** — all under
  `artifacts/nwr-maintenance-v2/public/data/`:
  - `calendar_events`
  - `inspections`
  - `site_statuses`
  - `urgent_action_items`
  - `resource_links`

- **`maintenance_log` timestamp requirement:** every `maintenance_log` entry
  **must** include a `timestamp` field that is an **ISO-8601 UTC string**
  (e.g. `"2026-07-21T15:18:00Z"`). The log view queries with
  `orderBy('timestamp')`, so any entry missing this field is silently excluded
  and will not display in the app. Always set it on write.
