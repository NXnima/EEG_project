# EEG Emotion Recognition

This project focuses on emotion recognition from EEG signals using the **DREAMER dataset**.

The main goal is to extract meaningful EEG features related to emotional states and prepare them for machine learning and deep learning models.

## Dataset

The project uses the **DREAMER dataset**, which contains EEG recordings from:

* **23 subjects**
* **18 video stimuli per subject**
* **14 EEG channels**
* **EEG sampling rate: 128 Hz**

The emotional responses are represented using three labels:

* **Valence**
* **Arousal**
* **Dominance**

## EEG Channels

The 14 EEG electrodes used in the dataset are:

```text
AF3, F7, F3, FC5, T7, P7, O1,
O2, P8, T8, FC6, F4, F8, AF4
```

## Preprocessing Pipeline

The EEG data is processed through the following pipeline:

```text
DREAMER EEG
     ↓
2-second windowing
     ↓
50% overlap
     ↓
0.5–45 Hz Band-pass filtering
     ↓
Feature extraction
     ├── Correlation
     ├── Alpha Power
     ├── Beta Power
     ├── Alpha Asymmetry
     ├── Beta Asymmetry
     └── Mutual Information
     ↓
Feature Fusion
     ↓
Machine Learning / Deep Learning Models
```

### Windowing

The EEG signals are divided into 2-second windows with 50% overlap.

With a sampling rate of 128 Hz:

```text
Window size = 2 × 128 = 256 samples
Step size = 256 × 0.5 = 128 samples
```

For the current dataset, this produces:

```text
85330 windows
```

### Band-pass Filtering

A 4th-order Butterworth band-pass filter is applied between:

```text
0.5 Hz – 45 Hz
```

### Alpha and Beta Power

Welch's method is used to estimate the Power Spectral Density (PSD).

The frequency bands are defined as:

```text
Alpha: 8–13 Hz
Beta: 13–30 Hz
```

The extracted features have the following dimensions:

```text
Alpha Power      → (85330, 14)
Beta Power       → (85330, 14)
```

