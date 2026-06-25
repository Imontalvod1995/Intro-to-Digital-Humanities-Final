# Intro-to-Digital-Humanities-Final
Author: Ivan Montalvo

Language: Python 3

Libraries: `pytesseract`, `Pillow` (PIL), `stanza`

## What this is
A small pipeline that takes a scanned image of a Spanish-language document, extracts the text from it with OCR, runs it through an NLP model to find named entities (people, places, organizations, etc.), and counts how often each entity shows up. This code was devised to analyze the first Spanish translation of Thomas More's Utopia. 

## How it works

1. OCR (`pytesseract` + `PIL`)

Opens the image file `00000009.jpg` (The first page of the aforementioned book) and runs `Tesseract OCR` on it, specifying Spanish . The result is the raw extracted text.

2. NLP setup (stanza)

Downloads Stanford's Stanza language model for Spanish (`stanza.download('es')`) and builds an NLP pipeline (`stanza.Pipeline('es')`).

3. Entity extraction

Runs the OCR'd text through the pipeline (`nlpz(moro_cord)`) and pulls out the list of named entities Stanza detected in the document.

4. Counting

Loops through every detected entity and counts how many times each one appears in the full entity list, then builds a dictionary mapping each entity to its count.

5. Output

Prints  a frequency table of named entities found in the document.

6. How to run it

1. Install the dependencies: `pip install pytesseract pillow stanza`

  Important: `pytesseract` is just a Python wrapper — you also need the actual Tesseract OCR engine installed on your system (e.g., via `apt install tesseract-ocr` on Linux, `brew install tesseract` on macOS, or the Windows     installer from the Tesseract project), plus the Spanish language pack for Tesseract.

2. Place the image `00000009.jpg` in the same folder as the script (swap the name out if you want to run this on a different image).

4. Run: `python Deep_Dive.py`

The first run will download Stanza's Spanish model, which can take some time. After that, it'll print a dictionary of `{entity: count}`.
