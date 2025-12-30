# AI Summarizer

## Overview
AI Summarizer is a powerful, user-friendly web application designed to condense long articles and text documents into concise, easy-to-read summaries. Built with **Streamlit** and powered by state-of-the-art **Hugging Face Transformers**, this tool leverages the `sshleifer/distilbart-cnn-12-6` model to deliver accurate and coherent abstractive summaries.

## Features
- **Long Text Support**: Automatically handles texts longer than the model's token limit by intelligently splitting them into chunks.
- **State-of-the-Art Model**: Uses a distilled version of the BART model, optimized for summarization tasks (CNN/Daily Mail dataset).
- **Simple Interface**: Clean and intuitive UI built with Streamlit.
- **Adjustable Parameters**: (Code structure allows for future expansion to adjust min/max summary length).

## How It Works

### 1. The Transformer Model
The core of this application is the **DistilBART** model (`sshleifer/distilbart-cnn-12-6`).
- **Transformers Library**: We use the Hugging Face `transformers` library to easily load and run this pre-trained model.
- **Distillation**: This model is a "distilled" version of the larger BART model. It retains most of the performance while being smaller, faster, and requiring less memory, making it ideal for web deployment.
- **Abstractive Summarization**: Unlike extractive summarization (which just picks important sentences), this model generates *new* sentences to capture the essence of the text, similar to how a human would summarize.

### 2. Intelligent Chunking
Transformer models have a maximum limit on the amount of text they can process at once (typically 512 or 1024 tokens). To summarize long articles, this project implements a smart chunking strategy:
1.  **Sentence Splitting**: The input text is first split into individual sentences to avoid breaking the context in the middle of a sentence.
2.  **Chunk Creation**: Sentences are grouped together into chunks. We ensure that each chunk does not exceed 500 words (approximate token count) to stay safely within the model's limit.
3.  **Batch Processing**: Each chunk is fed into the summarization pipeline independently.
4.  **Aggregation**: The summaries from all chunks are concatenated to form the final summary.

## Installation

1.  **Clone the repository** (or download the files):
    ```bash
    git clone <repository-url>
    cd Summarizer
    ```

2.  **Install dependencies**:
    It is recommended to use a virtual environment.
    ```bash
    pip install streamlit transformers torch
    ```
    *Note: `torch` (PyTorch) is required as the backend for the transformers library.*

## Usage

1.  **Run the Streamlit app**:
    ```bash
    streamlit run app.py
    ```

2.  **Use the Application**:
    - A local web server will start, and a new tab should open in your default browser (usually at `http://localhost:8501`).
    - Paste your long text or article into the text area.
    - Click the **Summarize** button.
    - Wait for the model to process the text and view your summary below!

## Project Structure
- `app.py`: The main application script containing the Streamlit UI, chunking logic, and model pipeline.
- `README.md`: This documentation file.
