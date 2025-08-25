# 🎬 Amazon Prime Video — Content Insights Dashboard

A data storytelling project exploring **Amazon Prime Video** titles: content mix, ratings, genres, geography, and release trends — all in one interactive Power BI report.

---

## 🔗 Live Dashboard
👉 **[Open the Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiNDU1NGNjNDQtYWQxOS00OTljLTgzYTMtNDlhMzBjNzc0YjFkIiwidCI6IjRmNDcyOThkLTI3OWMtNDhiYS1hOTgzLTJhMDk1YmUxODU1YiIsImMiOjEwfQ%3D%3D)**

![Dashboard Preview]  
![Image](assets/prime-video-dashboard.png)

---

## 📂 Project Files
- **amazon_prime_titles.csv** → Dataset used for analysis  
- **prime-video-dashboard.pbix** → Power BI file  
- **README.md** → Documentation  

---

## 📊 Snapshot (from the report)
- **Total Titles:** 9,655  
- **Unique Ratings:** 25  
- **Unique Genres:** 519 *(post split/normalization)*  
- **Unique Directors:** 5,771  
- **Coverage:** 1920 → 2021  

---

## 🌟 Key Insights

### 🎭 Content Mix
- **TV Shows:** ~7.81K (**80.8%**)  
- **Movies:** ~1.85K (**19.2%**)  
➡️ Prime Video catalog in this snapshot is **TV-first**.

---

### 🔖 Ratings (by total shows)
- **13+** → ~2.1K  
- **16+** → ~1.5K  
- **ALL** → ~1.3K  
- **18+** → ~1.2K  
- **R** → ~1.0K  
- **PG-13 / 7+ / other** → ~0.4K each  
➡️ Family/teen-friendly certificates dominate.

---

### 🎬 Top Genres (by total shows)
- **Drama** → **986**  
- **Comedy** → **536**  
- **Drama, Suspense** → **399**  
- **Comedy, Drama** → **377**  
- **Animation, Kids** → **356**  
- **Documentary** → **350**  
- **Kids** → **334**  
- **Action, Drama** → **297**  
➡️ **Drama** leads, with strong blends like *Comedy-Drama* and *Drama-Suspense*.

---

### 🗺️ Geography
- Broad global footprint with strong concentrations across **North America**, **Europe**, and **South Asia**.  
➡️ The catalog reflects **diverse regional production hubs**.

---

### 📈 Release Trend
- A steady rise through the 2000s → **sharp growth in the late 2010s**.  
➡️ Content acceleration mirrors the streaming boom.

---

## 🛠️ Build Notes

### Data Prep (Power Query)
- Trim/clean **type**, **rating**, **country** fields  
- Split multi-genre field (e.g., `listed_in`) into rows → build a **Genre Bridge** for correct counts  
- Validate **release_year** and derive year range  
- Optional: map/standardize country names for the filled map

### Sample Measures (DAX)
```DAX
-- Core KPIs
Total Titles     = COUNTROWS('Titles')
Total Ratings    = DISTINCTCOUNT('Titles'[rating])
Total Directors  = DISTINCTCOUNT('Titles'[director])
Start Year       = MIN('Titles'[release_year])
End Year         = MAX('Titles'[release_year])

-- Type split
Movies           = CALCULATE(COUNTROWS('Titles'), 'Titles'[type] = "Movie")
TV Shows         = CALCULATE(COUNTROWS('Titles'), 'Titles'[type] = "TV Show")
% Movies         = DIVIDE([Movies], [Total Titles])
% TV Shows       = DIVIDE([TV Shows], [Total Titles])

-- If using a normalized genre bridge
Total Genres     = DISTINCTCOUNT('Genre Bridge'[genre])
