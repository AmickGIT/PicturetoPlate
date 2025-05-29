````markdown
# PictureToPlate

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![Torch](https://img.shields.io/badge/torch-1.12.0+-red) ![License](https://img.shields.io/badge/license-MIT-green)

---

## Overview

**PictureToPlate** is an agentic multimodal system that converts food images (and optional noisy titles) into structured, professional 3-step recipes. Leveraging vision-language models such as Qwen2.5-VL-3B-Instruct with 4-bit quantization for efficient inference, the pipeline:
1. Understands the image (ingredients, textures, dish name)  
2. Generates a concise 3-step recipe using few-shot text prompts  
3. Evaluates outputs against ground-truth using ROUGE metrics for benchmarking  

## Features

- Image Understanding: Produces detailed descriptions—ingredients, color, texture, and predicted dish name.  
- Recipe Generation: Crafts a 3-step professional recipe summary based on image descriptions and examples.  
- Efficient Inference: 4-bit quantization of Qwen2.5-VL-3B for lower memory footprint and faster runtime.  
- Benchmarking: Automatic ROUGE-1, ROUGE-2, and ROUGE-L scoring against test summaries.  
- Notebook Workflow: End-to-end pipeline implemented in `PictureToPlate.ipynb`.  

## Project Structure

```plaintext
.
├── Images/                # Training set images
├── Titles/                # Training dish titles (noisy)
├── Summaries/             # Training 3-step summaries
├── Test_Images/           # Test set images
├── Test_Titles/           # Test dish titles
├── Test_Summaries/        # Ground-truth summaries for evaluation
├── PictureToPlate.ipynb   # Jupyter Notebook: pipeline code & inference
├── prompts/               # Example prompts for description & recipe generation
└── offload/               # (future extensions)
````

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/your_username/PictureToPlate.git
   cd PictureToPlate
   ```

2. **Create a virtual environment**:

   ```bash
   python3.8 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**:

   ```bash
   pip install --upgrade pip
   pip install torch transformers accelerate
   pip install qwen-vl-utils[decord]==0.0.8
   ```

   > **Note**: Installing `transformers` and `accelerate` from source ensures Qwen2.5-VL compatibility and avoids `KeyError: 'qwen2_5_vl'`.

## Usage

1. **Prepare Inputs**: Place your images in `Test_Images/` (and optional `Test_Titles/` if using noisy titles).
2. **Launch Notebook**:

   ```bash
   jupyter notebook PictureToPlate.ipynb
   ```
3. **Run Inference**:

   * **Step 1**: Load and preprocess image.
   * **Step 2**: Generate a descriptive summary:

     ```python
     prompt = f"""Describe the food image with ingredients, texture, etc.

     Dish: {dish_title}
     """
     ```
   * **Step 3**: Generate a 3-step recipe:

     ```python
     prompt = f"""You are a professional recipe generator.

     Dish: {predicted_dish}
     Description: {description_text}
     Format: 3 steps
     1. ...
     2. ...
     3. ...

     Now generate the recipe.
     """
     ```
4. **Evaluate**: Compare generated summaries with ground-truth in `Test_Summaries/` to compute ROUGE scores.

## Pipeline Details

1. **Description Generation**

   * Prompt extracts ingredients, textures, color, and predicts dish name.
   * Few-shot examples include dishes like mustard fish, butter chicken, cheesy bake.

2. **Recipe Generation**

   * Uses the description to frame a concise, 3-step professional recipe.
   * Enforces structure: `Dish: <Name>` and `Summary: 1. ... 2. ... 3. ...`.

3. **Quantized Inference**

   * Utilizes 4-bit quantization (`bitsandbytes`) to accelerate Qwen2.5-VL-3B.

4. **Benchmarking**

   * ROUGE-1 F1 improved from 0.39 → 0.42 when using image description context.
   * Example metrics: Precision 0.361, Recall 0.592, F1 0.443 on ROUGE-1.

## Evaluation Results

| Metric     | Without Description | With Description |
| ---------- | ------------------: | ---------------: |
| ROUGE-1 F1 |                0.39 |             0.42 |
| ROUGE-2 F1 |               0.048 |                — |
| ROUGE-L F1 |               0.254 |                — |

## Examples

* **Input**: `Rice` + image of stir-fried rice
  **Output**: 3-step Fried Rice recipe capturing veggies, shrimp, seasoning

* **Input**: `Soupy Noodles` + bowl of ramen
  **Output**: 3-step Spicy Ramen recipe with broth, noodles, toppings

## Contributing

Contributions welcome! Please open an issue or submit a pull request. Ensure code quality and add tests for new features.

## License

This project is licensed under the MIT License. See `LICENSE` for details.

## Acknowledgements

* **Qwen2.5-VL-3B-Instruct** for vision-language capabilities
* **Hugging Face Transformers** for model integration
* **bitsandbytes** for 4-bit quantization

```
```
