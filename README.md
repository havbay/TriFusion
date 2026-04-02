

#  TriThreatFusion – Multi-Layer Malware Detection Platform

## Project Overview

**TriThreatFusion** is an advanced malware detection system that combines **three complementary analysis methods**—hash verification, YARA signature scanning, and entropy analysis—to identify malicious files, ransomware, and encrypted threats. By integrating multiple detection techniques, it provides **high-accuracy threat assessments** and actionable intelligence in real-time.

---

## 🎯 Features

* **Multi-Method Detection** – Combines hash checking, signature scanning, and entropy analysis.
* **VirusTotal Integration** – Validate files against 70+ antivirus engines.
* **Extensive YARA Rules** – 446+ malware signatures for accurate detection.
* **Entropy Analysis** – Detects encrypted, compressed, or highly random files.
* **Beautiful Terminal Interface** – Color-coded, emoji-enhanced output.
* **Flexible Reporting** – Export results in JSON, CSV, or interactive HTML.
* **Batch & Recursive Scanning** – Scan files, directories, or entire systems.
* **Threat Scoring** – Intelligent scoring system (0.0–1.0) to classify threats as CLEAN, SUSPICIOUS, or MALICIOUS.

---

## 📋 Prerequisites

* Python 3.8 or higher
* Internet connection (for VirusTotal API, optional but recommended)
* 50MB free disk space (for YARA rules)

---

## 🔧 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/Nara-sakurai/TriThreatFusion.git
cd TriThreatFusion
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

Dependencies include:

* `requests>=2.31.0` – VirusTotal API communication
* `python-dotenv>=1.0.0` – Environment variable management
* `yara-python>=4.3.1` – YARA signature scanning
* `rich>=13.7.0` – Beautiful terminal output

### Step 3: Setup VirusTotal API (Optional)

1. Get a free API key from [VirusTotal](https://www.virustotal.com).
2. Create a `.env` file in the project root:

```
VIRUSTOTAL_API_KEY=your_api_key_here
```

> Without an API key, hash checking will be disabled, but signature and entropy analysis will still work.

### Step 4: Verify Installation

```bash
python main.py --scan samples/eicar.com
```

---

## 📖 Usage Guide

### Scan a Single File

```bash
python main.py --scan <filepath>
```

Example:

```bash
python main.py --scan samples/eicar.com
```

### Scan a Directory

```bash
python main.py --dir <directory>
```

Example:

```bash
python main.py --dir samples/
```

### Recursive Directory Scan

```bash
python main.py --dir <directory> --recursive
```

### Scan Specific File Types

```bash
python main.py --dir <directory> --ext exe,dll,bin,txt
```

### Generate Reports

* JSON:

```bash
python main.py --dir samples/ --report results.json --format json
```

* CSV:

```bash
python main.py --dir samples/ --report results.csv --format csv
```

* HTML:

```bash
python main.py --dir samples/ --report report.html --format html
```

---

## 🔬 Detection Methods

### 1. Hash-Based Detection

* Algorithms: SHA256 & MD5
* Purpose: Identify known malware using cryptographic fingerprints
* API: VirusTotal v3 (70+ engines)

### 2. Signature-Based Detection

* Engine: YARA v4.3.1
* Rules: 446+ compiled malware signatures
* Purpose: Detect known malware, ransomware, trojans, and exploits

### 3. Entropy Analysis

* Algorithm: Shannon Entropy
* Range: 0.0 – 8.0 bits per byte
* Purpose: Detect encrypted, compressed, or random data patterns

---

## 📊 Threat Scoring System

| Indicator                       | Weight |
| ------------------------------- | ------ |
| VirusTotal Malicious Detection  | 0.8    |
| VirusTotal Suspicious Detection | 0.4    |
| YARA High Severity Match        | 0.7    |
| YARA Medium Severity Match      | 0.5    |
| High Entropy Detection          | 0.6    |
| Suspicious File Extension       | 0.3    |

**Threat Levels:**

* CLEAN (0.0 – 0.39)
* SUSPICIOUS (0.4 – 0.69)
* MALICIOUS (0.7 – 1.0)

---

## 🧪 Testing

* **EICAR Test Virus:**

```bash
python main.py --scan samples/eicar.com
```

Expected: MALICIOUS (Score: 1.0/1.0)

* **Clean File:**

```bash
python main.py --scan samples/clean/hello.py
```

Expected: CLEAN (Score: 0.0/1.0)

* **Encrypted File:**

```bash
python main.py --scan samples/encrypted_large.bin
```

Expected: MALICIOUS or SUSPICIOUS (High entropy detected)

---

## 🚀 Future Improvements

* Machine learning-based detection
* PE file analysis (imports, sections)
* Sandbox execution for dynamic analysis
* Database for scan history
* Web interface for easier use
* Custom YARA rule creation wizard
* Multi-threaded scanning for faster performance
* Network traffic scanning
* Integration with additional threat intelligence APIs

---

## 🔒 Security Practices

* API keys stored in `.env`
* Input validation (file existence & type)
* Graceful error handling
* Respect VirusTotal rate limits
* Chunk-based file reading
* Safe scanning without code execution
* Timeout protection for YARA scans

---

## 🙏 Acknowledgments

* YARA Project – Pattern matching engine
* VirusTotal – Malware detection API
* Rich Library – Beautiful terminal output
* Open Source Community – YARA rule contributions


