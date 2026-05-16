<div align="center">
  <h1>🚀 Real-Time ASL Neural Translator</h1>
  <p><strong>Edge AI Tabanlı, Çerçevesiz (Framework-less) Amerikan İşaret Dili Çevirmeni</strong></p>
</div>

<br>

![ASL Translator Demo](docs/placeholder_asl_demo.gif)

## 📖 Proje Hakkında
Bu proje, işitme engelli bireyler için tasarlanmış gerçek zamanlı bir İşaret Dili (ASL) çevirmenidir. Projenin en büyük mühendislik başarısı, ağır Derin Öğrenme kütüphanelerinin (TensorFlow/Keras/PyTorch) uç cihazlarda (Edge Devices) yarattığı yüksek bellek tüketimini ve sistem kilitlenmelerini kökünden çözmesidir.

**30GB RAM tüketimi ve Mutex Deadlock** sorunları aşılmış; Keras ağırlıkları (weights) saf NumPy matrislerine dönüştürülerek sadece **~95 MB RAM tüketimi** ve saniyede **185+ FPS** hızına ulaşılmıştır.

---

## 🏗️ Sistem Mimarisi

* **Veri Çıkarımı:** MediaPipe omurgası ile 21 noktalı (3 Boyutlu) el iskeleti çıkarılır.
* **Uzamsal Normalizasyon:** Bilek noktası $(0,0,0)$ orijinine taşınır ve el ölçeği normalize edilir (Scale & Translation Invariant).
* **Hafifletilmiş MLP:** 63 girdili (21x3), Batch Normalization ve ReLU destekli 4 katmanlı Multi-Layer Perceptron (MLP) modeli koşturulur.
* **Sinyal Filtreleme (Smoothing):** Kare kare tahminlerdeki anlık titremeleri (flickering) engellemek için `collections.deque` kullanılarak **Sürgülü Pencere (Sliding Window)** algoritması ile son 10 karenin İstatistiksel Mod'u alınır. Çıktı kusursuz ve titreşimsizdir.

---

## 🛠️ Kurulum ve Kullanım

```bash
git clone https://github.com/KULLANICI_ADINIZ/ASL-Neural-Translator.git
cd ASL-Neural-Translator
python3 -m venv venv
source venv/bin/activate  # Windows için: .\venv\Scripts\activate
pip install -r requirements.txt
```

Uygulamayı başlatmak için:
```bash
python Live_ASL_App/realtime_asl.py
```
*(Uygulama açıldığında kameraya işaret dilindeki harfleri gösterin. Klavyeden 'C' tuşu ile harfi metne ekleyebilir, 'Space' ile boşluk bırakabilir, 'Backspace' ile silebilirsiniz.)*

<br>

**Geliştirici:** Sizin Adınız & Soyadınız  
**Lisans:** MIT License
