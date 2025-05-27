# PictureToPlate

## Overview

**PictureToPlate** is a project that leverages vision-language models to generate concise, 3-step recipes from images of dishes. By utilizing advanced models like Qwen2.5-VL, the system can analyze a food image, describe it, and then generate a professional recipe summary in a standardized format.

## Features

- **Image-to-Recipe Generation:** Upload a food image and receive a 3-step recipe summary.
- **Vision-Language Model:** Uses Qwen2.5-VL for image understanding and text generation.
- **Dataset Structure:** Includes images, dish titles, and recipe summaries for both training and testing.
- **Jupyter Notebook Workflow:** The main logic is implemented in `PictureToPlate.ipynb`.

## Project Structure

```
.
├── Images/             # Main dataset images
├── Titles/             # Dish names for main dataset
├── Summaries/          # 3-step recipe summaries for main dataset
├── Test_Images/        # Test set images
├── Test_Titles/        # Dish names for test set
├── Test_Summaries/     # 3-step recipe summaries for test set
├── PictureToPlate.ipynb # Main Jupyter notebook for model inference
└── offload/            # (Empty or for future use)
```

## How It Works

1. **Image Input:** Provide a food image (e.g., from `Test_Images/`).
2. **Model Inference:** The notebook loads the Qwen2.5-VL model and processes the image to generate a description.
3. **Recipe Generation:** The model is prompted to generate a 3-step recipe summary based on the image and its description.
4. **Output:** The generated recipe is printed or saved for further use.

## Example

Given an image of "Fried Rice", the model might output:

```
Dish: Fried Rice
Summary:
1. Cook rice according to package instructions. In a large skillet, heat oil over medium-high heat. Add chopped red bell peppers, green bell peppers, and onion. Stir-fry for 2-3 minutes until softened. Add shrimp and cook for another 2-3 minutes until lightly browned. Add rice and stir-fry for 1-2 minutes until heated through. Season with soy sauce, sesame oil, and any desired seasonings such as garlic, ginger, or chili flakes. Garnish with chopped green onions and serve hot.
```

## Requirements

- Python 3.8+
- torch
- transformers (latest, built from source)
- accelerate
- qwen-vl-utils[decord]==0.0.8
- Jupyter Notebook

### Installation

To ensure compatibility with Qwen2.5-VL, install the latest Hugging Face Transformers and Accelerate from source:

```bash
pip install git+https://github.com/huggingface/transformers accelerate
```

> **Note:** If you do not install from source, you might encounter the following error:
> 
> ```
> KeyError: 'qwen2_5_vl'
> ```

We also offer a toolkit to help you handle various types of visual input more conveniently, as if you were using an API. This includes base64, URLs, and interleaved images and videos. Install it with:

```bash
# It's highly recommended to use the `[decord]` feature for faster video loading.
pip install qwen-vl-utils[decord]==0.0.8
```

## Usage

1. Clone the repository and navigate to the project directory.
2. Download or prepare your food images and place them in the appropriate folder.
3. Install the required dependencies as described above.
4. Open `PictureToPlate.ipynb` in Jupyter Notebook.
5. Follow the notebook instructions to run the model and generate recipes.
6. **After generating a recipe summary, compare it with the ground-truth summaries in `Test_Summaries/` to evaluate the model's performance.**

## Dataset

- **Images/** and **Test_Images/**: JPEG images of dishes.
- **Titles/** and **Test_Titles/**: Text files with dish names.
- **Summaries/** and **Test_Summaries/**: Text files with 3-step recipe summaries.

## Acknowledgements

- [Qwen2.5-VL](https://huggingface.co/Qwen/Qwen2.5-VL-3B-Instruct) for the vision-language model.
- HuggingFace Transformers library.
