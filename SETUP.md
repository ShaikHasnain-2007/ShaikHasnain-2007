# Setup & Deployment Guide for Shaik Hasnain's GitHub Profile

This repository is named **`ShaikHasnain-2007`**, matching your GitHub username (`github.com/ShaikHasnain-2007/ShaikHasnain-2007`). That magic repo's `README.md` is what automatically displays on your GitHub profile overview.

---

## 1. Local Preview & Tuning

You can open `preview.html` in your browser at any time to preview your generated SVGs (portrait, skill radar, language radar, and project cards) across both GitHub Dark and Light themes.

### Re-tuning your Dot-Matrix Portrait (Optional):
```powershell
# Default Color Reveal scan (current):
python scripts\dotify.py assets\avatar.png -o assets\portrait --cols 100 --equalize --detail 0.5 --color --reveal

# Green monochrome terminal look:
python scripts\dotify.py assets\avatar.png -o assets\portrait --cols 88 --equalize --detail 0.5 --animate

# Binary (0s and 1s matrix look):
python scripts\dotify.py assets\avatar.png -o assets\portrait --mode binary --cols 62 --equalize --detail 0.5
```

### Refreshing Skill Radar:
Edit `assets/skills.json` and run:
```powershell
python scripts\radar.py --data assets\skills.json -o assets\radar
```

---

## 2. Push to GitHub

1. Create a **New Repository** on GitHub named exactly **`ShaikHasnain-2007`**.
2. Make sure the repository is **Public** (required for GitHub profile READMEs and image rendering).
3. Push this directory to GitHub:

```bash
git init
git branch -M main
git add .
git commit -m "feat: initial profile readme and automated visual cards"
git remote add origin https://github.com/ShaikHasnain-2007/ShaikHasnain-2007.git
git push -u origin main
```

---

## 3. Enable GitHub Actions Workflow Permissions

To allow the automated workflows to refresh your charts, repo cards, and snake contribution animation:

1. In your GitHub repo, go to **Settings** → **Actions** → **General**.
2. Scroll down to **Workflow permissions**.
3. Select **Read and write permissions**.
4. Click **Save**.

---

## 4. Add `METRICS_TOKEN` (for 3D Isometric Calendar & Stats)

`lowlighter/metrics` needs a GitHub Personal Access Token (PAT) to read profile data and contributions:

1. Go to [https://github.com/settings/tokens](https://github.com/settings/tokens) → **Generate new token (classic)**.
2. Note: `ShaikHasnain-Profile-Metrics`
3. Scopes to check:
   - **`read:user`**
   - **`repo`** (optional, if you want private repository contributions counted)
4. Click **Generate token** and copy the token string (`ghp_...`).
5. Go to your repo: **Settings** → **Secrets and variables** → **Actions** → **New repository secret**.
6. Name: **`METRICS_TOKEN`**
7. Value: *(paste your generated token)* → Click **Add secret**.

---

## 5. Run the Workflows for the First Time

Go to your repository's **Actions** tab on GitHub:

1. Click on **Metrics** → click **Run workflow** → **Run workflow**. (Generates `assets/metrics.isocalendar.svg`, `assets/metrics.languages.svg`, and `assets/metrics.achievements.svg`).
2. Click on **Snake** → click **Run workflow** → **Run workflow**. (Generates snake animations onto the orphan `output` branch).
3. Click on **Charts and cards** → click **Run workflow** → **Run workflow**. (Refreshes your repo cards and language radar automatically).

> **Note:** The snake image URL references the `output` branch via `raw.githubusercontent.com`. It will appear as soon as the Snake workflow finishes its first run.
