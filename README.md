
# 🌐 Neural Enhanced Bloom Filter for URL Classification

This project implements an efficient hybrid system for classifying URLs as **malicious** or **benign** using a combination of deep learning and Bloom Filters. The hybrid approach aims to **accelerate filtering** by reducing reliance on expensive model inference, while improving **accuracy and memory efficiency** compared to traditional Bloom Filters.

---

## 📌 Key Features

- ✅ Combines deep neural networks with Bloom Filters for fast and accurate membership testing.
- 🔄 Implements three systems:
  - **Normal Bloom Filter**
  - **Neural Learned Bloom Filter (NLBF)**
  - **Sandwich Learned Bloom Filter (SLBF)**
- 🧠 Uses a fast hybrid neural network for URL classification.
- 📊 Benchmarks accuracy of all methods at varying false positive rates.
- 📈 Interactive visualizations with Plotly.

---

## 🚀 How It Works

### 🔢 Data Preparation

- Reads labeled URLs (`good` or `bad`) from `test_input.txt`.
- Balances the dataset to have 30,000 malicious and 30,000 benign URLs.

### 🔤 Tokenization

- Each URL is tokenized **character-wise** using a predefined alphabet.
- Sequences are padded to a fixed length (1014).

### 🧠 Model Architecture

Three variants are implemented:

1. **Fast Hybrid Model** (`fast_hybrid`)
   - Embedding → Separable Conv1D → MaxPooling
   - Bidirectional LSTM
   - Concatenated features passed through dense layers.

2. **Fast CharCNN Only** (`fast_charcnn`)
   - Stacked Separable Conv1D layers with pooling.
   - Pure CNN-based approach for maximum speed.

3. **Hybrid CNN + BiLSTM + Attention** (`hybrid_model`)
   - CharCNN + CNN-BiLSTM with Attention
   - Fused via concatenation and trained jointly.

### 🌸 Bloom Filters

- **Bloom Filter (BF):** Probabilistic data structure for set membership.
- **Learned Bloom Filter (LBF):** Replaces part of the filter with a classifier.
- **Sandwich Learned Bloom Filter (SLBF):** Wraps the classifier between two filters for improved precision and recall.

### 📈 Evaluation

- Trains the model to identify good URLs (`label = 1`).
- Filters are tested on the full dataset.
- Accuracy is measured at various error rates (1% to 10%).

---

## 📊 Results

An interactive Plotly graph shows the accuracy comparison:

- **Neural LBF** outperforms traditional Bloom Filter in most cases.
- **Sandwich LBF** offers a robust trade-off between **false positives** and **memory usage**.

> SLBF shows **higher accuracy** than BF at comparable error rates, making it well-suited for applications like spam detection, firewall filtering, and web crawlers.

---

## 💡 What is a Bloom Filter?

A **Bloom Filter** is a space-efficient probabilistic data structure used to test whether an element is a member of a set. It supports **false positives** but no false negatives. Key properties:

- Fast insertion and querying (O(1))
- No deletions
- Memory-efficient

**Learned Bloom Filters** integrate neural networks to reduce memory usage and error rates.

---

## 🛠️ Installation

```bash
pip install bloom_filter tensorflow tensorflow_hub plotly
```

Make sure your data file `test_input.txt` is in the working directory.

---

## 📂 Project Structure

```
.
├── LearnedBloomFilters.ipynb   # Main code for training, evaluation and filtering
├── test_input.txt              # Input data file (URLs and labels)
```

---

## 🔮 Future Work

- ⏱️ Train for more epochs and tune model hyperparameters.
- 🧪 Use larger datasets and multilingual URLs.
- 🔐 Integrate with real-time URL scanners or firewalls.
- 🧬 Explore Transformer-based architectures like BERT for improved classification.
- 📦 Package as a Python module or REST API.
- 🧹 Improve preprocessing and normalization of URLs.

---

## 🤝 Contributions

Pull requests and suggestions are welcome! Let’s build smarter filters together.

---

## 📜 License

This project is under the MIT License.
