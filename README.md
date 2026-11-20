# Environmental Monitoring and Data Analysis

Course material for the Master's course *Environmental Monitoring and Data Analysis* (1st semester, environmental science), Chair of Sensor-based Geoinformatics, University of Freiburg. Winter semester 2026/27.
Lab website: <https://uni-freiburg.de/enr-geosense>

In this course you follow a set of five flux towers through the whole life of environmental data: you download their measurements, add satellite, climate and site data, clean and analyse the time series, model the fluxes, put everything into a shared database, and present what you found on a poster. Along the way you learn the tools of reproducible data science: Git and GitHub, R or Python, Quarto reports and the bwUniCluster.

**Fridays, 8:30–12:00.** Each block has about two hours of teaching and about two hours of assignment work.
**Teaching team:** Negin Katal, Teja Kattenborn, Markus Weiler (Blocks 6–7), Joachim Maack (Blocks 11–12).

## Contents

- [Quick start](#quick-start)
- [Course schedule](#course-schedule)
- [Assignments and assessment](#assignments-and-assessment)
- [What is in this repository](#what-is-in-this-repository)
- [Getting new material every week: `upstream`](#getting-new-material-every-week-upstream)
- [Your data](#your-data)
- [Software you need](#software-you-need)
- [Online tools](#online-tools)
- [Help](#help)
- [Data citation and licence](#data-citation-and-licence)

## Quick start

1. **Fork** this repository on GitHub (button at the top right). The fork is your own copy.
2. **Clone your fork** to your laptop:
   ```bash
   git clone https://github.com/YOUR-USER/datascience_env_monit.git
   cd datascience_env_monit
   ```
3. **Connect it to the course repository** once, so you can get new material later:
   ```bash
   git remote add upstream https://github.com/negin-katal/datascience_env_monit.git
   git remote -v
   ```
   You should see `origin` (your fork) and `upstream` (this course repository).
4. Every week: **sync**, then follow the assignment sheet in `assignments/`. Commit small, push to your fork, hand in on ILIAS.

You never push to this repository. You work in your fork, so your changes never touch the course material.

## Course schedule

| Block | Date | Topic | Lead | Material |
| --- | --- | --- | --- | --- |
| 1 | 23 Oct 2026 | Introduction, R and VS Code: the course, your tower sets, a working setup and a first reproducible figure | Negin Katal | ILIAS |
| 2 | 30 Oct 2026 | Git/GitHub and remote computing: your project becomes a Git repository; run code on bwUniCluster over SSH | Negin Katal| [Assignment](assignments/block-2-git-github-cluster.md), [SSH guide](https://negin-katal.github.io/datascience_env_monit/ssh-connection/) |
| 3 | 6 Nov 2026 | Excursion to ECOSENSE: flux towers and sensors in the field | Negin Katal | ILIAS (meeting point) |
| 4 | 13 Nov 2026 | Data acquisition I: download your towers' flux data, read documentation and quality flags, import cleanly | Negin Katal| [Assignment](assignments/block-4-flux-data-summary.md), `scripts/get_my_towers` |
| 5 | 20 Nov 2026 | Data acquisition II: add climate, soil, plant, extreme-event, biodiversity and satellite data and merge them | Negin Katal| [Assignment](assignments/block-5-complementary-data.md), [`scripts/block5/`](scripts/block5/) |
| 6 | 27 Nov 2026 | Extreme values and time-series analysis: droughts, heat waves, decomposing time series | Markus Weiler | follows |
| 7 | 4 Dec 2026 | Outliers and data quality: detect outliers, check plausibility, document every cleaning step | Markus Weiler | follows |
| 8 | 11 Dec 2026 | Modelling I: empirical models and prediction of flux time series | Teja Kattenborn and Negin Katal| follows |
| 9 | 18 Dec 2026 | Modelling II: validation, uncertainty and transfer to other towers | Teja Kattenborn and Negin Katal | follows |
| – | 25 Dec 2026, 1 Jan 2027 | Winter break | | |
| 10 | 8 Jan 2027 | Modelling III: interpretation and links to ecosystem functional properties | Teja Kattenborn and Negin Katal | follows |
| – | 15 Jan 2027 | Independent work on your tower set (no lecture, support as agreed) | | |
| 11 | 22 Jan 2027 | Databases I: structure, validation and ingestion of the course data | Joachim  Maack| follows |
| 12 | 29 Jan 2027 | Databases II: queries and integrated analysis of all towers | Joachim Maack| follows |
| 13 | 5 Feb 2027 | Independent project completion: finish your report and poster (no lecture, support as agreed) | | |
| 14 | 12 Feb 2027 | Poster presentations and discussion across towers | Teaching team | |

Slides are on ILIAS (folder *Slides*). Dates and rooms are announced on ILIAS; ILIAS is always right if this table and ILIAS disagree.

## Assignments and assessment

**Weekly assignments.** Most blocks end with an assignment sheet in [`assignments/`](assignments/). You start it in class and finish it before the next block. The usual hand-in on ILIAS is:

1. the rendered report (HTML) or the result the sheet asks for, and
2. the link to your fork on GitHub with the source (`.qmd`, `.Rmd`, `.ipynb`, scripts).

Each sheet has a time plan, *Check:* boxes after every step, a hand-in checklist and a troubleshooting table.

| Block | Assignment | Due |
| --- | --- | --- |
| 2 | [Git, GitHub and your first cluster job](assignments/block-2-git-github-cluster.md) | before Block 3 |
| 4 | [Download your towers and write a data summary](assignments/block-4-flux-data-summary.md) | before Block 5 |
| 5 | [Test one question with your towers and two more datasets](assignments/block-5-complementary-data.md) | before Block 6 |

New sheets are added here as the course goes on.

**Assessment.** The examination (Prüfungsleistung) is **one written report** in the middle of semester (after block 7) and a **poster presentation** in Block 14. Both build on the work you do on your towers during the semester, so the weekly assignments are your building blocks: keep them tidy and reproducible.

## What is in this repository

```
datascience_env_monit/
├── README.md              this file
├── assignments/           one assignment sheet per block
├── scripts/               scripts used in the assignments (R and Python twins)
│   ├── cluster_hello.*        Block 2: first job on bwUniCluster
│   ├── get_my_towers.*        Block 4: download your five towers with the FLUXNET Shuttle
│   └── block5/                Block 5: ERA5-Land, WorldClim, Dheed, SoilGrids, PlantTraits,
│                              deadtrees.earth, iNaturalist, MODIS NDVI/EVI, merge (see its README)
├── jobs/                  Slurm job scripts for bwUniCluster
├── docs/                  templates and notes, e.g. STORAGE_TEMPLATE.md
├── ssh-connection/        SSH guide for bwUniCluster (also online, see below)
├── flux4student/          FLUXNET site explorer and weekly data of all course towers (also online)
└── LICENSE
```

**Folders you create in your fork** (they are not in the course repository):

| Folder | What goes in | In Git? |
| --- | --- | --- |
| `data/raw/` | Original downloads, untouched (FLUXNET zips, snapshot) | **no** |
| `data/external/` | Block 5 datasets, one subfolder per dataset | **no** |
| `data/processed/` | Tables you make from the raw data | **no** |
| `reports/` | Your Quarto reports or notebooks (`.qmd`, `.ipynb`) | yes |
| `docs/STORAGE.md` | Where your data and results live, and when they expire | yes |

Run all scripts from the top folder of your project (the one that contains `data/` and `scripts/`).

## Getting new material every week: `upstream`

Your fork is a copy of the course repository *from the day you forked it*. New material (assignment sheets, scripts) does **not** appear in your fork by itself, and `git pull` alone only talks to your fork (`origin`). You bring new material from the course repository (`upstream`):

```
negin-katal/datascience_env_monit  (upstream)  ──pull──▶  your laptop  ──push──▶  YOUR-USER/datascience_env_monit  (origin)
```

**Once:** add `upstream` (step 3 of the [quick start](#quick-start)). `git remote add` says `remote upstream already exists`? Then you have done it already.

**Every week, before you start:**

```bash
git status                            # must say: nothing to commit, working tree clean
git pull --no-rebase upstream main    # bring in the new course material
git push                              # send it on to your fork on GitHub
```

- Commit (or `git stash`) your own changes first.
- Always name the branch (`main`) and keep `--no-rebase`: your fork has your own commits, so Git must merge.
- If Git opens an editor for the merge message, keep the text, save and close (in vim: `:wq` and Enter).

**If Git reports a conflict in `README.md`:** you replaced the README with your own in Block 2, and this course README changes too. Keep your own:

```bash
git checkout --ours README.md
git add README.md
git commit -m "Merge course updates, keep my README"
git push
```

For a conflict in any other file: open it, decide which lines to keep, delete the `<<<<<<<`, `=======` and `>>>>>>>` lines, then `git add` the file and commit. Lost? `git merge --abort` takes you back to before the pull.

**On github.com** you can also click **Sync fork → Update branch** on your fork's page, then run `git pull` on your laptop. If GitHub offers **Discard commits**, do not click it: that throws away your own work. Use the command line instead.

## Your data

- **Data never go into Git.** Add `data/` to your `.gitignore` (Block 4, Part A2). Git is for code and reports; data come from their original source, which your scripts and your report document.
- **Course files** that are not in this repository, such as `tower_sets_block4.csv` (your five towers), are on ILIAS in the folder *DATA*.
- **On bwUniCluster**, keep data and results in your workspace (`envmon`), not in your home folder, and note when it expires in `docs/STORAGE.md`. Workspaces are deleted after they expire.
- **Shared course data.** After Block 5 the course collects everyone's data in a shared cloud folder for the database blocks (11–12). Instructions follow on ILIAS.
- **Cite every dataset you use.** Each script states its citation in the header; the assignment sheets say what to put in your report.

## Software you need

| What | Why | Notes |
| --- | --- | --- |
| Git and a GitHub account | Version control, your fork | Set `git config --global user.name` and `user.email`. On Windows use Git Bash. |
| **R + Positron** *or* **Python + VS Code** | Analysis | Choose one route and keep it; every script exists in both languages. Setup: Block 1 material on ILIAS. |
| Quarto | Reports that render to HTML | Included in Positron. VS Code: install from <https://quarto.org> and the Quarto extension. |
| Python 3.9 or newer | The FLUXNET Shuttle (Block 4) is a Python tool | Needed on the R route too; `get_my_towers.R` sets it up for you. |
| bwUniCluster account | Remote computing, big files | Register before Block 2. Only reachable from the university network: use the VPN from home. |
| Copernicus CDS account | ERA5-Land in Block 5 | Free; accept the dataset licence on the dataset page. |

R and Python packages are listed at the top of each script and in [`scripts/block5/README.md`](scripts/block5/README.md).

## Online tools

- **flux4student explorer:** map, data availability and weekly time series of all course towers: <https://negin-katal.github.io/datascience_env_monit/flux4student/>
- **SSH connection guide for bwUniCluster:** <https://negin-katal.github.io/datascience_env_monit/ssh-connection/>
- **Climate data viewer** <https://negin-katal.github.io/datascience_env_monit/climate-data-viewer/>

## Help

- **Stuck for more than 10 minutes?** Post the exact command and the last lines of the error on ILIAS, or raise your hand in class. Somebody else probably has the same problem.
- Every assignment sheet ends with a **troubleshooting table**; check it first.
- When you ask for help, say: what you ran, what you expected, what happened (copy the error text, not a photo), and whether you use R or Python, Windows, macOS or Linux.

## Data citation and licence

Course material: see [LICENSE](LICENSE).

The FLUXNET data in `flux4student/` are CC-BY-4.0 with citation requirements per site; see [`flux4student/README.md`](flux4student/README.md). When you use flux data, cite each site's data product, Pastorello et al. (2020), *Scientific Data* 7, 225, <https://doi.org/10.1038/s41597-020-0534-3>, and include the FLUXNET acknowledgement given there. The Block 5 datasets each have their own citation, listed in the header of every script.
