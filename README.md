## Prepared By
- Praveen Kumar Palaboyina 

## Languages Used
- English, Telugu, Konkani

---

## 1. Introduction �
**Objective:** Embark on an exciting journey to build a multilingual autoregressive language model (LM) from the ground up! This project covers the full adventure—from data collection to fine-tuning and evaluation.

**Scope:**
- **Languages:** English (50%), Mother Tongue (30-40%), Indian Language (10-20%)
- **Token Target:** ~3 Billion tokens
- **Model Size:** 100M–150M parameters
- **Frameworks:** PyTorch, SentencePiece

---

## 2. Project Timeline & Phases 
### Overview of Phases
- **Phase 1: Data Collection & Preprocessing**
- **Phase 2: Tokenization**
- **Phase 3: Pre-training**
- **Phase 4: Fine-tuning on Reasoning Tasks**
- **Phase 5: Evaluation & Analysis**

Each phase comes with its own deliverables, scripts, and outputs—detailed below!

---

## 2. Phase 1 – Data Collection & Preprocessing 
### 2.1 English Corpus
- **Source:** Wikipedia dumps, Common Crawl (C4 subset), Project Gutenberg (public domain English books)
- **Tools:** Python scripts for downloading and cleaning
- **Process:**
  - Downloaded Wikipedia and Common Crawl datasets
  - Removed HTML tags, special symbols, and normalized Unicode
  - Deduplicated repeated sentences and segmented into smaller chunks
  - Stored articles into chunked text files (~10 MB each) for efficient processing

### 2.2 Telugu Corpus
- **Source:** Project Gutenberg (public domain Telugu books), Google Translation API (English → Telugu), Wikipedia Telugu pages
- **Tools:** `requests`, `BeautifulSoup` for scraping; Google Drive for storage
- **Process:**
  - Extracted Telugu book links from Project Gutenberg index
  - Downloaded plain text (UTF-8) versions of books
  - Used Google Translate API to expand Telugu data from English parallel corpora
  - Scraped Telugu Wikipedia pages and other digital texts
  - Cleaned metadata and unnecessary characters
  - Stored files in chunked format (~10 MB each); larger files (books/wiki dumps) kept as-is due to size

### 2.3 Konkani Corpus
- **Source:** Konkani literature datasets, blogs, and online articles (public domain)
- **Tools:** Web scraping with `requests`, `BeautifulSoup`; manual cleaning for some texts
- **Process:**
  - Collected Konkani text from digital libraries and online repositories
  - Scraped available Konkani Wikipedia articles
  - Normalized text (UTF-8 encoding, punctuation cleanup)
  - Deduplicated repeated lines and removed boilerplate content
  - Stored as text files (~10 MB per file) in Google Drive for consistency

**Token Statistics:** [To be updated with actual stats]

---

## 3. Phase 2 – Tokenization 
### 3.1 Tokenizer Choice
- **Method:** SentencePiece (BPE/Unigram model)
- **Vocabulary Size:** [To be filled] tokens (sufficient to cover English, Telugu, and Konkani)
- **Special Tokens:** `<pad>`, `<unk>`, `<bos>`, `<eos>`

### 3.2 Training Process
- Individual `.txt` files from the multilingual corpus (English, Telugu, Konkani) were used
- Data was shuffled and balanced according to the target token distribution:
  - English – ~50%
  - Telugu – ~30–40%
  - Konkani – ~10–20%
- SentencePiece was trained with appropriate vocabulary size

**Deliverables:**
- Trained tokenizer files (`tokenizer.model`, `tokenizer.vocab`)

---

## 4. Phase 3 – Pre-training 
### 4.1 Model Configuration
- **Architecture:** Transformer-based autoregressive language model
- **Parameter Size:** Between 100M–150M
- **Layers/Heads/Hidden Size:** Configured within resource limits
- **Objective:** Next token prediction (causal LM)

### 4.2 Training Setup
- **Framework:** PyTorch with Hugging Face Transformers
- **Compute Resources:** Google Colab / Kaggle T4 GPU
- **Scheduler:** Cosine learning rate schedule with warmup
- **Checkpointing:** Enabled to resume training in case of GPU timeouts

### 4.3 Training Logs
- Training monitored for loss and perplexity over epochs
- Resource utilization (GPU memory, runtime) tracked
- Checkpoints stored in Google Drive for persistence

**Deliverables:**
- Pretrained model checkpoints
- Training logs and metrics (loss, perplexity)

---

## 5. Phase 4 – Fine-tuning on Reasoning Tasks 
### 5.1 Reasoning Tasks
- **Task 1: Sequence of Actions**
  - **Common Sense MCQ Tasks:** "Question: Before you can eat soup, you should...  
    A) Put it in the fridge  
    B) Pour it into a bowl  
    C) Step on it  
    D) Turn on the TV"  
    **Answer: B) Pour it into a bowl**

- **Task 2: Stylistics & Pragmatics**
  - **Sarcasm vs. Irony Distinction:** "Oh, fantastic, another meeting, said after a long day. Is this more likely sarcasm or irony?"  
    **Answer: Sarcasm**

### 5.2 Fine-tuning Approach
- Collected random data for tasks and saved in JSON files
- Applied fine-tuning with these data

### 5.3 Results
- **Task 1 & Task 2:**
  - **English:** 100%
  - **Telugu:** 100% for Task1 & 62% for Task2
  - **Konkani:** 100% for Task1 & 43% for Task2

**Summary:**
- For some tasks, the model’s predictions for Telugu and Konkani deviated from gold-standard answers, showing variability and occasional random outputs instead of consistent reasoning

**Observations:**
- Balanced token distribution improved multilingual coverage
- SentencePiece tokenizer handled multilingual text effectively
- Resource constraints (limited GPU) required checkpointing and small-batch training
- Fine-tuning significantly improved reasoning performance, especially in English and Telugu

---

All scripts attached in Colab Notebook

---

## References 
- Hugging Face Transformers Documentation
- SentencePiece Documentation
- Project Gutenberg (English & Telugu texts)
- Indic NLP Datasets and Wikipedia dumps
- AI tools for Data collection and Few scripts
