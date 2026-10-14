# Regional Integrated Energy Benchmark

**A Geospatially Constrained Benchmark for Joint Construction of Regional Integrated Energy Networks**

This package connects geographic channels, asset interfaces, service demands, electricity, gas, cooling, and communication components in one regional test system. It provides the selected network, its candidate domain, component parameters, chronological inputs, engineering results, executable reconstruction and evaluation tools, and an interactive GIS.

The reference contains **370 service objects** and **100 electricity, 44 gas, and 56 cooling source networks**. These source networks are research boundaries, not a count of observed utility stations. Of the service objects, 307 have cooling demand; 63 zero-demand geographic objects are retained without mandatory new facilities. Service-object counts and professional terminal-instance counts are recorded separately. Public asset observations, constructed interfaces, planning candidates, and selected professional connections have separate identifiers.

## Download and directory

Repository: <https://github.com/lltscu/regional-energy-benchmark>

The package version is **1.0.0**. Complete archives are distributed through the repository's Releases page. Extract the complete archive to a short D-drive path, for example `D:\RIES_Benchmark`. The tested command interface uses Windows and a D-drive Python interpreter.

| Directory | Content |
| --- | --- |
| `config/` | Registered model settings and the selected-reference pointer |
| `data/raw/` | Public factual records, spatial inputs, weather, and source records |
| `data/reference_2025_actual_calibration_v2/` | Active 2025 input revision and demand profiles |
| `data/reference_2025_v1/assets/` | Asset, equipment, year, and calculation mappings |
| `results/installation_construction/` | Candidate graph and the one selected system with its engineering results |
| `results/direct_construction/.../common/` | Fixed operating input catalogue used by the reconstruction |
| `fts/`, `joint/`, `annual_v2/`, `tools/` | Construction and evaluation implementation |
| `docs/` | Technical documentation, field guide, and operating instructions |
| `release/` | Version identity, reference metrics, file inventory, and numerical checks |
| `GIS.html` | Interactive local map |

The internal path labels identify immutable computational inputs. They do not define additional published benchmark systems. The published selection is identified by `config/active_finite_reference.json`.

## Quick start

Opening `GIS.html` displays the system without installing a solver. Layers distinguish public facilities, candidate channels, selected professional networks, and installation arrangements. Clicking an object displays its IDs and engineering attributes.

The following commands use an installed D-drive Python 3.12 interpreter. Replace the interpreter path if necessary.

```powershell
cd D:\RIES_Benchmark
& D:\Python312\python.exe -B ries.py check
& D:\Python312\python.exe -B ries.py summary
```

`check` verifies the packaged file inventory using the Python standard library. `summary` reports the selected-system identity and reference indicators. Neither requires an optimization license.

The lightweight release tests also use the standard library:

```powershell
& D:\Python312\python.exe -B -m unittest discover -s tests_release -v
```

## Computational environment

The tested environment uses Python 3.12.14, Gurobi 12.0.3, pandapower 3.3.3, pandapipes 0.14.0, NumPy 2.5.3, and SciPy 1.16.3. The complete tested dependency list is in `requirements-lock.txt`.

```powershell
& .\setup_environment.ps1 -Python D:\Python312\python.exe
$env:GRB_LICENSE_FILE = 'D:\Licenses\gurobi.lic'
```

The setup script places libraries, downloads, and temporary files under this package's D-drive `runtime/` directory. Gurobi construction and dispatch tasks require the user's own valid license. A requirements lock records the tested environment; this release preparation has not independently tested a fresh online installation of every locked dependency.

## Reconstruct and evaluate

```powershell
& D:\Python312\python.exe -B ries.py build --attempt-id reader_build_01
& D:\Python312\python.exe -B ries.py validate
& D:\Python312\python.exe -B ries.py run-year --attempt-id reader_year_01
```

`build` reconstructs the published decisions on the packaged candidate graph. It is a fixed-reference reconstruction, not a new free-topology optimization. `run-year` recomputes chronological dispatch, AC power flow, gas, cooling, and the communication energy requirements for the selected construction. To qualify a newly computed annual result, use its printed stage identifier:

```powershell
& D:\Python312\python.exe -B ries.py validate --year communication_operation_NEW_ID
```

Existing results are preserved. Use a fresh attempt identifier for a new calculation. Heavy computations run serially, use two solver threads, and apply a 60% available-memory budget. Resource failures, time limits, physical violations, and numerical non-convergence have distinct output states.

For `build`, exit code 4 means the graph was reconstructed but fixed-model verification was incomplete; inspect `reconstruction.json`. A resource limit does not establish infeasibility. The successful independent reconstruction used approximately 1.04 GB total working memory, with 0.57 GB additional working memory; a later archive check with only 0.53 GB available physical memory reached its 60% resource budget.

## GIS export

```powershell
& D:\Python312\python.exe -B ries.py export-gis --export-attempt reader_gis_01
& D:\Python312\python.exe -B ries.py export-gis --gis-id review_GIS_NEW_ID
```

The first command exports vector layers; the second produces the HTML browser for that printed GIS identifier. Map coordinates use WGS84; engineering distances and spatial inputs use the coordinate system recorded in each dataset, principally EPSG:32650. Spatial intersection does not establish a professional connection. Supply and return water connections remain distinct even when they share geometry.

## Reference checks

Independent D-drive reproduction reconstructed all 200 professional networks with the selected manifest unchanged, recomputed 8760 hours, passed 17 engineering gates, and passed **461 numerical comparisons covering 3,950,829 array elements**. The comparison tolerance is specified per metric in `release/numerical_comparison.csv`.

The minimum annual voltage is 0.956249 p.u.; the maximum device loading is 86.915943%; the actual 20-year line-related present value is CNY 10.628632 billion. The exact reference values and their source files are in `release/reference_metrics.json` and the technical documentation.

## Data and use

Read `docs/FIELD_GUIDE.md` and `docs/USAGE_CN.md` before changing demands, service assignments, or installation catalogues. The complete candidate domain and selected system are provided together so that the basis of each connection and specification can be inspected. New research tasks should use a new output directory and rerun the relevant physical checks.

Original code is licensed under MIT. Original parameters and documentation use CC BY 4.0. OpenStreetMap-derived databases retain ODbL 1.0; other third-party sources retain their applicable terms. See `THIRD_PARTY_NOTICES.md`, `LICENSE_CODE_MIT.txt`, `LICENSE_DATA.txt`, and `release/release_file_inventory.csv`.

For citation, use the release version and repository together. `CITATION.cff` supplies the title and authors; a published release identifier should be recorded when the public asset is available.
