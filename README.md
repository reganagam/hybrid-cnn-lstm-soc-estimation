# 🔋 Lightweight Hybrid CNN-LSTM for Battery SoC Estimation

**Author:** Regan Agam (NIM: 24/PTK/552177/16439)[cite: 21]  
**Program:** Master's in Electrical Engineering, Universitas Gadjah Mada (UGM)[cite: 21]  
**Course:** Teknik Klasifikasi dan Pengenalan Pola (Pattern Recognition and Classification Techniques)

## 📌 Project Overview
Estimasi *State of Charge* (SoC) yang akurat adalah pilar fundamental dalam Sistem Manajemen Baterai (BMS) untuk kendaraan listrik (EV)[cite: 21]. Proyek ini mengusulkan dan mengevaluasi arsitektur *hybrid* CNN-LSTM yang ringkas untuk prediksi SoC[cite: 21]. Model dievaluasi melalui pendekatan ganda: sebagai tugas **Regresi** untuk memprediksi nilai kontinu, dan sebagai tugas **Klasifikasi** untuk menentukan rentang SoC baterai[cite: 21].

## 📊 Dataset & Preprocessing
Dataset yang digunakan adalah dataset primer *time-series* dari parameter operasional baterai[cite: 21].
*   **Total Data:** 186.715 baris data[cite: 22].
*   **Fitur Input (6 Fitur):** `voltage`, `current`, `temp 1`, `temp 2`, `temp 3`, `temp 4`[cite: 22].
*   **Variabel Target:** `SOC`[cite: 22].

**Preprocessing Pipeline:**
1.  **Normalisasi:** Seluruh fitur input dan target dinormalisasi ke rentang [0, 1] menggunakan `MinMaxScaler`[cite: 21].
2.  **Sequence Generation:** Data diubah menjadi sekuens yang tumpang tindih dengan panjang 10 *timesteps* untuk memprediksi nilai SoC berikutnya[cite: 21].
3.  **Data Split:** Dataset dibagi secara acak menjadi data latih (70%), data validasi (20%), dan data uji (10%)[cite: 21].

## 🧠 Model Architecture (Lightweight Design)
Model ini mengintegrasikan lapisan Conv1D untuk ekstraksi fitur spasial dan lapisan LSTM untuk menangkap dependensi temporal[cite: 21]. Arsitektur ini dirancang agar sangat efisien dengan total hanya **23.415 parameter**, menjadikannya solusi praktis untuk perangkat *edge* BMS[cite: 21].

![Arsitektur CNN-LSTM](assets/gambar.png)

*   **Input Layer:** Menerima sekuens data berdimensi (10, 6)[cite: 21].
*   **Conv1D Layer:** 64 filter, kernel size 3, aktivasi ReLU[cite: 21].
*   **LSTM Layer:** 50 unit, aktivasi ReLU[cite: 21].
*   **Dropout Layer:** Rate 0.2 untuk regularisasi[cite: 21].
*   **Dense Layer:** 1 neuron output[cite: 21].

## 📈 Results: Regression Performance
Evaluasi regresi menunjukkan tingkat akurasi yang luar biasa dalam memprediksi nilai kontinu SoC[cite: 21].

| Metric | Score |
| :--- | :---: |
| **Mean Squared Error (MSE)** | 0.0124[cite: 21] |
| **R-squared ($R^2$)** | 0.9870[cite: 21] |

### Training Dynamics
Kurva *validation loss* bergerak secara paralel dengan *training loss* dan mencapai konvergensi pada nilai yang sangat rendah tanpa indikasi *overfitting*[cite: 21].

![Training vs Validation Loss](assets/grafik1.png)

### Time-Series Prediction Tracking
Kurva prediksi berimpit hampir sempurna dengan kurva aktual, mengonfirmasi kemampuan model dalam melacak dinamika temporal seperti fase *charging* dan *discharging*[cite: 21].

![Actual vs Predicted SoC Time-Series](assets/grafik2.png)

### Prediction Consistency (Scatter Plot)
Titik data membentuk klaster yang sangat rapat di sepanjang garis diagonal, membuktikan korelasi kuat dan performa yang konsisten di seluruh rentang SoC (rendah, sedang, tinggi)[cite: 21].

![Actual vs Predicted SoC Scatter Plot](assets/grafik3.png)

## 📊 Results: Classification Performance
Kemampuan model juga dinilai dalam mengkategorikan status baterai ke dalam 5 kelas interval SoC secara otomatis[cite: 21]. 

| Metric | Score |
| :--- | :---: |
| **Accuracy** | 90.07%[cite: 21] |
| **Macro Avg Precision** | 0.9015[cite: 21] |
| **Macro Avg Recall** | 0.9007[cite: 21] |
| **Macro Avg F1-Score** | 0.8980[cite: 21] |

### Confusion Matrix
Sebagian besar prediksi berada di sepanjang diagonal utama (prediksi benar), dengan kesalahan klasifikasi minor yang hanya terjadi pada kelas-kelas yang saling berdekatan[cite: 21].

![Confusion Matrix](assets/cm.png)

## 💡 Key Engineering Insights
Mencapai akurasi $R^2$ sebesar 0.9870 pada regresi dan 90.07% pada klasifikasi dengan model berparameter sangat minim (~23k) membuktikan bahwa arsitektur Hybrid CNN-LSTM ini tidak hanya akurat secara prediktif, tetapi juga sangat efisien secara komputasional untuk aplikasi industri[cite: 21].

## 🚀 How to Run
1. Clone repository ini.
2. Buka `TKPP.ipynb` menggunakan Jupyter Notebook atau Google Colab untuk mengeksekusi *pipeline* pemrosesan data, arsitektur model, dan evaluasi grafis.
