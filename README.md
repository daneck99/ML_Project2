# ML_Project2

## 🧩 Reproducibility Notes

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
