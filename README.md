# Basin Shape Ratio

This module computes a simple measure of basin elongation from a polygon and its river outlet.

It provides two ratios:
- Hydrology-based ratio: aligns the basin along the main flow direction (outlet → divide)
- PCA ratio: purely geometric, based on the basin shape

Data for the 100-largest (Hydrosheds LVL6) is summarized in ./data 

## Usage

```
pip install -r requirements.txt
```

```python
import pickle
from your_module import getBasin_ratio

# load data
with open("HS_basins_06.pkl", "rb") as f:
    data = pickle.load(f)

# example (adapt keys if needed)
shape = data["basin"]
network = data["network"]
outlet_id = data["outlet_id"]

result = getBasin_ratio(
    shape=shape,
    network=network,
    id=outlet_id
)

print(result["ratio"], result["ratio_pca"])
```

## Output

- ratio → elongation based on flow direction (0 ≈ square, >0 wider basins)  
- ratio_pca → elongation from geometry only  
- width_km, height_km → basin size  
- outlet_loc → outlet position across basin width  

## Notes

- Input geometry must be in WGS84 (EPSG:4326)  
- The outlet coordinates are read from the network (x, y)  
- Works for both Polygon and MultiPolygon  
