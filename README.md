# AI Workshop · Lab 2 · One defensible feature (group G1)

**Pair:** Baptiste Vial · Vicente Rodriguez

**Question:** Can one pre-race feature, `estimated_grid_position = qualifying_position + grid_penalty`, improve validation balanced accuracy for the top-10 prediction? The prediction moment is after qualifying and before the race.

**Result:** No. Validation balanced accuracy on weeks 11–14 was 0.5000 for the dummy baseline, 0.8625 without the feature and 0.8625 with it, with identical predictions on all 80 rows. We **reject** the feature. The feature is an exact sum of two columns the model already receives, so it adds no new information: the model weights one grid-penalty place at about 0.31 of one qualifying place without it and 0.32 with it. The reserved test (weeks 15–18) was not scored. The data is synthetic, so it says nothing about real F1 performance.

## Files

| File | Purpose |
|---|---|
| `AIW_Lab02_G1_one_feature.ipynb` | **Submitted, executed notebook**: the Week 4 pipeline plus lab sections L0–L6 |
| `w04_race_weekends_synthetic_v3.csv` | Course dataset (360 rows); it must be in the same folder as the notebook |
| `W04_Thu_Pipelines_Student_v3.ipynb` | Original Thursday Week 4 notebook, unmodified, for reference |
| `requirements.txt` | Pinned package versions |

Data retrieval, if the CSV is missing: download `w04_race_weekends_synthetic_v3.csv` from the course Canvas (<https://udd.instructure.com/courses/81962/files/9285499/download?download_frd=1>) into the repository root. Section L6 of the notebook prints a SHA-256 fingerprint (line endings normalised to LF) that should read `b7dbafdcdffa9491`.

## Run steps

```bash
# 1. Create the environment with Python 3.12 (Linux/macOS)
python3.12 -m venv .venv
.venv/bin/pip install -r requirements.txt
#    Windows: py -3.12 -m venv .venv  then  .venv\Scripts\pip install -r requirements.txt

# 2a. Interactive: open the notebook, then choose Kernel → Restart & Run All
.venv/bin/jupyter notebook AIW_Lab02_G1_one_feature.ipynb

# 2b. Headless alternative (equivalent to Restart & Run All)
.venv/bin/jupyter nbconvert --to notebook --execute --inplace AIW_Lab02_G1_one_feature.ipynb
```

Expected result: every cell runs without an assertion error; the L2 score table shows 0.5000 / 0.8625 / 0.8625 with 0 disagreeing rows; L3 shows a penalty cost of 0.31 / 0.32. The committed notebook was executed on 8 October 2026 with Python 3.12.15, numpy 2.1.2, pandas 2.2.3 and scikit-learn 1.7.2 on Linux. An earlier run on Windows 10 (Python 3.12.10, same packages) gave the same scores. A re-run of a copy on 8 October in a separate Linux environment (Python 3.12.3, same packages) reproduced every output except the Python/OS line of L6. The run is deterministic (no random split, `random_state=42`).
