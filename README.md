Aisya Mufidah Najwa/1206230026
## Eksplorasi Mandiri (Tugas 2 Infrastruktur dan Platform untuk Sains Data)
• Pilih dan download/import dataset dari https://www.kaggle.com/datasets, kemudian lakukan
EDA - Exploratory Data Analysis: mengunakan Python Functions
1. Load data
2. basic information about the dataset
3. Cek nilai duplikat, nilai unik
4. Visualisasikan jumlah nilai unik
5. Menemukan null values
6. replace semua null values
7. Mengetahui tipe data dari dataset yang sedang diekplorasi untuk mempermudah proses
8. filter data
9. create a box plot
10. correlation


## Proses EDA pada data StudentsPerformance  
Menggunakan data StudentsPerformance yang didapat dari kaggle: https://www.kaggle.com/datasets/spscientist/students-performance-in-exams

### 1. Load Data
Sebelum load data, pastikan telah mengimpor library yang diperlukan.
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

Lalu load data StudentsPerformance
```python
df=pd.read_csv('dataset/StudentsPerformance.csv')
df
```

### 2. Basic Information about the Dataset
Data overview dengan menampilkan data
```python
df
```
![image](https://github.com/user-attachments/assets/945e14ea-eb0e-442a-88b4-715865ba922d)

Gunakan `df.info()` untuk mendapatkan gambaran umum mengenai struktur data yang ada di DataFrame, seperti jumlah baris, jumlah kolom, tipe data setiap kolom, serta jumlah nilai non-null di setiap kolom.
```python
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999
Data columns (total 8 columns):
 #   Column                       Non-Null Count  Dtype 
---  ------                       --------------  ----- 
 0   gender                       1000 non-null   object
 1   race/ethnicity               1000 non-null   object
 2   parental level of education  1000 non-null   object
 3   lunch                        1000 non-null   object
 4   test preparation course      1000 non-null   object
 5   math score                   1000 non-null   int64 
 6   reading score                1000 non-null   int64 
 7   writing score                1000 non-null   int64 
dtypes: int64(3), object(5)
memory usage: 62.6+ KB
```


Gunakan `df.describe()` untuk memberikan statistik deskriptif dari kolom numerik, membantu mendapatkan wawasan umum tentang distribusi data, seperti rata-rata, nilai minimum dan maksimum, serta kuartil.

```python
df.describe()
```

|                | Math Score | Reading Score | Writing Score |
|----------------|------------|---------------|---------------|
| **Count**      | 1000.00000 | 1000.000000   | 1000.000000   |
| **Mean**       | 66.08900   | 69.169000     | 68.054000     |
| **Std**        | 15.16308   | 14.600192     | 15.195657     |
| **Min**        | 0.00000    | 17.000000     | 10.000000     |
| **25%**        | 57.00000   | 59.000000     | 57.750000     |
| **50% (Median)**| 66.00000   | 70.000000     | 69.000000     |
| **75%**        | 77.00000   | 79.000000     | 79.000000     |
| **Max**        | 100.00000  | 100.000000    | 100.000000    |

### 3. Cek nilai duplikat, nilai unik
#### Nilai duplikat:
```python
df.duplicated().sum() #cek nilai duplikat
```
```
np.int64(0)
```
artinya, tidak ada nilai duplikat.

#### Nilai unik:
Menghitung unik dari kolom data
```python
jumlah_unik = df.nunique() # cek nilai unik
jumlah_unik
```
```
gender                          2
race/ethnicity                  5
parental level of education     6
lunch                           2
test preparation course         2
math score                     81
reading score                  72
writing score                  77
dtype: int64
```
### 4. Visualisasikan jumlah nilai unik
```python
plt.figure(figsize=(10, 6)) # bar plot nilai unik
jumlah_unik.plot(kind='bar')
plt.title('Nilai Unik Per Kolom')
plt.xlabel('Kolom')
plt.ylabel('Jumlah Nilai nik')
plt.xticks(rotation=45)

for i, count in enumerate(jumlah_unik):
    plt.text(i, count + 0.3, str(count), ha='center') # biar tau brp unik di setiap kolom

plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/b6bae8b6-f4ce-4d2d-8a50-8ec228bb0f16)

### 5. Menemukan null values

Menemukan null values dengan menggunakan `df.isnull().sum()`
```python
df.isnull().sum()
```
```
gender                         0
race/ethnicity                 0
parental level of education    0
lunch                          0
test preparation course        0
math score                     0
reading score                  0
writing score                  0
dtype: int64
```
Pada data StudentsPerformance tidak ditemukan missing values.

### 6. Replace semua null values
Karena tidak ditemukan null values, proses ini dilewati.

### 7. Mengetahui tipe data
Menggunakan `df.dtypes`
```python
df.dtypes
```
```
gender                         object
race/ethnicity                 object
parental level of education    object
lunch                          object
test preparation course        object
math score                      int64
reading score                   int64
writing score                   int64
dtype: object
```
object ada 5 dan int64 ada 3
### 8. Filter Data
Misalnya hanya ingin melihat pola dengan nilai matematika diatas 60, kita bisa melakukan filter pada data.
```python
#nilai matematika diatas 60
math_60 = df[df['math score'] > 60] 
math_60
```

### 9. Create Box Plot
Distribusi data melalui lima statistik ringkasan, minimum, Q1, Q2, Q3, dan maksimum dari dataset.
Disini menggunakan fungsi matplotlib dan seaborn untuk membuat box plot:
```python
plt.figure(figsize=(10, 6))
sns.boxplot(data=df) # untuk math score, reading score dan writing score
plt.title('Box Plot Skor')
plt.xticks(rotation=0)
plt.show()
```
![image](https://github.com/user-attachments/assets/bb8fe031-dfd5-48f8-829a-eaa1275893a7)

Misalnya ingin melihat box plot distribusi skor matematika berdasarkan gender
```python
plt.figure(figsize=(8, 5))
sns.boxplot(x='gender', y='math score', data=df)
plt.title('Skor Matematika berdasarkan Gender')
```
![image](https://github.com/user-attachments/assets/d67ae348-65be-4671-b083-80a98d9c3625)

Atau ingin melihat distribusi skor matematika berdasarkan race/ethnicity
```python
plt.figure(figsize=(8, 5))
sns.boxplot(x='race/ethnicity', y='math score', data=df)
plt.title('Skor Matematika berdasarkan Group')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/a3692957-6e10-47dd-b9eb-5d1c49283a9c)

### 10. Correlation
Digunakan untuk mengukur dan menggambarkan hubungan antara dua variabel, biasanya digunakan untuk memahami sejauh mana perubahan dalam satu variabel dapat berhubungan dengan perubahan dalam variabel lain.
```python
# korelasi
correlation_matrix = df[['math score', 'reading score', 'writing score']].corr()

plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='OrRd', fmt='.2f')
plt.title('Korelasi Skor')
plt.show()
```
![image](https://github.com/user-attachments/assets/19e794ff-3870-4718-b642-442c42495f71)

Warna coolwarm tidak digunakan karena tidak ada nilai negatif. Seperti yang bisa dilihat, korelasi antar skor menunjukkan angka yang tinggi, siswa yang memiliki skor tinggi dalam satu subjek cenderung juga memiliki skor tinggi di subjek lainnya.

Kode dapat dilihat di https://github.com/aisyanajwa/ipsd/blob/main/ipsd_tugas2.ipynb
