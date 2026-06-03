# Sistem de Detecție a Deepfake-urilor Video bazat pe Analiză Facială

[cite_start]Acest proiect reprezintă o aplicație desktop automatizată capabilă să extragă, să proceseze și să clasifice fluxurile video pentru identificarea manipulărilor de tip deepfake[cite: 88]. [cite_start]Proiectul combină eficiența modelului **ResNet18** (via Transfer Learning) cu o arhitectură inovatoare de fuziune multi-strat (**MFNN - Multi-Layer Fusion Neural Network**) pentru a surprinde artefacte artificiale la diferite niveluri de profunzime[cite: 94, 130, 194, 198].

[cite_start]Aplicația include, de asemenea, o interfață grafică interactivă dezvoltată în **Tkinter** [cite: 246] [cite_start]și un modul avansat de testare la stres pentru evaluarea robusteții modelului în condiții de calitate degradată[cite: 257].

---

## 🚀 Caracteristici Principale

* [cite_start]**Preprocesare și Detecție Facială de Înaltă Precizie**: Tranziția de la metodele clasice (Haar Cascade) la **MediaPipe (BlazeFace)** pentru o localizare rapidă și robustă în timp real[cite: 173, 176, 177].
* [cite_start]**Decupare Optimizată (1.4x)**: Coordonatele feței sunt lărgite cu un factor de 1.4x pentru a include linia maxilarului și regiunea gâtului, unde artefactele de îmbinare (*blending*) sunt cele mai pronunțate[cite: 122, 123, 183, 184].
* [cite_start]**Arhitectură Multi-Layer Fusion (MFNN)**: Extragerea și fuzionarea hărților de caracteristici din trei puncte distincte ale rețelei pentru a identifica defecte specifice[cite: 130, 203]:
    * [cite_start]*Nivel de suprafață (Shallow)*: Zgomot microscopic și statistici la nivel de pixel[cite: 102, 103, 131].
    * [cite_start]*Nivel intermediar (Middle)*: Defecte mezoscopice și texturi nenaturale[cite: 104, 105, 131].
    * [cite_start]*Nivel profund (Deep)*: Defecte macroscopice, proporții și logică semantică[cite: 107, 109, 133].
* [cite_start]**Strategia de Vot Majoritar (Majority Voting)**: Pentru a asigura stabilitatea deciziei pe întregul flux video și a reduce alarmele false cauzate de mișcări bruște sau compresie[cite: 152].
* [cite_start]**Modul Stress Test Live**: Permite utilizatorului să aplice degradări intenționate (compresie JPEG, blur, distorsionarea pixelilor) pentru a analiza limitele de detecție ale rețelei[cite: 257, 258].

---

## 🧠 Detalii Tehnice și Algoritmi

### 1. Operația de Convoluție
[cite_start]Filtrele convoluționale glisează spațial peste imagini pentru a detecta trăsăturile vizuale locale, conform ecuației[cite: 127]:

$$(I*K)[i,j]=\sum_{m}\sum_{n}I[i+m,j+n]\cdot K[m,n]$$

### 2. Funcția de Decizie (Majority Voting)
Verdictul final $V$ al videoclipului este determinat prin agregarea deciziilor binare pe fiecare cadru individual ($c_i$), unde $N$ este numărul total de cadre analizate[cite: 156]:

$$V = \begin{cases} \text{FAKE}, & \text{dacă } \frac{1}{N} \sum_{i=1}^{N} P(c_i) > 0.5 \\ \text{REAL}, & \text{altfel} \end{cases}$$

---

## 📊 Performanțe Obținute

Modelul a fost antrenat și evaluat pe un subset izolat din standardul academic **FaceForensics++**[cite: 68, 91, 166].

* [cite_start]**Acuratețe pe cadre nealterate (Clean Test)**: **97.07%**[cite: 256, 296].
* [cite_start]**Comportament la Stress Test**: În cazul compresiei extreme sau al pixelării puternice, acuratețea scade la **31.84%**[cite: 320, 322]. [cite_start]Acest lucru evidențiază o limitare critică a modelelor actuale: eliminarea urmelor microscopice prin "netezirea" forțată aplicată de algoritmii de compresie distruge indiciile fine de falsificare[cite: 291, 323].

### Matricea de Confuzie (Set Nealterat vs. Alterat)
[cite_start]Proiectul include analize detaliate ale matricelor de confuzie, demonstrând controlul excelent al alarmelor false în condiții optime [cite: 297] [cite_start]și tendința de fals-negativ în condiții de stres[cite: 290].

---

## 🛠️ Tehnologii Utilizate

* [cite_start]**Limbaj**: Python [cite: 169, 246]
* [cite_start]**Framework Deep Learning**: PyTorch (cu suport CUDA GPU pentru accelerare hardware) [cite: 162, 220]
* [cite_start]**Procesare Multimedia**: OpenCV & MediaPipe (BlazeFace) [cite: 163, 176]
* [cite_start]**Interfață Grafică**: Tkinter [cite: 246]
* [cite_start]**Tehnici de Antrenare**: Transfer Learning (ResNet18 pre-antrenat pe ImageNet) [cite: 94, 201][cite_start], Data Augmentation (Color Jitter, rotații) [cite: 216][cite_start], WeightedRandomSampler (pentru gestionarea dezechilibrului claselor)[cite: 220].

---

## 📈 Planuri de Viitor

* [cite_start]Implementarea analizei audio-video pentru a detecta desincronizările specifice tehnicilor de *voice cloning*[cite: 344, 346].
* [cite_start]Optimizarea modelului în format **ONNX** pentru a permite inferența în timp real pe apeluri video live[cite: 346].
* [cite_start]Tranziția către arhitecturi bazate pe mecanisme de atenție, precum **Vision Transformers (ViT)**[cite: 346].

---

## 🎓 Autori și Îndrumători

* [cite_start]**Autor**: Vlăduțu Alexandru-Nicuşor, an III, grupa 333AA [cite: 13]
* [cite_start]**Instituție**: Universitatea Națională de Știință și Tehnologie POLITEHNICA din București, Facultatea de Automatică și Calculatoare, Departamentul Automatică şi Informatică Industrială [cite: 1, 2, 3, 4]
* **Îndrumător Științific**: dr. conf. [cite_start]Ștefan Mocanu [cite: 15]
