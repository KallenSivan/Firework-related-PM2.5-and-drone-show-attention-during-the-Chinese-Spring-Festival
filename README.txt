Chinese Spring Festival PM2.5 — data and downstream reproduction code

CURRENT RELEASE
Figure 2 uses row-standardized Queen contiguity, 999 permutations, seed 42 and one worker. The observed festival-window PM2.5 means are the LISA outcome, as in the submitted methods. Concentration completion uses the submitted IDW procedure; IDW does not create spatial neighbors. Each year has 375 spatial units, 372 tested units and 3 islands (Zhoushan, Taiwan, Sansha). Island I, p and quadrant are missing and explicitly marked Not tested (island).

Figure 2: results/figures/FIGURE2_Queen.png (300 dpi).
Annual counts: results/figures/Figure2_annual_counts.csv.
City statistics, island flags and complete weight neighbor lists: results/moran_analysis_updated_B/local_moran/.
HH counts for 2020–2025: 80, 82, 80, 98, 85, 68.
LL counts for 2020–2025: 104, 106, 84, 95, 89, 53.
The figure preserves the submitted drawing configuration and rendering block, including projection, map limits, inset, colors and border. The island category is an explicit additional legend item. No historical 200 km LISA output is the current Figure 2 result.

REPRODUCE
Install requirements.txt in a compatible Python environment. From any working directory run:
  python /path/to/data/code/run_downstream.py
To redraw Figure 2 only from the included corrected statistics:
  python /path/to/data/code/07_figure2_queen.py
All input/output paths in release scripts are package-relative. Outputs are written under results/. New GWR diagnostic runs go to results/gwr/diagnostics_rerun/ so they do not overwrite the original reported diagnostic CSV. The plotting script independently verifies the Queen islands and reuses existing LISA statistics; it does not retrain or change statistical estimates. Text CSVs use UTF-8/BOM except the unmodified assembled training input, which retains original bytes/encoding.

CONTENTS AND SCOPE
festival_predictions_B_剔除烟花.csv: supplied prediction version used downstream.
城市年面板_2023_2024.csv: regression covariates/exposure panel restricted to 2023–2024, with 625 city-year rows (291 in 2023; 334 in 2024), before model-specific missing-value exclusions. Values and row order are unchanged from the complete source panel. PM2.5, positive residual means and hourly counts were checked against predictions within rounding. The complete 2023–2025 panel is backed up outside this release. The hourly predictions and annual spatial-analysis inputs still include 2025 for Figure 2.
城市坐标.csv and shapefiles/: coordinates and administrative boundaries.
inputs/: socioeconomic source tables and city aggregate event/attention inputs.
raw/hourly/: assembled training input, not every original provider download.
code/: submitted-method derivatives, including training/NLP reference scripts and runnable downstream scripts 01–07.
results/: Global/Local Moran, GWR, OLS, Figure 2 and archived nested 10-fold summary.
The training and cross-validation were not rerun in this release. The nested-CV summary is an existing result. Raw social-media posts and complete independent manual validation labels were not located; city aggregates are supplied. Do not claim independent reproduction of the entire NLP pipeline.

OTHER METHODS
GWR uses log1p(Records), standardized pd/Green/NTL, adaptive Gaussian kernel and AICc bandwidth selection. Records==0 retains the submitted missing-value convention. Income and low-altitude policy counts are not included. OLS uses city-clustered standard errors. GWR diagnostics retain the original fixed bandwidths of 23 (2023) and 25 (2024).

RESIDUAL DIAGNOSTICS
results/gwr/gwr_diagnostics_log1p_records.csv is the original submitted diagnostic output, restored byte-for-byte, not regenerated output. It uses row-standardized spatial weights, 999 permutations, and original bandwidths 23/25. The original script does not fix a permutation seed; this calculation has been preserved. New executions may yield different permutation p-values and are saved separately in results/gwr/diagnostics_rerun/. The reported eight-neighbor residual tests have p=0.059 in 2023 and p=0.001 in 2024. Four-neighbor diagnostics and sensitivity results are also included in the original CSV.

CODE AUDIT
CODE_AUDIT.json records comparison against the submitted source. For scripts 00 (training), 01, 03, 04, 05 and 06, only package paths and the necessary CSV encoding adaptation remain; calculation logic matches the original. Notebook cell sources are unchanged. Queen LISA repairs and the corresponding Figure 2 drawing code are retained. Training and CV were not rerun.

DEPOSIT METADATA
Authors should supply repository DOI, article citation, authorship metadata, source citations and applicable input-data redistribution terms when depositing. This package does not impose a blanket license on third-party inputs. FILE_MANIFEST.csv records every included file except itself, with byte size and SHA-256. Earlier exploratory reconstructions and troubleshooting histories are archived outside this data folder.

FINAL INDEPENDENT VERIFICATION
See FINAL_VERIFICATION.json. Byte-identical original scripts 01/03/05/06 were executed against the study inputs in an isolated directory. Fourteen downstream tables agree, with maximum numeric difference below 5e-15. The original GWR diagnostic output and existing CV summary are byte-identical to their original files. Six years of Queen neighbor lists, local statistics, p-values and classifications were independently verified. An isolated Figure 2 redraw is byte-identical to the included PNG. No calculation settings or result files were altered by this verification. The manuscript/eproof needs the authorized corrected Figure 2 image, counts and island caption. Training and complete NLP validation are outside this check.

GITHUB LARGE FILE
raw/hourly/全部年份_完整地级单位.csv is 1,892,039,885 bytes and cannot be pushed as an ordinary GitHub Git object. Use Git LFS or a GitHub Release asset to distribute the full data package. Keep the file at the documented location when reproducing training. Official documentation: https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github and https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases .
