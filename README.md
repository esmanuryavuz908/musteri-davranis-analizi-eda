# Müşteri Davranış Analizi ve Segmentasyon (EDA)

200 müşterilik sentetik perakende verisi üzerinde Python kullanarak keşifsel veri analizi (EDA), harcama bazlı müşteri segmentasyonu ve görselleştirme gerçekleştiren veri analitiği projesi.

![Python](https://img.shields.io/badge/Python-3.14-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Veri%20Analizi-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Sentetik%20Veri-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Görselleştirme-11557C?style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-İstatistiksel%20Grafik-4C72B0?style=for-the-badge)

---

## Projenin Amacı ve Çözdüğü Problem

Perakende ve e-ticaret işletmeleri, müşteri tabanlarının yaş, cinsiyet, gelir düzeyi, üyelik süresi ve indirim kullanımına göre nasıl alışveriş yaptığını anlamadan etkili kampanya veya sadakat stratejileri kurgulayamaz.

Bu proje, uçtan uca bir müşteri analitiği akışını göstermek amacıyla oluşturulmuştur:
- Ham müşteri demografisi ve alışveriş alışkanlıklarını simüle eder.
- Alışveriş sıklığı ve ortalama sepet tutarından yeni finansal metrikler (aylık toplam harcama ve harcama/gelir oranı) üretir.
- Müşterileri ortalama sepet tutarlarına göre 4 segmente ayırır ve kategorik değişkenleri sayısal formata (encoding) dönüştürür.
- Gelir, üyelik süresi, indirim kullanımı ve cinsiyet eksenindeki ilişkileri istatistiksel özetler ve grafiklerle görünür kılar.

---

## Veri Seti Yapısı

Projede harici bir veri dosyası yerine `NumPy` kullanılarak 200 müşteri kaydı içeren sentetik bir veri seti üretilmiştir.

| Sütun Adı | Tür | Açıklama / Değer Aralığı |
| :--- | :--- | :--- |
| `CustomerId` | Ham Veri | Benzersiz müşteri kimliği (`1` – `200`) |
| `Age` | Ham Veri | Müşteri yaşı (`18` – `69`) |
| `Gender` | Ham Veri | Cinsiyet (`Female`, `Male` → encoding sonrası `0`, `1`) |
| `MonthlyIncome` | Ham Veri | Aylık gelir (`5.000` – `39.999 TL`) |
| `ShoppingFrequency` | Ham Veri | Aylık alışveriş sıklığı (`1` – `14`) |
| `AverageBasket` | Ham Veri | Ortalama sepet tutarı (`50,00` – `3.500,00 TL`) |
| `MembershipYears` | Ham Veri | Üyelik süresi (`1` – `10 yıl`) |
| `DiscountUsage` | Ham Veri | İndirim kullanımı (`Yes`, `No`) |
| `CustomerSegment` | Türetilmiş | Ortalama sepet tutarına göre segment (`Düşük`, `Orta`, `Yüksek`, `Çok Yüksek` → `0`–`3`) |
| `MonthlySpending` | Türetilmiş | Aylık toplam harcama (`ShoppingFrequency × AverageBasket`) |
| `IncomeSpendingRatio` | Türetilmiş | Aylık harcamanın aylık gelire oranı (`MonthlySpending / MonthlyIncome`) |

> **Not:** Veri üretimi sırasında sabit bir rastgelelik tohumu (`np.random.seed`) tanımlanmadığı için notebook yeniden çalıştırıldığında değerler yeni sentetik dağılıma göre güncellenir. Aşağıdaki bulgular notebook içerisindeki kayıtlı çalıştırma çıktısına aittir.

---

## Öne Çıkan Özellikler ve Gerçek Proje Bulguları

### Yapılan Analiz Adımları
- **Sentetik Veri Üretimi:** `NumPy` ve `Pandas` ile 200 satırlık, 8 ham değişkenli müşteri tablosu oluşturuldu.
- **Kural Tabanlı Segmentasyon:** Ortalama sepet tutarına göre `≤ 500 TL` **Düşük**, `501–1.500 TL` **Orta**, `1.501–3.000 TL` **Yüksek** ve `> 3.000 TL` **Çok Yüksek** olmak üzere 4 müşteri segmenti tanımlandı.
- **Özellik Mühendisliği (Feature Engineering):** `MonthlySpending` ve `IncomeSpendingRatio` sütunları hesaplandı.
- **Kategorik Dönüşüm (Encoding):** `Gender` (`Female: 0`, `Male: 1`) ve `CustomerSegment` (`Düşük: 0` → `Çok Yüksek: 3`) sütunları sayısal değerlere eşlendi.
- **Veri Görselleştirme:** Histogram (KDE eğrili), dağılım grafikleri (scatter plot), sütun grafiği (count plot) ve kutu grafiği (box plot) ile 5 farklı görsel analiz üretildi.

### Kayıtlı Çalıştırma Çıktıları
- **Ortalama Müşteri Yaşı:** `46`
- **Ortalama Aylık Gelir:** `21.469,74 TL`
- **Ortalama Sepet Tutarı:** `1.822,40 TL`
- **En Yüksek Sepet Tutarı:** `3.478,99 TL`
- **En Sık Alışveriş Yapan İlk 5 Müşteri:** `CustomerId` `4`, `25`, `33`, `59` ve `65` (aylık `14` alışveriş)
- **Cinsiyete Göre Ortalama Sepet Tutarı:**
  - Kadın (`Female`): `1.804,91 TL`
  - Erkek (`Male`): `1.841,36 TL`
- **İndirim Kullanımına Göre Ortalama Alışveriş Sıklığı:**
  - İndirim Kullanmayanlar (`No`): `7,41`
  - İndirim Kullananlar (`Yes`): `6,74`
- **Üyelik Süresine Göre Aylık Ortalama Harcama:** En yüksek ortalama harcama `4 yıllık` üyelerde (`17.478,03 TL`), en düşük ortalama harcama `3 yıllık` üyelerde (`9.213,25 TL`) gözlemlendi.
- **Ortalama Aylık Harcaması En Yüksek İlk 5 Yaş:** `18` (`24.830,58 TL`), `36` (`24.674,34 TL`), `63` (`23.919,74 TL`), `27` (`23.147,02 TL`) ve `29` (`21.561,30 TL`).

---

## Kullanılan Teknolojiler ve Kütüphaneler

- **Programlama Dili:** Python 3.14
- **Veri Manipülasyonu ve Sayısal Hesaplama:** `pandas`, `numpy`
- **Veri Görselleştirme:** `matplotlib`, `seaborn`
- **Geliştirme Ortamı:** Jupyter Notebook

---

## Kurulum ve Çalıştırma

Projeyi yerel bilgisayarında çalıştırmak için aşağıdaki adımları izle:

1. **Repoyu klonla:**
   ```bash
   git clone https://github.com/esmanuryavuz908/musteri-davranis-analizi-eda.git
   cd musteri-davranis-analizi-eda
   ```

2. **(Önerilen) Sanal ortam oluştur ve etkinleştir:**
   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # macOS / Linux:
   source venv/bin/activate
   ```

3. **Gerekli kütüphaneleri yükle:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

4. **Jupyter Notebook'u başlat ve dosyayı çalıştır:**
   ```bash
   jupyter notebook
   ```
   Açılan arayüzden `musteri_davranis_analizi.ipynb` dosyasını seçip hücreleri sırayla (`Run All`) çalıştırabilirsin.

---


