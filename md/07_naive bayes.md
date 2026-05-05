# Analisis Data Menggunakan Naive Bayes

## 1. Pendahuluan

Naive Bayes merupakan metode klasifikasi berbasis probabilitas yang mengacu pada Teorema Bayes. Metode ini mengasumsikan bahwa setiap fitur bersifat independen terhadap fitur lainnya.

Metode ini banyak digunakan karena sederhana, cepat, dan memiliki performa yang cukup baik terutama pada dataset dengan fitur kategorikal.

## 2. Dasar Teori Naive Bayes

Naive Bayes merupakan metode klasifikasi yang menggunakan konsep probabilitas berdasarkan Teorema Bayes.

Rumus dasar Naive Bayes adalah sebagai berikut:

$$
P(C_i \mid X) = \frac{P(X \mid C_i) \cdot P(C_i)}{P(X)}
$$

### Keterangan:
- $P(C_i \mid X)$ : probabilitas kelas $C_i$ terhadap data $X$ (posterior)
- $P(X \mid C_i)$ : probabilitas data terhadap kelas (likelihood)
- $P(C_i)$ : probabilitas awal kelas (prior)
- $P(X)$ : probabilitas data

---

### Perhitungan Prior

Prior dihitung dengan rumus:

$$
P(C_i) = \frac{\text{jumlah data pada kelas } C_i}{\text{total data}}
$$

---

### Perhitungan Likelihood

Untuk data kategorikal, likelihood dihitung dengan:

$$
P(x_j \mid C_i) = \frac{\text{jumlah kemunculan } x_j \text{ pada } C_i}{\text{jumlah data pada } C_i}
$$

---

### Likelihood Gabungan

Karena Naive Bayes mengasumsikan independensi antar fitur, maka:

$$
P(X \mid C_i) = \prod_{j=1}^{n} P(x_j \mid C_i)
$$

---

### Perhitungan Posterior

Posterior dihitung dengan:

$$
P(C_i \mid X) \propto P(X \mid C_i) \cdot P(C_i)
$$

---

### Keputusan Klasifikasi

Kelas yang dipilih adalah kelas dengan nilai probabilitas tertinggi:

$$
\hat{C} = \arg\max_{C_i} \left[ P(X \mid C_i) \cdot P(C_i) \right]
$$

## 2. Dataset

Dataset yang digunakan adalah dataset Mushroom yang diperoleh dari Kaggle.

Dataset ini digunakan untuk mengklasifikasikan jamur menjadi dua kelas:
- Edible (e) → dapat dimakan
- Poisonous (p) → beracun

Seluruh fitur dalam dataset ini bersifat kategorikal, sehingga diperlukan proses encoding sebelum digunakan dalam model machine learning.

## 3. Import Data

Dataset dibaca menggunakan node **CSV Reader** pada KNIME.

![WhatsApp Image 2026-05-05 at 22.40.43.jpeg](5c7f5b93-20ce-41cd-a8f3-ab7677c5b2de.jpeg)

## 4. Penanganan Missing Value

Data kemudian diperiksa menggunakan node **Missing Value** untuk memastikan tidak terdapat nilai kosong.

Jika ditemukan missing value, maka dilakukan penanganan seperti penghapusan baris atau penggantian nilai.


![WhatsApp Image 2026-05-05 at 22.44.25.jpeg](f6888be0-4ed8-49a4-adcb-387e789c52fb.jpeg)

## 5. Implementasi Naive Bayes dengan Python

Pada tahap ini digunakan Python Script di KNIME untuk melakukan klasifikasi menggunakan metode Naive Bayes.

Tahapan yang dilakukan:
1. Mengambil data dari KNIME
2. Memisahkan fitur dan label
3. Encoding data kategorikal
4. Split data training dan testing
5. Training model
6. Prediksi dan evaluasi


```python
import knime.scripting.io as knio
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import OrdinalEncoder, LabelEncoder
from sklearn.naive_bayes import CategoricalNB
from sklearn.metrics import accuracy_score, classification_report

df = knio.input_tables[0].to_pandas()

X = df.drop("class", axis=1)
y = df["class"]

encoder = OrdinalEncoder()
X_encoded = encoder.fit_transform(X)

label_encoder = LabelEncoder()
y_encoded = label_encoder.fit_transform(y)

X_train, X_test, y_train, y_test = train_test_split(
    X_encoded, y_encoded, test_size=0.2, random_state=42
)

model = CategoricalNB()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
print("Accuracy:", accuracy)

print("\nClassification Report:\n", classification_report(y_test, y_pred))
```

## 6. Hasil dan Evaluasi

Berikut adalah hasil prediksi model:

![WhatsApp Image 2026-05-05 at 22.44.25.jpeg](d0540305-6de0-4ec4-9a67-8b9ec679a52d.jpeg)

Hasil evaluasi menunjukkan bahwa model memiliki akurasi yang tinggi, sehingga dapat digunakan untuk klasifikasi data dengan baik.

## 7. Analisis

Model Naive Bayes menunjukkan performa yang baik pada dataset ini karena seluruh fitur bersifat kategorikal.

Proses encoding memungkinkan data diproses oleh model tanpa menghilangkan informasi penting.

Namun, penggunaan OrdinalEncoder dapat memberikan urutan pada data kategorikal, sehingga dalam beberapa kasus dapat mempengaruhi hasil model.


## 8. Kesimpulan

Berdasarkan hasil analisis:

- Naive Bayes efektif digunakan untuk dataset kategorikal
- Model menghasilkan akurasi yang tinggi
- Dataset mushroom cocok untuk metode ini

Dengan demikian, metode Naive Bayes dapat digunakan sebagai solusi klasifikasi yang sederhana dan efisien.
