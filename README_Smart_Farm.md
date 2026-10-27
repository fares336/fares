# Smart Farm: Code Explanation and Publishing Guide

**Authors:** Fares Hazem Moheb and Mostafa M. El-Shenawy

## 1. What the project is
A single-file web app (`smartfarm.html`) for farm decision support: soil zones, crop suitability, irrigation, fertilizer records, costs/profit, harvest calendar and backups. It uses plain HTML, CSS and JavaScript only. There is no server and no external library.

## 2. File structure (inside smartfarm.html)
1. **`<style>`**: colors are CSS variables (`--pr`, `--g`, `--y`, `--r`) with a dark-mode set. Layout uses CSS grid. Arabic right-to-left is handled by setting `dir="rtl"` on `<html>`.
2. **`CR`**: the crop database (20 crops, English and Arabic names, pH range, EC threshold, temperature range, water need, duration, yield range). These are approximate generic values. Verify them with local agricultural sources before real use.
3. **`L`**: Arabic translations. `t(key)` returns the Arabic text if the language is Arabic, otherwise the key itself.
4. **`S`**: the whole app state (zones, irrigation log, fertilizer log, finance inputs, weather, water EC). `save()` writes it to `localStorage`.
5. **Helpers**: `n()` converts input to a number or `null`, `f()` formats numbers (missing shows "—"), `dv()` is a safe division (no division by zero).
6. **`st(z)`**: zone status. Grey if pH, EC or moisture is missing; red for a significant issue; yellow for attention; green only when data is complete and no issue is found.
7. **`sc(z,c)`**: suitability score for a zone and a crop, based on pH, EC and temperature only. It lists missing factors and gives no score without pH and EC.
8. **`fin(o)`**: finance formulas (total cost, expected/actual revenue, net profit, margin, cost per kg).
9. **`V`**: one render function per tab (Dashboard, Map, Crops, Best Crop, Irrigation, Fertilizer, Finance, Records, Weather, Calendar, Backup). `render()` redraws the current tab and keeps your data when the language changes.

## 3. New features added in this version
- **Names** of the authors under the title.
- **Irrigation water quality:** enter your water EC. Each zone gets a check against its crop threshold and a rough leaching estimate (formula ECw / (5·ECe − ECw)). Confirm with an agronomist.
- **Crop rotation warning:** "Previous crop" field per zone; warns if it equals the current crop.
- **Harvest calendar:** estimated harvest = planting date + crop duration, with a labor-peak flag when 10 or more zones fall in the same week.
- **Backup and restore:** export all data as JSON and import it later (it asks before replacing data).
- **Bulk entry:** apply the same pH, EC or moisture to a range of zones.
- **Sanity check:** asks for confirmation if moisture changes by more than 40 points between readings.

## 4. Known limits
Data is stored only in the browser (no accounts, no sync). Weather is entered manually. There are no sensor connections, no irrigation volume estimates, no NPK recommendations and no PDF export yet.

## 5. How to publish
**Option A: Netlify Drop (easiest, free):** go to app.netlify.com/drop and drag `smartfarm.html` in. Rename the file to `index.html` first. You get a public link.

**Option B: GitHub Pages (free):**
1. Create a GitHub repository and upload the file as `index.html`.
2. Open Settings, then Pages, choose the `main` branch and the root folder, and save.
3. After a minute your site is at `https://<username>.github.io/<repo>/`.

**Option C: Share the Claude link:** open the published artifact in Claude and use its Share option.

You can also open `smartfarm.html` directly in any browser to use it locally.

## 6. How to change things
- Add or edit crops: edit the `CR` text block (one crop per line, fields separated by `|`).
- Add Arabic words: add entries in the `L.ar` object.
- Change colors: edit the variables at the top of `<style>`.
