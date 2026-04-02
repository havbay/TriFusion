# CTIP - Cryptographic Threat Intelligence

## 🔐 Project Overview

CTIP (Cryptographic Threat Intelligence Platform) is an advanced malware detection system that combines multiple analysis techniques to identify malicious files, ransomware, and encrypted threats. The system uses cryptographic hashing, signature-based detection, and entropy analysis to provide comprehensive threat assessment.

---

## 🎯 Project Description

CTIP is a multi-layered malware scanner that employs three distinct detection methods:

1. **Hash-based Detection (VirusTotal Integration)** - Calculates cryptographic hashes (SHA256, MD5) and checks them against VirusTotal's malware database
2. **Signature-based Detection (YARA Rules)** - Scans files using 446+ YARA malware signatures to identify known threat patterns
3. **Behavior Analysis (Shannon Entropy)** - Analyzes file randomness to detect encryption, compression, and suspicious data patterns

The system provides:
- Real-time threat scoring and classification
- Beautiful terminal output with color-coded results
- Comprehensive reports in JSON, CSV, and HTML formats
- Support for single file and directory scanning

---

## 🚀 Key Features

- ✅ **Multi-Method Detection** - Combines 3 detection techniques for high accuracy
- ✅ **VirusTotal Integration** - Validates files against 70+ antivirus engines
- ✅ **446 YARA Rules** - Extensive malware signature database
- ✅ **Entropy Analysis** - Detects encrypted files and ransomware
- ✅ **Beautiful TUI** - Color-coded, emoji-enhanced terminal interface
- ✅ **Multiple Report Formats** - Export results as JSON, CSV, or HTML
- ✅ **Batch Scanning** - Scan entire directories recursively
- ✅ **Threat Scoring** - Intelligent scoring system (0.0-1.0)
- ✅ **Clean Code** - Well-structured, maintainable, documented

---

## 📋 Prerequisites

- Python 3.8 or higher
- Internet connection (for VirusTotal API)
- 50MB free disk space (for YARA rules)

---

## 🔧 Installation & Setup

### Step 1: Clone the Repository
```bash
git clone https://github.com/Nara-sakurai/CryptographicThreatIntelligencePlatform-CTIP-.git
cd CryptographicThreatIntelligencePlatform-CTIP-
```
### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

**Dependencies:**
```
requests>=2.31.0
python-dotenv>=1.0.0
yara-python>=4.3.1
rich>=13.7.0
```

### Step 3: Setup VirusTotal API (Optional but Recommended)

1. Get a free API key from [VirusTotal](https://www.virustotal.com/gui/join-us)
2. Create a `.env` file in the project root:
```bash
VIRUSTOTAL_API_KEY=your_api_key_here
```

**Note:** Without an API key, hash checking will be disabled, but signature and entropy analysis will still work.

### Step 4: Verify Installation
```bash
python main.py --scan samples/eicar.com
```

---

## 📖 Usage Guide

### Basic Usage

#### Scan a Single File
```bash
python main.py --scan <filepath>
```

**Example:**
```bash
python main.py --scan samples/eicar.com
```

#### Scan a Directory
```bash
python main.py --dir <directory>
```

**Example:**
```bash
python main.py --dir samples/
```

#### Recursive Directory Scan
```bash
python main.py --dir <directory> --recursive
```

**Example:**
```bash
python main.py --dir samples/ --recursive
```

#### Scan Specific File Types
```bash
python main.py --dir <directory> --ext <extensions>
```

**Example:**
```bash
python main.py --dir samples/ --ext exe,dll,bin,txt
```

### Generate Reports

#### JSON Report
```bash
python main.py --dir samples/ --report results.json --format json
```

#### CSV Report
```bash
python main.py --dir samples/ --report results.csv --format csv
```

#### HTML Report (Interactive)
```bash
python main.py --dir samples/ --report report.html --format html
```

---

## 📊 Usage Examples

### Example 1: Detect EICAR Test Virus
```bash
$ python main.py --scan samples/eicar.com

🔐 CTIP - Cryptographic Threat Intelligence Platform
====================================================================
📁 File: eicar.com
   Size: 69 bytes

1. 🔑 VirusTotal Hash Check
   🚨 54/76 engines detected malware

2. 🔍 Malware Signature Detection
   🎯 Found 2 signature matches
   ⚠️ HIGH SEVERITY (1)
   • eicar - Rule to detect Eicar pattern

3. 📊 File Behavior Analysis (Entropy)
   Entropy: 4.91 bits
   📝 TYPICAL_BINARY

4. 🎯 Final Threat Assessment
   🚨 MALICIOUS FILE DETECTED
   Threat Score: 1.0/1.0 | Confidence: HIGH
   Multiple detection methods confirm this file is malicious

   Detection Indicators:
   🔑 VirusTotal: 54 engines detected as malicious
   🔍 Signature: 1 high severity rule: eicar
====================================================================
```

### Example 2: Detect Encrypted/Ransomware File
```bash
$ python main.py --scan samples/encrypted_large.bin

3. 📊 File Behavior Analysis (Entropy)
   Entropy: 7.92 bits
   🔒 LIKELY_ENCRYPTED
   Very high entropy (7.9) with 100% unique bytes suggests encryption

4. 🎯 Final Threat Assessment
   🚨 MALICIOUS FILE DETECTED
   Threat Score: 0.77/1.0 | Confidence: MEDIUM

   Detection Indicators:
   📊 Behavior: High entropy (7.92) - possible encryption detected
```

### Example 3: Scan Directory and Generate HTML Report
```bash
$ python main.py --dir samples/ --report scan_results.html --format html

📁 Scanning directory: samples/
📊 Found 7 file(s) to scan
[Scanning progress...]
📄 Generating HTML report: scan_results.html
✅ Report saved to: scan_results.html

📊 SCAN SUMMARY
📄 Files scanned: 7
🚨 Malicious: 4
⚠️  Suspicious: 0
✅ Clean: 3
```

---

## 🏗️ Project Structure

```
CTIP/
├── main.py                      # Main entry point
├── requirements.txt             # Python dependencies
├── .env                         # API keys (create this)
├── README.md                    # This file
├── all-yara-rules-database/     # YARA malware signatures (446 files)
├── samples/                     # Test files
│   ├── clean/                   # Clean test files
│   │   ├── hello.py
│   │   ├── data.txt
│   │   └── document.txt
│   ├── suspicious/              # Suspicious test files
│   │   ├── encrypted.bin
│   │   ├── svchost.exe
│   │   └── photo.jpg.encrypted
│   ├── eicar.com                # EICAR test virus
│   ├── random.bin               # High entropy file
│   └── encrypted_large.bin      # Encrypted test file
└── src/                         # Source code modules
    ├── __init__.py              # Package initialization
    ├── hash_checker.py          # VirusTotal hash checking
    ├── signature_scanner.py     # YARA signature scanning
    ├── entropy_detector.py      # Entropy analysis
    ├── classifier.py            # Threat classification
    ├── display.py               # Terminal output formatting
    └── reporter.py              # Report generation
```

---

## 🔬 Technical Details

### Detection Methods

#### 1. Hash-Based Detection (Cryptographic Verification)
- **Algorithm:** SHA256 and MD5 hashing
- **Purpose:** Identify known malware by cryptographic fingerprint
- **API:** VirusTotal API v3
- **Coverage:** 70+ antivirus engines

**How it works:**
1. Calculate SHA256 hash of the file
2. Query VirusTotal API with the hash
3. Retrieve detection statistics from multiple engines
4. Contribute to threat score if malicious

#### 2. Signature-Based Detection (Pattern Matching)
- **Engine:** YARA v4.3.1
- **Rules:** 446 compiled YARA files
- **Coverage:** Malware families, ransomware, trojans, exploits
- **Severity Levels:** High, Medium, Low

**How it works:**
1. Load and compile 446 YARA rule files
2. Scan file against all compiled rules
3. Match patterns, strings, and byte sequences
4. Classify matches by severity
5. Contribute to threat score based on severity

#### 3. Entropy Analysis (Statistical Analysis)
- **Algorithm:** Shannon Entropy
- **Range:** 0.0 - 8.0 bits per byte
- **Purpose:** Detect encryption, compression, and random data

**Entropy Interpretation:**
- **0.0 - 4.0:** Plain text, structured data (low randomness)
- **4.0 - 6.5:** Normal binary files (images, executables)
- **6.5 - 7.5:** Compressed data (ZIP, RAR)
- **7.5 - 8.0:** Encrypted or highly random data (ransomware indicator)

**Formula:**
```
H(X) = -Σ P(xi) * log2(P(xi))
```
Where P(xi) is the probability of byte value xi in the file.

### Threat Scoring System

**Scoring Weights:**
- VirusTotal Malicious Detection: **0.8**
- VirusTotal Suspicious Detection: **0.4**
- YARA High Severity Match: **0.7**
- YARA Medium Severity Match: **0.5**
- High Entropy Detection: **0.6**
- Suspicious File Extension: **0.3**

**Threat Levels:**
- **CLEAN** (0.0 - 0.39): No significant threats
- **SUSPICIOUS** (0.4 - 0.69): Some warning indicators
- **MALICIOUS** (0.7 - 1.0): Multiple threat indicators

---

## 📦 Dependencies

| Library | Version | Purpose |
|---------|---------|---------|
| `requests` | ≥2.31.0 | VirusTotal API communication |
| `python-dotenv` | ≥1.0.0 | Environment variable management |
| `yara-python` | ≥4.3.1 | YARA signature scanning |
| `rich` | ≥13.7.0 | Beautiful terminal output |

Install all dependencies:
```bash
pip install -r requirements.txt
```

---

## 🧪 Testing

### Test with EICAR Test Virus
```bash
python main.py --scan samples/eicar.com
```
**Expected:** MALICIOUS (Score: 1.0/1.0)

### Test with Clean File
```bash
python main.py --scan samples/clean/hello.py
```
**Expected:** CLEAN (Score: 0.0/1.0)

### Test with Encrypted File
```bash
python main.py --scan samples/encrypted_large.bin
```
**Expected:** MALICIOUS or SUSPICIOUS (High entropy detected)

### Test Directory Scan
```bash
python main.py --dir samples/
```
**Expected:** Summary of all files in directory

---

## 🎓 Educational Purpose

This project demonstrates:
- **Cryptographic Hashing** (SHA256, MD5)
- **Entropy Analysis** (Shannon Entropy)
- **Pattern Matching** (YARA signatures)
- **API Integration** (VirusTotal REST API)
- **Multi-factor Detection** (Combining multiple methods)
- **Threat Intelligence** (Signature databases)
- **Clean Code Practices** (Modular design, documentation)

---

## 🔒 Security Practices Implemented

1. **API Key Protection** - Stored in `.env` file, not in code
2. **Input Validation** - File existence and type checking
3. **Error Handling** - Graceful failure with informative messages
4. **Rate Limiting** - Respects VirusTotal API limits
5. **Safe File Reading** - Chunk-based reading to prevent memory issues
6. **No Code Execution** - Only reads and analyzes files, never executes
7. **Timeout Protection** - YARA scanning with 60-second timeout

---

## 📝 Known Limitations

1. **VirusTotal Rate Limits** - Free API limited to 4 requests/minute
2. **False Positives** - YARA rules may flag legitimate files
3. **Encrypted Archives** - Cannot scan inside encrypted ZIP/RAR files
4. **Large Files** - Entropy analysis uses first 8KB sample
5. **Obfuscated Malware** - May miss heavily obfuscated threats

---

## 🚧 Future Improvements

- [ ] Add machine learning-based detection
- [ ] Support for PE file analysis (import tables, sections)
- [ ] Sandbox execution for dynamic analysis
- [ ] Database to track scan history
- [ ] Web interface for easier use
- [ ] Custom YARA rule creation wizard
- [ ] Multi-threaded scanning for faster directory scans
- [ ] Support for scanning network traffic
- [ ] Integration with more threat intelligence APIs

---
## 🙏 Acknowledgments

- **YARA Project** - For the powerful pattern matching engine
- **VirusTotal** - For providing free malware detection API
- **Rich Library** - For beautiful terminal output
- **Open Source Community** - For YARA rule contributions


