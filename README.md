# Lab Paper Tracker (Local Mode)

Web app for paper-reading logs in Hasegawa Laboratory, running fully in browser local storage.

## Features

- Local `Join` flow (name + email) on first visit
- Automatic returning-session authentication from local browser session
- Paper record submission/edit/delete:
  - paper title
  - paper URL
  - reading time
  - memo link
- Personal dashboard:
  - paper count
  - reading time statistics
  - weekly trend chart
- Objective management:
  - one-time objective setup (immutable after save)
  - progress tracking with progress bar
- Shared leaderboard and profile views for all users stored in the same browser
- Paper list search + pagination
- Public profile URL routing (`?user=<uid>`)

## Stack

- Frontend: HTML, CSS, JavaScript
- Storage: Browser `localStorage`
- Chart: Chart.js

## Setup

1. Serve this folder with a local/static web server.
2. Open in browser.

Example:

```bash
npx serve .
```

No Firebase, OAuth, or external database is required.

## Publish Public Link (GitHub Pages)

1. Create a GitHub repository and push this project.
2. Keep your default branch name as `main` (or update workflow branch if different).
3. In GitHub repository settings:
   - Open `Settings` -> `Pages`
   - Set `Source` to `GitHub Actions`
4. Push to `main`. The included workflow deploys automatically.
5. Your public URL will be:
   - `https://<your-github-username>.github.io/<repo-name>/`

Included deployment files:

- `.github/workflows/deploy-pages.yml`
- `.nojekyll`

## Fast Publish Alternative (Netlify Drop)

If you want a quick temporary public URL without GitHub setup:

1. Open [Netlify Drop](https://app.netlify.com/drop)
2. Drag and drop this project folder.
3. Netlify immediately gives you a public link.

## Local Data Model (in localStorage)

- `users` map by uid
  - `uid`, `displayName`, `email`, `joinedAt`
- `papers` array
  - `id`, `uid`, `userName`, `paperTitle`, `paperUrl`, `readingMinutes`, `memoUrl`, `readAt`, `createdAt`, `updatedAt`
- `objectives` map by uid
  - `uid`, `targetPapers`, `startDate`, `endDate`, `createdAt`
- `sessionUid`
  - current signed-in local user

## Important Limitation

This mode stores all data only in each browser's local storage.

- Different devices/browsers do **not** automatically share data.
- Clearing browser storage will erase data.
- To support real multi-user shared data across devices, a backend (Firebase/Supabase/custom API) is required.
