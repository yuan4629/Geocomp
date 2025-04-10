# Geocomp
Official Github of "Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework"

This repository contains various scripts used for data preparation, inference, evaluation, and visualization in our geolocation framework. Below is a description of each Python file in the Geoeval/ directory:

- **acc.py**  
  Calculates cosine similarity between two texts using Sentence-BERT. Useful for comparing semantic similarity of location descriptions.

- **calc_index.py**  
  Evaluates model predictions (city, country, continent) against ground truth by computing accuracy, recall, and F1-score.

- **chan.py**  
  Resizes images, encodes them in Base64, and sends them to the OpenAI API for analysis. Useful for multimodal experiments.

- **chaxun.py**  
  Counts `.txt` files in a folder. A utility script to check dataset completeness.

- **distance.py**  
  Measures geodesic distance between predicted and ground-truth coordinates. Calculates the percentage of predictions within 1km, 25km, and 750km.

- **eval.py**  
  Sends text to OpenAI API for scoring. Handles retries and writes the evaluation results to output files.

- **gps.py**  
  Extracts panoIDs from `.txt` files and queries their GPS coordinates using external geocoding services.

- **info2text.py**  
  Converts structured information from a CSV (city, country, continent) into individual `.txt` files for each panoID.

- **lat.py**  
  Extracts panoIDs for specific countries from a large dataset CSV (e.g., `tuxun_combined.csv`), preparing data for focused experiments.

- **pre.py**  
  Resizes and encodes images, optionally sends them to APIs. Can be used for image preparation or inference.

- **pretest.py**  
  A simplified version of `pre.py` to test image resizing and encoding logic in isolation.

- **preview_csv.py**  
  Prints the first few rows of a CSV file for quick inspection and debugging.

- **score_more_100.py**  
  Computes average scores, top 10%, and bottom 10% performance for each country from game session logs.

- **script.py**  
  Empty placeholder script. Reserved for future development.

- **sql.py**  
  Copies files from one folder to another based on panoID match, typically for syncing prediction and ground truth folders.

- **test.py**  
  Tests full image-to-response pipeline using OpenAI's multimodal API. Includes resizing and encoding steps.

- **tey.py**  
  Filters panoIDs for a target country and saves them into a CSV. Used to extract subsets for analysis.

- **train.py**  
  Full pipeline for sending images to GPT-4, asking geolocation questions, extracting structured answers, and saving them.

- **type.py**  
  Similar to `train.py` but uses image path descriptions instead of actual image encoding. Lightweight geolocation prompt testing.

- **unit.py**  
  Aggregates values from `.txt` result files and computes column-wise averages. Often used for final metric summarization.

- **yuce.py**  
  Uses GPT-4 to extract a specific location from text, then converts it into latitude/longitude using the Google Maps API.

# Dataset on Hugging Face
We have also released a public dataset on Hugging Face to support reproduction and further research:
👉 https://huggingface.co/datasets/ShirohAO/tuxun

This dataset contains:

- All metadata used in our experiments

- The standardized metadata format

- The list of 500 panoIDs used in our benchmark evaluation

Feel free to explore and cite if you find it useful!