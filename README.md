# depressjon

A copy of the **Depresjon dataset**: minute-by-minute wrist activity recordings from 23 people with unipolar or bipolar depression and 32 people without depression, plus a table of clinical and demographic scores for each person.

The dataset was published by Simula Research Laboratory and the University of Bergen. This repository does not change the data; it holds the files exactly as distributed in `depresjon.zip` from the [official dataset page](https://datasets.simula.no/depresjon/).

## What's in this repository

```
depressjon/
├── condition/          23 activity files, one per participant with depression
│   ├── condition_1.csv
│   └── … condition_23.csv
├── control/            32 activity files, one per participant without depression
│   ├── control_1.csv
│   └── … control_32.csv
├── scores.csv          one row per participant: demographics and depression scores
└── README.md
```

| Path | What it holds | Size on disk |
|---|---|---|
| `condition/` | Activity recordings for the 23 participants with depression | 18 MB |
| `control/` | Activity recordings for the 32 participants without depression | 33 MB |
| `scores.csv` | 55 rows, one per participant, linking each file name to that person's details | 4 KB |

The file name of each activity recording (for example `condition_7`) matches the `number` column in `scores.csv`. All 55 recordings have a matching row, and every row has a recording.

## How the activity was recorded

According to the [dataset page](https://datasets.simula.no/depresjon/), each participant wore an actigraph watch on the right wrist (Actiwatch, Cambridge Neurotechnology Ltd, model AW4). The watch samples movement 32 times a second and registers movements above 0.05 g. It stores the result as an *activity count* for each minute: the higher the count, the more intense the movement in that minute.

The data was originally collected for a study of motor activity in schizophrenia and major depression ([Berle et al., 2010, *BMC Research Notes*](https://bmcresnotes.biomedcentral.com/articles/10.1186/1756-0500-3-149)).

## Activity files (`condition/*.csv`, `control/*.csv`)

Each file is one participant's recording, one row per minute.

| Column | Meaning | Example |
|---|---|---|
| `timestamp` | Start of the one-minute interval | `2003-05-07 12:01:00` |
| `date` | Calendar date of that minute | `2003-05-07` |
| `activity` | Activity count for that minute from the watch | `143` |

From my own count of the files: recordings run from 19,299 to 65,407 minutes (roughly 13 to 45 days), the timestamps fall between May 2002 and February 2006, and the highest activity count in the data is 8,000.

## Scores file (`scores.csv`)

One row per participant. The column meanings below are quoted from the [dataset page](https://datasets.simula.no/depresjon/); the "Notes" column is mine.

| Column | Meaning | Notes |
|---|---|---|
| `number` | Participant identifier | Matches the activity file name, e.g. `condition_1` |
| `days` | Number of days of measurement | See "Things to know" below |
| `gender` | `1` = female, `2` = male | |
| `age` | Age, grouped into 5-year bands | e.g. `35-39` |
| `afftype` | `1` = bipolar II, `2` = unipolar depressive, `3` = bipolar I | Depression group only |
| `melanch` | `1` = melancholia, `2` = no melancholia | Depression group only |
| `inpatient` | `1` = inpatient, `2` = outpatient | Depression group only |
| `edu` | Education, grouped in years | e.g. `6-10`, `11-15`, `16-20` |
| `marriage` | `1` = married or cohabiting, `2` = single | Depression group only |
| `work` | `1` = working or studying, `2` = unemployed, sick leave or pension | Depression group only |
| `madrs1` | MADRS score when measurement started | Depression group only |
| `madrs2` | MADRS score when measurement stopped | Depression group only |

MADRS is the Montgomery–Åsberg Depression Rating Scale, a clinician-rated measure of depression severity; a higher score means more severe depression.

### Who is in the data

Counted from `scores.csv`:

| | Depression group (`condition`) | Control group (`control`) |
|---|---|---|
| Participants | 23 | 32 |
| Female / male | 10 / 13 | 20 / 12 |
| Unipolar depression | 15 | n/a |
| Bipolar II / bipolar I | 7 / 1 | n/a |
| Inpatients / outpatients | 5 / 18 | n/a |
| MADRS at start (range) | 13 to 29 | n/a |

## Things to know before using the data

- **Control rows are mostly empty.** For the 32 controls, every column after `age` is `NA` or blank. Only `number`, `days`, `gender` and `age` are filled in.
- **Some values are missing in the depression group too.** `melanch` is `NA` for 3 participants, and `edu` is blank for 1.
- **The recordings are longer than the `days` column.** In all 55 files, the recording covers more calendar dates than `days` says. For example, `condition_1` has `days = 11` but spans 17 dates, and `control_1` has `days = 8` but spans 37. My reading, not stated on the dataset page, is that `days` counts the days used in the study and the files also include extra time before or after it. Decide how to handle this before comparing participants; a common approach is to keep only the first `days` full days of each recording.
- **First and last days are partial.** Recordings start and stop mid-day (the sample file `condition_1` starts at 12:00), so the first and last dates do not cover 24 hours.
- **Activity count is not steps.** It is a device-specific measure of movement intensity from a 2000s-era research actigraph. It is not directly comparable with step counts or activity scores from modern consumer wearables without some form of calibration.

## Citation and terms of use

The dataset page's terms of use say: *"In all documents and papers that report experimental results based on the Depresjon Dataset, a reference to this study should be included."* No other licence is stated on the page.

Cite the dataset as:

> Enrique Garcia-Ceja, Michael Riegler, Petter Jakobsen, Jim Tørresen, Tine Nordgreen, Ketil J. Oedegaard and Ole Bernt Fasmer. 2018. *Depresjon: A Motor Activity Database of Depression Episodes in Unipolar and Bipolar Patients.* In Proceedings of the 9th ACM Multimedia Systems Conference (MMSys '18), Amsterdam, The Netherlands. ACM. https://doi.org/10.1145/3204949.3208125

```bibtex
@inproceedings{Garcia:2018:NBP:3083187.3083216,
  title     = {Depresjon: A Motor Activity Database of Depression Episodes in Unipolar and Bipolar Patients},
  author    = {Enrique Garcia-Ceja and Michael Riegler and Petter Jakobsen and
               Jim T\o rresen and Tine Nordgreen and Ketil J. Oedegaard and
               Ole Bernt Fasmer},
  booktitle = {Proceedings of the 9th ACM on Multimedia Systems Conference},
  series    = {MMSys'18},
  year      = {2018},
  location  = {Amsterdam, The Netherlands},
  url       = {http://doi.acm.org/10.1145/3204949.3208125},
  doi       = {10.1145/3204949.3208125},
  publisher = {ACM},
  address   = {New York, NY, USA}
}
```

## Source and contact

- Dataset page: https://datasets.simula.no/depresjon/
- Original download: https://datasets.simula.no/downloads/depresjon.zip
- Questions about the dataset go to its authors; contact details are on the dataset page.
