cat > data/README.md << 'EOF'
# Data Sources

This repository does not track large raw data files due to GitHub size constraints.
Download and place them in the paths below before running any pipeline.

## Required files

### Geography
| File | Path | Source | Notes |
|------|------|--------|-------|
| `00mun.shp` (+ sidecar files) | `data/raw/geography/municipalities/` | [INEGI - Marco Geoestadístico](https://www.inegi.org.mx/app/biblioteca/ficha.html?upc=889463807469) | Municipal boundaries, EPSG:6372 |
| `lc_rep_mex_v_2024.shp` (+ sidecar files) | `data/raw/geography/mexico_land_polygon/` | [INEGI](https://www.inegi.org.mx) | Mexico land polygon 2024 |

### Logistics
| File | Path | Source | Notes |
|------|------|--------|-------|
| `via_ferrea.shp` (+ sidecar files) | `data/raw/logistics/railways_shp/` | [SCT / INEGI](https://www.inegi.org.mx) | National railway network |
| `rnc2025.gpkg` | `data/raw/logistics/highways_gpkg/` | [SCT - Red Nacional de Caminos](https://datos.gob.mx/busca/dataset/red-nacional-de-caminos) | National highway network 2025 |

### Resources
| File | Path | Source | Notes |
|------|------|--------|-------|
| `MEX_power-density_100m.tif` | `data/raw/resources/wind_density_tif/` | [Global Wind Atlas](https://globalwindatlas.info) | Wind power density at 100m, GeoTIFF |

### Security
| File | Path | Source | Notes |
|------|------|--------|-------|
| `Municipal-Delitos-2015-2025_abr2026.csv` | `data/raw/security/crime_rates_csv/` | [SESNSP](https://www.gob.mx/sesnsp/acciones-y-programas/datos-abiertos-de-incidencia-delictiva) | Municipal crime incidence 2015–2025, released April 2026 |

### Market
| File | Path | Source | Notes |
|------|------|--------|-------|
| `denue_inegi_31-33_.dbf` (+ sidecar files) | `data/raw/market/economic_units_locations_shp/` | [INEGI - DENUE](https://www.inegi.org.mx/app/mapa/denue/) | Economic units, manufacturing sector (SCIAN 31–33) |

## Notes
- All files should be placed exactly at the paths above; pipelines reference them by these locations.
- Coordinate system for shapefiles: EPSG:6372 (INEGI Lambert Conformal Conic) unless otherwise noted.
- The `data/processed/` directory is fully tracked by git.
EOF