# Used Car Price Prediction — Data Science Lab Mini-Project

## Files
- `Used_Car_Price_Prediction.ipynb` — the complete notebook (run from top to bottom).
- `used_car_data.csv` — offline dataset included so the notebook needs no download.
- `Project_Report.md` — report draft aligned to the Data Science Lab syllabus.
- `requirements.txt` — Python libraries used.

## Important dataset note
The included dataset is **synthetic educational data** with Indian-market-like ranges, deliberate missing fields and duplicate rows for demonstrating cleaning. It is not real listing data and model predictions are not real market valuations. For a research or production use case, replace it with a properly licensed real listing dataset that has compatible columns.

## Run in Jupyter Notebook / JupyterLab
1. Upload this ZIP into your Jupyter environment and extract it.
2. Open the extracted `Used_Car_Price_Prediction.ipynb`.
3. Ensure `used_car_data.csv` is in the same folder (it is included in the ZIP).
4. Select a Python 3 kernel and choose **Run All**.
5. The final cells save `best_used_car_price_model.joblib` in the working folder.

## Run in Google Colab
1. Upload the ZIP to the Colab session.
2. Run this in a cell to extract it:

```python
from zipfile import ZipFile
with ZipFile('/content/Used_Car_Price_Prediction_Project.zip', 'r') as z:
    z.extractall('/content/Used_Car_Price_Prediction_Project')
%cd /content/Used_Car_Price_Prediction_Project
```
3. Open the notebook from the Colab file browser or upload the extracted `.ipynb`, then run all cells. If using a notebook already open in Colab, make sure the CSV is available in the current working folder.

## Libraries
Install if needed:

```bash
pip install -r requirements.txt
```

## Notes for presentation/viva
Be prepared to explain: data cleaning, missing-value imputation, one-hot encoding, Linear Regression, Random Forest, train/test split, MAE, RMSE, R², MAPE, hypothesis testing and limitations of synthetic data.
