# V2X-QoS-Prediction
---

**📡 Overview**

Project ini bertujuan untuk memprediksi Quality of Service (QoS) pada komunikasi Vehicle-to-Everything (V2X) menggunakan pendekatan machine learning regression. Target prediksi berupa throughput jaringan (bps) yang merepresentasikan kualitas koneksi kendaraan terhadap jaringan seluler.

Pendekatan ini relevan untuk penerapan 5G/6G, smart cities, dan kendaraan otonom, di mana keterlambatan atau penurunan kualitas komunikasi dapat berdampak langsung pada keselamatan dan efisiensi sistem transportasi.

---

**🧠 Problem Statement**
Metode tradisional seperti:
- rule-based monitoring
- static thresholding
- tidak mampu menangani:
- lingkungan urban yang dinamis
- hubungan non-linear antar parameter jaringan
- variasi spasial-temporal kendaraan

Oleh karena itu, digunakan machine learning untuk memprediksi QoS secara proaktif.

---

**📊 Dataset**

Nama dataset: Berlin V2X Dataset
Lokasi: Berlin, Jerman
Sumber: Proyek AI4Mobile, didukung BMBF Germany
Metode pengambilan: Drive test di jalur nyata sepanjang 17.2 km
Mode pengujian:
- Platoon (11 putaran)
- 2x2 (6 putaran)

Teknologi jaringan:
- LTE (Vodafone & Deutsche Telekom)
- Sidelink (5.9 GHz, SDR)

---

**🧩 Features & Target**

- Target (Label)

Throughput (bps) yang merepresentasikan Quality of Service (QoS)

---

**Input Features**

1. Cellular Parameters
- PCell & SCell:
RSRP, RSRQ, RSSI, SNR, Downlink Num RBs, TB Size, Average MCS, Bandwidth, Carrier Frequency, dll

2. Environmental & Mobility

- GPS: Latitude, Longitude, Altitude, Speed (km/h), COG
- Weather: temperature, humidity, pressure, wind speed, rain
- Traffic Jam Factor
- Area type (Avenue, Park, Residential, Highway, Tunnel)

---

**🛠️ Data Preprocessing**

Langkah preprocessing utama:
- Drop Cell Identity (tidak informatif)
- Imputasi nilai kosong: SCell non-aktif → diisi 0, Bandwidth → mean conditional
- Outlier handling: Winsorization (0.1% – 99.9%)
- Encoding: One-hot encoding (device, area)
- Feature scaling: Standardization (mean = 0, std = 1)
- Custom preprocessing pipeline (end-to-end)

**⚙️ Feature Engineering**

Beberapa metrik jaringan yang diturunkan:
- SINR
- Shannon Capacity
- Doppler Spread
- Flat & Fast Fading
- Frequency Selective Fading

**🤖 Machine Learning Approach**

- Problem Type: Regression
- Individual Models: Elastic Net, Random Forest Regressor, MLP Regressor, XGBoost Regressor, LightGBM Regressor, CatBoost Regressor
- Hyperparameter Tuning: BayesSearchCV
- Evaluation metric: RMSE

---

**🧬 Stacking Model**

- Base Learners: XGBoost, LightGBM, CatBoost

- Meta Learners: Random Forest Regressor

---

**📈 Evaluation Metrics**

- RMSE
- MAE
- MAPE
- R² Score
(Target throughput diskalakan karena bernilai besar)

---

**🏆 Results**

- Best individual models: XGBoost, LightGBM, CatBoost
- Best overall model:
👉 Stacking Model dengan Random Forest sebagai Meta Learner

Final performance:
- RMSE ≈ 9.07
- MAPE ≈ 13.6%

---

**🚀 Use Cases**

- Prediksi area QoS rendah (terowongan, area padat bangunan)
- Optimasi penempatan RSU / repeater
- Network resource allocation secara proaktif
- Simulasi perencanaan kota berbasis V2X

**⚠️ Limitations & Future Work
Limitations**

- Dataset terbatas (subset dari data mentah)
- Keterbatasan komputasi
- Future Improvements
- Memproses raw dataset untuk skala besar

---

**👥 Contributors**

- Ardell Nurahim
- M. Rakha Saidina
