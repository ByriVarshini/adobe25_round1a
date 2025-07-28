

````markdown
# 📄 Adobe Hackathon – Challenge 1A  
## 🧠 PDF Document Outline Extraction

---

## 🚀 Overview

This solution tackles **Challenge 1A** of the Adobe Hackathon.  
The goal is to convert a given PDF document into a structured outline with a clear hierarchy of:

- **Title**
- **Headings** (H1, H2, H3)
- **Page numbers**

This enables smart document navigation and downstream tasks such as semantic search or summarization.

---

## 📦 Folder Structure

```bash
CHALLENGE-1A/
├── sample_dataset/
│   ├── outputs/              # JSON outputs will be saved here
│   ├── pdfs/                 # Input PDF files go here
│   └── schema/
│       └── output_schema.json   # Output format reference
├── process_pdfs.py          # Main Python script
├── Dockerfile               # Docker configuration
├── requirements.txt         # Python dependencies
└── README.md                # This file
````

---

## 📥 Input

Place all `.pdf` files inside the folder:

```
sample_dataset/pdfs/
```

---

## 📤 Output

The corresponding `.json` files will be saved to:

```
sample_dataset/outputs/
```

Each output JSON will follow the structure defined in `output_schema.json`:

```json
{
  "title": "Understanding AI",
  "outline": [
    { "level": "H1", "text": "Introduction", "page": 1 },
    { "level": "H2", "text": "What is AI?", "page": 2 },
    { "level": "H3", "text": "History of AI", "page": 3 }
  ]
}
```

---

## 🧠 How It Works

* The script uses `PyMuPDF` to extract visual and positional text info.
* Heuristics are applied to detect:

  * Title (largest, top-most font near start)
  * Headings (by size, styling, format)
* All results are saved as structured JSON files.

---

## 🐳 Docker Usage

### 🔨 Build the Docker Image

```bash
docker build -t challenge1a.processor .
```

> `challenge1a.processor` is your custom image tag (you can rename it if needed).

---

### 🚀 Run the Processor

```bash
docker run --rm \
  -v ${PWD}/sample_dataset/pdfs:/app/input:ro \
  -v ${PWD}/sample_dataset/outputs:/app/output \
  --network none challenge1a.processor
```

> This command:

* Reads PDFs from `sample_dataset/pdfs`
* Writes JSONs to `sample_dataset/outputs`
* Uses `--network none` to ensure **offline execution**

---

## 📋 Constraints

| Requirement    | Limit                        |
| -------------- | ---------------------------- |
| Execution Time | ≤ 10 seconds per 50-page PDF |
| Model Size     | ≤ 200MB (if applicable)      |
| Environment    | CPU-only, offline mode       |
| Platform       | Must support `linux/amd64`   |

---

## 🧪 Testing & Validation

You can validate your JSON against the schema:

```
sample_dataset/schema/output_schema.json
```

Use tools like [https://jsonschema.net](https://jsonschema.net) or a script using `jsonschema` Python package.

---


## 🔗 References

* [Adobe Challenge Repo](https://github.com/jhaaj08/Adobe-India-Hackathon25)
* [PyMuPDF Documentation](https://pymupdf.readthedocs.io/en/latest/)

```

