# SAM2_UNIMC_DEMO — Segmentazione Video con SAM2 (Ultralytics)

<a target="_blank" href="https://colab.research.google.com/github/lorenzo-stacchio/Sam-2-Demo-Colab/blob/main/SAM2_DEMO.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

Questo notebook dimostrativo presenta l'uso del modello **SAM2VideoPredictor** della libreria Ultralytics per eseguire **segmentazione video guidata da punti selezionati**, in ambiente Google Colab. L'attività è stata progettata per fini educativi presso l'Università degli Studi di Macerata (UNIMC).

---

## 🎯 Obiettivi

- Utilizzare il modello SAM2 per segmentare oggetti in video
- Sperimentare la selezione interattiva di punti per l’inferenza
- Familiarizzare con l’uso della segmentazione interattiva e semantica in Colab

---

## ⚙️ Setup iniziale

Esegui le prime celle del notebook per:

1. **Installare Ultralytics e dipendenze**:
    ```python
    !pip install ultralytics opencv-python matplotlib
    ```

2. **Verificare l’ambiente Colab**:
    - Python ≥ 3.11
    - GPU attiva (Tesla T4 consigliata)

⚠️ *Vai su `Runtime > Change runtime type > GPU` per abilitare l'acceleratore hardware.*

---

## 🧑‍💻 Come usare il notebook

### 1. Apri in Google Colab

- Vai su [https://colab.research.google.com](https://colab.research.google.com)
- Clicca su “Carica” e seleziona `SAM2_DEMO.ipynb.ipynb`
- Oppure clicca sul badge **“Open in Colab”** in alto

### 2. Carica un video

- Puoi caricare un tuo file video tramite la barra laterale a sinistra
- Oppure utilizzare un video di esempio fornito nel notebook

### 3. Seleziona i punti da segmentare

- Il notebook mostra un frame del video per selezionare **punti manuali**
- Questi punti servono da guida per il modello di segmentazione

### 4. Avvia la segmentazione

Utilizza il modello SAM2 come segue:

```python
from ultralytics.models.sam import SAM2VideoPredictor

# Crea un oggetto predictor con i parametri desiderati
overrides = dict(conf=0.25, task="segment", mode="predict", imgsz=1024, model="sam2_b.pt")
predictor = SAM2VideoPredictor(overrides=overrides)

# Avvia la predizione sul video e i punti selezionati
results = predictor(source=video_path, points=selected_points, labels=[1]*len(selected_points))
```


Il modello esegue la segmentazione su ciascun frame del video, evidenziando gli oggetti corrispondenti ai punti selezionati.

### 5. Visualizza e salva i risultati

- Il video segmentato viene visualizzato direttamente all'interno del notebook  
- Il file risultante viene salvato nella directory `/runs/segment/`  
- Può essere scaricato cliccando a destra nel pannello “File” di Colab  

---

## 🛠️ Personalizzazioni

Puoi modificare:

- Il modello (`sam2_b.pt`, `sam2_t.pt`, ecc.)  
- La dimensione delle immagini (`imgsz`)  
- I punti e le etichette selezionati  
- La soglia di confidenza (`conf`)  

---

## 📦 Requisiti

- Account Google Colab  
- Acceleratore GPU abilitato  
- Librerie necessarie:
  - `ultralytics`
  - `opencv-python`
  - `matplotlib`
