# Hugging Face Intro

A beginner-friendly Google Colab notebook that demonstrates the core Hugging Face workflow: using the Hugging Face Hub, accessing models and datasets, working with tokens, calling inference APIs, creating and uploading repositories, using `datasets`, exploring tokenizers, loading Transformer models, and generating embeddings.

This repository is intended as a learning notebook for students or developers who are getting started with Hugging Face, Transformers, tokenization, and LLM-related workflows.

## Repository Contents

| File | Description |
|---|---|
| `huggingface_intro.ipynb` | Main introductory notebook covering Hugging Face Hub, datasets, tokenizers, models, inference, and embeddings. |
| `huggingface_conti.ipynb` | Continuation notebook for additional Hugging Face practice and experiments. |
| `README.md` | Project documentation. |
| `LICENSE` | MIT License. |

## What This Notebook Covers

The notebook includes hands-on examples for:

- Accessing Hugging Face tokens securely in Google Colab
- Using `huggingface_hub` APIs
- Viewing model metadata such as tags, downloads, files, and commit SHA
- Searching models on the Hugging Face Hub
- Listing files inside model repositories
- Viewing dataset repository information
- Using Hugging Face Inference API
- Using Gemini as an alternative LLM API from Google Colab
- Connecting Hugging Face models with LangChain
- Creating a Hugging Face repository programmatically
- Uploading files to a Hugging Face repository
- Loading datasets using the `datasets` library
- Exploring pretraining, instruction-tuning, preference, and sentiment datasets
- Filtering, shuffling, selecting, and mapping over datasets
- Creating a custom dataset from a pandas DataFrame
- Pushing a dataset to the Hugging Face Hub
- Tokenizing text with different Transformer tokenizers
- Building a small custom BPE tokenizer
- Loading BERT and inspecting its layers, attention blocks, and hidden states
- Running masked language modeling with BERT
- Loading and generating text with a causal language model
- Downloading a model locally using `snapshot_download`
- Creating sentence embeddings and computing cosine similarity

## Tech Stack

- Python
- Google Colab
- Hugging Face Hub
- Hugging Face Transformers
- Hugging Face Datasets
- Hugging Face Tokenizers
- Sentence Transformers
- LangChain
- Google Gemini API
- PyTorch
- pandas

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/SamirSanyal312/huggingface_intro.git
cd huggingface_intro
```

### 2. Open the Notebook

You can open the notebook in Google Colab or Jupyter Notebook.

For Google Colab:

1. Go to [Google Colab](https://colab.research.google.com/)
2. Click **File > Open notebook**
3. Select the GitHub tab
4. Paste the repository URL
5. Open `huggingface_intro.ipynb`

### 3. Install Dependencies

Most dependencies are installed inside the notebook. If you are running locally, install the main packages with:

```bash
pip install huggingface_hub datasets transformers tokenizers sentence-transformers torch pandas
pip install langchain-huggingface langchain-community langchain-google-genai google-genai
```

## Required API Keys and Tokens

This notebook uses API tokens for Hugging Face and Gemini.

### Hugging Face Tokens

Create tokens from your Hugging Face account settings:

- `HF_TOKEN_READ` for reading models and datasets
- `HF_TOKEN_WRITE` for creating repositories and uploading datasets/files

In Google Colab, store them using:

1. Open the left sidebar
2. Click the **Secrets** key icon
3. Add:
   - `HF_TOKEN_READ`
   - `HF_TOKEN_WRITE`
4. Enable notebook access for both secrets

### Gemini API Key

For Gemini examples, add this Colab secret:

- `GEMINI_API_KEY`

## Important Security Note

Do not hardcode API keys or tokens directly in the notebook.

Use Colab Secrets or environment variables instead:

```python
from google.colab import userdata

READ_TOKEN = userdata.get("HF_TOKEN_READ")
WRITE_TOKEN = userdata.get("HF_TOKEN_WRITE")
GEMINI_API_KEY = userdata.get("GEMINI_API_KEY")
```

Before pushing your notebook to GitHub, make sure it does not contain:

- Raw Hugging Face tokens
- Gemini API keys
- Private credentials
- Personal access tokens
- Sensitive output logs

## Example Usage

### Get Hugging Face model metadata

```python
from huggingface_hub import HfApi

api = HfApi()
model_info = api.model_info(repo_id="bert-base-uncased")

print(model_info.tags)
print(model_info.downloads)
print(model_info.siblings)
```

### Load a dataset

```python
from datasets import load_dataset

dataset = load_dataset("stanfordnlp/imdb")
print(dataset)
```

### Use a tokenizer

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-cased")
output = tokenizer("I love AI")

print(output)
print(tokenizer.convert_ids_to_tokens(output["input_ids"]))
```

### Create sentence embeddings

```python
from sentence_transformers import SentenceTransformer
import torch.nn.functional as F

model = SentenceTransformer("all-MiniLM-L6-v2")

embedding1 = model.encode("I love AI", convert_to_tensor=True)
embedding2 = model.encode("I love cars", convert_to_tensor=True)

similarity = F.cosine_similarity(
    embedding1.unsqueeze(0),
    embedding2.unsqueeze(0)
)

print(similarity.item())
```

## Recommended Folder Structure

```text
huggingface_intro/
│
├── huggingface_intro.ipynb
├── huggingface_conti.ipynb
├── README.md
├── LICENSE
└── .gitignore
```

## Suggested `.gitignore`

```gitignore
# Python
__pycache__/
*.py[cod]
*.pyo
*.pyd
.Python
.env
.venv
venv/

# Jupyter
.ipynb_checkpoints/

# Secrets
.env
*.key
*.pem

# Model and dataset artifacts
download-model-on-disk/
my_tokenizer_hf/
custom-tokenizer.json

# OS files
.DS_Store
Thumbs.db
```

## Notes

Some cells may require a valid Hugging Face write token, especially the examples that create repositories or push datasets to the Hugging Face Hub.

Some models may require gated access, enough inference credits, or a machine with sufficient memory. If a model fails due to access or memory limits, try a smaller public model such as:

- `bert-base-uncased`
- `distilbert-base-uncased`
- `TinyLlama/TinyLlama-1.1B-Chat-v1.0`
- `google/flan-t5-small`
- `all-MiniLM-L6-v2`

## Learning Goal

By the end of this notebook, you should understand how to:

- Navigate the Hugging Face ecosystem
- Use models and datasets from the Hub
- Work with tokenizers
- Inspect Transformer model internals
- Run basic model inference
- Create and upload custom datasets
- Generate sentence embeddings for similarity tasks

## Author

**Samir Sanyal**

GitHub: [@SamirSanyal312](https://github.com/SamirSanyal312)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
