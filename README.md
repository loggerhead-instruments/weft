# Weft

Desktop app for bioacoustic and spatiotemporal data analysis. Train acoustic classifiers, analyze millions of detections with maps and charts, and create publication-ready reports. Local-first — your data stays on your machine.

**Weft** is built around three workspaces:

- **Warp** — Audio labeling, model training, and batch processing for bioacoustic classification
- **Weft** — Data analysis and visualization for acoustic monitoring and environmental data *(coming soon)*
- **Weave** — Reports, posters, and interactive data stories *(coming later)*

## Download

| Platform | Download |
|----------|----------|
| macOS (Apple Silicon) | [Latest .dmg](https://github.com/loggerhead-instruments/weft/releases/latest) |
| Windows | [Latest .exe](https://github.com/loggerhead-instruments/weft/releases/latest) |

> **Note:** macOS builds require an Apple Silicon Mac (M1/M2/M3/M4/M5). Intel Macs are not supported.

## System Requirements

- macOS 11+ (Apple Silicon only) or Windows 10+
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
- Import CSV, Parquet, NDJSON, JSON, and DuckDB files
- Interactive map view with dots, heatmap, and hexbin layers
- Timeline, category, numeric distribution, and day-hour heatmap charts
- Data table with virtual scrolling
- Environmental data enrichment (weather, air quality, elevation)
- AI-powered analysis advisor with natural language queries
- Aggregation by any numeric column with SUM, AVG, MAX, MIN
- Year-over-year comparison mode
- Six colorblind-safe palettes with per-category color customization
- Dark/light chart themes for print-ready output

### Weave Workspace *(coming soon)*
- Reports, posters, and interactive data stories from your analysis


# Weft Analysis Guide

Weft is the analysis workspace for spatiotemporal data. Import detection CSVs from Warp (or any tabular data with coordinates and timestamps), visualize on interactive maps and charts, enrich with environmental data, and explore with the AI Advisor.

## Getting Started

### Creating a Project

1. Go to the **Projects** tab
2. Click **New Project**, give it a name and choose a location
3. The project creates a local DuckDB database to store your data

### Importing Data

Go to the **Data** tab and click **Import**. Supported formats:

- **CSV** — Comma-separated values (most common for Warp processing output)
- **Parquet** — Columnar binary format (fast, compact)
- **JSON / NDJSON** — Newline-delimited JSON records
- **DuckDB** — Import tables from another DuckDB database

### Column Mapping

After import, map your columns in the sidebar so Weft knows how to interpret your data:

| Column | Purpose |
|--------|---------|
| **Datetime** | Timestamp column — enables timeline charts, time-based aggregation |
| **Category** | Grouping column — species, call type, etc. |
| **Latitude / Longitude** | Enables map view and environmental enrichment |
| **Numeric columns** | Any numeric field available for aggregation (confidence, count, etc.) |

---

## Map View

The map shows your data geographically. Requires latitude and longitude columns to be mapped.

### Display Modes

| Mode | Description |
|------|-------------|
| **Dots** | Individual points at each location, sized by count or aggregated variable |
| **Heatmap** | Continuous density surface |
| **Hexbin** | Hexagonal grid aggregation |

### Map Styles

Six base map styles: Dark Matter, Light, Streets, Satellite, Ocean, and Terrain.

### Location Selection

Click individual points to select locations, or use box selection (Shift+drag) to select a region. Selected locations filter the charts and table views.

### Color Palettes

Six colorblind-safe palettes: Okabe-Ito, Wong, Tol Bright, Tol Muted, Set 2, Paired. You can also customize colors per category by clicking the color chip next to each category name.

---

## Charts View

### Available Charts

| Chart | Description |
|-------|-------------|
| **Summary Metrics** | Quick statistics — total detections, rate, date range |
| **Timeline** | Activity over time, binned by your chosen time interval |
| **Category Breakdown** | Distribution across categories |
| **Numeric Distributions** | Histograms for numeric columns |
| **Day x Hour Heatmap** | Activity patterns by day of week and hour of day |

### Chart Controls

- Toggle chart visibility in the sidebar
- Click a chart title to expand it full-screen (Esc to exit)
- Drag the bottom edge to resize height
- Switch between bar, line, and dot chart types
- Toggle dark/light theme for print-friendly charts

### Year-over-Year Mode

Enable in the sidebar to overlay years. Each year becomes a separate trace, aligned by day of year. Useful for comparing seasonal patterns across years. When YoY is active, time bins smaller than one day are disabled.

---

## Aggregation Pipeline

Weft uses a **two-stage aggregation pipeline** to efficiently summarize large datasets for the map, timeline, and other visualizations.

### Stage 1: Backend SQL Aggregation

The backend groups your raw data by **(latitude, longitude, time_bin, category)** and applies the selected aggregation function. For example, if you have 10,000 raw detections at a location over a week, a "Week" time bin with "SUM(detectionCount)" produces one row per location per week with the summed value.

```sql
-- Simplified example
SELECT lat, lon, time_bucket('7 day', datetime) AS time_bin,
       category, SUM(detectionCount) AS detectionCount_sum
FROM detections
GROUP BY lat, lon, time_bin, category
```

Each location gets back a record with:
- `count` — number of raw rows in the group
- `numerics` — a map of `{column}_{agg}` keys (e.g. `detectionCount_sum`, `confidence_avg`)

### Stage 2: Frontend Cross-Location Summing

The timeline and category charts **sum the pre-aggregated values across all locations** for each time bin. This collapses the spatial dimension so you see a single time series.

**Example:** 3 locations, weekly bins, SUM(detectionCount)

| Location | Week 1 | Week 2 |
|----------|--------|--------|
| A | 45 | 52 |
| B | 30 | 28 |
| C | 25 | 31 |
| **Timeline** | **100** | **111** |

### Aggregation Variable

By default, the map and charts use **Count** (number of rows). You can switch to any numeric column in the sidebar under **Variable**:

| Function | Description | Example |
|----------|-------------|---------|
| **Count** | Number of rows per group (default) | 150 detections this week |
| **Sum** | Total of the numeric column | Total detectionCount = 847 |
| **Average** | Mean of the numeric column per location | Avg confidence = 0.82 |
| **Maximum** | Highest value in the group | Peak confidence = 0.99 |
| **Minimum** | Lowest value in the group | Min confidence = 0.51 |

### Time Bin Size

The time bin controls the resolution of the timeline and heatmap:

| Bin | Best For |
|-----|----------|
| **Hour / 6 Hours** | Short-duration datasets with fine detail |
| **Day** | Default — good balance of detail and readability |
| **Week / Month** | Smooths out noise, reveals long-term trends |
| **Custom** | Specify any number of hours (1–720) |

### Threshold Filter

After aggregation, you can filter by the aggregated value. For example, set a minimum of 5 to hide locations with fewer than 5 detections per time bin. This filters both map points and chart data.

### Day x Hour Heatmap Aggregation

The heatmap uses a separate SQL query that groups by day-of-week and hour-of-day directly from the raw table. When a numeric aggregation variable is selected, the heatmap applies that function (e.g., `SUM(detectionCount)`) instead of `COUNT(*)`.

> **Note on Average aggregation:** When using Average, the timeline sums per-location averages across locations. This is a sum-of-averages, not a true global average. For a single location it is exact, but across multiple locations with different row counts, it weights each location equally regardless of sample size.

---

## Filters

Filters in the left sidebar constrain which data is displayed across all views (map, charts, table).

| Filter | Description |
|--------|-------------|
| **Category** | Check/uncheck categories. Use the search box to find specific categories |
| **Date Range** | Set From and To dates to focus on a specific time period |
| **Numeric Range** | Set min/max bounds on any numeric column (e.g., confidence >= 0.8) |

Numeric range filters are applied to raw data **before** aggregation. The threshold filter is applied **after** aggregation.

### Large Dataset Mode

For tables with more than 100 million rows, filters are not applied automatically. Instead, adjust your filters and click **Update** to re-query. This prevents accidental long-running queries.

---

## Environment Tab

The Environment tab shows relationships between your detection data and environmental variables. Requires latitude, longitude, and datetime columns.

### Astronomical Charts

Always available when coordinates and timestamps are mapped:

- **Activity Relative to Sunrise** — Detection timing relative to sunrise/sunset
- **Activity by Moon Phase** — Detection counts across lunar phases
- **Nocturnal by Moon Phase** — Same as above, filtered to nighttime only

### Weather & Air Quality

Available after computing weather enrichment on the Data tab. Select variables from the picker to add timeline and correlation charts for temperature, precipitation, wind speed, air quality, and more.

### Elevation

Available after computing elevation enrichment. Shows elevation distribution and detection-vs-elevation correlation charts.

---

## Data Enrichment

On the **Data** tab, the Enrich section lets you add environmental context to your data. Each enrichment source creates a new table that is joined to your detection data for analysis.

### Available Sources

| Source | Type | What It Adds |
|--------|------|-------------|
| **Weather** | Daily, per location | Temperature, precipitation, humidity, wind, cloud cover, pressure, solar radiation |
| **Air Quality** | Daily, per location | AQI (US/EU), PM2.5, PM10, O3, NO2, SO2, CO (bundled with weather) |
| **Elevation** | Static, per location | Elevation in meters (90m SRTM data, computed locally) |

### How Enrichment Works

1. Click **Compute** on an enrichment card
2. Weft extracts the unique locations and date range from your data
3. Data is fetched (from API or local library) and stored as a new table
4. Progress is shown in real-time with a cancel button
5. Once computed, environment charts and advisor access become available

Enrichment tables are named with a prefix (e.g., `_weather_detections`, `_elevation_detections`) and are visible in the Data tab.

---

## AI Advisor

The AI Advisor lets you ask natural-language questions about your dataset. It can write and execute SQL queries, create charts, run Python analysis, and save results as new tables.

### What You Can Ask

- Summarize my data — counts, date ranges, top categories
- Compare detection rates between locations or time periods
- Create charts — bar, line, scatter, histogram, heatmap
- Run statistical tests — correlations, trends, seasonality
- Cross-reference with enrichment data (weather, elevation)
- Save query results as new tables for further analysis

### Artifact Cards

Advisor results are shown as interactive artifact cards:

- **Table cards** — Query results with copy SQL, download CSV, collapsible SQL view
- **Chart cards** — Interactive Plotly charts with CSV data download, PNG export, dark/light theme
- **Code cards** — Python code with copy, download as .py file, stdout and result display

### Tips

- Be specific — "Show monthly detection counts by species for 2024" works better than "analyze my data"
- The advisor sees your table schema, enrichment tables, and column types
- Use the theme toggle (sun/moon icon) to switch advisor charts between dark and light themes
- Saved tables appear in the Data tab and can be used in future queries

---

## Combining Data

On the Data tab, use **Combine** to merge multiple tables:

- **Union** — Stack tables with matching columns (e.g., combine detection CSVs from multiple deployments)
- **Join** — Link tables on shared key columns (e.g., add metadata to detections)

Combined data is created as a view. The original tables remain unchanged.

---

# Warp Quick Start Guide

Warp is the training workspace in Weft. It turns audio recordings into trained neural networks that can automatically classify sounds — bird calls, whale vocalizations, bat echolocation, or any acoustic signal.

## Choose Your Starting Point

- **[I have unlabeled audio](#1-labeling-audio)** — Start here to sort your recordings into categories
- **[I have labeled audio](#2-training-a-model)** — Jump straight to training a classifier
- **[I have a trained model](#3-processing-audio)** — Run batch classification on new recordings

---

## 1. Labeling Audio

Create a **Sorting Project** to organize your audio files into categories (species, call types, noise, etc.).

### Setup

There are two ways to start a sorting project:

**Option A: Start from raw audio**
1. Click **New Sorting Project** and give it a name
2. Point it at your folder of audio files
3. Add categories from the standardized list (e.g., `Megaptera novaeangliae`, `SYS_anthropogenic`, `SYS_unknown`)
4. Sort files one by one using the sorting interface

**Option B: Import pre-sorted audio**
1. Click **New Sorting Project** and give it a name
2. Point it at a folder where audio files are already organized into subfolders named by category
3. Warp imports the folder structure — subfolder names are automatically mapped to standardized GBIF and system category names

### Category Names

Category names are standardized using **GBIF (Global Biodiversity Information Facility)** identifiers. This ensures that models and detections can be shared consistently across projects and researchers.

- **Species categories** use scientific names (e.g., `Megaptera novaeangliae` for humpback whale)
- **System categories** use a `SYS_` prefix (e.g., `SYS_anthropogenic` for boat noise and other human-made sounds)

Arbitrary category names are not supported. If you need a category that isn't available, please [submit a feature request](https://github.com/loggerhead-instruments/weft/issues/new?template=feature_request.md).

### Sorting Interface

Each file loads with a spectrogram display and audio playback:

- **Play** the audio (Space bar)
- **Assign** to a category by clicking the category button or pressing **1–9** for quick assignment
- **Skip** with the right arrow key (→) if you're unsure
- **Go back** with the left arrow key (←) to revisit the previous file
- **Undo** with Cmd+Z if you make a mistake

### Chunking Long Files

If your recordings are long (minutes to hours), enable **chunking** to split them into shorter segments:

- Set a **chunk duration** (e.g., 3 seconds) that's long enough to see your signal of interest
- Warp will step through the file chunk by chunk
- Each chunk you label gets saved as its own WAV file in the category folder

### Spectrogram Display Settings

Adjust the spectrogram view to see your signals clearly:

- **Frequency range** (freq_min / freq_max): Zoom into the frequency band where your species vocalizes
- **FFT points**: Higher values = better frequency detail
- **Colormap**: Choose a color scheme that makes your signals stand out (inferno, viridis, grayscale)
- **Brightness** (vmin / vmax): Adjust contrast to highlight faint calls

These display settings are independent of the training spectrogram settings.

### Reviewing Your Labels

Switch to **Library** mode to review what you've sorted:

- Filter by category to check consistency
- Play back files to verify they're in the right category
- Move misclassified files to the correct category
- Delete bad recordings

---

## 2. Training a Model

Create a **Training Project** to build a neural network from your labeled audio.

### Setup

1. Click **New Training Project**
2. **Add a data source** — link to your sorting project(s) containing labeled audio
3. Select which categories to include in training

### Spectrogram Settings

These control how audio is converted to images for the neural network. The defaults work well for most bioacoustic applications:

| Setting | Default | What It Does |
|---------|---------|-------------|
| **n_fft** | 1024 | FFT window size. Higher = better frequency detail, coarser time detail |
| **hop_length** | 280 | Gap between FFT frames. Lower = better time resolution |
| **freq_min** | 100 Hz | Low frequency cutoff. Set above your noise floor |
| **freq_max** | 10,000 Hz | High frequency cutoff. Set just above your highest signal |
| **freq_bins** | 128 | Vertical resolution of the spectrogram image |
| **time_frames** | 256 | Horizontal resolution of the spectrogram image |

**Tip:** Preview a spectrogram before training to make sure your signal is visible and fills a reasonable portion of the image.

### Training Settings

All models use **EfficientNet-B0**, a proven architecture for image classification. The defaults are a good starting point:

| Setting | Default | What It Does |
|---------|---------|-------------|
| **Epochs** | 50 | Number of passes through the training data. More epochs = more learning time, but diminishing returns after the model converges |
| **Batch Size** | 32 | Samples processed at once. Reduce to 16 if you run low on memory |
| **Learning Rate** | 0.0002 | How aggressively the model updates. Too high = unstable, too low = slow. The default is well-tuned |
| **Min Specs per Class** | 10 | Categories with fewer samples are excluded from training |
| **Max Files per Class** | 0 (unlimited) | Cap samples per category. Useful if one category vastly outnumbers others |
| **Augment** | On | Randomly varies spectrograms during training to improve generalization |
| **Balance Method** | Weighted Loss | How to handle unequal category sizes. Weighted loss penalizes errors on rare categories more heavily |

### Start Training

Click **Train** and watch the live progress:

- **Training accuracy**: How well the model fits the training data
- **Validation accuracy**: How well it generalizes to unseen data (this is what matters)
- **Loss curves**: Should trend downward; if validation loss starts rising while training loss drops, the model is overfitting

Training auto-saves a checkpoint at each epoch. You can stop early and keep the best model.

### Reading the Confusion Matrix

After training, the confusion matrix shows you exactly where the model succeeds and struggles:

- **Diagonal cells** = correct predictions (you want these to be high)
- **Off-diagonal cells** = mistakes (the model confused one category for another)
- Click on any cell to see the actual files — listen to them and decide if the model is wrong or if the file was mislabeled

---

## 3. Processing Audio

Create a **Processing Project** to run a trained model on new, unlabeled recordings.

### Setup

1. Click **New Processing Project**
2. **Select a model** from one of your training projects
3. **Select the input folder** containing audio files to classify

### Processing Settings

| Setting | Default | What It Does |
|---------|---------|-------------|
| **Chunk duration** | 3.0 s | Length of each audio segment analyzed. Should match your training clip length |
| **Step size** | 50% | Overlap between chunks. 50% means each moment of audio is analyzed twice |
| **Min confidence** | 50% | Only export detections above this confidence threshold |
| **Save chunks** | Off | Optionally save WAV clips of detected sounds |
| **Consecutive detections** | 1 | Require N chunks in a row with the same label before reporting a detection |

### Consecutive Detections

When processing with overlapping chunks, you can require multiple consecutive chunks to predict the same label before reporting a detection. This reduces false positives by confirming that a signal persists across overlapping windows.

**How it works:** After classification, chunks are grouped by file and sorted by position. The system finds runs of consecutive chunks with the same predicted label. A run of length L with threshold N produces floor(L/N) detections — one every N chunks. Runs shorter than N are discarded entirely.

**Example — 50% overlap, consecutive = 2:**
```
Chunks:  [whale] [whale] [whale] [whale] [noise]
Result:  2 detections (whale run of 4 → floor(4/2) = 2, at chunks 1 and 3)
         The lone [noise] is discarded.
```

**Example — 50% overlap, consecutive = 2:**
```
Chunks:  [whale] [whale] [noise] [whale] [noise]
Result:  1 detection (whale run of 2 → floor(2/2) = 1)
         The lone [whale] at chunk 4 is discarded — only 1 in a row.
```

**Example — consecutive = 1 (default):**
```
Chunks:  [whale] [noise] [whale] [whale] [noise]
Result:  5 detections (every chunk reported as-is, no filtering)
```

### Output

Processing produces a **CSV file** with one row per detection:

- Timestamp and file path
- Detected species/category
- Confidence score (0–100%)
- Duration and offset within the source file

This CSV follows the observation schema used by Weft's analysis workspace — you can import it directly for mapping, charting, and statistical analysis.

---

## Tips for Building a Successful Classifier

### Label Quality Matters More Than Quantity

- **Be consistent**: If you're unsure about a file, skip it rather than guessing. A few mislabeled files are OK — you'll catch them during training.
- **Include background noise**: Always include normal background sounds in your training set. The model needs to learn what is NOT a signal.
- **Use the confusion matrix**: After training, review the files the model got wrong. You'll often discover target signals hiding in your background category that can be moved to the correct label. Fix and retrain.

### Get Enough Labels

- **Aim for at least 100 samples per category.** More is better, but 100 is a practical minimum for reliable training.
- **10 samples** is the absolute floor (set by min_specs_per_class). The model will train but won't generalize well.
- **Imbalanced categories are OK** — the weighted loss function handles this. But try to avoid extreme ratios (1000:10).

### Choose the Right Clip Duration

- **The clip should be long enough to show your complete signal.** A 3-second clip works for most bird calls. Whale songs may need 10–30 seconds. Bat echolocation may only need 0.5 seconds.
- **The clip should be short enough that the signal fills a meaningful portion of the spectrogram.** A 0.1-second bird chirp in a 30-second spectrogram will be invisible to the model.
- **Match your processing chunk duration to your training clip duration.**

### Set Your Frequency Range

- **Narrow the frequency range** to focus on your signal. If your bird calls are between 2,000–8,000 Hz, set freq_min=1500 and freq_max=9000. This removes irrelevant noise and gives the model a clearer picture.
- **Leave a small margin** above and below your signal's frequency range.

### Iterate: Train, Process, Relabel, Retrain

The most effective workflow is iterative:

1. **Label a small set** (100–200 files per category)
2. **Train a model** — it won't be perfect, but it'll be useful
3. **Process unlabeled recordings** with this model
4. **Review the results** — the model will find examples you missed, and its mistakes reveal what it needs more training on
5. **Add the good detections to your training set** and fix the bad ones
6. **Retrain** with the expanded dataset

Each cycle produces a better model. Two or three iterations usually get you to a production-quality classifier.

### Use Noise Categories

- **Always include a noise or background category** (e.g., `SYS_anthropogenic`, `SYS_unknown`). The model needs to learn what is NOT a signal.
- **Include common confusers**: similar species, weather noise, etc. Give each its own category so the model can distinguish them.

### When Training Stalls

- **Validation accuracy plateaus below 80%**: You likely need more data, cleaner labels, or better frequency range settings. Check the confusion matrix — the problem categories will be obvious.
- **Validation loss increases while training loss drops**: The model is overfitting. Try reducing epochs, increasing augmentation, or adding more training data.
- **Training is very slow**: Reduce batch size if running low on memory. Training time is proportional to the number of samples and epochs.

---

## Project Storage & Deletion

### Where Projects Are Saved

All projects are saved in your home folder under `WeftProjects` by default:

- **macOS:** `~/WeftProjects/`
- **Windows:** `C:\Users\<username>\WeftProjects\`

Organized by type:

- `WeftProjects/sorting/` — Sorting projects
- `WeftProjects/training/` — Training projects
- `WeftProjects/processing/` — Processing projects
- `WeftProjects/weft/` — Weft analysis projects

### Deleting Projects

Deleting a project is a **soft delete** — it removes the project from the app but leaves all files on disk. To free up disk space, you need to manually delete the project folder from `~/WeftProjects`.

There is no way to undelete a project in the app. However, since the files remain on disk, you can import them into a new project if a project was accidentally deleted.

---

## Project Relationships

```
Sorting Project(s)  →  Training Project  →  Processing Project
   (labeled audio)      (trained model)      (batch classification)
```

- One training project can pull from multiple sorting projects
- One trained model can be used in multiple processing projects
- Processing output (CSV) can be imported into Weft for analysis

---

## Feedback & Support

- [Report a Bug](https://github.com/loggerhead-instruments/weft/issues/new?template=bug_report.md)
- [Request a Feature](https://github.com/loggerhead-instruments/weft/issues/new?template=feature_request.md)

---

© 2026 Loggerhead Instruments
