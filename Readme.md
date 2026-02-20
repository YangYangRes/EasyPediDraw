**Principal Investigator**: Dongmei Ji

**Key Contributor**: Ning Zhang, Yang Yang, Haoyu He

# EasyPediDraw User Guide

## 📋 Table of Contents
- [Quick Start](#quick-start)
- [Page Layout](#page-layout)
- [Features](#features)
- [Data Input Guide](#data-input-guide)
- [Result Interpretation](#result-interpretation)
- [FAQ](#faq)

---

## 🚀 Quick Start

EasyPediDraw is a professional pedigree chart drawing and analysis tool that helps you:
- Draw professional pedigree charts
- Automatically validate data integrity
- Intelligently predict inheritance patterns
- Export high-quality charts

---

## 🖥️ Page Layout

The interface is divided into **two columns**:

### Left Control Panel (1/3 width)

**1. Template Library**
   - Preset template selection
   - File upload function
   - Data editor
   - Symbol size adjustment
   - Basic export functions

**2. Smart Layout Engine**
   - Layout mode selection (Compact/Standard/Spacious)

**3. Advanced Export**
   - Multiple format options (PDF/PNG/SVG/EPS)
   - Page size settings
   - Resolution adjustment

### Right Display Panel (2/3 width)

Top-to-bottom order:

**1. Smart Data Validation**
   - Real-time display of data errors and warnings

**2. Pedigree Chart**
   - Visual family tree display

**3. Statistics Summary**
   - Statistical information

**4. Inheritance Pattern Analysis**
   - 🔍 **Algorithm prediction results** (Predicted by algorithm for reference only)

---

## 🔧 Features

### 1. Template Library

#### 📂 Preset Template Selection
The system provides 7 preset templates:

| Template Name | Description | Use Case |
|--------------|-------------|----------|
| Empty Template | Blank template | Start from scratch |
| Autosomal Dominant (AD) | Autosomal dominant | Huntington's disease, etc. |
| Autosomal Recessive (AR) | Autosomal recessive | Cystic fibrosis, etc. |
| X-Linked Recessive (XLR) | X-linked recessive | Hemophilia, etc. |
| Y-Linked (YL) | Y-linked | Male infertility, etc. |
| Large Complex Family | Large complex family | 4 generations, 22 individuals |
| Incorrect Pedigree (Demo) | Error demonstration | Learn data validation |

**How to use**:
1. Click the "Load Template" dropdown menu
2. Select any template
3. Data will be automatically filled into the data editor

---

#### 📤 File Upload
Supports uploading CSV, TXT, TSV format files

**Steps**:
1. Click the "Browse..." button
2. Select a local file
3. System automatically reads and fills data

---

#### ✏️ Data Editor
Directly edit pedigree data in the text box

**Quick operations**:
- Paste Excel data directly (Tab-separated)
- Paste CSV data directly (comma-separated)
- Manually edit any field

---

#### 🎚️ Symbol Size
Slider to adjust the size of individual symbols in the pedigree chart
- Range: 0.5 - 2.5
- Default: 1.0
- Recommended: Use smaller values for large families (0.8-1.0)

---

#### 💾 Basic Export
Quick export functions:
- **PDF** button: Export PDF format (vector graphics, suitable for printing)
- **PNG** button: Export PNG format (bitmap, suitable for presentations)

---

### 2. Smart Layout Engine

**Layout Mode**:

| Mode | Characteristics | Use Case |
|------|----------------|----------|
| Compact | Dense layout | Large families (>20 people) |
| Standard | Standard layout | General families (default) |
| Spacious | Loose layout | Small families, need clear display |

---

### 3. Advanced Export

#### 📄 Format Selection
- **PDF (Vector)**: Vector format, lossless scaling, suitable for publication
- **PNG (Bitmap)**: Bitmap format, suitable for PPT presentations
- **PNG (Transparent)**: Transparent background PNG, suitable for overlay design
- **SVG (Vector)**: Web vector format, suitable for web display
- **EPS (Publication)**: Publication-grade vector format, suitable for journal submission

#### 📐 Size (Page Size)
- A4 Portrait / Landscape
- Letter Portrait / Landscape
- Slide 16:9 / 4:3 (PPT sizes)

#### 🎨 DPI (Resolution, PNG only)
- 300 DPI: Standard print quality
- 600 DPI: High-quality printing
- 1200 DPI: Publication-grade quality

---

## 📝 Data Input Guide

### Data Format Requirements

Pedigree data must contain the following columns (CSV format):

```csv
id,dadid,momid,sex,affected,status,note
```

### Field Descriptions

| Field | Required | Type | Description | Example Values |
|-------|----------|------|-------------|----------------|
| **id** | ✅ | Text | Unique individual identifier | I-1, II-3, III-5 |
| **dadid** | ✅ | Text | Father ID | I-1 (0 = unknown) |
| **momid** | ✅ | Text | Mother ID | I-2 (0 = unknown) |
| **sex** | ✅ | Number | Sex | 1=male, 2=female |
| **affected** | ✅ | Number | Disease status | 0=unaffected, 1=affected |
| **status** | ✅ | Number | Vital status | 0=alive, 1=deceased |
| **note** | ❌ | Text | Additional notes | Proband, Carrier, etc. |

### Input Example

#### Example 1: Three-Generation Simple Family

```csv
id,dadid,momid,sex,affected,status,note
I-1,0,0,1,1,0,Affected father
I-2,0,0,2,0,0,Mother
II-1,I-1,I-2,1,1,0,Affected son
II-2,I-1,I-2,2,0,0,Daughter
III-1,II-1,II-2,2,1,0,Affected granddaughter
```

**Interpretation**:
- **I-1**: Generation 1 male (sex=1), affected (affected=1), alive (status=0)
- **I-2**: Generation 1 female (sex=2), unaffected (affected=0), alive (status=0)
- **II-1**: Generation 2, father is I-1, mother is I-2, male, affected
- **III-1**: Generation 3, father is II-1, mother is II-2, female, affected

---

### Naming Convention Recommendations

**Generation-Number format** (Recommended):
- I-1, I-2, I-3 (Generation 1)
- II-1, II-2, II-3 (Generation 2)
- III-1, III-2, III-3 (Generation 3)

**Other usable formats**:
- A1, A2, B1, B2
- 001, 002, 003
- Any text without commas

---

### ⚠️ Common Data Errors

The system will automatically detect the following errors:

| Error Type | Description | Example |
|-----------|-------------|---------|
| **Sex error** | Father marked as female | Individual with dadid has sex=2 |
| **Sex error** | Mother marked as male | Individual with momid has sex=1 |
| **Missing individual** | Parent ID not found in dataset | dadid=I-5, but no I-5 row exists |
| **Single parent warning** | Only father or only mother | dadid=I-1, momid=0 |

---

## 📊 Result Interpretation

### 1. Smart Data Validation

#### ✅ Validation Passed
```
✓ All validations passed!
Your pedigree data is structurally correct
```
**Meaning**: Data format is completely correct, you can proceed with analysis

---

#### ❌ Error Messages (Error)
```
✗ 2 Error(s) Found:
Error: Individual II-1 - Father I-1 is marked as female
Error: Individual II-3 - Mother I-5 not found in dataset
```

**Meaning**:
- **First error**: Individual II-1's father I-1 has incorrect sex marking (should be male)
- **Second error**: Individual II-3's mother I-5 cannot be found in dataset

**Solution**:
1. Change I-1's sex field to 1 (male)
2. Add I-5's data row, or change II-3's momid to correct value

---

#### ⚠️ Warning Messages (Warning)
```
⚠ 1 Warning(s):
Warning: Individual III-2 has father but no mother
```

**Meaning**: Individual III-2 has only father information, no mother information

**Need to fix?**:
- Warnings won't prevent analysis
- Recommended to complete data for more accurate inheritance pattern prediction

---

### 2. Pedigree Chart

#### Symbol Legend

| Symbol | Meaning |
|--------|---------|
| □ | Male (square) |
| ○ | Female (circle) |
| ■ | Affected male (filled square) |
| ● | Affected female (filled circle) |
| ／ | Deceased individual (diagonal line) |
| ─ | Marriage relationship (horizontal line) |
| │ | Offspring relationship (vertical line) |

#### Chart Interpretation
- **Horizontal arrangement**: Same generation individuals
- **Vertical arrangement**: Different generations
- **Symbol size**: Adjustable via Symbol Size
- **Labels**: Display ID and note information

---

### 3. Statistics Summary

Six statistical cards display:

| Metric | Description |
|--------|-------------|
| **Total** | Total number of individuals |
| **Male** | Number of males |
| **Female** | Number of females |
| **Affected** | Number of affected individuals |
| **Deceased** | Number of deceased individuals |
| **Affected Rate** | Percentage of affected individuals |

**Example**:
```
Total: 15
Male: 8
Female: 7
Affected: 5
Deceased: 2
Affected Rate: 33.3%
```

**Interpretation**:
- This family has 15 individuals
- 5 are affected, accounting for 33.3%
- 2 are deceased
- Male-female ratio is relatively balanced

---

### 4. Inheritance Pattern Analysis ⭐

> **Important Note**: This result is automatically predicted by algorithm, for reference only (Predicted by algorithm for reference only)

#### Analysis Result Structure

**Top Main Result**:
```
🧬 X-Linked Recessive
Confidence Level: 85%
█████████████████░░░ 85%
```

**Meaning**:
- **Predicted pattern**: X-Linked Recessive
- **Confidence**: 85% (algorithm's confidence in this prediction)
- **Visual progress bar**: Intuitive display of confidence

---

#### Confidence Interpretation

| Confidence Range | Interpretation | Recommendation |
|-----------------|----------------|----------------|
| **≥ 80%** | Highly reliable | Pattern is very likely accurate |
| **60-79%** | Moderately reliable | Possibly accurate, suggest clinical correlation |
| **40-59%** | Low reliability | High uncertainty, need more data |
| **< 40%** | Insufficient data | Sample size too small, cannot reliably predict |

---

#### Analysis Details

**Example 1: Standard Analysis**
```
Analysis based on 8 affected (7M/1F) out of 25 total individuals.

Key findings:
- AD vertical transmission: 2 cases
- AR unaffected parents: 3 cases
- XLR male bias: Yes (6 maternal transmission)
- XLD female bias: No
- YL characteristics: Not detected
```

**Field Explanation**:

| Field | Meaning |
|-------|---------|
| **affected (7M/1F)** | 8 patients (7 males, 1 female) |
| **AD vertical transmission** | Autosomal dominant: number of vertical transmission cases |
| **AR unaffected parents** | Autosomal recessive: number of cases with unaffected parents |
| **XLR male bias** | X-linked recessive: presence of male bias |
| **maternal transmission** | Number of maternal transmission cases |
| **XLD female bias** | X-linked dominant: presence of female bias |
| **YL characteristics** | Y-linked: characteristics detected |

---

**Example 2: Analysis with Exclusions**
```
Analysis based on 5 affected (5M/0F) out of 18 total individuals.

Key findings:
- AD vertical transmission: 3 cases (1 3-gen chains)
- AR unaffected parents: 0 cases
- XLR male bias: Yes (3 maternal transmission)
- XLD female bias: No
- YL characteristics: Detected

Exclusions:
Male-to-male transmission detected (2 cases) - excludes all X-linked inheritance
Affected male with unaffected son(s) (1 cases) - excludes Y-linked inheritance
```

**Exclusions Interpretation**:

The system automatically excludes impossible inheritance patterns based on genetic rules:

| Exclusion Reason | Excluded Pattern | Genetic Basis |
|-----------------|------------------|---------------|
| **Male-to-male transmission** | XLR, XLD | Male-to-male phenomenon, X chromosome cannot transmit father-to-son |
| **Affected father with unaffected daughter** | XLD | In X-linked dominant, affected father's daughters must be affected |
| **Affected male with unaffected son** | YL | In Y-linked, affected male's sons must be affected |
| **Affected female with unaffected father** | XLR | In X-linked recessive, affected female's father must be affected |
| **Affected parents with unaffected children** | AR | In autosomal recessive, both affected parents must have affected children |

---

**Example 3: Uncertainty Warning**
```
⚠️ UNCERTAINTY WARNING: Multiple patterns possible!
Top pattern: 65.2%, Second pattern (Autosomal Recessive): 58.7%
Difference only 6.5 points - consider additional clinical evidence.
```

**Meaning**:
- Two patterns have similar scores (difference < 15 points)
- First pattern: 65.2%
- Second pattern (Autosomal Recessive): 58.7%
- **Recommendation**: Need more clinical evidence (such as genetic testing, family history, age of onset, etc.)

---

#### Pattern Scores

Below the analysis details, scores for all 5 inheritance patterns will be displayed:

```
📊 Pattern Scores

Autosomal Dominant: ████████░░ 45%
Autosomal Recessive: ███░░░░░░░ 30%
X-Linked Recessive: █████████░ 85%
X-Linked Dominant: ██░░░░░░░░ 20%
Y-Linked (Holandric): ░░░░░░░░░░ 0%
```

**Interpretation**:
- System scores all 5 patterns (0-100%)
- Highest scoring pattern is the predicted result
- You can view relative likelihood of all patterns

---

#### Five Inheritance Pattern Descriptions

| Pattern | Abbreviation | Characteristics | Typical Diseases |
|---------|--------------|----------------|------------------|
| **Autosomal Dominant** | AD | Generation-to-generation transmission, both sexes affected | Huntington's disease |
| **Autosomal Recessive** | AR | Skip-generation inheritance, unaffected parents | Cystic fibrosis |
| **X-Linked Recessive** | XLR | More males affected, maternal transmission | Hemophilia, color blindness |
| **X-Linked Dominant** | XLD | More females affected, father-daughter transmission | Vitamin D-resistant rickets |
| **Y-Linked** | YL | Only males affected, father-son transmission | Male infertility (AZF deletion) |

---

### Result Usage Recommendations

#### ✅ What You Can Do
1. **Preliminary determination** of inheritance pattern
2. **Assist decision-making** on whether genetic testing is needed
3. Provide **reference for family counseling**
4. **Teaching demonstration** of genetic patterns

#### ❌ What You Should Not Do
1. **Cannot replace** professional genetic counseling
2. **Cannot serve as** clinical diagnosis basis
3. **Cannot ignore** other clinical evidence
4. **Cannot be used for** legal or medical disputes

#### 🔬 Recommended Next Steps
- Confidence ≥ 80%: Recommend genetic testing related to this pattern
- Confidence 60-79%: Recommend consulting genetic specialist
- Confidence < 60%: Recommend expanding sample size or supplementing clinical information

---

## 🔍 Case Studies

### Case 1: X-Linked Recessive (Hemophilia)

**Data Input**:
```csv
id,dadid,momid,sex,affected,status,note
I-1,0,0,1,0,0,Unaffected father
I-2,0,0,2,0,0,Carrier mother
II-1,I-1,I-2,1,1,0,Affected son
II-2,I-1,I-2,2,0,0,Carrier daughter
II-3,I-1,I-2,1,0,0,Unaffected son
```

**Prediction Result**:
```
🧬 X-Linked Recessive
Confidence Level: 92%
```

**Analysis Details**:
- 3 affected (3M/0F): All male patients ✓
- XLR male bias: Yes: Strong male bias ✓
- maternal transmission: 3 cases: Maternal transmission ✓

**Conclusion**: Typical X-linked recessive inheritance pattern, consistent with hemophilia genetics

---

### Case 2: Autosomal Dominant (Huntington's Disease)

**Data Input**:
```csv
id,dadid,momid,sex,affected,status,note
I-1,0,0,1,1,0,Affected grandfather
I-2,0,0,2,0,0,Grandmother
II-1,I-1,I-2,1,1,0,Affected father
II-2,I-1,I-2,2,0,0,Aunt
III-1,II-1,0,1,1,0,Affected son
III-2,II-1,0,2,0,0,Daughter
```

**Prediction Result**:
```
🧬 Autosomal Dominant
Confidence Level: 88%
```

**Analysis Details**:
- AD vertical transmission: 3 cases (1 3-gen chains): Three consecutive generations ✓
- Male/Female ratio balanced: Balanced ratio of male and female patients ✓

**Conclusion**: Typical autosomal dominant inheritance, generation-to-generation transmission

---

### Case 3: Insufficient Data

**Data Input**:
```csv
id,dadid,momid,sex,affected,status,note
I-1,0,0,1,1,0,Patient
I-2,0,0,2,0,0,Wife
```

**Prediction Result**:
```
⚠️ Insufficient data
Confidence Level: 0%

Only 1 affected individual(s) found.
At least 3 affected individuals are recommended for reliable pattern analysis.
Results should be interpreted with extreme caution.
```

**Recommendations**:
- Add more family member data
- Trace grandparents' generation
- Investigate children's generation
- Inquire about siblings

---

## ❓ FAQ

### Q1: Why does my data show "parsing failed"?
**A**: Check the following:
- Are you using correct separators (comma or Tab)?
- Are column names correct (id, dadid, momid, sex, affected, status)?
- Are there blank lines or special characters?
- Are sex and affected fields numeric?

---

### Q2: What causes low confidence?
**A**: Possible reasons:
1. **Sample size too small** (patients < 3)
2. **Poor data quality** (missing parent information)
3. **Complex inheritance pattern** (polygenic inheritance, sporadic cases)
4. **Data contradictions** (doesn't fit any classical inheritance pattern)

---

### Q3: What if multiple high-scoring patterns appear?
**A**: When uncertainty warning appears:
1. Check Pattern Scores, compare differences between patterns
2. Combine with clinical features (age of onset, symptom severity)
3. Consider genetic testing for verification
4. Consult professional genetic counselor

---

### Q4: How to adjust when pedigree chart appears chaotic?
**A**: Try the following adjustments:
1. Adjust **Symbol Size**
2. Change **Layout Mode** (Compact/Standard/Spacious)
3. Export as PDF and view with other software
4. Check data for duplicate IDs

---

### Q5: How to export charts for publication?
**A**: Recommended settings:
- **Format**: PDF (Vector) or EPS (Publication)
- **Size**: A4 Landscape or Letter Landscape
- **Layout Mode**: Standard or Spacious
- **Symbol Size**: 1.0 - 1.2

---

### Q6: Can the system analyze polygenic diseases?
**A**: 
- System only supports **single-gene disorders** classical pattern analysis
- **Not supported**: Polygenic inheritance, mitochondrial inheritance, epigenetic
- Complex diseases recommended to use professional genetic analysis software

---

### Q7: What is the maximum family size supported?
**A**:
- Theoretically unlimited
- Recommended < 100 people (optimal performance)
- Very large families (> 100 people) may cause display crowding, suggest:
  - Use Compact layout mode
  - Reduce Symbol Size
  - Analyze in segments (by generation or branch)

---

## 📚 Appendix

### A. Data Template Download

7 built-in templates available for direct use:
1. Empty Template
2. Autosomal Dominant
3. Autosomal Recessive
4. X-Linked Recessive
5. Y-Linked
6. Large Complex Family
7. Incorrect Pedigree (Demo)

### B. Recommended CSV File Editing Tools
- **Excel** (Recommended): Direct editing, save as CSV
- **Google Sheets**: Online collaborative editing
- **Notepad**: Lightweight editing
- **VS Code**: Professional text editor

### C. Genetic Terminology Reference

| Chinese | English |
|---------|---------|
| 系谱图 | Pedigree Chart |
| 先证者 | Proband |
| 携带者 | Carrier |
| 纯合子 | Homozygous |
| 杂合子 | Heterozygous |
| 外显率 | Penetrance |
| 遗传度 | Heritability |

---

## 📞 Technical Support

If you encounter technical issues or have suggestions for improvement, please contact the system administrator.

---

**Last Updated**: 2026-02-21  
**Document Version**: v1.0  
**Applicable Software Version**: EasyPediDraw ULTRA

---

**Disclaimer**:
The inheritance pattern predictions provided by this tool are for research and educational reference only and cannot serve as a basis for clinical diagnosis. Any medical decision should consult professional genetic physicians or genetic counselors.