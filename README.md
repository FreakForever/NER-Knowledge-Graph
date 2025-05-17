# 🧠 Medical Knowledge Graph using NER

This project builds a **medical knowledge graph** using Named Entity Recognition (NER) and manual annotation for high-accuracy extraction of medical relationships.

---

## 📌 Pipeline

1. **Train a spaCy NER model** to extract medical entities (`MEDICINE`, `MEDICAL_CONDITION`, `PATHOGEN`).
2. **Manual Annotation with Gemini API:**  
   - Use Gemini API to generate manual labels for entities and relationships.
   - Compare the performance of manual annotation vs. spaCy NER model.
   - *Note: Manual annotation (via Gemini or expert review) often yields higher-quality triplets than automated NER model training, especially in complex medical texts*.
3. **Extract Triplets:**  
   - Format:  
     - `(MEDICINE) --TREATS--> (MEDICAL_CONDITION)`
     - `(PATHOGEN) --CAUSES--> (MEDICAL_CONDITION)`
4. **Build a Knowledge Graph** using NetworkX.
5. **Visualize** the graph using Matplotlib.

---

## 📊 Visualization Sample

- **Nodes:**  
  - Blue: Entities (`MEDICINE`, `MEDICAL_CONDITION`, `PATHOGEN`)
- **Edges:**  
  - Green labels: Relationships (`TREATS`, `CAUSES`)
  - Directed arrows indicate relationship direction

---

## 📁 Sample Input Format


---

## 🚀 How to Run

1. **Entity Extraction:**  
   - Train a custom spaCy NER model or use Gemini API/manual annotation for labeling entities in your medical texts.
2. **Triplet Extraction:**  
   - Parse sentences to extract relationships:
     - If a `MEDICINE` treats a `MEDICAL_CONDITION`, create a `TREATS` edge.
     - If a `PATHOGEN` causes a `MEDICAL_CONDITION`, create a `CAUSES` edge.
3. **Graph Construction:**  
   - Use NetworkX to add nodes (entities) and edges (relationships).
4. **Visualization:**  
   - Plot the graph with Matplotlib, styling nodes and edges according to entity and relationship type.

---

## 📝 Example Code Snippet

