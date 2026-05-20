# Kuwait Exchange Network — Heatmap

Interactive heatmap of **BEC**, **Al Muzaini**, **Al Mulla** and **Al Ansari** exchange branches and kiosks across Kuwait. Built on Leaflet.js with a dark CartoDB basemap.

---

## 🗺️ Live Demo

After deploying, your map will be live at:
```
https://<your-username>.github.io/<repo-name>/
```

---

## ✏️ How to Add / Edit / Delete Branches

All location data lives in **`branches.xlsx`** — the Branches sheet.

### Adding a new branch
1. Open `branches.xlsx`
2. Add a new row at the bottom of the **Branches** sheet
3. Fill in every column:

| Column | Example | Notes |
|--------|---------|-------|
| Company | `BEC` | Must be exactly: `BEC`, `Al Muzaini`, `Al Mulla`, or `Al Ansari` |
| Branch Name | `New Salmiya Branch` | Any descriptive name |
| Area | `Salmiya` | Neighbourhood / area |
| Governorate | `Hawally` | `Asima`, `Hawally`, `Farwaniya`, `Ahmadi`, `Jahra`, `Mubarak` |
| Type | `Branch` | `Branch` or `Kiosk` |
| Latitude | `29.3320` | Right-click in Google Maps → copy coordinates |
| Longitude | `48.0600` | Second number from Google Maps |
| Address | `Block 5, Salem St` | Street address |
| Phone | `2228 0000` | Optional |
| Hours | `8AM-9PM` | Optional |
| Active | `Yes` | Set `No` to hide without deleting |

4. Save the file
5. Commit and push to GitHub → the map auto-updates in ~1 minute

### Deleting a branch
- **Hide it**: Set `Active` column to `No` (keeps the data)
- **Remove it**: Delete the entire row

### Getting coordinates from Google Maps
1. Open [maps.google.com](https://maps.google.com)
2. Navigate to the branch location
3. Right-click on the exact spot
4. Click the coordinates shown at the top of the menu — they copy to your clipboard
5. First number = **Latitude**, second = **Longitude**

---

## 🚀 Setup on GitHub

### 1 — Create a new repository
```bash
git init
git remote add origin https://github.com/<your-username>/<repo-name>.git
```

### 2 — Push all files
```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```

### 3 — Enable GitHub Pages
1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `gh-pages` / folder: `/ (root)`
4. Click **Save**

> The first deployment happens automatically after the first push triggers the GitHub Action.

### 4 — Enable Actions permissions (first time only)
Go to **Settings → Actions → General** and set:
- **Workflow permissions** → Read and write permissions ✅

---

## 🖥️ Running Locally

```bash
# 1. Install dependencies
pip install openpyxl

# 2. Convert Excel to JSON
python convert.py

# 3. Serve locally (any of these work)
python -m http.server 8000
# or
npx serve .
# or open index.html directly in most browsers
```

Then visit `http://localhost:8000`

> **Note:** Opening `index.html` directly via `file://` will fail to load `branches.json` due to browser CORS restrictions. Use a local server instead.

---

## 📁 File Structure

```
├── branches.xlsx        ← EDIT THIS to add/remove locations
├── branches.json        ← Auto-generated (do not edit manually)
├── index.html           ← The heatmap application
├── convert.py           ← Excel → JSON converter
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml   ← Auto-build & deploy on push
```

---

## 🔧 Map Features

| Feature | Description |
|---------|-------------|
| 🗺️ Real map | Dark CartoDB basemap with Kuwait streets |
| 🔥 Heatmap | Colour-coded density per company or combined |
| 🔍 Zoom | Scroll or pinch to zoom, drag to pan |
| 🏷️ Area labels | 33 Kuwait neighbourhoods labelled on map |
| ⊞ Grid | Lat/lng reference gridlines (toggleable) |
| 💬 Hover tooltip | Branch name, type, area, address, phone, hours |
| 📌 Click popup | Pinned info card at branch location |
| 🔘 Filters | Toggle by company (BEC / Muzaini / Mulla / Ansari) |
| 🏢 Type filter | Show/hide Branches and Kiosks separately |
| 🌡️ Combined heat | Merge all companies into single heat layer |

---

## 🤝 Contributing

Pull requests welcome. To add a new exchange company:
1. Add the company name to `VALID_COMPANIES` in `convert.py`
2. Add a colour to `COLORS` in `index.html`
3. Add a chip style in `index.html` CSS
4. Add the toggle checkbox in the header
