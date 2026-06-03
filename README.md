# Sistem de Detecție a Deepfake-urilor Video bazat pe Analiză Facială

Acest proiect reprezintă o aplicație desktop automatizată capabilă să extragă, să proceseze și să clasifice fluxurile video pentru identificarea manipulărilor de tip deepfake. Proiectul combină eficiența modelului **ResNet18** (via Transfer Learning) cu o arhitectură inovatoare de fuziune multi-strat (**MFNN - Multi-Layer Fusion Neural Network**) pentru a surprinde artefacte artificiale la diferite niveluri de profunzime.

Aplicația include, de asemenea, o interfață grafică interactivă dezvoltată în **Tkinter** ]și un modul avansat de testare la stres pentru evaluarea robusteții modelului în condiții de calitate degradată.

---

## 🚀 Caracteristici Principale

* **Preprocesare și Detecție Facială de Înaltă Precizie**: Tranziția de la metodele clasice (Haar Cascade) la **MediaPipe (BlazeFace)** pentru o localizare rapidă și robustă în timp real.
* **Decupare Optimizată (1.4x)**: Coordonatele feței sunt lărgite cu un factor de 1.4x pentru a include linia maxilarului și regiunea gâtului, unde artefactele de îmbinare (*blending*) sunt cele mai pronunțate].
* **Arhitectură Multi-Layer Fusion (MFNN)**: Extragerea și fuzionarea hărților de caracteristici din trei puncte distincte ale rețelei pentru a identifica defecte specifice[cite: 130, 203]:
    * *Nivel de suprafață (Shallow)*: Zgomot microscopic și statistici la nivel de pixel.
    * *Nivel intermediar (Middle)*: Defecte mezoscopice și texturi nenaturale.
    * *Nivel profund (Deep)*: Defecte macroscopice, proporții și logică semantică.
* **Strategia de Vot Majoritar (Majority Voting)**: Pentru a asigura stabilitatea deciziei pe întregul flux video și a reduce alarmele false cauzate de mișcări bruște sau compresie.
* **Modul Stress Test Live**: Permite utilizatorului să aplice degradări intenționate (compresie JPEG, blur, distorsionarea pixelilor) pentru a analiza limitele de detecție ale rețelei.

---

## 🧠 Detalii Tehnice și Algoritmi

### 1. Operația de Convoluție
Filtrele convoluționale glisează spațial peste imagini pentru a detecta trăsăturile vizuale locale, conform ecuației:

$$(I*K)[i,j]=\sum_{m}\sum_{n}I[i+m,j+n]\cdot K[m,n]$$

### 2. Funcția de Decizie (Majority Voting)
Verdictul final $V$ al videoclipului este determinat prin agregarea deciziilor binare pe fiecare cadru individual ($c_i$), unde $N$ este numărul total de cadre analizate:

$$V = \begin{cases} \text{FAKE}, & \text{dacă } \frac{1}{N} \sum_{i=1}^{N} P(c_i) > 0.5 \\ \text{REAL}, & \text{altfel} \end{cases}$$

---

## 📊 Performanțe Obținute

Modelul a fost antrenat și evaluat pe un subset izolat din standardul academic **FaceForensics++**.

* **Acuratețe pe cadre nealterate (Clean Test)**: **97.07%**[cite: 256, 296].
* **Comportament la Stress Test**: În cazul compresiei extreme sau al pixelării puternice, acuratețea scade la **31.84%**. [cite_start]Acest lucru evidențiază o limitare critică a modelelor actuale: eliminarea urmelor microscopice prin "netezirea" forțată aplicată de algoritmii de compresie distruge indiciile fine de falsificare.

### Matricea de Confuzie (Set Nealterat vs. Alterat)
Proiectul include analize detaliate ale matricelor de confuzie, demonstrând controlul excelent al alarmelor false în condiții optime și tendința de fals-negativ în condiții de stres.

---

## 🛠️ Tehnologii Utilizate

* **Limbaj**: Python 
* **Framework Deep Learning**: PyTorch (cu suport CUDA GPU pentru accelerare hardware)
* **Procesare Multimedia**: OpenCV & MediaPipe (BlazeFace) 
* **Interfață Grafică**: Tkinter
* **Tehnici de Antrenare**: Transfer Learning (ResNet18 pre-antrenat pe ImageNet) , Data Augmentation (Color Jitter, rotații) [cite: 216][cite_start], WeightedRandomSampler (pentru gestionarea dezechilibrului claselor).

---

## 📈 Planuri de Viitor

* Implementarea analizei audio-video pentru a detecta desincronizările specifice tehnicilor de *voice cloning*.
* Optimizarea modelului în format **ONNX** pentru a permite inferența în timp real pe apeluri video live.
* Tranziția către arhitecturi bazate pe mecanisme de atenție, precum **Vision Transformers (ViT)**.

---

## 🎓 Autori și Îndrumători

* **Autor**: Vlăduțu Alexandru-Nicuşor, an III, grupa 333AA 
* **Instituție**: Universitatea Națională de Știință și Tehnologie POLITEHNICA din București, Facultatea de Automatică și Calculatoare, Departamentul Automatică şi Informatică Industrială 
* **Îndrumător Științific**: dr. conf. Ștefan Mocanu 
