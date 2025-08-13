[README gitub bike sharing.md](https://github.com/user-attachments/files/21740920/README.gitub.bike.sharing.md)

## **Bike-Share Demand Forecasting**
---


Prediksi jumlah peminjam sepeda per jam untuk optimasi armada & layanan pelanggan.
---

 Proyek ini membangun pipeline ML end-to-end (EDA → preprocessing → modeling → tuning → XAI) 
 **Tujuan**
Memprediksi cnt (jumlah penyewa/jam) agar alokasi sepeda, rebalancing stasiun, dan penjadwalan staf lebih tepat.

Menjelaskan permintaan (jam, kalender, cuaca) dengan Explainable AI.

**Target**: cnt (kontinu, ≥0)

**Fitur inti:** 
- waktu (hr, dayofweek, is_weekend, year, month, season, week), cuaca (temp, hum, weathersit), libur (holiday).

 **Metodologi**

- Preprocessing: Simple Imputer (median), binning (hum,temp), encoding (OHE/ordinal), optional RobustScaler.

- Model: CatBoostRegressor menggunakan TransformedTargetRegressor (log target → train, exp → prediksi).

- Validasi & Tuning: 5-fold CV + RandomizedSearchCV hanya di train, evaluasi final di test.

 Hasil Utama (Test Set)
| Metric | Before Tuning | After Tuning |
|--------|--------------|--------------|
| MAE    | 28.07        | 16.90        |
| RMSE   | 47.42        | 28.60        |
| R²     | 0.930        | 0.975        |
| MAPE   | 0.261        | 0.120        |

Inti: Akurasi meningkat signifikan; model stabil pada data tak terlihat dan siap dipakai operasional.

**Explainability (XAI)**

- Global: Permutation Importance, SHAP summary → key drivers: hr (jam), kalender (weekend/dayofweek/year), temp (+), weathersit/hum (−).

**Implikasi Bisnis**

- Perencanaan lebih presisi per jam/hari untuk armada, rebalancing, dan shift staf.

- pengalaman pelanggan meningkat (stok habis & antrean menurun), potensi utilisasi & pendapatan naik.

**Exportn Model**

- Model di simpan dalam bentuk joblib ('model_bikesharing_capstone3.joblib')

 Sumber

Data set bike sharing from https://www.kaggle.com/datasets/lakshmi25npathi/bike-sharing-dataset

