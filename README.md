# ML_Project2

## 🧩 Reproducibility Notes
All experiments were conducted in a **Kaggle Notebook** environment using the following configuration:
 
- **Hardware**: Single NVIDIA T4 GPU * 2 (16*2GB VRAM)  
- **Execution time**: ~90 minutes for full fine-tuning (Step 3)

To ensure full reproducibility:

1. **Random Seeds**  
   - All random seeds were fixed to `42` for NumPy, PyTorch, and scikit-learn.  
   - Dataset splitting (`train_test_split`) used stratified sampling for consistent class balance.

2. **Offline Environment**  
   - The notebook was executed **without internet access**.  
   - All dependencies and models were preloaded from Kaggle datasets or `/kaggle/input` directories:  
     ```
     /kaggle/input/deberta-v3-small-local
     /kaggle/input/e5-small-v2
     /kaggle/input/llm-classification-finetuning
     ```
   - No online downloads or API calls were required.

3. **Deterministic Workflow**  
   - Cell 1: Define paths, environment variables, and shared arguments (`BASE_ARGS`)  
   - Cell 2–3: Load and preprocess CSVs (train/test/submit)  
   - Cell 4: Step1
   - Cell 5: Step2
   - Cell 6~: Step3~4

4. **Version Control & Dependencies**  
   - All package versions are pinned to prevent dependency drift.  
   - The same results can be reproduced on any Kaggle GPU runtime with the same model folders.

**Note:** No internet connection or external API access is required to reproduce the results.


### Import Models and Datasets

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
