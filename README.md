# Homework 3 - Human Activity Recognition

**Name:** Nakul Kumbria  
**GitHub:** nakicool007

This is my Homework 3 submission. I used the AReM dataset to extract time-domain features from human activity recordings. The notebook also contains the bootstrap confidence intervals, my feature choices, and the answers to Question 2 on linear and cubic regression.

## Files

```text
HW3/
├── README.md
├── .gitignore
├── requirements.txt
├── data/
│   ├── AReM/
│   │   ├── bending1/              # dataset1.csv–dataset7.csv
│   │   ├── bending2/              # dataset1.csv–dataset6.csv
│   │   ├── cycling/               # dataset1.csv–dataset15.csv
│   │   ├── lying/                 # dataset1.csv–dataset15.csv
│   │   ├── sitting/               # dataset1.csv–dataset15.csv
│   │   ├── standing/              # dataset1.csv–dataset15.csv
│   │   ├── walking/               # dataset1.csv–dataset15.csv
│   │   ├── bendingType.pdf
│   │   └── sensorsPlacement.pdf
│   ├── train/                     # 69 files, grouped by activity
│   ├── test/                      # 19 files, grouped by activity
│   └── processed/
│       ├── features.csv
│       ├── instance_metadata.csv
│       └── feature_std_ci.csv
└── notebook/
    └── Kumbria_Nakul_HW3.ipynb
```

All the code is in the notebook. The data files and saved results are included so the notebook can be run without downloading the dataset again.

## Dataset and split

There are 88 instances in seven activity folders. Bending1 has 7 files, bending2 has 6, and each of the other folders has 15. Each file contains a timestamp and six sensor series.

Following the assignment, I used datasets 1 and 2 from bending1 and bending2 for testing. For the other activities, I used datasets 1, 2, and 3 for testing. The remaining files are training data. This gives **69 training instances and 19 test instances**.

One thing I found while checking the data is that `sitting/dataset8.csv` has 479 observations instead of 480. All the other files have 480. I kept the original data and used the available observations for that file. The notebook also handles spaces and extra trailing commas in some files.

## Running the notebook

Use Python 3.10 or newer. From this folder, run:

```powershell
python -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m jupyterlab
```

Open `notebook/Kumbria_Nakul_HW3.ipynb` and run all cells in order. The bootstrap uses 10,000 repetitions, so that part may take a little time.

To run the notebook from the terminal and save its outputs:

```powershell
.venv\Scripts\python -m nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=600 notebook/Kumbria_Nakul_HW3.ipynb
```

## Results

- `features.csv`: 88 instances with 42 features each, plus the instance ID. I calculated minimum, maximum, mean, median, sample standard deviation, and the first and third quartiles for each sensor series.
- `instance_metadata.csv`: the activity, filename, and train/test assignment for each instance.
- `feature_std_ci.csv`: the standard deviation of each feature across all 88 instances and its 90% bootstrap confidence interval. I used random seed 42.

The notebook recreates these files in `data/processed/`. The saved notebook includes the outputs from running all cells.

## Uploading to GitHub

Include `data/`, `notebook/`, `README.md`, `.gitignore`, and `requirements.txt`. The environment and cache files are excluded by `.gitignore`.

## Dataset source

Palumbo, F., Gallicchio, C., Pucci, R., & Micheli, A. (2016). *Activity Recognition system based on Multisensor data fusion (AReM)* [Dataset]. UCI Machine Learning Repository. [DOI: 10.24432/C5SS33](https://doi.org/10.24432/C5SS33).

The dataset is available on the [UCI AReM page](https://archive.ics.uci.edu/dataset/366/activity+recognition+system+based+on+multisensor+data+fusion) under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The raw files and reference PDFs are from this dataset. The train/test files are copies of the originals, and the result CSVs were calculated in the notebook.
