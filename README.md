# 🧠 Medical Knowledge Graph using NER -> KG-RAG

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

```json
{
  "text": "Remdesivir is used to treat COVID-19 caused by SARS-CoV-2.",
  "entities": [
    {"text": "Remdesivir", "label": "MEDICINE"},
    {"text": "COVID-19", "label": "MEDICAL_CONDITION"},
    {"text": "SARS-CoV-2", "label": "PATHOGEN"}
  ]
}
```

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

```python
import networkx as nx
import matplotlib.pyplot as plt

# Example triplets
triplets = [
    ("Remdesivir", "TREATS", "COVID-19"),
    ("SARS-CoV-2", "CAUSES", "COVID-19")
]

# Build graph
G = nx.DiGraph()
for subj, rel, obj in triplets:
    G.add_node(subj)
    G.add_node(obj)
    G.add_edge(subj, obj, label=rel)

# Visualization
pos = nx.spring_layout(G)
edge_labels = nx.get_edge_attributes(G, 'label')
nx.draw(G, pos, with_labels=True, node_color='skyblue', node_size=2000, font_size=12, arrows=True)
nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels, font_color='green')
plt.show()
```

---

## 💡 Notes

-  Annotation (e.g., via Gemini API) is highly recommended for creating high-quality knowledge graphs in the medical domain, as it reduces errors from automated extraction and improves the reliability of relationships[5][7].
- For large-scale projects, consider a hybrid approach: use NER models for initial extraction, then refine with manual or LLM-assisted annotation for critical relationships.

---

## 📚 References

- spaCy documentation for custom NER model training
- NetworkX and Matplotlib for graph construction and visualization
- Gemini API or similar LLMs for manual annotation and label validation
