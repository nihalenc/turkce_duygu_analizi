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

## Kullanılan Modeller 🤖

| Model | Tür | Kullanım |
|---|---|---|
| BERTurk | SLM | Fine-tuning |
| ELECTRA | SLM | Fine-tuning |
| LLaMA-3 8B | LLM | LoRA/QLoRA |
| Mistral 7B | LLM | LoRA/QLoRA |

Arayüz notebookunda kullanılan eğitilmiş model adresleri kod içinde verilmiştir. Bu adresler, hazır eğitilmiş modellerin Hugging Face üzerinden yüklenebilmesi için korunmuştur.

---

## Veri Seti

Projede kullanılan veri seti Hugging Face üzerinden indirilmektedir. Notebooklarda veri seti aşağıdaki kod ile alınmaktadır:

```python
dataset_path = hf_hub_download(
    repo_id="nihalenc/turkish-8class-emotion-dataset",
    filename="turkish-8class-emotion-dataset.csv",
    repo_type="dataset"
)
```

Bu nedenle veri seti dosyasının ayrıca manuel olarak yüklenmesine gerek yoktur. Veri setine erişim için Hugging Face bağlantısının çalışır durumda olması gerekmektedir.

---

## Kurulum ⚙️

Projeyi çalıştırmadan önce gerekli paketler yüklenmelidir:

```bash
pip install -r requirements.txt
```

Colab veya Kaggle ortamı kullanılıyorsa notebookların ilk hücrelerinde yer alan kurulum komutları çalıştırılmalıdır.

GPU kullanımı özellikle LLaMA ve Mistral modelleri için gereklidir. Colab ortamında çalışma zamanı türü GPU olarak seçilmelidir.

---

## Hugging Face Erişimi

Bazı modellerin kullanılabilmesi için Hugging Face hesabı gerekebilir.

LLaMA modeli gated olduğu için:

1. Hugging Face hesabında ilgili modele erişim izni bulunmalıdır.
2. Colab kullanılıyorsa Hugging Face token değeri Colab Secrets içine eklenmelidir.
3. Notebooklarda token adı `hf` olarak okunmaktadır.

```python
hf_token = userdata.get("hf")
```

Eğitim notebooklarında modellerin Hugging Face Hub'a kaydedilmesi için repo adresleri kod içinde verilmiştir. Kendi modellerini farklı bir Hugging Face hesabına kaydetmek isteyen kullanıcıların ilgili repo adreslerini değiştirmesi gerekmektedir.

---

## Notebookların Kullanımı 🚀

Projede iki farklı kullanım seçeneği bulunmaktadır.

### 1. Hazır Eğitilmiş Modellerle Tahmin Yapma

Hazır eğitilmiş modellerle tahmin yapmak için aşağıdaki notebook çalıştırılmalıdır:

```text
app.ipynb
```

Bu notebookta kullanıcıdan bir metin alınır ve seçilen model ile duygu tahmini yapılır. Hazır modeller Hugging Face üzerinden yüklenmektedir.

### 2. Modelleri Yeniden Eğitme

Modelleri yeniden eğitmek için ilgili eğitim notebookları çalıştırılmalıdır:

```text
berturk_electra.ipynb
llama.ipynb
mistral.ipynb
```

BERTurk ve ELECTRA modelleri daha düşük kaynaklarla çalıştırılabilir. LLaMA ve Mistral notebookları için GPU kullanılması gereklidir.

---

## Notebook İçerikleri

### `app.ipynb`

Hazır eğitilmiş modellerin arayüz üzerinden kullanılması için hazırlanmıştır. Kullanıcıdan alınan metin seçilen modele gönderilir ve duygu sınıfı tahmin edilir.

### `berturk_electra.ipynb`

BERTurk ve ELECTRA modellerinin eğitim, test ve karşılaştırma adımlarını içerir.

### `llama.ipynb`

LLaMA-3 8B modelinin LoRA/QLoRA ile eğitilmesi ve değerlendirilmesi için hazırlanmıştır.

### `mistral.ipynb`

Mistral 7B modelinin LoRA/QLoRA ile eğitilmesi ve değerlendirilmesi için hazırlanmıştır.

---

## Eğitim ve Çalıştırma Notları

- BERTurk ve ELECTRA daha düşük kaynaklarla çalıştırılabilir.
- LLaMA ve Mistral için GPU kullanılması gereklidir.
- LLM modellerinde 4-bit quantization ve LoRA yaklaşımı kullanılmıştır.
- LLaMA modelinin kullanılabilmesi için Hugging Face hesabında ilgili model erişiminin bulunması gerekir.
- Notebooklar, veri setini Hugging Face üzerinden indirecek şekilde hazırlanmıştır.

---

## Çıktılar

Notebooklar çalıştırıldığında aşağıdaki çıktılar üretilir:

- Classification report
- Confusion matrix
- Yanlış tahminlerin CSV çıktısı
- Inference time ölçümü
- Eğitilmiş model/checkpoint klasörleri


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
