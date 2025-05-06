Intrinsic Signatures for Scanned Documents Forensics : Effect of Font Shape and Size
Overview
This project implements a scanner identification system inspired by the research paper "Intrinsic Signatures for Scanned Documents Forensics: Effect of Font Shape and Size." The system extracts the character 'e' from scanned PDF documents, computes texture-based features using Gray-Level Co-occurrence Matrix (GLCM) and Gray-Level Difference Histogram (GLDH), and classifies the source scanner (Xerox, Kyocera, or Brother) using Linear Discriminant Analysis (LDA) and Support Vector Machine (SVM) models. The dataset, sourced from Kaggle (nayanjain28/cv-dataset), contains three single-page PDFs scanned by different printers. The system processes these PDFs to extract 762–835 'e' characters, analyzes scanner-specific texture patterns, and achieves 84% classification accuracy, though with zero recall for 'e' characters due to class imbalance. Visualizations and a detailed report are provided to interpret results and suggest improvements.
Dependencies
The project requires the following Python packages and system libraries:
Python Packages

kagglehub==0.3.12
pdf2image==1.17.0
opencv-python==4.11.0.86
pytesseract==0.3.13
scikit-learn==1.6.1
numpy==2.0.2
pillow==11.2.1
matplotlib==3.9.2
seaborn==0.13.2
pandas==2.2.3
scipy==1.15.2

System Libraries

tesseract-ocr (version 4.1.1)
poppler-utils (version 22.02.0)
libgif, libjpeg, libpng, libtiff, libwebp, libopenjp2 (for Tesseract and image processing)

Dataset
The dataset is sourced from Kaggle (nayanjain28/cv-dataset, version 1) and includes three single-page PDF files:

Xerox_Versalink.PDF
kyocera-*5*.*2*._2025-*11*.*28*._59.pdf
Brother.pdf

Each PDF is scanned by a different printer (Xerox, Kyocera, Brother), providing diverse scanner outputs for texture analysis. The dataset is downloaded automatically using kagglehub during script execution.
Installation
To set up the project environment, follow these steps:

Clone the Repository:
git clone https://github.com/your-username/scanner-identification-system.git
cd scanner-identification-system


Install System Dependencies (Ubuntu/Debian):
sudo apt-get update
sudo apt-get install -y tesseract-ocr poppler-utils


Set Up a Python Environment:Create and activate a virtual environment (Python 3.11 recommended):
python3 -m venv venv
source venv/bin/activate


Install Python Packages:
pip install kagglehub pdf2image opencv-python pytesseract scikit-learn numpy pillow matplotlib seaborn pandas scipy


Configure Tesseract:Ensure Tesseract is accessible:
tesseract --version

Update the Tesseract path in CV_project.ipynb if necessary:
pytesseract.pytesseract.tesseract_cmd = '/usr/bin/tesseract'


Authenticate Kaggle:Set up Kaggle API credentials for dataset download:

Obtain your Kaggle API key from kaggle.com/account.
Place kaggle.json in ~/.kaggle/:mkdir -p ~/.kaggle
cp kaggle.json ~/.kaggle/
chmod 600 ~/.kaggle/kaggle.json





Usage
To replicate the results, run the Jupyter notebook in a Google Colab environment or locally:

Open the Notebook:

Google Colab:
Upload CV_project.ipynb to Google Colab.
Ensure the runtime uses a GPU (T4 recommended) for faster processing.


Local:jupyter notebook CV_project.ipynb




Execute All Cells:

Run all cells sequentially to:
Download the dataset.
Install dependencies.
Extract 'e' characters from PDFs.
Compute GLCM and GLDH features.
Train and evaluate LDA and SVM classifiers.
Generate visualizations (GLCM/GLDH plots, confusion matrices, sample images).


Expected output:GRAND TOTAL 'e' CHARACTERS IN ALL PDFs: 835
GRAND TOTAL 'e' CHARACTERS IN BLOCKS: 729
LDA Accuracy: ~84.08%
SVM Accuracy: ~84.19%
Majority Voting Accuracy: ~84.19%




Generate LaTeX Report:

Compile e_extraction_report.tex in Overleaf or locally using PDFLaTeX.
Ensure the following images are in the same directory as e_extraction_report.tex:
Normalized GLCM.png
Normalized GLDH.png
LDA confusion.png
SVM confusion.png
majority_confusion.png
x_extracted.png
K_extracted.png
B_extracted.png


Local compilation:latexmk -pdf e_extraction_report.tex




Download Results (Colab):

Zip and download generated images:!zip -r report_figures.zip *.png
from google.colab import files
files.download('report_figures.zip')





File Structure
The repository contains the following files:

CV_project.ipynb: Jupyter notebook implementing the scanner identification system.
e_extraction_report.tex: LaTeX source for the project report.
README.md: This file, providing project documentation.
output/ (generated during execution):
Normalized GLCM.png: Bar plot of GLCM features.
Normalized GLDH.png: Bar plot of GLDH features.
LDA confusion.png: Confusion matrix for LDA.
SVM confusion.png: Confusion matrix for SVM.
majority_confusion.png: Confusion matrix for majority voting.
x_extracted.png: Sample 'e' characters from Xerox PDF.
K_extracted.png: Sample 'e' characters from Kyocera PDF.
B_extracted.png: Sample 'e' characters from Brother PDF.



Results
The system achieved the following key results:

Character Extraction: Extracted 762 'e' characters using Tesseract’s image_to_boxes (more accurate than image_to_string, which reported 835 due to OCR errors).
Feature Extraction:
GLCM features (contrast, correlation, energy, homogeneity) captured spatial texture patterns.
GLDH features (energy, entropy) quantified intensity differences across 762 characters.


Classification:
LDA and SVM models achieved ~84% accuracy but zero recall for 'e' characters due to class imbalance (4057 non-'e' vs. 762 'e' characters).
Majority voting did not improve performance.


Visualizations:
Bar plots showed scanner-specific texture differences (e.g., higher contrast in Xerox scans).
Confusion matrices highlighted classification challenges.
Sample 'e' images illustrated visual texture variations.


