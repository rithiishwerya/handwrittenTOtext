# PDF Image Extraction and OCR Pipeline
This script processes a PDF file to extract images, performs OCR (Optical Character Recognition) on the extracted images, and saves the resulting text to a file. It is designed to handle various scenarios, including invalid file types, missing file paths, and PDFs without images.

### How It Works

##### 1. Input Validation
Before proceeding, the script checks:
File Type: The input must be a .pdf file. If the file is not a PDF, an error is raised:
                      "The input file must be a PDF."
File Existence: The script verifies if the file path exists. If the file is not found, an error is raised:
                      "The specified PDF file does not exist."

##### 2. Image Extraction
Function: extract_images_from_pdf(pdf_path)
Library Used: fitz (PyMuPDF)
Process:
The PDF is opened using fitz.open(pdf_path).
For each page in the PDF, the get_images() method identifies embedded images.
Each image is extracted using extract_image(xref) and converted to a PIL.Image object.
The extracted images are stored in a list.
Output: A list of PIL.Image objects representing all images in the PDF.
If no images are found, the script prints:
"No images found in the PDF."

##### 3. OCR on Extracted Images
Function: perform_ocr_on_images(images)
Library Used: pytesseract (Tesseract OCR)
Process:
Each image from the extracted list is passed to pytesseract.image_to_string() for OCR.
The text from all images is combined, with page delimiters (--- Page X ---) added for clarity.
Output: A single string containing all the extracted text.

##### 4. Save Extracted Text
Function: save_text_to_file(text, output_path)
Library Used: Built-in Python file handling (open function).
Process:
The combined text from the OCR step is saved into a .txt file.
The output file is written using UTF-8 encoding to ensure proper character representation.
Output: A .txt file containing the extracted text.

##### 5. Main Function
Function: main(pdf_path, output_txt_path)
This is the pipeline orchestrator. It:
Validates the input file.
Extracts images using extract_images_from_pdf.
Performs OCR on the extracted images with perform_ocr_on_images.
Saves the extracted text to a file via save_text_to_file.
Handles errors and edge cases at each step.



### Dependencies
#### fitz (PyMuPDF):
A Python library for working with PDF and other document formats, enabling tasks like extracting images, text, and metadata from PDF files.
#### pytesseract:
A Python wrapper for Google's Tesseract-OCR engine, used for extracting text from images using optical character recognition (OCR).
#### PIL (Pillow):
A Python Imaging Library fork that provides image processing capabilities, such as opening, manipulating, and saving image files in various formats.


##### Install Required Libraries:
      pip install pymupdf pillow pytesseract

##### Tesseract Setup:
      pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
