# Summarizer
# Podcast Summarizer

A Python-based tool to transcribe audio podcasts, summarize their content, and store summaries in Pinecone for retrieval. This project leverages local Whisper for transcription, a local summarization model (distilbart-cnn-12-6) as a fallback, and Pinecone for vector storage, all running in Google Colab.

## Features
- Transcribes audio files (e.g., MP3) using Whisper's `tiny` model.
- Generates concise 2-3 sentence summaries of podcast transcripts.
- Stores summaries as embeddings in a Pinecone index for potential future querying.
- Runs entirely on Colab's free tier with local processing to avoid API limitations.

## Requirements
- Python 3.12
- Google Colab environment
- Required libraries (installed via pip):
  - `langgraph`
  - `pyautogen`
  - `pinecone`
  - `sentence-transformers`
  - `openai-whisper`
  - `transformers`
  - `torch`

Set Up Google Colab

Open Google Colab (colab.research.google.com).
Create a new notebook and upload this repository's script (e.g., podcast_summarizer.py).
Install Dependencies

Run the following cell in Colab to install required packages:
python!pip install langgraph pyautogen pinecone sentence-transformers openai-whisper
Configure Environment Variables

Obtain a Pinecone API key from Pinecone Console.
Optionally, get a Hugging Face API key from Hugging Face (though local fallback is used).
Add these to your Colab environment:
pythonos.environ["PINECONE_API_KEY"] = "your-pinecone-api-key"
os.environ["HUGGINGFACE_API_KEY"] = "your-huggingface-api-key"  
Create a Pinecone Index

Ensure a Pinecone index named podcast-summaries exists with dimension 384 (matches all-MiniLM-L6-v2) in the us-east1-aws environment. The script creates it if absent.
Usage

Upload Audio

Run the script in Colab. It will prompt you to upload an audio file (e.g., sunsetgun_01_parker_64kb.mp3).


Process the Podcast

The script transcribes the audio, summarizes the transcript, and stores the summary in Pinecone.


View Results

Output will display the transcript and summary in the Colab console, e.g.:
textTranscript: [Transcribed text]
Summary: [2-3 sentence summary]
Stored in Pinecone: [Summary preview]...




Example Output
For an audio file of Dorothy Parker's "Sunset Gun" (LibriVox recording):

Transcript: Full text of the podcast section.
Summary: "Sunset Gun by Dorothy Parker, read by Winifred Aspen, is a LibriVox recording featuring poems like 'Godmother' and 'The Red Dress.' The collection explores themes of sadness, love, and mortality through poetic narratives."

Troubleshooting

Summary Repetition: If the summary repeats, adjust chunk size in the call_huggingface function (e.g., change 200 to 250, 150 to 200).
Pinecone Issues: Verify the API key and index name. Check storage with print(index.describe_index_stats()).
Performance: For longer audio, consider switching to whisper.load_model("base") (slower but more accurate).
