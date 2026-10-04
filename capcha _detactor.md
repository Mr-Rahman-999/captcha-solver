###### main.py







import cv2

import pytesseract



def detect\_captcha(image\_path: str) -> str:

&#x20;   """Preprocess image and extract text from CAPTCHA."""

&#x20;   image = cv2.imread(image\_path)

&#x20;   if image is None:

&#x20;       raise FileNotFoundError(f"Image not found at {image\_path}")



&#x20;   # Convert to grayscale \& apply thresholding to remove background noise

&#x20;   gray = cv2.cvtColor(image, cv2.COLOR\_BGR2GRAY)

&#x20;   \_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH\_BINARY\_INV)



&#x20;   # Extract text using OCR

&#x20;   config = "--psm 8 -c tessedit\_char\_whitelist=ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

&#x20;   text = pytesseract.image\_to\_string(thresh, config=config)

&#x20;   return text.strip()



if \_\_name\_\_ == "\_\_main\_\_":

&#x20;   sample\_image = "captcha\_sample.png"

&#x20;   try:

&#x20;       result = detect\_captcha(sample\_image)

&#x20;       print(f"Detected CAPTCHA Text: {result}")

&#x20;   except Exception as e:

&#x20;       print(f"Error: {e}")











###### requirements.txt



Plaintext

opencv-python

pytesseract

pillow





###### README.md



Markdown



\# CAPTCHA Detector



A simple Python-based tool to preprocess and extract text from CAPTCHA images using OpenCV and Tesseract OCR.



\## Features

\- Grayscale \& Thresholding image preprocessing

\- Character extraction using Tesseract OCR



\## Setup

1\. Install Tesseract OCR on your system.

2\. Install dependencies:

&#x20;  ```bash

&#x20;  pip install -r requirements.txt





















Run the detector:





Bash

python main.py

