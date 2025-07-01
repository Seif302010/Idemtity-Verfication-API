# Identity Verification API

A Flask-based API for identity verification and ID card data extraction, leveraging computer vision and OCR technologies.

## Features

- **Facial Verification**: Compare an ID card photo with a user-provided image to verify identity
- **ID Data Extraction**: Extract textual information from ID cards using OCR
- **Dual-OCR Engine**: Combines the strengths of Pytesseract (for numbers) and EasyOCR (for text)

## Technologies Used

- **Backend**: Python Flask
- **Computer Vision**: DeepFace for facial verification
- **OCR**: 
  - Pytesseract (optimized for national ID number extraction)
  - EasyOCR (for general text extraction)
- **Image Processing**: OpenCV

## API Endpoints

### 1. Facial Verification Endpoint

`POST /verify_identity`

Compares a photo from an ID card with another photo to verify if they show the same person.

**Request:**
- Form-data with two image files:
  - `id_card`: ID card image
  - `user_photo`: User photo to compare against

**Response:**
```json
{
  "verified": boolean,
  "confidence": float,
  "message": string
}
```
### 2. ID Data Extraction Endpoint

`POST /extract_id_data`

Extracts textual information from ID card images using combined OCR technologies.

**Request Parameters:**
- `id_card`: (required) ID card image file (JPG/PNG)

**Response:**
```json
{
  "success": boolean,
  "data": {
    "national_id": "string",
    "full_name": "string",
    "date_of_birth": "YYYY-MM-DD",
    "address": "string",
    "issue_date": "YYYY-MM-DD",
    "expiry_date": "YYYY-MM-DD"
  },
  "processing_time": float,
  "ocr_engine": "string"
}
```

**Error Responses:**

```json
{
  "success": false,
  "error": "Invalid image format",
  "suggestion": "Please upload a JPG or PNG file"
}
```
**Common Error Types:**

| HTTP Code | Error Type               | Description                          | Suggested Solution                  |
|-----------|--------------------------|--------------------------------------|-------------------------------------|
| 400       | Bad Request              | Invalid input format or parameters   | Check request format and parameters |
| 413       | Payload Too Large        | File exceeds maximum allowed size    | Reduce image file size (<5MB)       |
| 422       | Unprocessable Entity     | OCR processing failed                | Improve image quality/resolution    |
| 500       | Internal Server Error    | Server-side processing error         | Check server logs and retry         |

---

## 📦 Installation

**System Requirements:**
- Python 3.8+
- Tesseract OCR 5.0+
- 2GB RAM minimum (4GB recommended)

**Setup Instructions:**
```bash
# 1. Clone repository
git clone https://github.com/Seif302010/Idemtity-Verfication-API.git
cd Idemtity-Verfication-API

# 2. Install Python dependencies
pip install -r dependencies.txt

# 3. Install Tesseract OCR
# For Ubuntu/Debian:
sudo apt install tesseract-ocr
# For Windows: Download installer from UB Mannheim
```

## 📜 License

MIT License

Copyright (c) [2025] [Seif302010]

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

1. The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

2. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

For full details, see the [LICENSE](LICENSE) file in the project root.

---

## ❓ Support & Contact

**Getting Help:**
- 🐛 **Report Bugs:** [Open a GitHub Issue](https://github.com/Seif302010/Idemtity-Verfication-API/issues)
- 💡 **Feature Requests:** Use the "Feature request" template

**Before Submitting:**
1. Check existing issues
2. Include:
   - Error logs
   - Sample images (redacted)
   - Steps to reproduce
   - Expected vs actual behavior

**Maintainers:**
- [seif302010] ([@GitHubHandle](https://github.com/seif302010))

**Alternative Contact:**
✉️ Email: [seif302010@gmail.com]  

---

## 🙏 Acknowledgments

Special thanks to:
- The developers of [DeepFace](https://github.com/serengil/deepface)
- The [PyTesseract](https://github.com/madmaze/pytesseract) team
- [EasyOCR](https://github.com/JaidedAI/EasyOCR) contributors
- All our open source dependencies
