# Perhitungan Jarak Data Campuran


```python
from sqlalchemy import create_engine
import pandas as pd

engine = create_engine(
    "postgresql+psycopg2://postgres:123@127.0.0.1:5432/titanic"
)

df = pd.read_sql('SELECT * FROM public."titanic_data";', engine)

df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>passengerid</th>
      <th>survived</th>
      <th>pclass</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



## Penjelasan

Kode di atas digunakan untuk menghubungkan Python dengan database PostgreSQL serta mengambil data dari tabel yang ada di dalam database tersebut.

Pada baris pertama dilakukan import library yang diperlukan, yaitu **SQLAlchemy** dan **Pandas**. Library SQLAlchemy digunakan untuk membuat koneksi antara Python dengan database PostgreSQL, sedangkan Pandas digunakan untuk membaca dan mengolah data dalam bentuk DataFrame.

Selanjutnya dibuat sebuah koneksi ke database menggunakan fungsi `create_engine()`. Pada bagian ini dimasukkan informasi koneksi berupa **username**, **password**, **alamat host**, **port**, serta **nama database**. Dalam contoh ini Python terhubung ke database PostgreSQL bernama **titanic** yang berada pada alamat lokal (`127.0.0.1`) dengan port **5432**.

Setelah koneksi berhasil dibuat, data diambil dari tabel **titanic_data** menggunakan perintah SQL:

`SELECT * FROM public."titanic_data"`

Perintah tersebut berarti mengambil seluruh data (`*`) dari tabel **titanic_data** yang berada pada schema **public** di dalam database PostgreSQL.

Data yang diambil dari database kemudian dibaca oleh Pandas menggunakan fungsi `pd.read_sql()` dan disimpan ke dalam variabel **df** dalam bentuk **DataFrame**.

Terakhir, fungsi `df.head()` digunakan untuk menampilkan **5 baris pertama dari dataset Titanic**. Tujuan dari langkah ini adalah untuk melihat struktur awal data yang meliputi atribut seperti **passengerid, survived, pclass, name, sex, age, sibsp, parch, ticket, fare, dan cabin** sehingga memudahkan proses analisis data pada tahap selanjutnya.


```python
print("\nInfo Dataset:")
df.info()

print("\nUkuran Dataset (baris, kolom):")
print(df.shape)
```

    
    Info Dataset:
    <class 'pandas.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   passengerid  891 non-null    int64  
     1   survived     891 non-null    int64  
     2   pclass       891 non-null    int64  
     3   name         891 non-null    str    
     4   sex          891 non-null    str    
     5   age          714 non-null    float64
     6   sibsp        891 non-null    int64  
     7   parch        891 non-null    int64  
     8   ticket       891 non-null    str    
     9   fare         891 non-null    float64
     10  cabin        204 non-null    str    
     11  embarked     889 non-null    str    
    dtypes: float64(2), int64(5), str(5)
    memory usage: 83.7 KB
    
    Ukuran Dataset (baris, kolom):
    (891, 12)
    

## Penjelasan

Kode tersebut digunakan untuk menghubungkan Python dengan database PostgreSQL serta mengambil data dari tabel yang terdapat di dalam database tersebut agar dapat diolah menggunakan library Pandas.

Pada bagian awal kode dilakukan proses **import library** yang dibutuhkan, yaitu `create_engine` dari library **SQLAlchemy** dan library **Pandas**. Library SQLAlchemy digunakan untuk membuat koneksi antara Python dan database PostgreSQL, sedangkan Pandas digunakan untuk membaca data dari database dan mengelolanya dalam bentuk **DataFrame** sehingga lebih mudah untuk dianalisis.

Selanjutnya dibuat sebuah objek koneksi menggunakan fungsi `create_engine()`. Pada bagian ini dimasukkan informasi koneksi berupa **username**, **password**, **alamat host**, **port**, serta **nama database**. Dalam kode tersebut, Python terhubung dengan database PostgreSQL menggunakan user **postgres** dengan password **123**, yang berada pada alamat lokal **127.0.0.1** dengan port **5432**, serta mengakses database bernama **titanic**.

Setelah koneksi berhasil dibuat, data diambil dari database menggunakan fungsi `pd.read_sql()`. Pada fungsi tersebut digunakan perintah SQL:

`SELECT * FROM public."titanic_data"`

Perintah tersebut berarti mengambil seluruh data (`*`) dari tabel **titanic_data** yang berada pada schema **public** di dalam database PostgreSQL. Data yang diambil kemudian disimpan ke dalam variabel **df** dalam bentuk **DataFrame**.

Terakhir, fungsi `df.head()` digunakan untuk menampilkan **5 baris pertama dari dataset Titanic**. Tujuan dari langkah ini adalah untuk melihat gambaran awal dataset yang berisi atribut seperti **passengerid, survived, pclass, name, sex, age, sibsp, parch, ticket, fare, cabin, dan embarked**, sehingga memudahkan dalam memahami struktur data sebelum dilakukan proses analisis lebih lanjut.


```python
print("\nJumlah class:")
print(df['pclass'].nunique())

print("\nJumlah data per class:")
print(df['pclass'].value_counts())
```

    
    Jumlah class:
    3
    
    Jumlah data per class:
    pclass
    3    491
    1    216
    2    184
    Name: count, dtype: int64
    

## Penjelasan

Kode tersebut digunakan untuk mengetahui jumlah kelas yang terdapat pada dataset serta menghitung jumlah data pada setiap kelas yang ada.

Pada baris pertama digunakan perintah `print("\nJumlah class:")` untuk menampilkan judul output agar hasil yang ditampilkan lebih mudah dipahami dan terstruktur.

Selanjutnya, fungsi `df['pclass'].nunique()` digunakan untuk menghitung **jumlah nilai unik** pada kolom **pclass**. Kolom `pclass` pada dataset Titanic merepresentasikan kelas tiket penumpang kapal, yaitu **kelas 1 (First Class), kelas 2 (Second Class), dan kelas 3 (Third Class)**. Fungsi `nunique()` akan menghitung berapa banyak kategori kelas yang berbeda pada kolom tersebut.

Setelah itu, perintah `print("\nJumlah data per class:")` digunakan untuk menampilkan judul kedua sebelum menampilkan hasil perhitungan jumlah data pada masing-masing kelas.

Kemudian fungsi `df['pclass'].value_counts()` digunakan untuk menghitung **jumlah kemunculan setiap nilai pada kolom `pclass`**. Fungsi ini akan menampilkan berapa banyak penumpang yang berada pada masing-masing kelas tiket.

Hasil yang diperoleh menunjukkan bahwa dataset Titanic memiliki **3 kelas penumpang**, dengan distribusi data sebagai berikut:
- Kelas 3 memiliki 491 penumpang
- Kelas 1 memiliki 216 penumpang
- Kelas 2 memiliki 184 penumpang

Informasi ini berguna untuk memahami distribusi data pada dataset sebelum dilakukan analisis lebih lanjut, seperti analisis pola data atau perhitungan jarak antar data pada tahap berikutnya.


```python
# CEK MISSING VALUES
print("\nMissing values per kolom:")
print(df.isnull().sum())

print("\nTotal missing values:")
print(df.isnull().sum().sum())
```

    
    Missing values per kolom:
    passengerid      0
    survived         0
    pclass           0
    name             0
    sex              0
    age            177
    sibsp            0
    parch            0
    ticket           0
    fare             0
    cabin          687
    embarked         2
    dtype: int64
    
    Total missing values:
    866
    

## Penjelasan

Kode tersebut digunakan untuk memeriksa apakah terdapat **data yang hilang (missing values)** pada dataset. Pemeriksaan missing values penting dilakukan sebelum proses analisis data karena data yang kosong dapat mempengaruhi hasil analisis atau perhitungan yang dilakukan.

Pada baris pertama digunakan perintah `print("\nMissing values per kolom:")` untuk menampilkan judul output agar hasil yang ditampilkan lebih terstruktur dan mudah dibaca.

Selanjutnya digunakan fungsi `df.isnull().sum()` untuk menghitung jumlah nilai kosong pada setiap kolom di dalam dataset. Fungsi `isnull()` akan memeriksa setiap nilai dalam dataframe dan mengembalikan nilai **True** jika data tersebut kosong (NULL) dan **False** jika data tersedia. Kemudian fungsi `sum()` digunakan untuk menjumlahkan seluruh nilai True pada setiap kolom sehingga diperoleh jumlah data yang hilang pada masing-masing atribut.

Setelah itu, perintah `print("\nTotal missing values:")` digunakan untuk menampilkan judul kedua sebelum menampilkan jumlah total data yang hilang pada seluruh dataset.

Terakhir, fungsi `df.isnull().sum().sum()` digunakan untuk menghitung **jumlah keseluruhan missing values** pada dataset. Fungsi `sum()` pertama menjumlahkan missing values pada setiap kolom, sedangkan fungsi `sum()` kedua menjumlahkan seluruh hasil tersebut sehingga diperoleh total data yang hilang dalam dataset.

Informasi mengenai missing values ini sangat penting untuk menentukan langkah selanjutnya dalam proses analisis data, seperti melakukan **data cleaning**, **menghapus data yang kosong**, atau **mengisi nilai yang hilang (imputation)** agar dataset siap digunakan pada tahap analisis berikutnya.


```python
# CEK DATA DUPLIKAT
print("\nJumlah data duplikat:")
print(df.duplicated().sum())
```

    
    Jumlah data duplikat:
    0
    

## Penjelasan

Kode tersebut digunakan untuk memeriksa apakah terdapat **data duplikat** pada dataset. Pemeriksaan data duplikat merupakan salah satu langkah penting dalam proses **data cleaning**, karena data yang berulang dapat mempengaruhi hasil analisis dan menyebabkan perhitungan menjadi tidak akurat.

Pada baris pertama digunakan perintah `print("\nJumlah data duplikat:")` untuk menampilkan judul output sehingga hasil yang ditampilkan lebih jelas dan terstruktur.

Selanjutnya digunakan fungsi `df.duplicated().sum()` untuk menghitung jumlah baris data yang memiliki nilai duplikat. Fungsi `duplicated()` akan memeriksa setiap baris pada dataframe dan mengembalikan nilai **True** jika baris tersebut merupakan duplikat dari baris sebelumnya, dan **False** jika data tersebut unik. Setelah itu fungsi `sum()` digunakan untuk menjumlahkan seluruh nilai **True**, sehingga diperoleh jumlah total data yang duplikat dalam dataset.

Berdasarkan hasil output yang ditampilkan, jumlah data duplikat pada dataset adalah **0**, yang berarti tidak terdapat baris data yang berulang. Hal ini menunjukkan bahwa dataset sudah cukup bersih dari masalah duplikasi data dan dapat digunakan untuk proses analisis selanjutnya tanpa perlu melakukan penghapusan data duplikat.


```python
# STATISTIK DESKRIPTIF
print("\nStatistik deskriptif:")
display(df.describe())
```

    
    Statistik deskriptif:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>passengerid</th>
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>714.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>446.000000</td>
      <td>0.383838</td>
      <td>2.308642</td>
      <td>29.699118</td>
      <td>0.523008</td>
      <td>0.381594</td>
      <td>32.204208</td>
    </tr>
    <tr>
      <th>std</th>
      <td>257.353842</td>
      <td>0.486592</td>
      <td>0.836071</td>
      <td>14.526497</td>
      <td>1.102743</td>
      <td>0.806057</td>
      <td>49.693429</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.420000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>223.500000</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>20.125000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.910400</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>446.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>28.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>14.454200</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>668.500000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>38.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>891.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>80.000000</td>
      <td>8.000000</td>
      <td>6.000000</td>
      <td>512.329200</td>
    </tr>
  </tbody>
</table>
</div>


## Penjelasan

Kode tersebut digunakan untuk menampilkan **statistik deskriptif** dari dataset. Statistik deskriptif bertujuan untuk memberikan gambaran umum mengenai distribusi data numerik sebelum dilakukan analisis lebih lanjut.

Pada baris pertama digunakan perintah `print("\nStatistik deskriptif:")` untuk menampilkan judul output sehingga hasil yang ditampilkan lebih terstruktur dan mudah dipahami.

Selanjutnya digunakan fungsi `df.describe()` untuk menghitung berbagai ukuran statistik pada kolom numerik dalam dataset. Fungsi ini akan menampilkan beberapa informasi penting, antara lain:

- **count** : jumlah data yang tersedia pada setiap kolom  
- **mean** : nilai rata-rata dari data pada kolom tersebut  
- **std** : standar deviasi yang menunjukkan tingkat penyebaran data  
- **min** : nilai minimum pada kolom  
- **25%** : kuartil pertama (Q1) atau nilai di mana 25% data berada di bawah nilai tersebut  
- **50%** : median atau nilai tengah dari data  
- **75%** : kuartil ketiga (Q3) atau nilai di mana 75% data berada di bawah nilai tersebut  
- **max** : nilai maksimum pada kolom

Pada kode tersebut digunakan fungsi `display()` agar hasil dari `df.describe()` dapat ditampilkan dalam bentuk tabel yang lebih rapi di Jupyter Notebook.

Dari hasil statistik deskriptif tersebut dapat diperoleh gambaran mengenai karakteristik dataset Titanic, seperti rata-rata usia penumpang, distribusi kelas tiket penumpang, serta variasi harga tiket (**fare**). Informasi ini membantu dalam memahami pola dasar data sebelum dilakukan proses analisis lanjutan seperti pengolahan data, perhitungan jarak data, atau pemodelan data.


```python
import numpy as np
import pandas as pd

# One-hot encoding
df_encoded = pd.get_dummies(df, drop_first=True)

# Ubah semua ke float
df_encoded = df_encoded.astype(float)

# Ambil 2 baris
p = df_encoded.iloc[0].values
q = df_encoded.iloc[1].values

# Hitung jarak
d_e = np.linalg.norm(p - q)
d_m = np.sum(np.abs(p - q))

print(f"Euclidean: {d_e:.4f}")
print(f"Manhattan: {d_m:.4f}")
```

    Euclidean: 66.1004
    Manhattan: 91.0333
    

## Penjelasan

Kode tersebut digunakan untuk melakukan **encoding data kategorikal** serta menghitung **jarak antar dua data** menggunakan metode **Euclidean Distance** dan **Manhattan Distance**.

Pada bagian awal dilakukan proses import library yang dibutuhkan yaitu **NumPy** dan **Pandas**. Library NumPy digunakan untuk melakukan operasi matematika dan perhitungan jarak antar data, sedangkan Pandas digunakan untuk mengolah dataset dalam bentuk DataFrame.

Selanjutnya dilakukan proses **One-Hot Encoding** menggunakan fungsi `pd.get_dummies()`. Encoding ini bertujuan untuk mengubah data kategorikal menjadi data numerik agar dapat digunakan dalam perhitungan matematis. Parameter `drop_first=True` digunakan untuk menghindari terjadinya **multicollinearity** dengan menghilangkan satu kategori dari setiap variabel kategorikal.

Setelah proses encoding selesai, seluruh data kemudian diubah menjadi tipe **float** menggunakan fungsi `astype(float)`. Hal ini dilakukan agar semua nilai dalam dataset memiliki tipe data numerik yang seragam sehingga dapat digunakan dalam proses perhitungan jarak.

Pada langkah berikutnya diambil **dua baris data pertama** dari dataset yang telah diencoding menggunakan `iloc`. Baris pertama disimpan dalam variabel **p**, sedangkan baris kedua disimpan dalam variabel **q**. Kedua baris ini kemudian diubah menjadi array menggunakan `.values` agar dapat diproses oleh fungsi matematika dari NumPy.

Selanjutnya dilakukan perhitungan jarak antara dua data tersebut menggunakan dua metode yang berbeda:

- **Euclidean Distance** dihitung menggunakan fungsi `np.linalg.norm(p - q)`. Metode ini menghitung jarak garis lurus antara dua titik dalam ruang multidimensi.
- **Manhattan Distance** dihitung menggunakan `np.sum(np.abs(p - q))`. Metode ini menghitung jumlah selisih absolut dari setiap atribut antara dua data.

Terakhir, hasil perhitungan jarak ditampilkan menggunakan fungsi `print()`. Nilai jarak Euclidean dan Manhattan ditampilkan dengan format empat angka di belakang koma menggunakan format `{:.4f}`.

Hasil tersebut menunjukkan seberapa besar perbedaan antara dua data penumpang pada dataset Titanic berdasarkan atribut yang telah diencoding.


```python
import numpy as np
import pandas as pd

# Ambil 2 data
data_1 = df.iloc[0]
data_2 = df.iloc[1]

# ==============================
# KELOMPOK TIPE DATA
# ==============================

kolom_numerik = ['age','sibsp','parch','fare']

kolom_ordinal = ['pclass']

kolom_nominal = ['sex','embarked']

kolom_binary = ['survived']

# ==============================
# VARIABEL RUMUS GOWER
# ==============================

jumlah_jarak = 0.0
jumlah_delta = 0

# ==============================
# NOMINAL
# ==============================

for kolom in kolom_nominal:
    if pd.notna(data_1[kolom]) and pd.notna(data_2[kolom]):
        jarak = 0 if data_1[kolom] == data_2[kolom] else 1
        jumlah_jarak += jarak
        jumlah_delta += 1

# ==============================
# BINARY
# ==============================

for kolom in kolom_binary:
    if pd.notna(data_1[kolom]) and pd.notna(data_2[kolom]):
        jarak = 0 if data_1[kolom] == data_2[kolom] else 1
        jumlah_jarak += jarak
        jumlah_delta += 1

# ==============================
# ORDINAL
# ==============================

for kolom in kolom_ordinal:
    
    min_val = df[kolom].min()
    max_val = df[kolom].max()
    
    if max_val != min_val:
        z1 = (data_1[kolom] - min_val) / (max_val - min_val)
        z2 = (data_2[kolom] - min_val) / (max_val - min_val)
        
        jarak = abs(z1 - z2)
        jumlah_jarak += jarak
        jumlah_delta += 1

# ==============================
# NUMERIK
# ==============================

for kolom in kolom_numerik:
    if pd.notna(data_1[kolom]) and pd.notna(data_2[kolom]):
        
        min_val = df[kolom].min()
        max_val = df[kolom].max()
        
        if max_val != min_val:
            jarak = abs(data_1[kolom] - data_2[kolom]) / (max_val - min_val)
            jumlah_jarak += jarak
            jumlah_delta += 1

# ==============================
# HASIL AKHIR
# ==============================

jarak_campuran = jumlah_jarak / jumlah_delta

print("Hasil Perhitungan Jarak Data Campuran")
print("-------------------------------------")
print("Total penjumlahan seluruh nilai jarak tiap atribut =", jumlah_jarak)
print("Jumlah atribut yang ikut dihitung =", jumlah_delta)
print("Nilai akhir jarak campuran antara data 1 dan data 2 =", jarak_campuran)

if jarak_campuran < 0.3:
    print("Interpretasi: Kedua data sangat mirip.")
elif jarak_campuran < 0.6:
    print("Interpretasi: Kedua data cukup mirip.")
else:
    print("Interpretasi: Kedua data berbeda cukup jauh.")
```

    Hasil Perhitungan Jarak Data Campuran
    -------------------------------------
    Total penjumlahan seluruh nilai jarak tiap atribut = 4.326040219413797
    Jumlah atribut yang ikut dihitung = 8
    Nilai akhir jarak campuran antara data 1 dan data 2 = 0.5407550274267247
    Interpretasi: Kedua data cukup mirip.
    

## Penjelasan

Kode tersebut digunakan untuk menghitung **jarak data campuran (mixed data distance)** antara dua data menggunakan konsep **Gower Distance**. Metode ini digunakan ketika dataset memiliki berbagai tipe data seperti **numerik, ordinal, nominal, dan binary**.

### Normalisasi Data Ordinal

Pada atribut ordinal, nilai data terlebih dahulu dinormalisasi menggunakan rumus berikut:

$$
z = \frac{x - min}{max - min}
$$

Normalisasi ini bertujuan untuk mengubah nilai ordinal menjadi rentang **0 sampai 1**, sehingga perhitungan jarak dapat dilakukan secara proporsional. Setelah proses normalisasi, jarak antara dua data dihitung menggunakan **selisih absolut** dari nilai normalisasi tersebut.

### Perhitungan Jarak Data Numerik

Pada atribut **numerik**, jarak dihitung dengan menggunakan selisih absolut antara dua nilai yang kemudian dinormalisasi menggunakan rentang nilai minimum dan maksimum dari atribut tersebut.

### Rumus Jarak Data Campuran (Gower Distance)

Setelah seluruh atribut dihitung, nilai jarak total dibagi dengan jumlah atribut yang ikut dihitung menggunakan rumus berikut:

$$
D = \frac{\sum (\delta \times d)}{\sum \delta}
$$

di mana:

- **D** : nilai jarak data campuran  
- **d** : jarak antara dua data pada suatu atribut  
- **δ (delta)** : indikator apakah atribut tersebut ikut dihitung atau tidak  

Nilai **D** berada pada rentang **0 hingga 1**, di mana nilai yang semakin kecil menunjukkan bahwa kedua data semakin mirip, sedangkan nilai yang semakin besar menunjukkan bahwa kedua data semakin berbeda.
