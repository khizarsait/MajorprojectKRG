# Query-Based Video Segment Retrieval Using Knowledge Graphs


##  Project Structure

```
📂 Backend
   ├── Video_Transcript.ipynb    Video audio extraction, Whisper transcription
   ├── OCR_and_textmerge.ipynb # OCR-based visual text extraction # Merging audio-visual modality, segmentation
   └── text_to_KG.ipynb         # Entity-Relationship Extraction using REBEL and KG construction

📂 Frontend
   ├── app_retrieval_frontend.py           # Query-based Retrieval System (streamlit app + hybrid search)
```

---

## Setup Instructions



### 1. Install Required Packages
Install the following Python libraries:

```bash
pip install -r requirements.txt
```
Create a `requirements.txt` with:

```
re
nltk
transformers
sentence_transformers
numpy
streamlit
neo4j
```

OR manually install:

```bash
pip install nltk transformers sentence-transformers numpy streamlit neo4j
```

### 3. Additional Setup
- Download **Whisper** model weights automatically (handled internally during transcription).
- Install **CTranslate2** if using faster Whisper inference (optional).
- Setup a **Neo4j Aura Free** account:
  - Create a new **Neo4j Aura** database.
  - Save the **URI**, **Username**, and **Password** for later use.

---

## Dataset Preparation

1. **Prepare your videos** (local `.mp4` or similar files).
2. **Organize them** into a local directory (e.g., `videos/`).

---

## Execution Instructions

### Step 1: Backend (Data Preparation and KG Construction)

#### (a) Run Pipeline 1: Video to Transcript and OCR

- Open `Video_Transcript.ipynb` in **Google Colab**.
- Upload or mount your local video directory.
- This script:
  - Extracts audio
  - Generates transcripts using **Whisper**
-Open `OCR_and_textmerge.ipynb` in **Google Colab**.
  - Extracts visual text via **OCR**
  - Merges them into enriched text files

#### (b) Run Pipeline 2: Text to Knowledge Graph

- Open `text_to_KG.ipynb ` in **Google Colab**.
- **Important**:  
  - Replace your Neo4j **URI**, **Username**, and **Password** in the script.
- This script:
  - Processes the enriched transcript text
  - Extracts **(head, relation, tail)** triples using **REBEL**
  - Enriches entities using **NER**
  - Populates the **Neo4j Knowledge Graph** with segments, entities, and relationships

---

### Step 2: Frontend (Query-Based Retrieval)

####  Setup
- Open `app_retrieval_frontend.py` in **VS Code** (or your preferred IDE).
- Replace the following:
  - Neo4j **URI**, **Username**, **Password** in the connection section
  - `video_path` variable with the path to your **local video storage**

####  Modify Hyperparameters (optional)
- Set the value of **K** (top-k retrieval results) in the code if needed.

####  Run the Streamlit App
```bash
streamlit run app_retrieval_frontend.py
```

This launches a web-based frontend where users can enter natural language queries and retrieve matched video segments based on hybrid KG and semantic retrieval.

