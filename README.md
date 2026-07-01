# Türkçe Metin Verisinden Duygu Analizi 🧠

Bu proje, Türkçe metinlerde duygu sınıflandırması yapmak amacıyla dört farklı Transformer tabanlı modelin eğitilmesini, karşılaştırılmasını ve arayüz üzerinden kullanılmasını kapsar.

Projede kullanılan modeller:

- **BERTurk**
- **ELECTRA**
- **LLaMA-3 8B**
- **Mistral 7B**

LLaMA ve Mistral modelleri LoRA/QLoRA yaklaşımıyla ince ayarlanmıştır. BERTurk ve ELECTRA modelleri ise sınıflandırma görevi için fine-tune edilmiştir.

---

## Proje Kapsamı 📌

Model, Türkçe metinleri aşağıdaki 8 duygu sınıfından birine atar:

```text
mutluluk, üzüntü, öfke, korku, şaşkınlık, iğrenme, minnet, pişmanlık
```

Proje kapsamında:

- Veri ön işleme adımları uygulanmıştır.
- BERTurk ve ELECTRA modelleri eğitilmiştir.
- LLaMA-3 8B ve Mistral 7B modelleri LoRA/QLoRA ile eğitilmiştir.
- Modeller accuracy, precision, recall ve macro F1 metrikleriyle değerlendirilmiştir.
- Eğitilmiş modellerin tek arayüz üzerinden karşılaştırmalı tahmin yapması sağlanmıştır.

---

## Dosya Yapısı 📁

```text
.
├── app.ipynb                 # Eğitilmiş modellerle tahmin arayüzü
├── berturk_electra.ipynb     # BERTurk ve ELECTRA eğitim/değerlendirme notebooku
├── llama.ipynb               # LLaMA-3 LoRA eğitim/değerlendirme notebooku
├── mistral.ipynb             # Mistral LoRA eğitim/değerlendirme notebooku
├── requirements.txt          # Gerekli Python kütüphaneleri
├── .gitignore                # GitHub'a eklenmemesi gereken dosyalar
└── README.md                 # Proje açıklaması
```

---

## Kullanılan Modeller 🤖

| Model | Tür | Kullanım |
|---|---|---|
| BERTurk | SLM | Fine-tuning |
| ELECTRA | SLM | Fine-tuning |
| LLaMA-3 8B | LLM | LoRA/QLoRA |
| Mistral 7B | LLM | LoRA/QLoRA |

Arayüz notebookunda kullanılan eğitilmiş model adresleri kod içinde verilmiştir. Bu adresler, hazır eğitilmiş modellerin Hugging Face üzerinden yüklenebilmesi için korunmuştur.

---

## Kurulum ⚙️

Projeyi çalıştırmadan önce gerekli paketler yüklenmelidir:

```bash
pip install -r requirements.txt
```

Colab veya Kaggle ortamı kullanılıyorsa notebookların ilk hücrelerinde yer alan kurulum komutları çalıştırılmalıdır.

---

## Hugging Face Erişimi

Bazı modellerin kullanılabilmesi için Hugging Face hesabı gerekebilir.

Özellikle LLaMA modeli gated olduğu için:

1. Hugging Face hesabında ilgili modele erişim izni bulunmalıdır.
2. Colab kullanılıyorsa Hugging Face token değeri Colab Secrets içine eklenmelidir.
3. Notebooklarda token adı `hf` olarak okunmaktadır.

```python
hf_token = userdata.get("hf")
```

Token değeri doğrudan notebook içine yazılmamalıdır.

---

## Notebookların Kullanımı 🚀

### 1. Arayüz notebooku

Hazır eğitilmiş modellerle tahmin yapmak için aşağıdaki notebook kullanılmalıdır:

```text
app.ipynb
```

Bu notebookta kullanıcıdan bir metin alınır ve seçilen model ile duygu tahmini yapılır.

### 2. BERTurk ve ELECTRA eğitimi

```text
berturk_electra.ipynb
```

Bu notebook BERTurk ve ELECTRA modellerinin eğitim, test ve karşılaştırma adımlarını içerir.

### 3. LLaMA eğitimi

```text
llama.ipynb
```

Bu notebook LLaMA-3 8B modelinin LoRA/QLoRA ile eğitilmesi ve değerlendirilmesi için hazırlanmıştır.

### 4. Mistral eğitimi

```text
mistral.ipynb
```

Bu notebook Mistral 7B modelinin LoRA/QLoRA ile eğitilmesi ve değerlendirilmesi için hazırlanmıştır.

---

## Eğitim ve Çalıştırma Notları

- BERTurk ve ELECTRA daha düşük kaynaklarla çalıştırılabilir.
- LLaMA ve Mistral için GPU kullanılması gereklidir.
- LLM modellerinde 4-bit quantization ve LoRA yaklaşımı kullanılmıştır.
- Model ağırlıkları GitHub'a eklenmemelidir; Hugging Face üzerinde tutulmalıdır.
- CSV raporları ve checkpoint klasörleri GitHub'a yüklenmemelidir.

---

## Çıktılar

Notebooklar çalıştırıldığında aşağıdaki çıktılar üretilebilir:

- Classification report
- Confusion matrix
- Yanlış tahminlerin CSV çıktısı
- Inference time ölçümü
- Eğitilmiş model/checkpoint klasörleri

Bu çıktılar deney takibi için kullanılabilir, ancak GitHub reposuna eklenmeleri önerilmez.

---

## Gereksinimler

Temel kütüphaneler:

```text
transformers
datasets
accelerate
peft
bitsandbytes
scikit-learn
pandas
numpy
torch
matplotlib
seaborn
huggingface_hub
```

Tam liste `requirements.txt` dosyasında verilmiştir.

---

## Not

Bu repo, Türkçe duygu sınıflandırması için geliştirilen model eğitim notebooklarını ve eğitilmiş modelleri kullanmaya yönelik arayüz notebookunu içerir. Büyük model dosyaları GitHub yerine Hugging Face üzerinde tutulmalıdır.
