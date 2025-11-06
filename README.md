# ML_Project2

## 🧩 Reproducibility Notes




### ✅ Step 1. Import Models and Datasets

Before running the notebook, add all required models and datasets to your Kaggle environment.

#### 📦 How to Add
1. Go to the right sidebar in your Kaggle Notebook → **"Add data"**
2. Add the following inputs (either as **Models** or **Datasets**):
   - `microsoft/deberta-v3-small` → (as model, or upload as dataset: `/kaggle/input/deberta-v3-small-local/`)
   - `llm-classification-finetuning` → (dataset with `train.csv`, `test.csv`, `sample_submission.csv`)

> 💡 You can find these either under **“Models”** tab in Kaggle, or upload them manually as datasets.  
> Make sure **Internet is OFF**, since all weights and data are local.
>
> 

This section documents all details required to reproduce the experiments.

### 🔧 Environment
- **Runtime:** Kaggle GPU (T4 * 2)
- **Core Libraries:**
  - `torch`
  - `transformers`
  - `sentence-transformers`
  - `datasets`
  - `scikit-learn`
  - `pandas`, `numpy`, `matplotlib`, `tqdm`
- **Mixed Precision:** `torch.amp.autocast("cuda")` (automatic mixed precision enabled)

### ⚙️ Final Model Training Configuration
| Setting | Value |
|----------|--------|
| `random_state` | 42 |
| `epochs` | 5 |
| `optimizer` | AdamW (lr = 1.2e-5) |
| `scheduler` | Cosine with 6% warmup |
| `label_smoothing` | 0.08 |
| `weight_decay` | 0.03 |
| `dropout` | 0.2 (hidden/classifier) |
| `early_stopping` | patience = 2 |

### 🔒 Handling No-Internet Constraint
All external model weights were **pre-uploaded to `/kaggle/input/`** directories:
