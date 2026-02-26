# 🌟 Astronomical Star Type Visualisation
### Hertzsprung-Russell Diagram · 6 Stellar Classes · EDA Suite · Matplotlib & Seaborn

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualisation-orange?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-green?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-240%20Stars%20·%206%20Classes-blueviolet?style=flat-square)
![Task](https://img.shields.io/badge/Task-Astronomical%20EDA-red?style=flat-square)

---

## 🔭 Project Overview

Stars are not all alike. From tiny **Brown Dwarfs** barely larger than Jupiter,  
to **Hypergiants** hundreds of times the size of our Sun —  
stellar classification is one of astronomy's most fundamental frameworks.

This project performs a complete **exploratory data analysis (EDA)**  
on a 240-star dataset, culminating in a hand-crafted  
**Hertzsprung-Russell (HR) Diagram** — the most important chart in stellar astronomy.

> **Goal:** Build a 5-chart EDA suite that reveals the physical relationships  
> between temperature, luminosity, radius, magnitude, and star type —  
> using Matplotlib and Seaborn from first principles.

---

## 🌠 The 6 Stellar Classes

| Code | Star Type | Characteristics |
|---|---|---|
| **0** | Brown Dwarf | Sub-stellar — too small for hydrogen fusion |
| **1** | Red Dwarf | Most common star — cool, small, long-lived |
| **2** | White Dwarf | Stellar remnant — dense, cooling ember |
| **3** | Main Sequence | Stars like our Sun in active fusion phase |
| **4** | Supergiant | Massive, short-lived, extremely luminous |
| **5** | Hypergiant | Rarest and largest known stars in the universe |

---

## 📡 Dataset

| Property | Details |
|---|---|
| **Source** | [Star Type Classification Dataset](https://drive.google.com/uc?id=1BQVc6MHjQFtDC9iP1isT_K4ojVe_Oil-) |
| **Rows** | 240 stars |
| **Features** | 6 features + 1 target |
| **Numeric Features** | Temperature (K), Luminosity (L/L☉), Radius (R/R☉), Absolute Magnitude (Mv) |
| **Categorical Features** | Star Color, Spectral Class |
| **Target** | Star Type (0–5) |

Where:
- L☉ = 3.828 × 10²⁶ Watts (average solar luminosity)
- R☉ = 6.9551 × 10⁸ m (average solar radius)

---

## 🧠 The 5-Chart EDA Suite

### Chart 1 — Star Count per Type (Custom Bar Chart)

```python
plt.figure(figsize=(4.3, 4.3))
plt.style.use('dark_background')
ax = star_df['Star type'].value_counts().plot(
    kind='bar',
    color=['brown', 'red', 'white', 'yellow', 'lightblue', 'orange']
)
ax.bar_label(ax.containers[0], color='red')
plt.xticks(ticks=[0,1,2,3,4,5],
           labels=['Brown\nDwarf','Red\nDwarf','White\nDwarf',
                   'Main\nSequence','Supergiants','Hypergiants'],
           rotation=45, color='lime')
```

**Design choice:** Each bar is coloured to match the **actual physical colour**  
of that star type — brown for Brown Dwarfs, red for Red Dwarfs, white for White Dwarfs.  
This is astronomy-aware design, not arbitrary styling.

---

### Chart 2 — Star Color Distribution (Seaborn Bar Chart)

```python
ax = sns.barplot(
    x=star_df['Star color'].value_counts().index,
    y=star_df['Star color'].value_counts(),
    palette='viridis'
)
```

Reveals the **diversity of observed stellar colours** and demonstrates  
how Seaborn extends Matplotlib for statistical visualisation with less code.

---

### Chart 3 — Outlier Detection (Boxplot Subplot Grid)

```python
plt.figure(figsize=(20, 8))
for i in range(4):
    plt.subplot(1, 4, i+1)
    sns.boxplot(x=star_df['Star type'], y=star_df.iloc[:, i])
    plt.title(star_df.columns[i], color='red')
```

A **1×4 subplot grid** — one boxplot per numeric feature, grouped by star type.  
Key finding: Supergiants and Hypergiants are extreme outliers in luminosity and radius  
— physically expected given their enormous size.

---

### Chart 4 — Feature Distribution (Line Plot Subplot)

```python
def line_subplot(star_df, colors, i):
    plt.subplot(4, 1, i+1)
    plt.plot(star_df.iloc[:, i], color=colors[i])
    plt.title(star_df.columns[i], color='red')

colors = ['royalblue', 'gold', 'lime', 'magenta']
for i in range(4):
    line_subplot(star_df, colors, i)
plt.tight_layout()
```

A **4×1 subplot** showing the raw distribution of each numeric feature —  
reveals the highly skewed, multi-modal nature of stellar physical properties.

---

### Chart 5 — Hertzsprung-Russell Diagram (Custom Scatter Plot)

The HR diagram is the **cornerstone of stellar astrophysics** — it maps  
temperature against absolute magnitude, revealing stellar evolution sequences.

```python
star_types = {
    0: {'label': 'Brown Dwarf',   'color': 'brown',   'size': 30,  'marker': '.'},
    1: {'label': 'Red Dwarf',     'color': 'red',     'size': 35,  'marker': '.'},
    2: {'label': 'White Dwarf',   'color': 'white',   'size': 40,  'marker': '.'},
    3: {'label': 'Main Sequence', 'color': 'cyan',    'size': 30,  'marker': 'o'},
    4: {'label': 'Supergiants',   'color': 'orange',  'size': 100, 'marker': 'o'},
    5: {'label': 'Hypergiants',   'color': 'maroon',  'size': 150, 'marker': 'o'},
}

# Sun plotted as reference point
ax_sun = plt.scatter(5778, 4.83, s=75, c='yellow', marker='o', label='Sun')
```

**Key design decisions:**
- **Marker size scales with stellar radius** — supergiants appear physically larger on the plot
- **Colour matches real stellar colour** — consistent with spectral classification
- **Sun plotted as reference point** at T=5778K, Mv=4.83 — gives astrophysical grounding
- **Duplicate legend entries suppressed** using a `labels` set — clean, professional output

---

## 📊 What the HR Diagram Reveals

The completed diagram shows the **main sequence diagonal** — the band where  
stars like our Sun spend most of their lives — plus the distinct clusters  
of White Dwarfs (bottom-left), Red Giants (top-right), and Hypergiants (top).

This is the same structure astronomers use to determine **stellar age, distance, and evolution stage.**

---

## 🚀 Real-World Relevance for Space Applications

| This Project | Space Industry Application |
|---|---|
| Multi-panel EDA dashboards | Mission data reporting & anomaly visualisation |
| Physics-aware colour/size encoding | Satellite status dashboards |
| HR diagram construction | Star-tracker calibration & attitude determination |
| Outlier identification in sensor data | Fault detection in spacecraft telemetry |
| Reusable subplot functions | Scalable data pipeline visualisation tools |

---

## 📁 Repository Structure

```
astronomical-star-visualisation/
│
├── Astronomical_Tabular_Data_Visualization.ipynb   ← Full notebook
├── README.md                                         ← You are here
└── requirements.txt                                  ← Dependencies
```

---

## ⚙️ How to Run

```bash
# 1. Clone the repo
git clone https://github.com/YOUR-USERNAME/astronomical-star-visualisation
cd astronomical-star-visualisation

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn

# 3. Open the notebook
jupyter notebook Astronomical_Tabular_Data_Visualization.ipynb
```

Dataset loads directly from Google Drive — no manual download needed:

```python
star_df = pd.read_csv('https://drive.google.com/uc?id=1BQVc6MHjQFtDC9iP1isT_K4ojVe_Oil-')
```

---

## 🔭 Future Work

- Add **interactive HR diagram** using Plotly for zoomable stellar exploration
- Extend to **Gaia DR3 catalogue** (1.8 billion stars) for large-scale HR diagram
- Apply **clustering algorithms** (K-Means, DBSCAN) to verify stellar class boundaries
- Build a **classification model** (Random Forest / SVM) on the same dataset

---

## 📚 References

- Hertzsprung-Russell Diagram: https://www.space.fm/astronomy/images/diagrams/hr.jpg
- Star Type Dataset: https://www.kaggle.com/datasets/deepu1109/star-dataset
- Matplotlib Documentation: https://matplotlib.org/stable/
- Seaborn Documentation: https://seaborn.pydata.org/

---

## 👩‍💻 Author

**Mubeena Hussain**
MSc Statistics
📧 mubeenahussain1205@gmail.com
🔗 [LinkedIn](www.linkedin.com/in/mubeena-hussain-a357b920b)


---

*"The HR diagram turned a sky full of random stars into a story of stellar evolution."*
