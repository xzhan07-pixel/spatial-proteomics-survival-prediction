# Spatial Proteomics-Based Cancer Survival Prediction

The project uses a CNN for feature extraction from 52-channel proteomics images and Random Forest regression for survival-time prediction.

Obtain permission from the authorized data provider before sharing or using original data outside the course. The supplied notebook expects data placed locally as follows:

```
data/
  train/train_data.csv
  train/images/1.tiff ...
  test/images/226.tiff ...
```

The public repository should **not** contain `data/` or notebook outputs from the original dataset.

## How to run with authorized data

1. Install the versions listed in `requirements.txt` in an environment compatible with your Python/TensorFlow installation.
2. Put authorized course data under `data/train` and `data/test` as shown above.
3. Start Jupyter from this repository folder and run `analysis.ipynb` from top to bottom.

## Methods

- Read 52-channel TIFF image intensities; rescale each channel of each image between its 1st and 99th percentiles, convert to `uint8`, and retain the original `/255.0` operation.
- Randomly reserve 20 patients as a holdout validation set.
- Fit a three-convolutional-layer CNN using survival month labels.
- Extract flattened CNN features and train 100-tree Random Forest regression.
- Report MAE/MSE on the holdout set and plot observed vs. predicted survival.
- Generate predictions for the 56 independent test images if provided.

## Notes

The source TIFF can be floating-point. The code explicitly creates an intermediate `uint8` representation before dividing by 255, and does not rewrite the original TIFFs. Per-image intensity scaling preserves spatial patterns but may remove cross-patient absolute intensity information; results require validation before biological interpretation.

The research is exploratory and should not be interpreted as a clinically validated prognostic model. No real-data performance metrics are asserted in the public notebook. The notebook requires authorized datasets and has not been executed in the public code package.
