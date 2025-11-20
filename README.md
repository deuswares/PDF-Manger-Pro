Below is a **complete, professional, and fully-structured README.md** for your GitHub repository.
It includes:

* Project introduction
* Features
* Full installation guide
* Required dependencies
* Tesseract & Poppler setup
* How to run the program
* PyInstaller build instructions
* Troubleshooting
* Folder structure
* Contribution, License, Credits

You can copy-paste this directly into your repository as **README.md**.

---

# **PDF Manager – Metadata Editor & OCR Preview (PyQt5 GUI)**

PDF Manager is a powerful, GUI-based desktop application built with **Python + PyQt5** for managing and editing PDF metadata, renaming files intelligently, previewing text (with optional OCR), batch-editing metadata fields, and general PDF workflow automation.

The tool is optimized specifically for **Persian (Farsi) bank circulars**, but it works universally with all PDF files.

This project includes a **custom file explorer**, **metadata editor**, **OCR engine**, **first-page preview**, **batch operations**, **undo system**, **right-to-left preview**, **special file status icons**, and more.

---

## **Table of Contents**

1. [Features](#features)
2. [Screenshots](#screenshots-optional)
3. [Requirements](#requirements)
4. [Installation](#installation)
5. [Tesseract OCR Setup](#tesseract-ocr-setup)
6. [Poppler Setup](#poppler-setup)
7. [How to Run](#how-to-run)
8. [Building the EXE (PyInstaller)](#building-the-exe-pyinstaller)
9. [Troubleshooting](#troubleshooting)
10. [Project Structure](#project-structure)
11. [Contributing](#contributing)
12. [License](#license)
13. [Credits](#credits)

---

## **Features**

### **1. Smart PDF File Browser**

* Displays all PDFs in a selected folder.
* Custom status icons:

  * **Green tick** → filename = title AND author matches pattern `1234-5678`
  * **Yellow circle** → filename ≠ title
  * **Red cross** → otherwise
* Supports **sorting**, context menu, and right-click marking.

### **2. Metadata Editing**

Edit and save:

* Title
* Author
* Subject
* Keywords
* Producer
* Creator
* Creation Date
* Modification Date

Auto-save on field change.

### **3. Intelligent Rename System**

* Optional toggle: *Rename file to Title*
* Filename and Title stay synced when enabled
* File renaming is safe and validated
* Undo support included

### **4. Preview With OCR Fallback**

* Extract text from first page automatically
* If extraction fails → auto-OCR (Farsi)
* Optional "No OCR Mode" toggle
* Fully **Right-to-Left (RTL)** rendering with Unicode fixes

### **5. Batch Operations**

* **Set ALL Authors from filenames**
* **Set ALL Titles from filenames**

Each operation preserves other metadata and modifies only one field.

### **6. Undo System**

* All metadata changes and renames are snapshot-based
* Undo restores:

  * Previous metadata
  * Previous filename (when applicable)

### **7. File Deletion Support**

* Press Delete to remove a file from disk instantly

### **8. Custom Fonts & Alignment**

* Change filename field font
* Change preview panel font
* RTL/LTR alignment

---

## **Requirements**

Tested on:

* **Python 3.11+**
* **Windows 10/11**

Python packages:

```
PyQt5
PyPDF2
pytesseract
PyMuPDF
Pillow
```

Install them:

```
pip install PyQt5 PyPDF2 pytesseract pymupdf Pillow
```

---

## **Installation**

1. Clone this repository:

```
git clone https://github.com/your-username/pdf-manager.git
cd pdf-manager
```

2. Install required Python libraries:

```
pip install -r requirements.txt
```

or manually:

```
pip install PyQt5 PyPDF2 pytesseract pymupdf Pillow
```

3. Install Tesseract and Poppler
   (Instructions below)

4. Run the application:

```
python pdf_manager_gui.py
```

---

## **Tesseract OCR Setup**

1. Download Tesseract for Windows:
   [https://github.com/UB-Mannheim/tesseract/wiki](https://github.com/UB-Mannheim/tesseract/wiki)

2. Install to:

```
C:\Program Files\Tesseract-OCR\
```

3. Ensure these exist:

```
tesseract.exe
tessdata\fas.traineddata
tessdata\fa.traineddata
```

4. Confirm Tesseract works:

```
tesseract --version
```

The application already points to:

```python
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
```

Modify if your path differs.

---

## **Poppler Setup**

Poppler is used for rendering the first PDF page for OCR.

1. Download Poppler for Windows:
   [https://github.com/oschwartz10612/poppler-windows/releases/](https://github.com/oschwartz10612/poppler-windows/releases/)

2. Extract to:

```
C:\Program Files\poppler-25.07.0\
```

3. Important files must be in:

```
C:\Program Files\poppler-25.07.0\Library\bin\
```

Make sure this folder includes:

```
pdfinfo.exe
pdftoppm.exe
```

---

## **How to Run**

After installing packages and setting up dependencies:

```
python pdf_manager_gui.py
```

---

## **Building the EXE (PyInstaller)**

You can build a standalone Windows executable using:

```
pyinstaller ^
  --onefile ^
  --windowed ^
  --name PDF_Manager ^
  --add-data "C:\Program Files\Tesseract-OCR\tesseract.exe;Tesseract-OCR" ^
  --add-data "C:\Program Files\Tesseract-OCR\tessdata;tessdata" ^
  --add-data "C:\Program Files\poppler-25.07.0\Library\bin;poppler_bin" ^
  pdf_manager_gui.py
```

After building:

* EXE output will appear in:
  `./dist/PDF_Manager.exe`

---

## **Troubleshooting**

### **Preview is blank**

* The PDF may contain only images → enable OCR mode
* Check Poppler installation
* Ensure PyMuPDF (pymupdf) is installed

### **OCR doesn't work**

* Check Tesseract path
* Ensure `fas.traineddata` exists in the tessdata folder

### **Application does not show any files**

* Make sure the folder contains `.pdf` files
* Ensure name filters:

```python
self.model.setNameFilters(["*.pdf", "*.PDF"])
```

### **EXE crashes on another computer**

* Poppler directory was not included
* Tesseract directory missing
* Build again with correct `--add-data` paths

---

## **Project Structure**

```
pdf-manager/
│
├── pdf_manager_gui.py           # Main application
├── README.md                    # Documentation
├── requirements.txt             # Python dependencies
└── /assets                      # (optional) screenshots, logos
```

---

## **Contributing**

Pull requests are welcome.
If you plan to add major features, please open an issue first to discuss what you would like to change.

---

## **License**

This project is licensed under the MIT License.

---

## **Credits**

Created by Hamid (MyFoxit Project)
Includes open-source components:

* PyPDF2
* PyMuPDF
* PyQt5
* Tesseract OCR
* Pillow

---

If you want, I can also:

* Generate a **requirements.txt**
* Generate a **LICENSE file**
* Create a **GitHub release template**
* Add **shields/badges** to README
* Create a **beautiful preview image** for the repo

Just tell me.
