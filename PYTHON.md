# PYTHON

## MATH
### avoid division by zero
```python

with np.errstate(divide="ignore", invalid="ignore"):
    ndvi = (nir-red)/ (nir+red)
ndvi = ndvi.where(np.isfinite(ndvi))

with np.errstate(divide="ignore", invalid="ignore"):
    ndvi = np.true_divide((nir-red), (nir+red))
    ndvi[ndvi == np.inf] = 0
    ndvi = np.nan_to_num(ndvi) 
```