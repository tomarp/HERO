# HERO – Human Experience in Regulated Offices

This repository is the main **project hub** for the  
**Human Experience in Regulated Offices (HERO)** study within the **MuSIC_IRP1** initiative.

It brings together:

- the **experimental design** and protocol,
- the **multimodal dataset** (via Zenodo),
- the **analysis and preprocessing pipelines** (EEG, EDA, skin temperature, environment, surveys),
- and the evolving **research questions and publications**.

If you are looking for the dataset itself, see:

> **Dataset:** MuSIC\_IRP1_HERO – Multimodal Human Experience in Regulated Offices  
> **Zenodo:** https://zenodo.org/records/17597414

---

## 1. Project snapshot

**Goal.** HERO investigates how controlled indoor thermal environments (cool vs warm office conditions) shape:

- **physiology** (EEG, electrodermal activity, skin temperature),
- **subjective experience** (thermal comfort, affect, workload),
- and **task performance** during realistic office-like activities.

**Core questions include:**

- How do moderate thermal loads (LT vs HT) change **brain rhythms**, **autonomic responses**, and **peripheral temperature** during office work?
- How well do physiological signals explain or predict **thermal sensation**, **comfort**, and **self-reported workload**?
- Can we derive robust features that support **adaptive, occupant-centric building control**?

HERO combines **building science**, **physiological signal processing**, and **affective computing** in one controlled lab study.

---

## 2. Study design

![Study overview](https://github.com/tomarp/HERO/blob/main/metadata/HERO_Overview.png)

### Participants

- **N = 24** healthy adults (pseudonymized as `P01`–`P24`)
- Approximate age range: 18–45 years  
- All data are de-identified; only pseudo-IDs and session labels are shared.

### Sessions and thermal conditions

Each participant was invited for up to **two sessions**:

- `PXX_LT` – **Lower Temperature (LT)**: ~22 °C (±0.5 °C)
- `PXX_HT` – **Higher Temperature (HT)**: ~30 °C (±0.5 °C)

This yields a planned total of **48 sessions** (24 LT + 24 HT).  
Some sessions are missing per modality (see `*_summary.csv` in the dataset).

### Experimental phases

Each session follows a structured **nine-phase protocol**:

1. `baseline`
2. `activity_reading`
3. `first_washout`
4. `activity_writing`
5. `second_washout`
6. `activity_discussion`
7. `third_washout`
8. `activity_call`
9. `fourth_washout`

Participants perform **office-like activities** (reading, writing, collaborative discussion, simulated call) under stable thermal conditions, with **washouts** in between.

The file `timeline.csv` (in the dataset) defines **start and end timestamps for every phase** and `ID_Session`, and serves as the **temporal backbone** for all processing.

---

## 3. Modalities and instrumentation

HERO is **multimodal** by design.

### 3.1 EEG – Muse S

- **Device:** Muse S, 4-channel consumer EEG.
- **Channels:**
  - `TP9`, `TP10` (temporal): near temporal lobes → auditory, memory, emotional processing.
  - `AF7`, `AF8` (frontal): near frontal cortex → attention, problem-solving, cognitive control, affect regulation.
- **Sampling rate:** ≈250–256 Hz.
- **Use in HERO:**  
  - Continuous recording over the full session.
  - Focus on **band-limited power** (delta, theta, alpha, beta), artefact structure, and thermal-condition effects on rhythms.

### 3.2 EmotiBit – Electrodermal activity (EDA) & skin temperature (ST)

**EmotiBit** is a wearable sensor platform for physiological monitoring.

In HERO, we exploit:

- **EDA (Electrodermal Activity)**
  - Units: microsiemens (µS).
  - Sampling: ≈15 Hz.
  - Reflects sympathetic arousal (sweat gland activity), often linked to stress, cognitive load, and affect.

- **ST (Skin Temperature)**
  - Units: °C.
  - Sampling: ≈7.5 Hz.
  - Tracks peripheral thermoregulation (distal skin temperature changes over time).

Other EmotiBit channels may be present in raw exports but are not part of the core Level-0 dataset.

### 3.3 Environmental sensing

Environmental nodes record **indoor climate** variables such as:

- Air temperature (°C),
- Relative humidity (%),
- And, where available, additional comfort-related parameters.

Sensors are placed at desk / room level, with typical sampling around 1 Hz.

### 3.4 Perceptual / survey data

Survey instruments capture, per participant/session/phase:

- **Thermal sensation** and **thermal comfort**,
- **Affective state** (e.g., valence and arousal),
- **Perceived workload** and task difficulty.

These are aligned via the same `ID_Session` and phase labels as the physiological data.

---

## 4. Dataset releases

The **canonical data releases** are hosted on Zenodo.  
This repository contains the **code that produced those releases**.

### 4.1 Level-0: timeline-filtered raw (current Zenodo release)

> **MuSIC_IRP1_HERO – Level-0 Physiology & Context**  
> Zenodo: https://zenodo.org/records/17597414

Level-0 consists of **device-level streams**, trimmed to the experimental timeline:

- EEG (`eeg/`):
  - `eeg/P01_LT_timeline_filtered.csv`, etc.
  - Columns: `ts`, `ts_dt`, `tp9`, `af7`, `af8`, `tp10`, `ID_Session`, `phase_name`, `phase_label`, `phase_order`.
- EDA (`eda/`):
  - `eda/P01/P01_LT_eda.csv`, etc.
  - Columns: `datetime`, `ID_Session`, `eda`, `phase_name`, `phase_label`, `phase_order`.
- ST (`st/`):
  - `st/P01/P01_LT_st.csv`, etc.
  - Columns: `datetime`, `ID_Session`, `st`, `phase_name`, `phase_label`, `phase_order`.
- (Optionally) ENV (`env/`) and SURVEY (`survey/`) tables.

**Important:**  
At Level-0, **no filters, artefact removal, re-referencing, or resampling are applied**.  
The only transformation is **temporal trimming to phases** + adding metadata.

Coverage summaries for each modality:

- `eeg_summary.csv`
- `eda_summary.csv`
- `st_summary.csv`

Each summary row reports:

- `ID_Session`,
- `n_raw_samples`,
- `n_kept_samples` (after trimming),
- `n_phases_with_data`,
- `status` (`ok`, `missing_raw`).

### 4.2 Planned Level-1 / Level-2 releases

Future releases (referenced here, but not yet necessarily on Zenodo) will include:

- **Level-1 (preprocessed physiologic streams)**  
  - EEG in MNE FIF format:
    - Band-pass and notch filtered.
    - Artefact annotations and ICA-cleaned versions.
    - Channel and session-level QC reports.
  - EDA/ST cleaned and synchronized streams.

- **Level-2 (features & analysis tables)**  
  - Window-level features (e.g. 2-s sliding-window band power).
  - Phase-level aggregations (per participant/session/phase).
  - Multimodal fusion tables combining physiology, environment, and surveys.

This GitHub repo contains the **pipelines that generate Level-1 and Level-2 from Level-0.**

---

## 5. Repository structure (conceptual)

The exact layout may evolve, but core components are:

```text
.
├─ code/
│   ├─ filter_raw_eeg_by_timeline.py        # Level-0 EEG trimming (ts → phases)
│   ├─ filter_emotibit_eda_st_by_timeline.py# Level-0 EDA/ST trimming (datetime → phases)
│   ├─ muse_eeg_pipeline.py                 # Level-1 EEG preprocessing (MNE + ICA)
│   ├─ eda_pipeline.py                      # Level-1 EDA preprocessing (planned/ongoing)
│   ├─ st_pipeline.py                       # Level-1 ST preprocessing (planned/ongoing)
│   └─ helpers/                             # Shared utilities
├─ notebooks/
│   ├─ 01_exploratory_eeg.ipynb
│   ├─ 02_exploratory_eda_st.ipynb
│   ├─ 03_multimodal_phases.ipynb
│   └─ ...
├─ docs/
│   ├─ protocol/
│   │   └─ hero_experiment_protocol.pdf
│   ├─ figures/
│   └─ ...
└─ README.md                                # (this file)
```


## 6. Pipelines
### 6.1 Level-0 construction 

EEG timeline filtering

```
python code/filter_raw_eeg_by_timeline.py \
  --timeline /path/to/timeline.csv \
  --raw-dir /path/to/raw_eeg_csvs \
  --out-dir /path/to/eeg_timeline_filtered
```

EDA/ST timeline filtering

```
python code/filter_emotibit_eda_st_by_timeline.py \
  --timeline /path/to/timeline.csv \
  --raw-root /path/to/emotibit_raw \
  --out-root /path/to/emotibit_timeline_filtered
```

### 6.2 Level-1 EEG preprocessing (MNE)

Key steps implemented in muse_eeg_pipeline.py and/or notebooks:

1. Import Level-0 *_timeline_filtered.csv into an mne.io.Raw object.
2. Apply band-pass filter (e.g. 1–40 Hz) and notch filter (50 Hz).
3. Perform adaptive amplitude-based artefact annotation using sliding windows.
4. Conduct channel-level QC (variance, peak-to-peak, PSD).
5. Apply average reference over good channels.
6. Fit ICA (using clean segments only), detect blink/motion components, and remove them.
7. Export cleaned EEG as FIF + QC reports and plots.

Similarly structured pipelines are being developed for EDA/ST (Level-1) and for feature extraction (Level-2).

---
### Citation and licensing

If you use the dataset, please cite the Zenodo record:

> Tomar, P., Pigliautile, I., & Pisello, A. L. (2025). Human Experience in Regulated Offices (HERO) dataset [Data set]. Zenodo. https://doi.org/10.5281/zenodo.17597414

### Licensing and conditions of use
Creative Commons Attribution 4.0 International
The Creative Commons Attribution license allows re-distribution and re-use of a licensed work on the condition that the creator is appropriately credited. [Read more](https://creativecommons.org/licenses/by/4.0/legalcode)