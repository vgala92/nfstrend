# Auto-updating RBI NFS Dashboard — Setup (one time, ~10 minutes)

This gives you a **public web link** that refreshes itself every day at **4:00 PM IST**.
A free GitHub robot downloads the latest RBI data, rebuilds the dashboard, and republishes
it — no computer of yours needs to be switched on.

You only do this setup **once**. After that it runs forever on its own.

---

## What's in this folder

| File | What it does |
|------|--------------|
| `index.html` | The dashboard itself (this is what your team opens). |
| `build_dashboard.py` | The robot's script: download RBI file → rebuild dashboard. |
| `requirements.txt` | The tools the script needs. |
| `.github/workflows/update.yml` | The daily 4 PM IST schedule. |

Keep the folder structure exactly as-is (especially the `.github/workflows` folder).

---

## Step-by-step

**1. Create a free GitHub account** — go to <https://github.com> and sign up (skip if you have one).

**2. Create a new repository**
   - Click the **+** (top-right) → **New repository**.
   - Name it e.g. `rbi-nfs-dashboard`.
   - Choose **Public**.
   - Click **Create repository**.

**3. Upload these files**
   - On the new repo page click **uploading an existing file**.
   - Drag in **everything from this folder**, including the `.github` folder.
     (If drag-drop misses the `.github` folder, that's OK — see the note at the bottom.)
   - Click **Commit changes**.

**4. Turn on the public link (GitHub Pages)**
   - Go to the repo's **Settings** → **Pages** (left menu).
   - Under "Build and deployment", set **Source = Deploy from a branch**.
   - Branch: **main**, folder: **/ (root)**. Click **Save**.
   - After a minute, your link appears at the top, like:
     **`https://YOUR-USERNAME.github.io/rbi-nfs-dashboard/`**
   - Share that link with your team. It also works as a phone home-screen app.

**5. Test it now (optional but recommended)**
   - Go to the **Actions** tab → click **Update RBI NFS dashboard** → **Run workflow**.
   - Watch it run (a minute or two). A green tick means it worked and republished.

That's it. From now on it runs automatically every day at 4 PM IST.

---

## Good to know

- **When data appears:** RBI publishes each day's figures on the **next working day**, and
  there's **no new data on weekends/holidays**. On those days the job runs, finds nothing new,
  and simply makes no change — that's normal.
- **Your team always sees the latest:** when the link updates, anyone who reopens it is shown
  the new data automatically (with a small "Updated to latest published data" note).
- **You can still update manually** anytime using the dashboard's own
  **Update Data → Download shareable file** button, then re-upload `index.html` to the repo.

## If the robot can't download the RBI file

RBI's website has bot protection. The script tries a normal download first, then falls back to
a full headless browser (Playwright) that clears the challenge. This works in the large majority
of cases. If RBI ever blocks the cloud runner's address and a run fails on the download step:

- Re-run it (Actions tab → Run workflow) — challenges are often intermittent, or
- As a fallback, open the live dashboard, use **Update Data → Upload RBI File** with the file
  you download manually from
  <https://www.rbi.org.in/Scripts/FS_PaymentsData.aspx?fn=9> ("Daily Settlement Data on select
  payment systems"), then **Download shareable file** and re-upload `index.html` to the repo.

## Note on the `.github` folder

GitHub's drag-and-drop sometimes skips folders that start with a dot. If the **Actions** tab
shows no workflow after uploading, create the file manually:
1. In the repo, click **Add file → Create new file**.
2. Name it exactly: `.github/workflows/update.yml`
3. Paste the contents of the `update.yml` from this folder, then **Commit**.
