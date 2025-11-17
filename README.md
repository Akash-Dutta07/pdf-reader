# Chat with PDF using Gemini 💁

A local, Streamlit-based application that allows you to chat with your PDF documents using Google's Gemini AI model. Upload multiple PDFs, ask questions, and get accurate answers based on the content of your documents. **This application runs entirely on your local system** - no deployment required.

## Features

- **Multi-PDF Support**: Upload and process multiple PDF files simultaneously
- **Intelligent Search**: Uses FAISS vector store for efficient semantic search
- **Conversational AI**: Powered by Google's Gemini 2.5 Flash model
- **Context-Aware Answers**: Provides detailed responses based strictly on the PDF content
- **Easy to Use**: Simple and intuitive Streamlit interface

## Prerequisites

- Python 3.11 or higher
- Google API Key for Gemini AI

## Installation

1. Download or clone this project to your local machine:
```bash
# If using git
git clone <your-repo-url>
cd <your-repo-name>

# Or simply download and extract the ZIP file
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file in the root directory and add your Google API key:
```
GOOGLE_API_KEY=your_google_api_key_here
```

To get a Google API key:
- Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
- Sign in with your Google account
- Create a new API key

## Usage

1. Run the Streamlit application locally:
```bash
streamlit run main.py
```

2. The application will automatically open in your default web browser at `http://localhost:8501`

3. **Upload PDFs**:
   - Click on the sidebar menu
   - Upload one or more PDF files from your local system
   - Click "Submit & Process" to process the documents

4. **Ask Questions**:
   - Once processing is complete, type your question in the text input field
   - Press Enter to get an AI-generated answer based on your PDF content

5. **To stop the application**:
   - Press `Ctrl + C` in the terminal where Streamlit is running

## How It Works

1. **PDF Processing**: Extracts text from uploaded PDF files using PyPDF2
2. **Text Chunking**: Splits the text into manageable chunks using LangChain's RecursiveCharacterTextSplitter
3. **Embeddings**: Converts text chunks into vector embeddings using HuggingFace's all-MiniLM-L6-v2 model
4. **Vector Storage**: Stores embeddings in a FAISS index for fast similarity search
5. **Question Answering**: Uses Google's Gemini model to generate accurate answers based on relevant document chunks

## Project Structure

```
.
├── main.py                          # Main application file
├── requirements.txt                 # Python dependencies
├── pyproject.toml                   # Project configuration
├── .env                            # Environment variables (create this)
├── .devcontainer/                  # Dev container configuration
│   └── devcontainer.json
└── README.md                       # This file
```

## Technologies Used

- **Streamlit**: Web application framework
- **LangChain**: Framework for building LLM applications
- **Google Gemini AI**: Large language model for question answering
- **FAISS**: Vector database for similarity search
- **HuggingFace Transformers**: Sentence embeddings
- **PyPDF2**: PDF text extraction

## Configuration

The application uses the following default settings:

- **Chunk Size**: 10,000 characters
- **Chunk Overlap**: 1,000 characters
- **Embedding Model**: all-MiniLM-L6-v2
- **LLM Model**: Gemini 2.5 Flash
- **Temperature**: 0.3 (for more focused answers)

## Notes

- **Local Application**: This runs entirely on your local machine - no internet deployment required
- The application stores the FAISS index locally in a `faiss_index` directory
- All PDF processing happens on your local system
- Your PDF files are never uploaded to any external server (except for API calls to Google Gemini for answering questions)
- Make sure your Google API key has access to the Gemini API
- The app will use your local resources (CPU/RAM) for processing PDFs

## Troubleshooting

**Issue**: "Answer is not available in the context"
- **Solution**: The question might be outside the scope of your uploaded PDFs. Try rephrasing or upload relevant documents.

**Issue**: API key errors
- **Solution**: Verify your `.env` file contains a valid `GOOGLE_API_KEY`

**Issue**: Processing takes too long
- **Solution**: Large PDFs may take time to process. Consider reducing chunk size or processing fewer documents at once.

