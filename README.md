# Chore Chart

Weekly chore tracker for Georgia and Isabella, with points, streaks, a reward shop and a shared team goal.
Built the same way as the Fitness Tracker.

- **App (this repo, public):** `index.html`, `manifest.json` and the `icon-cc-*.png` files, served by GitHub Pages.
- **Data (separate private repo):** a single `data.json`, written by the app through the GitHub API.
  This repo never holds any family data.

## How it works

- **Weeks run Sunday to Saturday.** The two daily jobs swap every Sunday:
  - Dishwasher every day + Bathroom on Saturday
  - Sweep the kitchen every day + Front stoop on Saturday
- **Saturday** both girls also do laundry: wash, dry, fold, put away.
- **The girls tap a job when it's done.** It turns amber ("waiting") until a parent OKs it in the Parent tab. Points only count once OK'd.
- **Daily jobs are due by 9:00 pm.** After that the girls can't tick today's jobs. A missed job just earns nothing and resets the streak.
- **Saturday jobs and laundry** score per step, plus a finish bonus when every step is OK'd.
- **Extras:** the girls pick from the extras menu, or type their own job and you set the points when you OK it.
- **Rewards:** hit the weekly target to win the weekly prize. Points also build up to spend in the Shop. Spending needs a parent OK.
- **Team goal:** both girls' points add up toward a shared family reward.
- **Streaks:** every 7 days in a row of daily jobs pays a streak bonus. A perfect week (all 7 daily jobs + Saturday job + laundry) pays a bonus too.
- **Parent mode** is behind a 4-digit PIN and locks itself after 10 minutes. In parent mode you can tick or untick any day's jobs, OK or decline, and change every setting: extras, rewards, points, job names, Saturday steps, rotation, team goal.

## Setup

1. Create a **private** repo named `chore-chart-data`, and tick "Add a README file" when you create it.
2. Create a fine-grained personal access token:
   GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.
   - Repository access: *Only select repositories* → `chore-chart-data`
   - Permissions → Repository permissions → **Contents: Read and write**
3. Enable GitHub Pages on this repo: Settings → Pages → Deploy from a branch → `main` / root.
4. Open the Pages URL on the iPad, tap **Parent**, create a PIN, then open **GitHub sync** and enter the username,
   `chore-chart-data` and the token. Add it to the Home Screen (Share → Add to Home Screen).
   Do the same on your phone if you want to OK chores from it.

## data.json shape

```json
{
  "version": 1,
  "logs": {
    "2026-10-10|georgia|daily": { "kind": "chore", "kid": "georgia", "k": "2026-10-10", "item": "daily",
                                  "name": "Empty the dishwasher", "pts": 10, "status": "ok", "at": 1791000000000 },
    "<id>": { "kind": "extra | custom | reward", "kid": "isabella", "k": "2026-10-10", "name": "...",
              "pts": 20, "status": "pending | ok | no", "at": 1791000000000 }
  },
  "settings": { "...": "kids, rotation, points, extras, rewards, team goal, PIN hash" }
}
```

Each save is a commit, so the repo history doubles as a full backup.
