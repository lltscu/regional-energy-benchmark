# Source attribution and data permissions

The file inventory records attribution by dataset family. The licenses of third-party spatial data are retained when their records or derived databases are redistributed. The original research code and numerical parameters do not replace these licenses.

## OpenStreetMap

Roads, mapped buildings, administrative spatial context, and databases derived from these records contain OpenStreetMap contributions. Attribution: **© OpenStreetMap contributors**. Database license: [Open Data Commons Open Database License 1.0](https://www.openstreetmap.org/copyright). Retain this attribution in maps and in redistributed spatial databases.

## GHSL built-up volume

Built-up volume inputs use the European Commission Joint Research Centre's Global Human Settlement Layer. The year 2025 is the product epoch and includes projected information; it is not a census of measured floor area. Product reference: **GHS-BUILT-V R2023A**, M. Pesaresi and P. Politis, 2023, [doi:10.2905/AB2F107A-03CD-47A3-85E5-139D8EC63283](https://doi.org/10.2905/AB2F107A-03CD-47A3-85E5-139D8EC63283). The regional volume summaries use total and nonresidential E2025 grids at 100 m, tile R7_C29, recorded in `fts/geography.py`.

Product records and derived volume summaries retain CC BY 4.0 attribution. The [GHSL citation instructions](https://human-settlement.emergency.copernicus.eu/GHSLhowToCite.php) additionally require the methodological reference: M. Pesaresi et al., "Advances on the Global Human Settlement Layer by joint assessment of Earth Observation and population survey data," *International Journal of Digital Earth*, vol. 17, no. 1, 2024. Partial OSM building-coverage metadata are recorded separately in `data/raw/building_coverage_status.json`.

## Weather

Hourly weather uses ERA5 reanalysis supplied through Open-Meteo. Attribution: **Open-Meteo; Copernicus Climate Change Service / ECMWF ERA5**. Distributed API data use CC BY 4.0 under [Open-Meteo's data terms](https://open-meteo.com/en/terms). Request coordinates, calendar, variables, retrieval metadata, and weather model are recorded in `data/raw/weather_source_status.json`.

## Land-cover constraints

Land-cover obstacle records are derived from ESA WorldCover 2021. Map attribution: **© ESA WorldCover project 2021 / Contains modified Copernicus Sentinel data (2021) processed by ESA WorldCover consortium**. Reference: D. Zanaga et al., "ESA WorldCover 10 m 2021 v200," 2022, [doi:10.5281/zenodo.7254221](https://doi.org/10.5281/zenodo.7254221). The source product is distributed under CC BY 4.0. Derived obstacle masks retain source attribution; their year is recorded separately from the 2025 demand calendar. See [ESA WorldCover data access and license information](https://esa-worldcover.org/en/data-access).

## Public planning and asset facts

Public government and operator sources support facility names, dates, rated quantities, land-use boundaries, and planning context. Source titles, publishers, dates, URLs, and extraction locators are recorded in `data/raw/public_source_registry.csv` and `data/reference_2025_v1/assets/canonical_source_registry.csv`.

These records are factual extractions and independently constructed numeric geometry or parameters. They do not grant a blanket license over the source publications, photographs, planning maps, logos, or illustrations. Original third-party publications and map images are not included in the release candidate. Direct source links are supplied for readers who need those materials. The file inventory marks source-specific derived material separately from openly licensed database content.

## Libraries

The package specifies scientific dependencies but does not redistribute their installed runtimes. NumPy, SciPy, NetworkX, Shapely, PyProj, Rasterio, pandapower, pandapipes, and other packages retain their own software licenses. Gurobi requires a separate valid user license.

## Original work

Original code: MIT (`LICENSE_CODE_MIT.txt`). Original parameters, documentation, and numeric results: CC BY 4.0, subject to the third-party database attribution and share-alike terms listed for each spatial dataset in `release/release_file_inventory.csv`.
