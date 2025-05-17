# 🧠 Medical Knowledge Graph using NER

This project builds a **medical knowledge graph** using Named Entity Recognition (NER) for the following entity types:
- `MEDICINE`
- `MEDICAL_CONDITION`
- `PATHOGEN`

## 📌 Pipeline

1. **Train a spaCy NER model** to extract medical entities.
2. *** Get the manual label marked using gemini api and compare the performance.(this is a better wat to create triplets compared to spacy model training)
3. **Extract triplets** in the form:
   - `(MEDICINE) --TREATS--> (MEDICAL_CONDITION)`
   - `(PATHOGEN) --CAUSES--> (MEDICAL_CONDITION)`
4. **Build a Knowledge Graph** using NetworkX.
5. **Visualize** the graph using Matplotlib.

## 📊 Visualization Sample

The graph nodes and edges are styled with labels and arrows:
- Blue nodes: entities
- Green edge labels: relationships (`TREATS`, `CAUSES`)

## 📁 Sample Input Format

```json
{
  "text": "Remdesivir is used to treat COVID-19 caused by SARS-CoV-2.",
  "entities": [
    {"text": "Remdesivir", "label": "MEDICINE"},
    {"text": "COVID-19", "label": "MEDICAL_CONDITION"},
    {"text": "SARS-CoV-2", "label": "PATHOGEN"}
  ]
}


