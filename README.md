# **[DeepSeek-OCR-experimental](https://huggingface.co/spaces/prithivMLmods/DeepSeek-OCR-experimental)**

DeepSeek-OCR-experimental is an advanced, multi-purpose visual document intelligence and object localization sandbox. Powered by the unredacted `prithivMLmods/DeepSeek-OCR-Latest-BF16.I64-v2.0` architecture, this suite is designed to deliver highly accurate, structure-aware image text extractions.

The application offers multiple structured pipelines including layout-preserving document-to-markdown conversion, structural figure parsing, and open-ended textual object localization. By programmatically decoding predicted coordinate bounds (`<|det|>` anchors), the system maps normalized values back to pixel space and paints dynamic bounding boxes directly onto the target document canvas. It is fully accelerated on local hardware using custom attention kernels and served via an elegant, Steel Blue Gradio interface.

<img width="1730" height="1417" alt="image" src="https://github.com/user-attachments/assets/614a9a23-70e1-4002-9435-f8bd9e2bcb84" />

### **Key Features**

* **Structural Document Parsing:** Transitions seamlessly from raw document pixels into structure-aware Markdown strings, cleanly isolating mathematical notation, formatting, and paragraphs.
* **On-the-Fly Object Grounding:** Programmatically reads normalized bounding coordinates out of raw output sequences and draws boundary rectangles over specified objects or phrases.
* **Adaptive Aspect Resolution Profiles:** Features explicit, multi-stage processing resolutions (Tiny, Small, Base, Large, Gundam) to adapt pixel-space parameters up to $1280\times1280$ for various document qualities.
* **VRAM Optimization Configuration:** Evaluates calculations directly via BF16 precision and local attention kernel extensions, protecting local hardware layers from major activation spikes.
* **Steel Blue UI Framework:** Built with a tailored, modern frontend aesthetic utilizing the `Outfit` font, clean image upload areas, and interactive multi-line output streams.

### **Repository Structure**

```text
├── examples/
│   ├── 1.jpg
│   ├── 2.jpg
│   └── 3.jpg
├── app.py
├── LICENSE
├── pre-requirements.txt
├── README.md
└── requirements.txt

```

### **Installation and Requirements**

To initialize the DeepSeek-OCR-experimental environment locally, set up a **Python 3.10** environment with the deep learning stack specified below. A system containing a dedicated CUDA cu13-enabled GPU is required.

#### **Standard PIP Installation**

**1. Upgrade Package Manager**
Ensure your local package manager is upgraded to align with modern build conditions:

```bash
pip install pip>=26.0.0

```

**2. Install Core Dependencies**
Install the primary deep learning stack, diffusion utilities, and ecosystem structures. This setup explicitly builds on **PyTorch 2.11.0 and CUDA cu13**:

```bash
pip install -r requirements.txt

```

#### **Core Requirements List (`requirements.txt`)**

```text
git+https://github.com/huggingface/transformers.git@v4.57.6
git+https://github.com/huggingface/accelerate.git
git+https://github.com/huggingface/diffusers.git
git+https://github.com/huggingface/peft.git
huggingface_hub
sentencepiece
torchvision
matplotlib
accelerate
easydict
kernels
addict
gradio==6.9.0
einops
spaces
torch==2.11.0
numpy

```

### **Usage**

Once your infrastructure configuration and dependencies are successfully validated, run the application by executing the primary script module:

```bash
python app.py

```

Upon initialization, the system handles setup and brings the baseline model into memory in evaluation mode. Open your browser to the local loopback address provided in your terminal (typically `http://127.0.0.1:7860/`).

1. **Upload Asset:** Drop a page photo, textbook sheet, screenshot, or diagram directly into the **Upload Image** box (supports direct clipboard pasting).
2. **Configure Pipeline:** Select your resolution profile from the **Resolution Size** dropdown and pick an operational task:
* **Free OCR:** Extracts pure text arrays sequentially.
* **Convert to Markdown:** Converts formatting layouts into standardized Markdown structure.
* **Parse Figure:** Translates diagrams and chart structures.
* **Locate Object by Reference:** Enter a custom string keyword inside the **Reference Text** box to programmatically highlight specific text bounds.


3. **Execute:** Click **Process Image** to trigger a CUDA worker thread. Text extractions stream straight into the OCR output area, while layout grounding layers appear dynamically on the lower image component.

### **License and Source**

* **License:** [Apache License 2.0](https://github.com/PRITHIVSAKTHIUR/DeepSeek-OCR-experimental/blob/main/LICENSE)
* **GitHub Repository:** [https://github.com/PRITHIVSAKTHIUR/DeepSeek-OCR-experimental.git](https://github.com/PRITHIVSAKTHIUR/DeepSeek-OCR-experimental.git)
