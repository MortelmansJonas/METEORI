# NU-WRF × AmeriFlux Dashboard

A tool to visually evaluate NU-WRF output against AmeriFlux observations. You point it at your WRF output and AmeriFlux data, run a single Python script, and get a self-contained HTML file you can open in any browser — no server needed, just double-click and go.

---

## Using the dashboard

### The map

The map shows all AmeriFlux stations across CONUS, coloured by IGBP land cover class. The legend is in the top-right corner of the map.

**To look at a station:** just click on it. The two panels on the right will populate with that station's time series and statistics. If no NU-WRF output is available during the observation period of the station, this will be clearly stated.

**To filter by state:** use the dropdown in the top-right of the page header. The map will zoom in to that state automatically. Switching back to "All USA" resets the view.

### The aggregated statistics

The bottom left panel shows the overal performance metrics (r, ubRMSD, and bias) over the selected state (or CONUS).

### The statistics panel

Once you click on a station, the top-right panel shows the per-site statistics. Three metrics are shown for each variable: 

- **r** — Pearson correlation.
- **ubRMSD** — unbiased RMSD.
- **bias** — mean(WRF − obs).

Where a station falls inside the d02 domain, you'll see d01 and d02 statistics side by side in blue and orange respectively.

At the top of the panel there's also a small **data availability bar** for each station. This shows the full AmeriFlux record (grey), the WRF evaluation window (blue), and valid LE observations within that window (green). This is useful for understanding why some stations show no statistics — either the record doesn't overlap your WRF window at all, or there just aren't enough good observations in that period.

### The time series panel

Once you click a station, the bottom-right panel shows the WRF output and AmeriFlux observations plotted over your evaluation window.

**Switching variables:** use the buttons along the top of the panel — Latent Heat, Sensible Heat, Air Temp 2m, SW Radiation.

**Toggling traces:** next to the variable buttons, there are three toggle buttons for `d01`, `d02`, and `AmeriFlux`. Click any of them to hide/show that trace. Useful if you want to compare just d01 vs observations without d02 cluttering the view.

**Zooming in:**
- **Scroll** to zoom in/out on the time axis
- **Click and drag** to box-zoom into a specific period
- **Double-click** to reset the zoom back to the full window
- The small toolbar that appears at the top-right of the chart when you hover also has zoom, pan, and reset buttons

---

## A few things to be aware of

- Sites in `EXCLUDE_SITES` (currently `US-Tw1`, `US-Myb`, `US-Sne`, `US-Var`) are dropped completely — known bad data.
- Stations outside the current NU-WRF study period still appear on the map but won't have any WRF data behind them.
- AmeriFlux observations with QC flag > 1 are masked out before computing any statistics.
- The HTML output embeds all the data as JSON, so it can get large (tens of MB) for a full CONUS run — just something to keep in mind if you're sharing this further.
