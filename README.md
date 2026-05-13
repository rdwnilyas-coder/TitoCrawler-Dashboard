# Tito Karnavian News Dashboard

Single-file interactive dashboard for the TitoCrawler dataset (3,750 articles from
21 Indonesian news portals, covering 2024-10-20 to 2026-05-12).

## Quick access

**Live URL** (GitHub Pages): https://<username>.github.io/TitoCrawler-Dashboard/

**Local**: Just double-click `index.html` — no server needed, all data embedded.

## Features

3 tabs, mobile-friendly:

1. **Overview** — KPI strip, Group A vs Group B donut split, monthly trend line
   chart (Group A · Group B · Combined), GitHub-style calendar heatmap of article
   density per day (569 days), top 10 portals bar chart.
2. **Reporters & Tags** — Top 20 reporters (bar chart, click to filter), top 30
   tags (bar chart, click to filter).
3. **Articles** — Full article search/filter/explore. Filters: search box (title
   + description), Group A/B, portal multi-select, date range, reporter. Click
   row → open article URL in new tab. Paginated 50/page.

## How it works

The HTML file is **self-contained** — all 3,745 article records plus
pre-aggregated stats are embedded as `<script type="application/json">` blocks.
No fetch, no CORS, no server required.

Chart library [ECharts 5](https://echarts.apache.org/) loaded from jsdelivr CDN
(~330 KB, cached by browser).

Total dashboard size: ~2 MB single HTML file.

## Update workflow

When new articles are crawled:

```bash
# In TitoCrawler (private) repo:
python analysis/code/build_dashboard.py
# This regenerates dashboard/index.html with fresh data.

# Then sync to public dashboard repo:
cp dashboard/index.html ../TitoCrawler-Dashboard/
cd ../TitoCrawler-Dashboard
git add index.html
git commit -m "data: refresh {N} articles"
git push
```

GitHub Pages auto-rebuilds in ~1 minute.

## Group definitions

- **Group A — POPULAR / mainstream (11 portals)**: Antara, Tempo, Liputan6, Kompas,
  Detik, tvOneNews, Tribunnews, CNBC Indonesia, Beritasatu, Pikiran Rakyat, Republika
- **Group B — ALTERNATIVE / niche (10 portals)**: Asatunews, IDN Times, Okezone,
  Babel Insight, Kumparan, Sindonews, Jawa Pos, Jakarta Post, Tagar.id, Aktual.com

Color codes: Group A = `#1f77b4` (biru), Group B = `#ff7f0e` (oranye).

## Source data not included

Article bodies (`isi_lengkap`) are NOT embedded — kept only the metadata.
Clicking a table row opens the original article URL at the publisher's website.
