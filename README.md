# Radar Visibility Map

Compute radar line-of-sight coverage maps at multiple flight altitudes while accounting for terrain blocking and Earth curvature.

## What This Project Does

Given:
- Terrain elevation data (`Nice_Terrain_Data.npz`)
- A radar site location and height
- A list of target flight altitudes

the model computes visible vs. non-visible areas and exports:
- `vis_overlay_FL*.png` coverage overlays
- `radar_visibility.kmz` for visualization in Google Earth

## Repository Structure

- `Data_loading.py` - Loads terrain data, defines radar configuration, and prepares coordinate grids.
- `Radar_Visibility_Model.py` - Runs the visibility computation and exports PNG/KMZ outputs.
- `Nice_Terrain_Data.npz` - Terrain dataset used by the model.
- `requirements.txt` - Python dependencies.

## Requirements

- Python 3.9+

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run

From the project root:

```bash
python Radar_Visibility_Model.py
```

The script iterates through configured flight altitudes, prints timing per altitude, and generates output files in the same directory.

## Configuration

Edit values in `Data_loading.py`:

- Radar position: `lat_radar`, `lon_radar`
- Radar above-ground height (m): `radar_height`
- Target altitudes (m): `flight_levels`

Optional performance tuning in `Radar_Visibility_Model.py`:

- `samples_per_km`
- `min_samples`
- `max_samples`

## Outputs

- `vis_overlay_FL<altitude>.png`: Per-altitude visibility overlays.
- `radar_visibility.kmz`: Combined multi-layer result for Google Earth.

## Notes

- Keep `Nice_Terrain_Data.npz` in the project root unless you update the load path in `Data_loading.py`.
- Runtime depends on terrain grid size and sampling configuration.
