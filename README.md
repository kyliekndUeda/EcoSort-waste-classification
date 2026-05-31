# EcoSort - AI-Powered Waste Classification

**EcoSort** is an AI-powered waste classification system that identifies waste types from user-uploaded images. Beyond classification, it explains the environmental impact of each item to encourage smarter and more sustainable disposal decisions. This project addresses the critical need for accurate waste sorting — essential for reducing landfill pollution and methane emissions.

> Developed for **CS 350: From Data Mining to Deep Learning** — Spring 2026, Elizabethtown College.

![EcoSort Web App](images/EcoSort_webapp.png)

---

## Features

- Upload an image and classify it into one of 10 waste categories
- Confidence score with a visual progress bar
- Per-category environmental facts:
  - Immediate impact of correct vs. incorrect disposal
  - Environmental insight (e.g., methane production, recycling savings)
  - Misclassification scenario (what goes wrong if sorted incorrectly)
- REST API backend (Flask) with a plain HTML/CSS/JS frontend — no framework required

---

## Waste Categories

| Category | Category |
|---|---|
| Cardboard | Metal |
| Food Organics | Miscellaneous Trash |
| Glass | Paper |
| Plastic (Opaque) | Textile Trash |
| Plastic (Transparent) | Vegetation |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Classification model | EfficientNetB7 (`waste_ENB7.keras`) |
| Backend | Python, Flask, Flask-CORS |
| Image processing | TensorFlow, NumPy, Pillow |
| Frontend | HTML, CSS, JavaScript (no framework) |

---

## Project Structure

```
waste-classification/
├── app.py               # Flask backend (prediction API)
├── index.html           # Frontend UI
├── waste_ENB7.keras     # Trained EfficientNetB7 classification model
├── requirement.txt      # Python dependencies
└── images/
    ├── EcoSort_webapp.png
    └── test_img.png
```

---

## Setup

### Prerequisites

- Python 3.11
- pip

### Installation

1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd waste-classification
   ```

2. Create and activate a virtual environment:
   ```bash
   python3.11 -m venv .venv311
   source .venv311/bin/activate   # Windows: .venv311\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirement.txt
   ```

4. Make sure `waste_ENB7.keras` is in the project root.

---

## Running the App

1. Start the Flask backend:
   ```bash
   python app.py
   ```
   The server starts at `http://127.0.0.1:5000`.

2. Open `index.html` in your browser (double-click the file or use a local server like Live Server in VS Code).

3. Choose an image, click **Classify**, and view the predicted waste category and environmental facts.

---

## API Endpoints

### `GET /RealWaste`
Health check — returns model load status.

**Response:**
```json
{ "status": "ok", "model_loaded": true }
```

### `POST /predict`
Classify a single uploaded image.

**Request:** `multipart/form-data` with field `image`

**Response:**
```json
{
  "class_index": 5,
  "label": "Paper",
  "confidence": 0.923,
  "all_predictions": {
    "Cardboard": 0.012,
    "Paper": 0.923,
    ...
  }
}
```

---

## Dataset

The model was trained on the **RealWaste** dataset, a real-world waste image dataset covering the 10 categories listed above.

---

## License

This project is licensed under the terms in the [LICENSE](LICENSE) file.
