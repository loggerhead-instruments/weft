# Weft

Desktop app for bioacoustic and spatiotemporal data analysis. Train acoustic classifiers, analyze millions of detections with maps and charts, and create publication-ready reports. Local-first — your data stays on your machine.

**Weft** is built around three workspaces:

- **Warp** — Audio labeling, model training, and batch processing for bioacoustic classification
- **Weft** — Data analysis and visualization for acoustic monitoring and environmental data *(coming soon)*
- **Weave** — Reports, posters, and interactive data stories *(coming later)*

## Download

| Platform | Download | Status |
|----------|----------|--------|
| macOS | [Latest .dmg](https://github.com/loggerhead-instruments/weft/releases/latest) | Tested |
| Windows | [Latest .msi](https://github.com/loggerhead-instruments/weft/releases/latest) | Experimental |

## System Requirements

- macOS 11+ or Windows 10+
- [Anaconda](https://www.anaconda.com/download) (free)
- 16 GB RAM minimum, 32 GB recommended
- 4 GB disk space (including Python environment)

## Installation

1. **Install Anaconda** — download the graphical installer from [anaconda.com/download](https://www.anaconda.com/download) and follow the setup wizard. If you already have Anaconda or Miniconda installed, skip this step.

2. **Install Weft** — download the installer for your platform from the link above.
   - **macOS**: Open the `.dmg` and drag Weft to your Applications folder.
   - **Windows**: Run the `.msi` installer.

3. **First launch** — Weft will detect your Anaconda installation and set up a Python environment automatically. This takes 5-10 minutes and only happens once. You'll see a progress screen — don't close the app during setup. Sign up for Weft using your email. 

4. **Subsequent launches** — the app starts in a few seconds.

## What's Included (Free Beta)

### Warp Workspace
- Create sorting, training, and processing projects
- Label audio with spectrogram viewer and playback
- Train PyTorch classifiers with live training charts
- Batch-process audio files and export detection CSVs
- GBIF-standardized species labels

### Weft Workspace
- Import CSV, NDJSON, JSON, and DuckDB files
- Interactive map view with point and heatmap layers
- Data table with virtual scrolling
- Metrics banner (detection count, rate, date range)
- Filter by category, confidence, and date range

### Coming Soon
- Charts and statistical analysis
- AI-powered analysis advisor
- Weave workspace for reports and data stories

## Updates

You can also check manually via **Settings > Check for Updates**. Updates install in-place — your projects and data are never affected.

## Your Data

All data stays on your machine in `~/WeftProjects/`. Weft does not upload your project data to any server. Anonymous usage telemetry (app launches, feature usage) is collected to improve the product — no personal data or project data is included.

## Feedback
- [Report a bug](https://github.com/loggerhead-instruments/weft/issues/new?template=bug_report.md)
- [Request a feature](https://github.com/loggerhead-instruments/weft/issues/new?template=feature_request.md)

## License

Copyright 2026 Loggerhead Instruments. All rights reserved.
