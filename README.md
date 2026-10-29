# Weft (Free Beta)

Weft is a desktop app for passive acoustic monitoring, in air or underwater, for any sound source: birds, bats, insects, frogs, fish, marine mammals, or anthropogenic noise. Train classifiers on your own labeled recordings, run them over large audio datasets, plot detections on maps and charts alongside environmental data, and prepare figures, papers and posters from the results. All processing runs locally. Weft is in **free beta**: every feature is free while we work out the rough edges.

## Features

- **Custom classifiers for any signal.** Train a classifier on your own labeled clips (species, call types, noise sources) and apply it to the recordings from an entire deployment. Sample rates up to 400 kHz+ are supported, so ultrasonic recordings (bats, odontocetes) work too.
- **Pretrained bird models.** For bird recordings, BirdNET and HaikuNet are built in for identification with no training, and can give a **Second opinion** on any detection.
- **Soundscape metrics.** For any recording, with no model: RMS, peak, SEL, spectral entropy, ACI, kurtosis and 1/3-octave band levels, calibrated to dB re 1 µPa or dB re 20 µPa.
- **Spatial and temporal plots.** Plot detections on maps and charts by hour, day, season or year, and compare sites and years.
- **Environmental covariates.** Add weather, air quality, tides, ocean conditions, elevation, sunrise, sunset and moon phase for each site and date.
- **Data quality checks.** Flag and correct invalid coordinates, unset recorder clocks and future timestamps before analysis.
- **AI advisor.** Describe an analysis in plain English. The advisor proposes a method with verified references and builds it as an editable notebook in SQL, Python or R.
- **Figures and manuscripts.** Save charts, maps and spectrograms as figures, and assemble them into papers and posters.
- **Community models.** Publish a trained model to the Weft community library with its authors and a citation, so others can use it and cite it. Browse and download models published by other researchers and run them on your own recordings.
- **Edge deployment.** Export models to ONNX or TFLite (INT8) to run on low-power recorders.
- **Local data.** Recordings, models and results stay on your computer.

## How your work is organised

Your work is organised into **projects**. A project is whatever you are working on — a survey, a site, a species, a field season. Home lists all your projects.

The bar across the top of the app has two groups:

```
Libraries   Models   │   Process   Data   Analyses   Documents
  shared across      │   inside the project you have open
  all projects       │
```

**Shared across all projects:**

- **Libraries** — example recordings you have sorted into categories (species, call types, noise). This is what models learn from.
- **Models** — classifiers trained on one or more libraries.

Libraries and models are shared, so a model you trained for one project can be used in any other. Each one remembers which project it was made in.

**Inside a project:**

- **Process** — your recordings, grouped by **deployment** (a place or recorder) and the **runs** you have done on them. A run finds sounds with a model (your own, a community model, BirdNET or HaikuNet), or measures sound levels with no model at all.
- **Data** — the project's tables: detections from your runs, files you import, Haikubox detections, sensor data, and the weather and other environmental data added to them. Everything slow happens here once, and every analysis uses it.
- **Analyses** — one analysis per question you ask of the data, each with its own filters, maps, charts and advisor notebook.
- **Documents** — figures, papers and posters made from your analyses and models.

## Download

| Platform | Download |
|----------|----------|
| macOS — Apple Silicon (M1/M2/M3/M4/M5) | [Latest .dmg](https://github.com/loggerhead-instruments/weft/releases/latest) |
| Windows | [Latest .exe](https://github.com/loggerhead-instruments/weft/releases/latest) |
| Linux — AppImage (auto-update supported) | [Latest .AppImage](https://github.com/loggerhead-instruments/weft/releases/latest) |
| Linux — Debian / Ubuntu | [Latest .deb](https://github.com/loggerhead-instruments/weft/releases/latest) |

Every link goes to the latest release page — pick the matching file under **Assets** at the bottom.

> **Notes:**
> - macOS builds require an Apple Silicon Mac (M1/M2/M3/M4/M5). Intel Macs are not supported.
> - Linux builds target x86_64 with glibc ≥ 2.35 (Ubuntu 22.04+, Debian 12+, Fedora 36+).

## System Requirements

- macOS 11+ (Apple Silicon only), Windows 10+, or x86_64 Linux (glibc ≥ 2.35)
- [Anaconda](https://www.anaconda.com/download) (free)
- 16 GB RAM minimum, 32 GB recommended (training)
- 4 GB disk space (including Python environment)

## Installation

1. **Install Anaconda** — download the graphical installer from [anaconda.com/download](https://www.anaconda.com/download) and follow the setup wizard. If you already have Anaconda or Miniconda installed, skip this step.

2. **Install Weft** — download the installer for your platform from the [latest release](https://github.com/loggerhead-instruments/weft/releases/latest).
   - **macOS (Apple Silicon)**: Open the `.dmg` and drag Weft to your Applications folder.
   - **Windows**: Run the `.exe` installer.
   - **Linux — AppImage** (recommended): `chmod +x Weft_*.AppImage`, then run it.
   - **Linux — Debian/Ubuntu**: `sudo apt install ./Weft_*.deb`.

3. **First launch** — Weft will detect your Anaconda installation and set up a Python environment automatically. This takes 5-10 minutes and only happens once. You'll see a progress screen — don't close the app during setup. Sign up for Weft using your email.

4. **Subsequent launches** — the app starts in a few seconds.

## What's Included (Free Beta)

### Projects
- Home shows all your projects. Open one to see its process runs, data, analyses and documents.
- Make a second library, model, run or analysis like one you already have, and Weft asks what is different about it, then shows that note in the list so you can tell them apart.
- **Duplicate** copies a library, model or run's settings, not its data, and remembers which one it came from.
- Recordings and large tables can stay on an external drive. If the drive is unplugged, reconnect it and carry on; if it moved, point Weft at the new place.
- Move a project to another computer as a package, with its external files copied to a drive of your choice.

### Libraries and Models
- Sort audio into categories with a spectrogram and playback, from folders on disk or straight from a Haikubox; label several chunks of a long file at once
- Each clip remembers its source recording, offset, sample rate and location; libraries can be fixed-rate, re-cut at another clip length, and cleaned in a grid view
- Train classifiers (EfficientNet-B0, EfficientNet-Lite, EfficientNet-ExtraLite) and watch the training curves as they go
- Multi-label training for clips where more than one species calls at once
- See exactly which sounds the model confuses, and listen to them
- Export models to ONNX or TFLite (INT8) to run on small devices
- **Publish Model** to the community library with authors and a citation; browse **Community Models** to download and run models published by others
- Species names follow GBIF, so models and detections line up across projects and research groups

### Process
- Run your model, a community model, BirdNET or HaikuNet over folders of recordings
- Check detections by ear and eye in **Review**, with a **Second opinion** from BirdNET or HaikuNet
- Measure the soundscape with no model: RMS, peak, SEL, spectral entropy, ACI, kurtosis, 1/3-octave bands and your own frequency bands
- Calibrate to absolute sound levels (dB re 1 µPa underwater or dB re 20 µPa in air)

### Data
- Bring in the project's runs directly, or import CSV, Parquet, NDJSON, JSON and DuckDB files, Haikubox detections and sensor logs
- Works with tables of billions of rows
- Find and fix bad data: coordinates off the globe or at 0, 0, unset recorder clocks, dates in the future
- Add weather, air quality, tides, ocean conditions and elevation for your sites and dates, once, for every analysis to use

### Analyses
- Plot detections on a map as dots, a heatmap or hexbins
- Plot activity over time, by category, as histograms, and by hour of day and day of week
- See when animals call relative to sunrise, sunset and moon phase
- Compare years side by side
- Total, average, maximum or minimum of any numeric column
- A table that scrolls through millions of rows
- **Save these rows** to turn a filtered subset into a table of its own on the Data tab, with a new analysis open on it
- Scale counts by the number of sites active in each period, worked out per day, with a choice of what counts as active
- Ask questions in plain English with the AI advisor (subscription): it proposes a method with checked references, builds the work as notebook steps in SQL, Python or R, and you can edit any step or export the notebook
- Six colourblind-safe palettes; set colours per category
- Dark or light charts for print

### Documents
- Click **+ Figure** on any chart, map, spectrogram or notebook step to save it. Edit, restyle and export figures.
- Build a figure from a table with a form: panels, shading, reference lines, error bars
- Papers: put figures in order and write the legends
- Posters: lay out figures and text on a page

# Quick Start Guide: Libraries, Models and Process

This section covers building a labeled library, training a classifier on it, and running the classifier over new recordings. The same workflow applies to bird calls, cetacean vocalizations, bat echolocation and other acoustic signals.

## Projects

Everything you record and analyse belongs to a project. Home lists your projects; click one to open it. Click **Home** to get back to the full list.

Libraries and models are shared between projects, so they sit on the left of the top bar and are always there. Process runs, data, analyses and documents belong to the project you have open.

## Choose Your Starting Point

- **[I have unlabeled audio](#1-labeling-audio)** — Start here to sort your recordings into categories
- **[I have labeled audio](#2-training-a-model)** — Jump straight to training a classifier
- **[I have a trained model](#3-processing-audio)** — Find sounds in new recordings
- **[I want to use an existing model](#3-processing-audio)** — Run a community model, or BirdNET or HaikuNet for birds, with no training

---

## 1. Labeling Audio

Open **Libraries** and start a library: your audio files sorted into categories (species, call types, noise, etc.).

### Setup

There are two ways to start a library:

**Option A: Start from raw audio**
1. In **Libraries**, click **+ New**
2. Point it at your folder of audio files
3. Add categories from the standardized list (e.g., `Megaptera novaeangliae`, `SYS_anthropogenic`, `SYS_unknown`)
4. Sort files one by one using the sorting interface

**Option B: Import pre-sorted audio**
1. In **Libraries**, click **+ New**
2. Point it at a folder where audio files are already organized into subfolders named by category
3. Weft imports the folder structure — subfolder names are automatically mapped to standardized GBIF and system category names

### Category Names

Category names are standardized using **GBIF (Global Biodiversity Information Facility)** identifiers. This means your models and detections use the same names as everyone else's, so they can be shared and combined across projects and research groups.

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

If your recordings are long (minutes to hours), turn on **chunking** to step through them in short pieces:

- Set a **chunk duration** (e.g., 3 seconds) that's long enough to see your signal of interest
- Weft steps through the file chunk by chunk
- Each chunk you label is saved as its own clip in the category folder
- Press **0** to ignore a chunk with nothing in it

A strip above the spectrogram shows the whole file. Click it to jump to a chunk; chunks you have labeled are marked in their category's colour, so you can see what is done when you come back to a file.

To label several chunks at once, pick them on the strip, then press a category: **Shift-click** selects from the current chunk to the one you click, **Ctrl/Cmd-click** adds or removes single chunks, and dragging across the strip selects a range. One **Undo** takes the whole batch back.

### Sample Rate

When you make a library you choose its sample rate: **Native** keeps each file at the rate it was recorded at, or pick a rate and every clip is resampled to it as it is added. A fixed rate keeps a library consistent when recordings come from different recorders. Once a library has clips, its chunk length and rate are locked; unlock them deliberately if you need to change them.

### Where Clips Came From

Each clip remembers the recording it was cut from, its offset in that file, its sample rate and its location. The **Library** tab shows these for the clip on screen, with a link to the file. Libraries made before this was recorded can fill it in with **Rebuild clip index**.

Locations can be set per source folder, or read from the recordings' paths with **Locations from the recordings' paths** when the folder names carry the site. Training can then balance across locations.

**Other clip length…** (beside **Chunk to New Project**) re-cuts a whole library at a different clip length into a new library, each clip re-taken from its source recording around its centre. Clips whose source is missing are copied unchanged and listed in the report.

### Spectrogram Display Settings

Adjust the spectrogram view to see your signals clearly:

- **Frequency range** (freq_min / freq_max): Zoom into the frequency band where your species vocalizes
- **FFT points**: Higher values = better frequency detail
- **Colormap**: Choose a color scheme that makes your signals stand out (inferno, viridis, grayscale)
- **Brightness** (vmin / vmax): Adjust contrast to bring out faint calls

These display settings only change what you see. They do not change the spectrograms the model trains on.

### Haikubox Integration (Remote Audio)

If you have a [Haikubox](https://haikubox.com) bird monitor, you can label its detections directly, without downloading files by hand.

**Setup:**
1. Go to **Settings** and add your Haikubox account using the API key from [listen.haikubox.com](https://listen.haikubox.com)
2. In a library, click **Haikubox Source** and select your account, device, species, and date range
3. Audio is fetched as you sort and kept on your computer

**How it works:**
- Weft looks up your Haikubox's detections for the species and dates you chose
- Clips are fetched ahead of time, so there is no wait between files
- Spectrogram, playback, chunking and keyboard shortcuts work just as they do for local files
- Labeled clips are saved to your library's category folders as WAV/FLAC files
- Weft remembers how far you got for each species and device, so you can pick up where you left off

**Use it to:**
- Build training sets for your own classifiers from Haikubox detections
- Check Haikubox detections species by species
- Mix Haikubox clips with local audio folders in the same library

### Reviewing Your Labels

Switch to **Library** mode to review what you've sorted:

- Filter by category to check consistency
- Play back files to make sure they're in the right category
- Move misclassified files to the correct category
- Delete bad recordings

**Grid** (beside **One clip**) shows a page of spectrogram thumbnails at once. Select the ones that are wrong, move them to another category in one go, and undo if you change your mind. It is the fast way to clean a category of a few hundred clips.

---

## 2. Training a Model

Open **Models** and create a model to learn your categories from your labeled audio.

### Setup

1. In **Models**, click **+ New**
2. **Add a data source** — pick the library (or libraries) with your labeled audio. Any library is available, whichever project it was made in.
3. Select which categories to include in training

### Spectrogram Settings

These control how audio is turned into the spectrogram images the model learns from. The defaults work well for most bioacoustic work:

| Setting | Default | What It Does |
|---------|---------|-------------|
| **n_fft** | 1024 | FFT window size. Higher = better frequency detail, coarser time detail |
| **hop_length** | 280 | Gap between FFT frames. Lower = better time resolution |
| **freq_min** | 100 Hz | Low frequency cutoff. Set above your noise floor |
| **freq_max** | 10,000 Hz | High frequency cutoff. Set just above your highest signal |
| **freq_bins** | 128 | Vertical resolution of the spectrogram image |
| **time_frames** | 256 | Horizontal resolution of the spectrogram image |

**Tip:** Preview a spectrogram before training to make sure your signal is visible and fills a reasonable part of the image.

### Architecture

Three model sizes are available:

| Architecture | Parameters | When to Use It |
|-------------|-----------|-------------|
| **EfficientNet-B0** | 4.0M | Best accuracy for most uses. Starts from a network pretrained on ImageNet and is fine-tuned on your spectrograms. |
| **EfficientNet-Lite** | 3.5M | Built to run on small, low-power devices (ESP32 via TFLite INT8) with little loss of accuracy. |
| **EfficientNet-ExtraLite** | 2.0M | The smallest, for the most constrained devices. |

When you switch architectures, the learning rate and early stopping patience are adjusted for you.

### Training Settings

| Setting | Default | What It Does |
|---------|---------|-------------|
| **Epochs** | 50 | Number of passes through the training data. More epochs give more learning time, with diminishing returns once the model settles |
| **Batch Size** | 32 | Samples processed at once. Reduce to 16 if you run low on memory |
| **Learning Rate** | Auto | Set for each architecture automatically. Can be overridden by hand |
| **Patience** | Auto | Epochs without improvement before training stops early |
| **Min Specs per Class** | 10 | Categories with fewer samples are left out of training |
| **Max Files per Class** | 0 (unlimited) | Cap samples per category. Useful if one category vastly outnumbers others |
| **Augment** | On | Randomly varies spectrograms during training so the model copes better with new recordings |
| **Multi-label** | Off | Lets the model report more than one category in the same clip (see below) |
| **Balance Method** | Weighted Loss | How to handle unequal category sizes (see below) |

### Class Balance Methods

| Method | Description |
|--------|-------------|
| **Weighted Loss** | Counts mistakes on rare categories more heavily, so the model pays more attention to them. All samples are used. Best for most cases |
| **Balanced Sampling** | Shows rare categories more often during training, so the model sees each class roughly equally. Useful when rare classes are distinctive but get drowned out by larger ones |
| **None** | No balancing. Categories with more samples have more influence. Only use when categories are already roughly equal in size |

**Balance by location** weights sampling so that no single site dominates a category, when clips carry locations (see *Where Clips Came From*). A model trained mostly on one site often only works at that site.

**Grouping categories.** Several library categories can be trained as one class, for example two subspecies as one, or every noise category as one background class. The grouping belongs to the model, so the library's categories stay as they are.

### Multi-label Mode

By default the model picks exactly one category per clip. Turn on **Multi-label** when more than one thing can be in the same clip — two species calling at once, whistles and clicks together, a dawn chorus or a busy reef. Each category then gets its own score. Leave it off when each clip holds one clear sound or your categories can't overlap.

### Start Training

Click **Train** and watch the live progress:

- **Training accuracy**: How well the model fits the clips it is learning from
- **Validation accuracy**: How well it does on clips it has not seen (this is the one that matters)
- **Loss curves**: Should trend downward. If validation loss starts rising while training loss keeps dropping, the model is overfitting

Training saves a checkpoint at each epoch. You can stop early and keep the best model.

### Reading the Confusion Matrix

After training, the confusion matrix shows exactly where the model gets things right and where it struggles:

- **Diagonal cells** = correct predictions (you want these to be high)
- **Off-diagonal cells** = mistakes (the model confused one category for another)
- Click any cell to see the actual files — listen to them and decide whether the model is wrong or the file was mislabeled

### Sharing a Model with the Community

Click **Publish Model** to add a trained model to the Weft community library. Enter the authors and a title, and Weft generates a citation (e.g., *Smith, J. 2026. Humpback song detector. Weft Community Models.*) that other researchers can use when they report results from your model. You can remove a published model from the library at any time.

To use someone else's model, open **Community Models**, download it, and select it when you set up a run. Each model shows its citation.

---

## 3. Processing Audio

Open **Process** in your project. Each item there is a **deployment**: a set of recordings from one place or recorder, and the runs you have done on them. Weft asks **Where were these recordings made?** so your detections carry their location onto the map.

There are two kinds of run:

- **Classification** — find species or other sounds with a model
- **Acoustic Analysis** — measure sound levels and acoustic indices, no model needed

### Setup

1. In **Process**, click **+ New** and say where the recordings were made
2. **Select the folder** of audio files
3. **Choose Classification or Acoustic Analysis** at the top of the page

---

### Classification Mode

Runs a model over your audio files to find and label sounds.

**Setup:** Select a model — your own from **Models**, a community model, or the built-in BirdNET or HaikuNet.

| Setting | Default | What It Does |
|---------|---------|-------------|
| **Chunk duration** | 3.0 s | Length of each piece of audio the model looks at. Should match your training clip length |
| **Step size** | 50% | Overlap between chunks. 50% means each moment of audio is checked twice |
| **Min confidence** | 50% | Only keep detections above this confidence |
| **Save chunks** | Off | Optionally save WAV clips of detected sounds |
| **Consecutive detections** | 1 | Require N chunks in a row with the same label before reporting a detection |

You can also turn on **Acoustic Metrics** to measure sound levels at the same time. Each detection then carries all the acoustic metric columns as well as the category and confidence.

When the run finishes, open **Review** to check detections by eye and ear. Click **Second opinion** on any detection to see what BirdNET or HaikuNet makes of it.

#### Consecutive Detections

Requiring several consecutive chunks to agree reduces false positives, because a real signal usually persists across overlapping chunks while transient noise does not.

**How it works:** Chunks are grouped by file and put in order. Weft finds runs of chunks in a row with the same label. A run of length L with threshold N gives floor(L/N) detections — one every N chunks. Runs shorter than N are dropped.

**Example — 50% overlap, consecutive = 2:**
```
Chunks:  [whale] [whale] [whale] [whale] [noise]
Result:  2 detections (whale run of 4 → floor(4/2) = 2, at chunks 1 and 3)
         The lone [noise] is dropped.
```

**Example — 50% overlap, consecutive = 2:**
```
Chunks:  [whale] [whale] [noise] [whale] [noise]
Result:  1 detection (whale run of 2 → floor(2/2) = 1)
         The lone [whale] at chunk 4 is dropped — only 1 in a row.
```

**Example — consecutive = 1 (default):**
```
Chunks:  [whale] [noise] [whale] [whale] [noise]
Result:  5 detections (every chunk reported as-is, no filtering)
```

---

### Acoustic Analysis Mode

Computes acoustic metrics without a classification model. Use it for soundscape characterization, noise monitoring, or baseline surveys.

**No model needed** — select a folder and start.

| Setting | Default | What It Does |
|---------|---------|-------------|
| **Window mode** | Per chunk | How audio is split up: per chunk, per file, or a custom length |
| **Window duration** | 3.0 s | Length of each window (for chunk and custom modes) |
| **Step size** | 100% | Window overlap. 100% = no overlap, 50% = each moment measured twice |
| **Sample rate** | 48000 Hz | Sample rate audio is loaded at |

#### What Is Measured

Every window gets all of these:

| Metric | Description |
|--------|-------------|
| **RMS level** | Root-mean-square level |
| **Peak level** | Maximum sample amplitude |
| **SEL** | Sound Exposure Level — total sound energy in the window |
| **Spectral Entropy** | 0 to 1. Low = tonal sound, high = broadband noise |
| **ACI** | Acoustic Complexity Index (Pieretti et al. 2011) — temporal variability of spectral amplitudes |
| **Kurtosis** | Excess kurtosis of the waveform. High = impulsive signal |
| **1/3-Octave Band Levels** | Standard ISO 266 bands from 25 Hz up to the highest frequency your recording holds. Works at sample rates up to 400 kHz+ |

#### Custom Frequency Bands

Add your own frequency bands to measure sound in a specific range (e.g., the band of a fish chorus). Each band gets its own column, like `band_chorus_db`.

#### Calibration (Optional)

Without calibration, levels are in **dBFS** (relative to the loudest sound the recorder can capture). With calibration, they are converted to absolute **Sound Pressure Level (SPL)** that can be compared across recorders and published:

| Setting | Description |
|---------|-------------|
| **Sensitivity** | End-to-end sensitivity in dBFS/Pa (e.g., -170 for a typical hydrophone) |
| **Recorder Gain** | System gain in dB. Read from the filename for Loggerhead recorders |
| **Medium** | Underwater (dB re 1 µPa) or Air (dB re 20 µPa) |

**Loggerhead recorders:** Gain is read automatically from the filename (e.g., `20230615T143022_1234565678_24.0dB_3.7V_ver1.0.wav` → 24.0 dB gain).

**Calibration formula:** `SPL = dBFS - sensitivity - gain`

---

### Output

Both kinds of run produce tables that the project's **Data** stage picks up directly — no export needed.

**Classification output** — one row per detection:
- Time, file and location
- Species or category, and confidence (0–100%)
- Duration and position within the source file
- Acoustic metrics (if turned on)

**Acoustic Analysis output** — one row per window:
- Time, file name and file path
- Window number, start time and duration
- All acoustic metric columns (RMS, peak, SEL, entropy, ACI, kurtosis, 1/3-octave bands)

Acoustic metric columns are recognised as numbers straight away, ready for histograms, timelines and maps.

---

## Tips for Building a Successful Classifier

### Label Quality Matters More Than Quantity

- **Be consistent**: If you're unsure about a file, skip it rather than guessing. A few mislabeled files are OK — you'll catch them after training.
- **Include background noise**: Always include normal background sounds. The model needs to learn what is NOT your signal.
- **Use the confusion matrix**: After training, listen to the files the model got wrong. You'll often find your target sound hiding in the background category. Move it, and retrain.

### Get Enough Labels

- **Aim for at least 1,000 samples per category.** More is better. Background/noise categories can have many more — 5,000+ is fine and helps the model learn what is NOT a signal.
- **Use several locations if you can.** A model trained at a single site often only works well at that site. Recordings from different places, microphones and conditions make a model that works more widely.
- **Unequal categories are OK** — weighted loss handles this. But avoid extreme ratios (1000:10).

### Choose the Right Clip Duration

- **The clip should be long enough to show the whole sound.** A 3-second clip works for most bird calls. Whale songs may need 10–30 seconds. Bat echolocation may only need 1 second.
- **The clip should be short enough that the sound fills a good part of the spectrogram.** A 0.1-second chirp in a 30-second spectrogram is invisible to the model.
- **Match your processing chunk duration to your training clip duration.**

### Set Your Frequency Range

- **Narrow the frequency range** to your signal. If your bird calls are between 2,000–8,000 Hz, set freq_min=1500 and freq_max=9000. This cuts out noise the model doesn't need to see.
- **Leave a small margin** above and below your signal.

### Iterate: Train, Process, Relabel, Retrain

The most effective workflow is iterative:

1. **Label a small set** (100–200 files per category)
2. **Train a model** — it won't be perfect, but it'll be useful
3. **Process unlabeled recordings** with it
4. **Review the results** — the model will find examples you missed, and its mistakes show what it needs more of
5. **Add the good detections to your library** and fix the bad ones
6. **Retrain** with the bigger library

Each round improves the model. Two or three rounds are usually enough for a reliable classifier.

### Use Noise Categories

- **Always include a noise or background category** (e.g., `SYS_anthropogenic`, `SYS_unknown`). The model needs to learn what is NOT a signal.
- **Include common look-alikes**: similar species, rain, wind, etc. Give each its own category so the model learns to tell them apart.

### When Training Stalls

- **Validation accuracy stuck below 80%**: You probably need more data, cleaner labels, or a better frequency range. Check the confusion matrix — the problem categories will stand out.
- **Validation loss rises while training loss drops**: The model is overfitting. Try fewer epochs, more augmentation, or more training data.
- **Training is very slow**: Reduce batch size if memory is low. Training time grows with the number of samples and epochs.

---

# Data Guide

**Data** is where a project's tables live: detections from your runs, files you import, Haikubox detections, sensor logs, and the environmental data added to them. You set things up here once — the column mapping, locations, cleaning and enrichment — and every analysis in the project uses the result.

## Bringing Data In

Open **Data** in your project. **Runs** lists the project's processing runs — pick the ones to combine, no export needed. Runs from other projects are offered too, so one deployment's detections can feed more than one project. Or click **Import** for a file:

- **CSV** — Comma-separated values
- **Parquet** — Columnar binary format (fast, compact)
- **JSON / NDJSON** — Newline-delimited JSON records
- **DuckDB** — Import tables from another DuckDB database

Use **Attach Sensor Data** to bring in a telemetry or logger file (temperature, depth, GPS track) with its own timestamps, to set next to your detections.

### Syncing Haikubox Data

If you have a [Haikubox](https://haikubox.com) bird monitor, you can bring its detections straight into a project.

1. Go to **Settings** and add your Haikubox account (API key from your account page on [listen.haikubox.com](https://listen.haikubox.com))
2. On the **Data** stage, click **Haikubox Sync**
3. Select an account, choose devices, and set a date range
4. Click **Sync** — detections come in with live progress

**What you get:**
- Every detection with its species, time, location, confidence and count
- Later syncs only fetch what is new
- Station names appear in your data
- Maps, charts and environmental data work as soon as the sync finishes

### Column Mapping

After import, tell Weft what your columns mean:

| Column | Purpose |
|--------|---------|
| **Datetime** | When each detection happened — turns on timelines and time-based summaries |
| **Category** | What was detected — species, call type, etc. |
| **Latitude / Longitude** | Where — turns on the map and environmental data |
| **Station** | Which recorder or site (a serial number or station name) — used by the station filter and by *Detections per active site* |
| **Numeric columns** | Any number to summarise (confidence, count, sound level, etc.) |

### Tables on External Drives

A table imported from a DuckDB file on an external drive stays there; Weft attaches the file rather than copying it. If the drive is unplugged, the table shows **Drive disconnected**; plug it back in and press **Reconnect**. If the file has moved, or the drive has a different letter or name on another computer, use **Locate…** to point the table at its new place. The project page lists everything a project needs from outside its own folder under **On external drives**.

## Finding and Fixing Data Problems

Click **Check data** on any table and Weft counts, for each station:

- Coordinates off the globe, at exactly 0, 0, or with only one of the pair
- Dates in 1970 (an unset clock) or in the future

For each problem you see the rows involved, and you choose what to do: **Exclude these rows**, or **Place this station…** at its real coordinates (Weft suggests where the station's other rows put it). Coordinates off the globe are left out automatically. Every fix can be undone, and your original data is never changed.

## Adding Environmental Data

The **Enrich** section adds environmental conditions for every site and date in your data. Each is computed once and used by every analysis in the project.

| Source | Resolution | What It Adds |
|--------|------|-------------|
| **Weather** | Daily, per location | Temperature, precipitation, humidity, wind, cloud cover, pressure, solar radiation |
| **Air Quality** | Daily, per location | AQI (US/EU), PM2.5, PM10, O3, NO2, SO2, CO (comes with weather) |
| **Tides** | Every 6 minutes, per location | Observed and predicted water level, tidal slope, daily tidal range (NOAA CO-OPS; free, for coastal sites within 100 km of a tide station) |
| **Ocean** | Daily, per location | Sea surface temperature and anomaly, chlorophyll-a, wave height/direction/period, swell height/direction/period (NOAA ERDDAP + Visual Crossing; paid tier) |
| **Elevation** | Fixed, per location | Elevation in meters (90 m SRTM data, computed on your computer) |

Click **Compute** on a card. Weft works out your sites and date range, fetches the data, and shows progress with a cancel button. Sunrise, sunset and moon phase need no fetching; they are worked out from your coordinates and times.

## Combining Data

Use **Combine** to merge tables:

- **Union** — stack tables with the same columns (e.g., detections from several deployments)
- **Join** — link tables on a shared column (e.g., add station details to detections)

The original tables are left unchanged.

---

# Analysis Guide

An analysis addresses one question about the project's data, such as diel calling patterns at each site, or vessel noise in relation to tidal state. Each analysis keeps its own filters, maps, charts and advisor notebook, so several questions can be worked on in parallel from the same data.

## Creating an Analysis

An analysis holds no data of its own. It reads the project's tables, which live on the **Data** tab: bring data in, map its columns, fix problems and add environmental data there, once, and every analysis in the project sees the result.

1. Open **Analyses** in the top bar, or click **+ New analysis** on the project page's Analyses card or in the header of an analysis you are in
2. Say what it is about; a note on what makes it different from the others is optional
3. Pick the table under **Data Source** in the left sidebar; the list is the project's Data tab

The sidebar's **Column Mapping** fold shows the mapping set on the Data tab; change it there and every analysis follows.

Rename an analysis from the project page's Analyses card or with **Rename** in its header. Names can carry apostrophes and other punctuation; the folder on disk is a plain version of the name.

Display choices (chart layout and colours, Year-over-Year, Detections per active site, the map's mode and base map) sit in the **Display** panel on the right and apply at once. Filters and the time step sit in the left sidebar and are applied with **Update**.

## Map View

Plot detections on a map by location. Needs latitude and longitude columns.

| Mode | Description |
|------|-------------|
| **Dots** | A point at each location, sized by count or by the value you choose |
| **Heatmap** | A smooth surface showing where detections are densest |
| **Hexbin** | Detections summed into a hexagonal grid |

Six base maps: Dark Matter, Light, Streets, Satellite, Ocean, and Terrain.

Click points to select locations, or Shift+drag to select a region. Charts and the table then show only those locations.

Six colourblind-safe palettes: Okabe-Ito, Wong, Tol Bright, Tol Muted, Set 2, Paired. Click the colour chip next to any category to set its colour.

## Charts View

| Chart | Description |
|-------|-------------|
| **Summary Metrics** | Total detections, rate, date range at a glance |
| **Timeline** | Activity over time, in the time steps you choose |
| **Category Breakdown** | How detections split across species or categories |
| **Numeric Distributions** | Histograms of any numeric column |
| **Day x Hour Heatmap** | When in the day and week activity happens |
| **Category x Time Heatmap** | One row per category, colour by activity in each time step, for comparing many species at a glance |

- Show or hide charts in the sidebar
- Click a chart title to expand it full-screen (Esc to exit)
- Drag the bottom edge to resize
- Switch between bar, line and dot charts
- Switch to light charts for print

### Year-over-Year Mode

Turn on **Year-over-Year** in the Display panel on the right (on the Charts and Map views) to lay each year over the others, lined up by the time step you have chosen: hours, days, weeks or months of the year. Use it to compare seasonal patterns or arrival dates between years. It replots at once; nothing is re-queried.

### Detections per Active Site

Raw counts rise and fall with how many recorders were listening. Tick **Detections per active site** (Display panel, Charts and Map views) to divide each period's count by the number of sites that were active in it. The timeline, the map's timeline, Year-over-Year and the two heatmaps all use it; the axis or colourbar says so.

**What a site is.** The station column, if your column mapping has one (for Haikubox data, the device serial). Otherwise the location, latitude and longitude rounded to three decimal places.

**What active means.** Choose with the two options under the checkbox:

- **All active sites, including those with no detections** (the default): a site counts in a period if it logged any detection at all in that period, of any species. A site that was listening and heard none of the species you selected still counts. A site that logged nothing at all, for example a recorder that was off or out of range, does not; Weft has no way to know it was there.
- **Only sites where the selected species were detected**: a site counts only if one of the species you have ticked was detected there in that period.

**How it is calculated.** Site activity is worked out per day. The first time you ask, Weft builds a per-day index for the table: one entry per day and site, with the site's location. On a large table that is one scan and takes a while, with "Counting active sites…" shown meanwhile; after that it is immediate and it is reused by every analysis of that table. The index is rebuilt by itself when the table grows or its column mapping changes.

- Day steps use the index directly.
- Week and month steps count the distinct sites across the days in the step, so a site active on one day of a week makes that week count it.
- Hour and 6-hour steps use the day's count for every step in that day; Weft does not track activity within a day.
- The Day x Hour heatmap divides each cell by the sites active on that day.
- Year-over-Year divides each year's period by the sites active in that period of that year.

The date range, station filter and selected places apply to the denominator. Numeric filters such as a score threshold do not: a site is active whatever the confidence of what it heard.

**Subsets.** An analysis made with **Save these rows** holds only the rows it kept, so on its own every site in it is a site with a detection. With the default option, the denominator is read from the table the subset came from, so sites that heard other species still count.

**Show active sites** draws the number of active sites on the timeline's second axis, and on the map marks the sites with no detection in the current period as grey rings, with a count. Use it to check the numbers the scale is dividing by.

## Environment Tab

See how detections relate to environmental conditions. Needs latitude, longitude and datetime columns.

- **Activity Relative to Sunrise** — when calling happens relative to sunrise and sunset
- **Activity by Moon Phase** — detections across the lunar cycle
- **Nocturnal by Moon Phase** — the same, at night only
- **Weather, air quality, tides and ocean** — once added on the **Data** stage, pick any variable for timeline and correlation charts
- **Elevation** — how detections spread across elevations

## Filters

Filters in the left sidebar narrow down what every view shows (map, charts, table).

| Filter | Description |
|--------|-------------|
| **Category** | Tick the categories to show. Use the search box to find one |
| **Date Range** | Focus on a period with From and To dates |
| **Numeric Range** | Set limits on any numeric column (e.g., confidence ≥ 0.8) |
| **Threshold** | Hide locations and time steps with fewer than a set number of detections |

For tables with more than 100 million rows, filters are not applied as you change them. Set your filters and click **Update** to run the query.

An analysis remembers its answers. When you reopen one, the Table, Map and Charts show what the last run found, marked *from the last run*, without querying again; they are forgotten when the table's data changes.

### Save These Rows

Click **Save these rows as a new analysis** to keep just the rows your filters select. The rows are copied into a new table in the project's Data tab, named after the analysis, with the original's column mapping and weather enrichment; the new analysis opens on that table with the same filters. The name is suggested from the filters, for example "Acorn Woodpecker 2024". Sunrise times are worked out again for the new table the first time they are needed. The original table is not changed.

## How Detections Are Summed

By default, maps and charts show **Count** — the number of detections. Under **Variable** in the sidebar you can switch to any numeric column instead:

| Function | Description | Example |
|----------|-------------|---------|
| **Count** | Number of rows (default) | 150 detections this week |
| **Sum** | Total of the column | Total detectionCount = 847 |
| **Average** | Mean of the column at each location | Avg confidence = 0.82 |
| **Maximum** | Highest value | Peak confidence = 0.99 |
| **Minimum** | Lowest value | Min confidence = 0.51 |

**Time step** sets how finely the timeline and heatmap are split:

| Step | Best For |
|-----|----------|
| **Hour / 6 Hours** | Short datasets where detail matters |
| **Day** | Default — a good balance of detail and readability |
| **Week / Month** | Smooths out noise, shows long-term trends |
| **Custom** | Any number of hours (1–720) |

<details>
<summary>How the numbers are worked out</summary>

Weft summarises in two steps.

**Step 1: per location.** Rows are grouped by **(latitude, longitude, time step, category)** and the chosen function applied. For example, 10,000 detections at one location over a week, with a "Week" step and "Sum of detectionCount", become one row for that location and week.

```sql
-- Simplified example
SELECT lat, lon, time_bucket('7 day', datetime) AS time_bin,
       category, SUM(detectionCount) AS detectionCount_sum
FROM detections
GROUP BY lat, lon, time_bin, category
```

**Step 2: across locations.** The timeline and category charts add up those per-location values for each time step, giving one line for all locations.

**Example:** 3 locations, weekly steps, Sum of detectionCount

| Location | Week 1 | Week 2 |
|----------|--------|--------|
| A | 45 | 52 |
| B | 30 | 28 |
| C | 25 | 31 |
| **Timeline** | **100** | **111** |

The Day x Hour heatmap groups the raw rows by day of week and hour of day directly, using the same function.

Numeric range filters apply to the raw rows **before** summing. The threshold filter applies **after**.

> **Note on Average:** with more than one location, the timeline adds up each location's average. That is exact for one location, but across several locations it weights each location equally whatever its number of rows. It is not a true overall average.

</details>

## The AI Advisor *(subscription)*

Ask a question about your data in plain English (for example, "Does the timing of the dawn chorus peak change with temperature?"), and the advisor:

1. Restates your question and says what in your data can answer it
2. Proposes a method, says why in a sentence, and gives references it has checked exist
3. Waits for you to agree or change the plan
4. Builds the analysis as a **notebook**: a list of steps, each with your request, the SQL, Python or R it wrote, the result (a table, numbers or a chart) and a short note on what it found

Every step shows its code and inputs, so the analysis can be checked and reproduced. Edit any step and everything below it runs again. You can keep several notebooks per analysis, send any step's chart or table to **Documents**, and export a notebook to keep or rerun outside Weft.

To use R, install it from [CRAN](https://cran.r-project.org). Weft finds it on its own; if it doesn't, point Weft at it in **Settings › Advisor**.

---

# Documents Guide

Documents turn your results into something you can publish or present.

- **Figures** — click **+ Figure** on any chart, map or spectrogram, or send a notebook step from the advisor. Restyle and export it. You can also build a figure from a table with a form: choose panels, shading, reference lines, spans and error bars. When the underlying analysis changes, update the figure and keep the previous version.
- **Papers** — put figures in order and write their legends.
- **Posters** — lay out figures and text on a page.

---

## Where Your Work Is Saved

Everything is saved in your home folder under `WeftProjects`:

- **macOS:** `~/WeftProjects/`
- **Windows:** `C:\Users\<username>\WeftProjects\`

```
WeftProjects/
  Libraries/        ← libraries, shared by all projects
  Models/           ← models, shared by all projects
  <Project name>/   ← one folder per project
    Runs/           ← processing runs
    Data/           ← the project's tables and environmental data
    Analyses/       ← one folder per analysis
  weave/            ← figures, papers and posters
  trash/            ← deleted items, until you empty the trash
```

Your own recordings stay where you put them; Weft does not copy them.

### Moving a Project to Another Computer

A project folder is self-contained apart from what it points to outside itself: recordings, attached tables and clips on other drives. To move one:

1. On the project page, click **Export package…**. Weft writes a single `.weftpack` file holding the project folder, with a README inside, and lists what it leaves out (temporary files, remembered query results, caches) and what the project needs from outside, with sizes. The package never contains the external files themselves.
2. If the project has files on an external drive, **Copy to another drive…** (on the **On external drives** list, or as an option while exporting) copies them to a drive you choose with the same layout, so the project finds them there. Large copies run as a job you can stop and resume, and each file is checked after copying.
3. On the other computer, click **Import package…** on the Projects page. Weft unpacks the project and, for each external drive it needs, asks where that drive is now and binds the files.

A project folder that is simply copied into `WeftProjects` is picked up on the next launch as well; the package route is there so nothing is missed.

### Deleting

Deleted libraries, models, runs and analyses go to the **Trash** on the Projects page, where you can **Restore** them to where they were, or **Delete forever**.

A project can only be deleted once it is empty. Libraries and models are shared, so they stay when a project is deleted.

**Exception:** deleting an imported table on the **Data** stage removes that data for good. Back it up first if you need it.

---

## How It Fits Together

```
Shared:   Libraries  →  Models
          (labeled      (trained
           audio)        classifiers)
                           │
Project:                   ▼
          Process    →    Data      →    Analyses   →   Documents
          (deployments,   (tables,       (maps,          (figures,
           runs and        cleaning,      charts,         papers,
           detections)     environment)   advisor)        posters)
```

- A model can learn from any number of libraries, from any project
- A model can be used in any number of runs, in any project. A run belongs to the project its recordings belong to
- Acoustic analysis runs need no model, just recordings
- The Data stage can bring in runs from any project. Every analysis in the project uses the same data
- Figures saved from an analysis or a model go to Documents

---

## Feedback & Support

- [Report a Bug](https://github.com/loggerhead-instruments/weft/issues/new?template=bug_report.md)
- [Request a Feature](https://github.com/loggerhead-instruments/weft/issues/new?template=feature_request.md)

---

[Privacy Policy](https://github.com/loggerhead-instruments/weft/blob/main/PRIVACY.md) · [Terms of Service](https://github.com/loggerhead-instruments/weft/blob/main/TERMS.md)

© 2026 Loggerhead Instruments
