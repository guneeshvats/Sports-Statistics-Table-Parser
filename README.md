# Sports Statistics Table Parser

## Overview

This repository provides a solution to extract structured data from PDF documents containing sports statistics tables, specifically for American football. The output includes metadata about each table and the extracted records, providing valuable insights into player and team performance.

UPDATE : Also going to submit a portion of this whole idea for the conference - "Mathsport" [for now its just an abstract]

### Problem Statement

**Input**: A PDF with several tables about sports statistics (American football) with player and team performance.

**Output**:
1. Structured data extracted from tables along with metadata.
2. Metadata for each table includes:
   - **Entity**: Whether the table is about a player or a team.
   - **Statistic**: Type of statistic (e.g., Rushing Yards, Touchdowns, Pass Attempts).
   - **StatPeriod**: Time period of the record (e.g., Game, Season, Career).

3. Extracted data fields include:
   - `PlayerName` (if applicable)
   - `OpponentName` (if applicable)
   - `StatValue`
   - `Ranking` (if applicable)
   - `Season` (if applicable)

4. Tables where the metadata does not apply are discarded.

---

## Repository Structure
Each file is a step in the process (and the step number is there in the name of `.py` file
- **`0_pdf_to_images.py`**: Converts PDF pages into high-resolution images.
- **`1_text_ocr.py`**: Applies OCR to extract text from images.
- **`1.1_text_cleaning.py`**: Cleans OCR output and consolidates fragmented lines.
- **`2_classified_tables_headers.py`**: Classifies table headers and filters relevant tables.
- **`3_final_parsed_tables.py`**: Parses tables into structured JSON format.
- **`3.1_improved_parsed_tables.py`**: Enhanced version with better handling of edge cases.
- **`enhanced_parsed_tables.json`**: Final structured output in JSON format.

---



## How to Run

1. Clone the repository:
   ```bash
   git clone <repository_url>
   cd <repository_name>
   ```
  
2. Install the modules and dependencies
   ```bash
   pip install -r requirements.txt

---

## Methodology

### 1. PDF to Image Conversion
- **Tool Used**: `pdf2image`
- **Process**:
  - Convert each PDF page into a high-resolution image for better OCR accuracy.
  - Output: `output_images/`

### 2. OCR Processing
- **Tool Used**: `Tesseract OCR`
- **Process**:
  - Extract text from the converted images.
  - Save the extracted text as plain text files.

### 3. Text Cleaning and Preprocessing
- **Process**:
  - Remove OCR artifacts and noise (e.g., special characters, line breaks).
  - Consolidate fragmented records into single lines.
  - Output: `preprocessed_tables.json`

### 4. Table Parsing
#### Rule-Based Parsing
- **Process**:
  - Use regex to extract key attributes like `PlayerName`, `OpponentName`, `StatValue`, and `Season`.
  - Address ambiguities using predefined patterns and fallback logic.
  - Output: `enhanced_parsed_tables.json`

#### LLM-Based Parsing
- **Tool Used**: Pre-trained LLM (e.g., Flan-T5 via Hugging Face)
- **Process**:
  - Design prompts to extract structured data in JSON format.
  - Refine prompts and preprocess inputs for better LLM performance.

### 5. Evaluation
- **Findings**:
  - Rule-based methods work well for straightforward cases but struggle with complex formats.
  - LLM outputs were inconsistent without domain-specific fine-tuning.

---

## Results

### Metadata Example
```json
{
  "metadata": {
    "entity": "Player",
    "statPeriod": "Game",
    "statistic": "Pass Attempts"
  },
  "records": [
    {
      "playerName": "Tyler Wilson",
      "opponentName": "Texas A&M",
      "statValue": 59,
      "ranking": 1,
      "season": 2012
    },
    .
    .
    .
  ]
}
```

## Tools and Frameworks

- **Programming Language**: Python
- **Libraries**:
  - `pdf2image`: For PDF-to-image conversion.
  - `pytesseract`: For OCR processing.
  - `re`: For regex-based parsing.
  - `transformers`: For LLM-based parsing.
- **Environment**: Local Python environment with dependencies listed in `requirements.txt`.

---

## Future Directions

1. **Domain-Specific LLM Fine-Tuning**:
   - Fine-tune LLMs for improved accuracy on sports statistics data.
2. **Hybrid Approach**:
   - Combine rule-based parsing for straightforward fields with LLMs for complex records.
3. **Enhanced Preprocessing**:
   - Develop advanced cleaning algorithms to handle OCR artifacts more effectively.
4. **Automated Evaluation**:
   - Integrate metrics to evaluate the completeness and accuracy of the extracted data.

---

