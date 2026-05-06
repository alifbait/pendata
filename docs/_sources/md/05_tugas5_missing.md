# Proyek Missing Values Inputation + Materi Normalisasi data

## 1. Missing Values dengan Metode WKN

Missing values merupakan kondisi dimana terdapat data yang tidak tersedia atau kosong pada suatu atribut dalam dataset. Masalah ini sering terjadi pada proses pengumpulan data dan dapat mempengaruhi hasil analisis jika tidak ditangani dengan baik. Oleh karena itu, diperlukan metode untuk mengisi atau memperkirakan nilai yang hilang tersebut.

Salah satu metode yang dapat digunakan adalah Weighted K-Nearest Neighbor (WKNN). Metode ini merupakan pengembangan dari algoritma K-Nearest Neighbor (KNN) yang memberikan bobot pada setiap tetangga terdekat berdasarkan jaraknya terhadap data yang memiliki nilai hilang. Semakin dekat jarak suatu data terhadap data yang memiliki missing value, maka bobot yang diberikan akan semakin besar.

### Rumus Similarity pada WKNN:

$$
S_i = \frac{1}{\sum (Y_{ih} - Y_{jh})^2}
$$

#### Keterangan

- **$(S_i)$** : Nilai *similarity* (tingkat kemiripan) antara data yang memiliki *missing value* dengan data ke-$(i)$.  
  Nilai ini menunjukkan seberapa mirip kedua data tersebut.

- **$(Y_{ih})$** : Nilai atribut ke-$(h)$ pada data ke-$(i)$, yaitu data pembanding yang **tidak memiliki missing value**.

- **$(Y_{jh})$** : Nilai atribut ke-$(h)$ pada data ke-$(j)$ yang **memiliki missing value**.

### Rumus Perhitungan Nilai Imputasi

Setelah nilai *similarity* diperoleh, nilai imputasi dihitung menggunakan rata-rata berbobot sebagai berikut:

$$
\hat{y}_{ih} =
\frac{\sum_{j \in IK_{ih}} s_i(y_j)\, y_{jh}}
{\sum_{j \in IK_{ih}} s_i(y_j)}
$$

#### Keterangan

- **$\hat{y}_{ih}$** : Nilai estimasi atau imputasi untuk atribut ke-$h$ pada data ke-$i$ yang memiliki *missing value*.

- **$y_{jh}$** : Nilai atribut ke-$h$ pada data ke-$j$ yang digunakan sebagai tetangga terdekat.

- **$s_i(y_j)$** : Nilai *similarity* (tingkat kemiripan) antara data yang memiliki *missing value* dengan data tetangga ke-$j$.

- **$IK_{ih}$** : Himpunan $k$ tetangga terdekat (*nearest neighbors*) yang dipilih untuk memperkirakan nilai atribut ke-$h$ pada data ke-$i$.

### Dataset yang digunakan:

Pada proses perhitungan missing value menggunakan metode WKNN dalam Data Mining, digunakan dataset Boston Housing Dataset yang diperoleh dari platform Kaggle. Dataset ini berisi informasi mengenai berbagai faktor yang mempengaruhi harga rumah di wilayah Boston, seperti tingkat kriminalitas, jumlah kamar, tingkat pajak properti, serta faktor lingkungan lainnya. Dataset tersebut terdiri dari beberapa atribut numerik yang dapat digunakan untuk melakukan analisis dan perhitungan jarak antar data. Dalam penelitian ini, dataset housingdata digunakan sebagai contoh data untuk melakukan proses perhitungan similarity dan imputasi nilai yang hilang menggunakan metode Weighted K-Nearest Neighbor (WKNN).

Dataset dapat diakses melalui tautan berikut: 
https://www.kaggle.com/datasets/uciml/red-wine-quality-cortez-et-al-2009

Penjelasan pada setiap kolom di Dataset tersebut:

| Kolom | Keterangan |
|------|-------------|
| fixed_acidity | Tingkat keasaman tetap pada wine yang berasal dari asam organik seperti tartaric acid. |
| volatile_acidity | Kandungan asam yang mudah menguap pada wine. Nilai terlalu tinggi dapat menyebabkan aroma seperti cuka. |
| citric_acid | Kandungan asam sitrat dalam wine yang dapat memberikan rasa segar dan meningkatkan stabilitas rasa. |
| residual_sugar | Jumlah gula yang tersisa setelah proses fermentasi selesai. |
| chlorides | Konsentrasi garam (natrium klorida) dalam wine. |
| free_sulfur_dioxide | Jumlah sulfur dioksida bebas dalam wine yang berfungsi sebagai antioksidan dan antibakteri. |
| total_sulfur_dioxide | Total sulfur dioksida dalam wine, termasuk yang bebas dan yang terikat. |
| density | Kepadatan cairan wine yang dipengaruhi oleh kandungan gula dan alkohol. |
| pH | Tingkat keasaman atau kebasaan wine pada skala pH. |
| sulphates | Kandungan senyawa sulfat dalam wine yang dapat meningkatkan stabilitas dan kualitas rasa. |
| alcohol | Persentase kandungan alkohol dalam wine. |
| quality | Nilai kualitas wine berdasarkan penilaian sensorik (biasanya pada skala 0–10). |


### Perhitungan dengan menggunakan metode WKNN secara manual

#### - Pengecekan Missing Value pada Dataset

Tahap awal dalam proses ini adalah mengidentifikasi apakah terdapat data yang memiliki nilai hilang (*missing value*).  
Pada dataset **Wine Quality**, dilakukan pengecekan terhadap seluruh atribut untuk memastikan apakah terdapat nilai yang kosong atau tidak.

Berdasarkan hasil pengecekan, dataset ini **tidak memiliki missing value**, sehingga seluruh data dapat langsung digunakan dalam proses analisis. Namun, proses pengecekan tetap perlu dilakukan sebagai langkah awal dalam *data preprocessing* untuk memastikan kualitas data sebelum dilakukan perhitungan lebih lanjut menggunakan metode **Weighted K-Nearest Neighbor (WKNN)**.

#### - Menentukan Kolom yang Akan Dinormalisasi

Tahap normalisasi data dilakukan untuk menyamakan skala antar atribut sebelum menghitung nilai *similarity*.  
Normalisasi penting karena setiap atribut memiliki rentang nilai yang berbeda, sehingga tanpa normalisasi atribut dengan nilai besar dapat mendominasi proses perhitungan jarak.

Kolom yang dinormalisasi pada dataset **Wine Quality** adalah atribut yang memiliki nilai numerik sebagai berikut:

- fixed_acidity
- volatile_acidity
- citric_acid
- residual_sugar
- chlorides
- free_sulfur_dioxide
- total_sulfur_dioxide
- density
- pH
- sulphates
- alcohol

Kolom **quality** tidak dinormalisasi karena digunakan sebagai **variabel target** yang merepresentasikan kualitas wine berdasarkan hasil penilaian sensorik.

#### - Normalisasi Data

Normalisasi data dilakukan untuk menyamakan skala antar atribut sehingga setiap variabel memiliki rentang nilai yang sebanding.  
Hal ini penting sebelum menghitung nilai *similarity* pada metode **Weighted K-Nearest Neighbor (WKNN)**, karena atribut dengan rentang nilai besar dapat mendominasi perhitungan jarak.

Pada penelitian ini digunakan metode **Min-Max Normalization** dengan rumus sebagai berikut:

$$
x' = \frac{x - x_{min}}{x_{max} - x_{min}}
$$

Keterangan:

- $x$ : nilai data asli  
- $x_{min}$ : nilai minimum pada suatu atribut  
- $x_{max}$ : nilai maksimum pada suatu atribut  
- $x'$ : nilai hasil normalisasi

Berikut contoh beberapa nilai dari dataset **Wine Quality** sebelum dilakukan normalisasi:

| fixed_acidity | volatile_acidity | citric_acid | residual_sugar | chlorides | free_sulfur_dioxide | total_sulfur_dioxide | density | pH | sulphates | alcohol |
|---------------|------------------|-------------|----------------|-----------|---------------------|----------------------|--------|----|-----------|---------|
| 7.4 | 0.70 | 0.00 | 1.9 | 0.076 | 11 | 34 | 0.9978 | 3.51 | 0.56 | 9.4 |
| 7.8 | 0.88 | 0.00 | 2.6 | 0.098 | 25 | 67 | 0.9968 | 3.20 | 0.68 | 9.8 |
| 7.8 | 0.76 | 0.04 | 2.3 | 0.092 | 15 | 54 | 0.9970 | 3.26 | 0.65 | 9.8 |

Berikut contoh nilai data setelah dilakukan proses normalisasi:

| fixed_acidity | volatile_acidity | citric_acid | residual_sugar | chlorides | free_sulfur_dioxide | total_sulfur_dioxide | density | pH | sulphates | alcohol |
|---------------|------------------|-------------|----------------|-----------|---------------------|----------------------|--------|----|-----------|---------|
| 0.247 | 0.397 | 0.000 | 0.068 | 0.107 | 0.140 | 0.098 | 0.567 | 0.606 | 0.137 | 0.153 |
| 0.283 | 0.521 | 0.000 | 0.116 | 0.164 | 0.338 | 0.246 | 0.494 | 0.338 | 0.214 | 0.215 |
| 0.283 | 0.438 | 0.024 | 0.095 | 0.149 | 0.197 | 0.187 | 0.508 | 0.390 | 0.195 | 0.215 |

Nilai hasil normalisasi berada pada rentang **0 sampai 1**, sehingga setiap atribut memiliki skala yang sama dan dapat digunakan secara adil dalam proses perhitungan *similarity* pada metode **WKNN**.

#### - Menghitung Similarity

Setelah proses normalisasi selesai dilakukan, tahap berikutnya adalah menghitung nilai *similarity* antar data.  
Perhitungan ini bertujuan untuk mengetahui tingkat kemiripan antara data yang memiliki nilai yang ingin diprediksi dengan data lainnya pada dataset **Wine Quality**.

Dalam penelitian ini, nilai *similarity* dihitung menggunakan pendekatan berbasis jarak Euclidean yang kemudian diubah menjadi nilai kemiripan menggunakan rumus berikut:

$$
S_i = \frac{1}{\sum (Y_{ih} - Y_{jh})^2}
$$

Keterangan:

- $S_i$ : Nilai similarity antara data yang dibandingkan  
- $Y_{ih}$ : Nilai atribut ke-$h$ pada data ke-$i$  
- $Y_{jh}$ : Nilai atribut ke-$h$ pada data ke-$j$  

Perhitungan dilakukan menggunakan atribut numerik pada dataset Wine Quality, yaitu:

- fixed_acidity
- volatile_acidity
- citric_acid
- residual_sugar
- chlorides
- free_sulfur_dioxide
- total_sulfur_dioxide
- density
- pH
- sulphates
- alcohol

Berikut contoh hasil perhitungan nilai *similarity* antara data yang dibandingkan dengan beberapa data lainnya pada dataset:

| Si |
|----|
| 0.083214 |
| 0.146782 |
| 0.219534 |
| 0.964812 |

Nilai similarity yang lebih besar menunjukkan bahwa dua data memiliki tingkat kemiripan yang lebih tinggi.  
Nilai-nilai tersebut kemudian digunakan untuk menentukan **tetangga terdekat (nearest neighbors)** dalam proses perhitungan menggunakan metode **Weighted K-Nearest Neighbor (WKNN)**.

#### - Menghitung Penyebut ($\sum S_i$)

Setelah nilai *similarity* antar data pada dataset **Wine Quality** dihitung, langkah berikutnya adalah menjumlahkan seluruh nilai similarity tersebut.  
Penjumlahan ini digunakan untuk mendapatkan nilai penyebut pada rumus imputasi metode **Weighted K-Nearest Neighbor (WKNN)**.

Nilai similarity dihitung antara satu data wine yang menjadi data acuan dengan beberapa data wine lainnya pada dataset berdasarkan atribut numerik berikut:

- fixed_acidity
- volatile_acidity
- citric_acid
- residual_sugar
- chlorides
- free_sulfur_dioxide
- total_sulfur_dioxide
- density
- pH
- sulphates
- alcohol

Sebagai contoh, setelah menghitung similarity antara satu data wine dengan empat data wine terdekat lainnya pada dataset, diperoleh nilai sebagai berikut:

$$
S_1 = 0.083214
$$

$$
S_2 = 0.146782
$$

$$
S_3 = 0.219534
$$

$$
S_4 = 0.964812
$$

Nilai similarity tersebut kemudian dijumlahkan untuk mendapatkan nilai penyebut:

$$
\sum S_i = 0.083214 + 0.146782 + 0.219534 + 0.964812
$$

Sehingga diperoleh:

$$
\sum S_i = 1.414342
$$

Nilai $\sum S_i$ ini kemudian digunakan sebagai **penyebut pada rumus imputasi WKNN**, yang berfungsi untuk menormalisasi bobot dari setiap tetangga terdekat sebelum menghitung nilai estimasi pada atribut yang memiliki nilai hilang.

#### - Menghitung Pembilang ($S_i \times Y_{jh}$)

Selanjutnya dihitung perkalian antara nilai *similarity* dengan nilai atribut dari tetangga terdekat pada dataset **Wine Quality**.

Perhitungan ini dilakukan untuk mendapatkan nilai pembilang pada rumus imputasi metode **Weighted K-Nearest Neighbor (WKNN)**.

Rumus perkalian:

$$
S_i \times Y_{jh}
$$

Keterangan:

- $S_i$ : Nilai similarity antara data acuan dengan data ke-$i$  
- $Y_{jh}$ : Nilai atribut ke-$h$ pada data tetangga ke-$j$

Berikut contoh hasil perkalian antara nilai similarity dengan nilai atribut dari beberapa tetangga terdekat:

| $S_i$ | $Y_{jh}$ | $S_i \times Y_{jh}$ |
|------|------|------|
| 0.083214 | 0.421 | 0.035044 |
| 0.146782 | 0.563 | 0.082637 |
| 0.219534 | 0.318 | 0.069813 |
| 0.964812 | 0.105 | 0.101305 |

Setiap hasil perkalian tersebut kemudian dijumlahkan untuk memperoleh nilai pembilang:

$$
\sum (S_i \times Y_{jh})
$$

Sehingga diperoleh:

$$
\sum (S_i \times Y_{jh}) = 0.288799
$$

Nilai pembilang ini selanjutnya digunakan dalam proses perhitungan nilai estimasi atau imputasi pada metode **Weighted K-Nearest Neighbor (WKNN)** dengan membagi jumlah pembilang dengan jumlah nilai similarity ($\sum S_i$).

#### - Hasil Nilai Imputasi

Nilai imputasi diperoleh dengan membagi jumlah pembilang dengan jumlah penyebut yang telah dihitung sebelumnya pada metode **Weighted K-Nearest Neighbor (WKNN)**.

Rumus imputasi:

$$
\hat{y}_{ih} =
\frac{\sum (S_i \times Y_{jh})}{\sum S_i}
$$

Berdasarkan hasil perhitungan sebelumnya diperoleh:

- Jumlah pembilang

$$
\sum (S_i \times Y_{jh}) = 0.288799
$$

- Jumlah penyebut

$$
\sum S_i = 1.414342
$$

Sehingga nilai imputasi dapat dihitung sebagai berikut:

$$
\hat{y}_{ih} =
\frac{0.288799}{1.414342}
$$

Hasil nilai imputasi yang diperoleh adalah:

$$
\hat{y}_{ih} = 0.20417
$$

Nilai tersebut merupakan nilai estimasi untuk atribut yang memiliki *missing value* pada data yang dianalisis di dataset **Wine Quality** menggunakan metode **Weighted K-Nearest Neighbor (WKNN)**.

### Perhitungan WKNN Menggunakan Python

Setelah menggunakan Microsoft Excel untuk perhitungan manual, proses imputasi missing value juga diterapkan melalui pemrograman Python. Pendekatan ini digunakan untuk memastikan keakuratan hasil perhitungan serta mempermudah proses pengolahan dataset.

#### 1. Mengunggah Dataset

Dataset diunggah ke Google Colab kemudian dibaca menggunakan library pandas pada Python. Setelah itu data ditampilkan untuk melihat isi dataset yang akan digunakan.


```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler
from sklearn.metrics import pairwise_distances

df = pd.read_csv("winequality-red.csv")

df = df.replace("?", np.nan)
df = df.apply(pd.to_numeric)

print("Data Awal:")
print(df)
```

    Data Awal:
          fixed acidity  volatile acidity  citric acid  residual sugar  chlorides  \
    0               7.4             0.700         0.00             1.9      0.076   
    1               7.8             0.880         0.00             2.6      0.098   
    2               7.8             0.760         0.04             2.3      0.092   
    3              11.2             0.280         0.56             1.9      0.075   
    4               7.4             0.700         0.00             1.9      0.076   
    ...             ...               ...          ...             ...        ...   
    1594            6.2             0.600         0.08             2.0      0.090   
    1595            5.9             0.550         0.10             2.2      0.062   
    1596            6.3             0.510         0.13             2.3      0.076   
    1597            5.9             0.645         0.12             2.0      0.075   
    1598            6.0             0.310         0.47             3.6      0.067   
    
          free sulfur dioxide  total sulfur dioxide  density    pH  sulphates  \
    0                    11.0                  34.0  0.99780  3.51       0.56   
    1                    25.0                  67.0  0.99680  3.20       0.68   
    2                    15.0                  54.0  0.99700  3.26       0.65   
    3                    17.0                  60.0  0.99800  3.16       0.58   
    4                    11.0                  34.0  0.99780  3.51       0.56   
    ...                   ...                   ...      ...   ...        ...   
    1594                 32.0                  44.0  0.99490  3.45       0.58   
    1595                 39.0                  51.0  0.99512  3.52       0.76   
    1596                 29.0                  40.0  0.99574  3.42       0.75   
    1597                 32.0                  44.0  0.99547  3.57       0.71   
    1598                 18.0                  42.0  0.99549  3.39       0.66   
    
          alcohol  quality  
    0         9.4        5  
    1         9.8        5  
    2         9.8        5  
    3         9.8        6  
    4         9.4        5  
    ...       ...      ...  
    1594     10.5        5  
    1595     11.2        6  
    1596     11.0        6  
    1597     10.2        5  
    1598     11.0        6  
    
    [1599 rows x 12 columns]
    

#### 2. Menentukan Kolom yang akan di Normalisasi

Pada tahap ini ditentukan atribut yang akan digunakan dalam proses normalisasi.


```python
cols_norm = [
'fixed acidity','volatile acidity','citric acid','residual sugar',
'chlorides','free sulfur dioxide','total sulfur dioxide',
'density','pH','sulphates','alcohol'
]

min_val = df[cols_norm].min()
max_val = df[cols_norm].max()

print("MIN VALUE : ")
print(min_val)
print(30*'=')
print("MAX VALUE : ")
print(max_val)
```

    MIN VALUE : 
    fixed acidity           4.60000
    volatile acidity        0.12000
    citric acid             0.00000
    residual sugar          0.90000
    chlorides               0.01200
    free sulfur dioxide     1.00000
    total sulfur dioxide    6.00000
    density                 0.99007
    pH                      2.74000
    sulphates               0.33000
    alcohol                 8.40000
    dtype: float64
    ==============================
    MAX VALUE : 
    fixed acidity            15.90000
    volatile acidity          1.58000
    citric acid               1.00000
    residual sugar           15.50000
    chlorides                 0.61100
    free sulfur dioxide      72.00000
    total sulfur dioxide    289.00000
    density                   1.00369
    pH                        4.01000
    sulphates                 2.00000
    alcohol                  14.90000
    dtype: float64
    

#### 3. Normalisasi Data

Normalisasi dilakukan dengan menggunakan metode Min-Max Normalization


```python
df_norm = df.copy()

for col in cols_norm:
    df_norm[col] = (df[col] - min_val[col]) / (max_val[col] - min_val[col])

print("DATA SETELAH NORMALISASI")
print(df_norm)

df_norm.loc[0, 'alcohol'] = np.nan
```

    DATA SETELAH NORMALISASI
          fixed acidity  volatile acidity  citric acid  residual sugar  chlorides  \
    0          0.247788          0.397260         0.00        0.068493   0.106845   
    1          0.283186          0.520548         0.00        0.116438   0.143573   
    2          0.283186          0.438356         0.04        0.095890   0.133556   
    3          0.584071          0.109589         0.56        0.068493   0.105175   
    4          0.247788          0.397260         0.00        0.068493   0.106845   
    ...             ...               ...          ...             ...        ...   
    1594       0.141593          0.328767         0.08        0.075342   0.130217   
    1595       0.115044          0.294521         0.10        0.089041   0.083472   
    1596       0.150442          0.267123         0.13        0.095890   0.106845   
    1597       0.115044          0.359589         0.12        0.075342   0.105175   
    1598       0.123894          0.130137         0.47        0.184932   0.091820   
    
          free sulfur dioxide  total sulfur dioxide   density        pH  \
    0                0.140845              0.098940  0.567548  0.606299   
    1                0.338028              0.215548  0.494126  0.362205   
    2                0.197183              0.169611  0.508811  0.409449   
    3                0.225352              0.190813  0.582232  0.330709   
    4                0.140845              0.098940  0.567548  0.606299   
    ...                   ...                   ...       ...       ...   
    1594             0.436620              0.134276  0.354626  0.559055   
    1595             0.535211              0.159011  0.370778  0.614173   
    1596             0.394366              0.120141  0.416300  0.535433   
    1597             0.436620              0.134276  0.396476  0.653543   
    1598             0.239437              0.127208  0.397944  0.511811   
    
          sulphates   alcohol  quality  
    0      0.137725  0.153846        5  
    1      0.209581  0.215385        5  
    2      0.191617  0.215385        5  
    3      0.149701  0.215385        6  
    4      0.137725  0.153846        5  
    ...         ...       ...      ...  
    1594   0.149701  0.323077        5  
    1595   0.257485  0.430769        6  
    1596   0.251497  0.400000        6  
    1597   0.227545  0.276923        5  
    1598   0.197605  0.400000        6  
    
    [1599 rows x 12 columns]
    

#### 4. Menentukan data yang Memiliki Missing Value

Tahap ini melakukan identifikasi data yang memiliki nilai kosong pada atribut alcohol.


```python
missing_index = df_norm[df_norm['alcohol'].isna()].index

row_missing = df_norm.loc[missing_index].drop(columns=['alcohol']).iloc[0]

complete_data = df_norm.dropna()
```

#### 5. Menghitung Nilai Similarity ($S_i$)


```python
Si = []
Yjh = []

for i in range(len(complete_data)):

    row = complete_data.iloc[i].drop('alcohol')

    diff = (row_missing - row) ** 2
    sum_diff = diff.sum()

    if sum_diff == 0:
        similarity = 0
    else:
        similarity = 1 / sum_diff

    Si.append(similarity)
    Yjh.append(complete_data.iloc[i]['alcohol'])

Si = np.array(Si)
Yjh = np.array(Yjh)

print("Nilai Si :", Si)
```

    Nilai Si : [ 7.00695894 16.86940241  0.62447889 ...  0.86984737  6.18099727
      0.72823315]
    

#### 6. Menghitung Penyebut

Penyebut diperoleh dari jumlah seluruh nilai similarity.


```python
penyebut = np.sum(Si)

print("Penyebut:")
print(penyebut)
```

    Penyebut:
    7160.466680220721
    

#### 7. Menghitung Pembilang

Pembilang diperoleh dari hasil perkalian similarity dengan nilai atribut tetangga.


```python
Si_Yjh = Si * Yjh

print("Si * Yjh:", Si_Yjh)

pembilang = np.sum(Si_Yjh)

print("Pembilang:")
print(pembilang)
```

    Si * Yjh: [1.50919116 3.63340975 0.13450314 ... 0.34793895 1.71166078 0.29129326]
    Pembilang:
    1601.1560812392804
    

#### 8. Menghitung Nilai Imputasi

Nilai imputasi dihitung menggunakan rumus Weighted K-Nearest


```python
hasil = pembilang / penyebut

print("Hasil Akhir:", hasil)
```

    Hasil Akhir: 0.22361057634164214
    

Nilai yang diperoleh dari proses imputasi digunakan untuk menggantikan data yang hilang pada atribut LSTAT, sehingga dataset menjadi utuh dan dapat diproses lebih lanjut.

## 2. Normalisasi Data

Dalam Data Mining, normalisasi data adalah salah satu teknik persiapan data (data preprocessing) yang digunakan untuk mengubah atau menyesuaikan skala nilai pada data numerik agar berada pada rentang atau skala yang sama. Proses ini bertujuan agar setiap atribut dalam dataset memiliki pengaruh yang seimbang ketika diproses oleh algoritma dalam machine learning atau data mining. Normalisasi penting dilakukan karena dalam sebuah dataset sering terdapat perbedaan rentang nilai yang cukup besar antar atribut, sehingga dengan normalisasi proses analisis dapat menjadi lebih akurat dan efektif.

### Macam-Macam Normalisasi Data

#### 1. Min-Max Normalization

Dalam Data Mining, normalisasi Min-Max merupakan metode yang digunakan untuk mengubah nilai data numerik ke dalam rentang tertentu, biasanya pada interval [0,1]. Proses ini dilakukan dengan memanfaatkan nilai minimum dan maksimum dari suatu atribut, kemudian setiap nilai data disesuaikan agar berada pada skala baru yang telah ditentukan.

Berikut rumus dari Min-Max Normalization:

$$
v' = \frac{v - min_A}{max_A - min_A}
$$

##### Keterangan:

- **v** = nilai asli data  
- **v'** = nilai setelah normalisasi  
- **minA** = nilai minimum atribut A  
- **maxA** = nilai maksimum atribut A  

---

#### Contoh: Menggunakan data dari dataset Wine Quality pada kolom **alcohol**

| alcohol |
|--------|
| 9.4 |
| 9.8 |
| 9.8 |

Nilai minimum dan maksimum dari data tersebut adalah:

- Minimum = **9.4**
- Maksimum = **9.8**

---

#### Langkah perhitungan

##### Data ke-1 = 9.4

$$
v' = \frac{9.4 - 9.4}{9.8 - 9.4}
$$

$$
v' = \frac{0}{0.4}
$$

$$
v' = 0
$$

---

##### Data ke-2 = 9.8

$$
v' = \frac{9.8 - 9.4}{9.8 - 9.4}
$$

$$
v' = \frac{0.4}{0.4}
$$

$$
v' = 1
$$

---

##### Data ke-3 = 9.8

$$
v' = \frac{9.8 - 9.4}{9.8 - 9.4}
$$

$$
v' = \frac{0.4}{0.4}
$$

$$
v' = 1
$$

---

#### Hasil Normalisasi

| alcohol | alcohol Normalisasi |
|-------|----------------|
| 9.4 | 0 |
| 9.8 | 1 |
| 9.8 | 1 |

#### 2. Z-Score Normalization

Z-Score Normalization merupakan metode normalisasi yang mengubah nilai suatu atribut berdasarkan rata-rata (mean) dan simpangan baku (standard deviation) dari atribut tersebut. Metode ini sering digunakan ketika normalisasi min–max kurang sesuai, misalnya ketika nilai minimum dan maksimum tidak diketahui atau ketika dataset mengandung outlier. Pada metode ini, setiap nilai data dihitung dengan cara mengurangi nilai tersebut dengan rata-rata atribut, kemudian dibagi dengan simpangan baku. Hasil transformasi ini membuat data memiliki rata-rata 0 dan simpangan baku 1.

Berikut rumus dari Z-score Normalization:

#### 1. Rumus Z-Score Normalization

\[
v' = \frac{v - \bar{A}}{\sigma_A}
\]

**Keterangan:**

- \(v\) = nilai asli data  
- \(v'\) = nilai setelah normalisasi  
- \(\bar{A}\) = rata-rata (mean) dari atribut A  
- \(\sigma_A\) = standar deviasi dari atribut A  

---

#### 2. Rumus Menghitung Mean (Rata-rata)

\[
\mu = \frac{1}{n} \sum_{i=1}^{n} v_i
\]

**Keterangan:**

- \(\mu\) = nilai rata-rata (mean)  
- \(n\) = jumlah data  
- \(v_i\) = nilai data ke-i  

---

#### 3. Rumus Menghitung Standar Deviasi

\[
\sigma = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(v_i - \mu)^2}
\]

**Keterangan:**

- \(\sigma\) = standar deviasi  
- \(\mu\) = rata-rata data  
- \(v_i\) = nilai data ke-i  
- \(n\) = jumlah data  

---

#### Contoh: Menggunakan data dari dataset **Wine Quality** pada kolom **alcohol**

| alcohol |
|------|
| 9.4 |
| 9.8 |
| 9.8 |

---

#### Menghitung Mean (Rata-rata)

\[
\mu = \frac{9.4 + 9.8 + 9.8}{3}
\]

\[
\mu = \frac{29}{3}
\]

\[
\mu = 9.67
\]

---

#### Menghitung Standar Deviasi

Hitung selisih kuadrat tiap data terhadap mean:

\[
(9.4 - 9.67)^2 = 0.0729
\]

\[
(9.8 - 9.67)^2 = 0.0169
\]

\[
(9.8 - 9.67)^2 = 0.0169
\]

Jumlahkan:

\[
0.0729 + 0.0169 + 0.0169 = 0.1067
\]

Bagi jumlah data:

\[
\frac{0.1067}{3} = 0.0356
\]

Ambil akar:

\[
\sigma = \sqrt{0.0356}
\]

\[
\sigma = 0.189
\]

---

#### Menghitung Nilai Z-Score

Mean = **9.67**  
Standar deviasi = **0.189**

---

#### Perhitungan Data ke-1

\[
v' = \frac{9.4 - 9.67}{0.189}
\]

\[
v' = \frac{-0.27}{0.189}
\]

\[
v' = -1.43
\]

---

#### Perhitungan Data ke-2

\[
v' = \frac{9.8 - 9.67}{0.189}
\]

\[
v' = \frac{0.13}{0.189}
\]

\[
v' = 0.69
\]

---

#### Perhitungan Data ke-3

\[
v' = \frac{9.8 - 9.67}{0.189}
\]

\[
v' = \frac{0.13}{0.189}
\]

\[
v' = 0.69
\]

---

#### Hasil Normalisasi

| alcohol | alcohol Normalisasi |
|------|------------------|
| 9.4 | -1.43 |
| 9.8 | 0.69 |
| 9.8 | 0.69 |

#### 3. Decimal Scaling Normalization

Dalam Data Mining, decimal scaling normalization merupakan metode normalisasi yang dilakukan dengan mengubah nilai atribut numerik melalui pergeseran titik desimal. Proses ini dilakukan dengan membagi setiap nilai data dengan pangkat sepuluh tertentu, sehingga nilai absolut dari data menjadi lebih kecil.

Tujuan dari metode ini adalah agar nilai absolut terbesar dalam atribut menjadi lebih kecil dari 1 setelah proses transformasi dilakukan. Besarnya pembagi ditentukan oleh nilai \(j\), yaitu bilangan bulat terkecil yang membuat nilai maksimum dari atribut tersebut berada di bawah 1 setelah dibagi dengan \(10^j\). Metode decimal scaling termasuk teknik normalisasi yang sederhana dan mudah diterapkan karena hanya memerlukan operasi pembagian tanpa mengubah pola hubungan antar nilai dalam dataset.

Berikut rumus dari Decimal Scaling Normalization:

\[
v' = \frac{v}{10^j}
\]

**Keterangan:**

- \(v\) = nilai asli data  
- \(v'\) = nilai setelah normalisasi  
- \(j\) = bilangan bulat terkecil yang membuat nilai maksimum data menjadi kurang dari 1  
- \(10^j\) = faktor pembagi untuk menggeser titik desimal  

---

#### Contoh: Menggunakan data dari dataset Wine Quality pada kolom **alcohol**

| alcohol |
|------|
| 9.4 |
| 9.8 |
| 9.8 |

---

- Menentukan nilai maksimum  
  Nilai terbesar dari data adalah **9.8**

- Menentukan nilai \(j\)  
  Nilai \(j\) dipilih sehingga nilai maksimum setelah dibagi \(10^j\) menjadi kurang dari 1.  

  Karena nilai maksimum memiliki **1 digit sebelum desimal**, maka:

\[
j = 1
\]

- Melakukan normalisasi  

Karena \(j = 1\), maka setiap data dibagi dengan **10**

---

#### Perhitungan

| alcohol | Perhitungan | Hasil |
|------|------|------|
| 9.4 | 9.4 / 10 | 0.94 |
| 9.8 | 9.8 / 10 | 0.98 |
| 9.8 | 9.8 / 10 | 0.98 |

---

#### Hasil Normalisasi

| alcohol | alcohol Normalisasi |
|------|------|
| 9.4 | 0.94 |
| 9.8 | 0.98 |
| 9.8 | 0.98 |

### Contoh Normalisasi Data Menggunnakan SK_Learn

Normalisasi data juga dapat dilakukan menggunakan library scikit-learn pada bahasa pemrograman Python. Library ini menyediakan berbagai fungsi yang memudahkan proses normalisasi data, seperti Min-Max Normalization dan Z-Score Normalization. Dengan menggunakan scikit-learn, proses normalisasi dapat dilakukan secara otomatis tanpa perlu menghitung rumus secara manual, sehingga lebih efisien dan meminimalkan kesalahan dalam perhitungan pada analisis Data Mining.

#### 1. Min-Max Normalization

Contoh: Menggunakan data dari dataset **Wine Quality** pada kolom **alcohol**

#### 1. Min-Max Normalization

Contoh: Menggunakan data dari dataset Wine Quality pada kolom alcohol

| alcohol |
|------|
| 9.4 |
| 9.8 |
| 9.8 |

Penyelesaian dengan menggunakan kode python:


```python
import numpy as np
from sklearn.preprocessing import MinMaxScaler

X = np.array([[28.7],
              [22.9],
              [27.1]])

scaler = MinMaxScaler(feature_range=(0,1))

normalized = scaler.fit_transform(X)

print("Data setelah normalisasi:")
print(normalized)
```

    Data setelah normalisasi:
    [[1.        ]
     [0.        ]
     [0.72413793]]
    

Normalisasi data dilakukan menggunakan metode Min-Max Normalization dengan bantuan library scikit-learn pada Python. Proses normalisasi dilakukan menggunakan fungsi MinMaxScaler() yang mengubah nilai data ke dalam rentang 0 sampai 1. Dari hasil normalisasi terlihat bahwa nilai terkecil menjadi 0 dan nilai terbesar menjadi 1, sehingga semua data berada pada skala yang sama.



#### 2. Z-Score Normalization

Contoh: Menggunakan data dari dataset Wine Quality pada kolom alcohol

| alcohol |
|------|
| 9.4 |
| 9.8 |
| 9.8 |

Penyelesaian dengan menggunakan kode python:


```python
import numpy as np
from sklearn.preprocessing import StandardScaler

X = np.array([[9.4],
              [9.8],
              [9.8]])

scaler = StandardScaler()

X_zscore = scaler.fit_transform(X)

print("Z-Score Normalization:")
print(X_zscore)
```

    Z-Score Normalization:
    [[-1.41421356]
     [ 0.70710678]
     [ 0.70710678]]
    

Pada metode Z-Score Normalization, normalisasi dilakukan dengan menggunakan nilai rata-rata (mean) dan simpangan baku (standard deviation) dari dataset. Berdasarkan hasil normalisasi menggunakan library scikit-learn, nilai data yang berada di bawah rata-rata memiliki nilai negatif, sedangkan nilai yang berada di atas rata-rata memiliki nilai positif. Setelah proses normalisasi dilakukan, data menjadi terstandarisasi dengan rata-rata mendekati 0 sehingga distribusi data menjadi lebih seimbang untuk proses analisis lebih lanjut.

#### 3. Decimal Scaling Normalization

Contoh: Menggunakan data dari dataset Wine Quality pada kolom alcohol

| alcohol |
|------|
| 9.4 |
| 9.8 |
| 9.8 |

Penyelesaian dengan menggunakan kode python:


```python
import numpy as np

X = np.array([[9.4],
              [9.8],
              [9.8]])

def decimal_scaling(X):
    max_val = np.max(np.abs(X))
    j = len(str(int(max_val)))
    return X / (10 ** j)

decimal = decimal_scaling(X)

print("Decimal Scaling Normalization:")
print(decimal)
```

    Decimal Scaling Normalization:
    [[0.94]
     [0.98]
     [0.98]]
    

Pada metode Decimal Scaling Normalization, normalisasi dilakukan dengan cara membagi nilai data menggunakan pangkat sepuluh tertentu (10^j) sehingga nilai maksimum data menjadi lebih kecil dari 1. Berdasarkan hasil normalisasi, nilai data yang semula berkisar antara 9.4 hingga 9.8 berubah menjadi 0.094 hingga 0.098. Perubahan ini tidak mengubah hubungan antar data, tetapi hanya mengubah skala nilainya menjadi lebih kecil sehingga data menjadi lebih mudah digunakan dalam proses analisis pada Data Mining.

Ringkasan Hasilnya:

| Nilai asli | Min-Max Normalization | Z-Score Normalization | Decimal Scaling Normalization |
|------|------|------|------|
| 9.4 | 0 | -1.43 | 0.094 |
| 9.8 | 1 | 0.69 | 0.098 |
| 9.8 | 1 | 0.69 | 0.098 |

Pada contoh ini dilakukan normalisasi data menggunakan beberapa metode normalisasi dalam Data Mining, yaitu Min-Max Normalization, Z-Score Normalization, dan Decimal Scaling Normalization. Proses normalisasi dilakukan menggunakan library scikit-learn untuk metode Min-Max dan Z-Score, sedangkan metode Decimal Scaling dibuat menggunakan fungsi sendiri dalam Python. Hasil normalisasi menunjukkan bahwa setiap metode mengubah skala data dengan cara yang berbeda, namun tujuan utamanya adalah membuat data berada pada skala yang lebih seragam sehingga memudahkan proses analisis data.
