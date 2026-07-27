# mh_libscriptEdit - Import NIST Webbook

Agilent MassHunter Quant 10.x Library Editor - Collection of updated Library Editor scripts as an alternative to OEM-provided functionality.

Massive credit to Inspecti. Most scripts in this repository are derived from or inspired by work from that developer.
I also used Copilot for additional reviews while making these scripts.

- No API keys are currently required to run these scripts.
- Basic rate limiting has been incorporated where possible.
- Synonym imports are limited to the first 10 entries to reduce load on external services.

Scripts are executed from Library Editor by opening a writable custom library (not a locked `.L` library) and selecting:  
  Tools → Run Script...
  
Recommended script location:
```
  [Install drive]\MassHunter\Scripts\LibraryEdit
```
## CAS Normalization
CAS normalization converts a valid `[CAS#]` number into a digit-only format by removing hyphens.

## Script Descriptions
### 1. CAS_GetMOL_Webbook-Pubchem.libedit.script
Uses a normalized CAS number to retrieve a MOL structure (`MolFile` column), first checking NIST WebBook and using PubChem as a fallback.
  Lookup Order:
  1. NIST Chemistry WebBook
  2. PubChem

### 2. CAS_NIST_Synonyms.libedit.script
Uses a normalized CAS number to retrieve alternate names from the NIST WebBook.
Populates:
- `AlternateNames`

### 3. NIST-Webbook_Import.libedit.script
NIST WebBook Compound Data Import.
`Formula` and `MolecularWeight` are extracted from NIST WebBook JSON-LD metadata.
`AlternateNames` are extracted from the NIST "Other names" field.

Retrieves from NIST WebBook using a valid CAS Number:
  - AlternateNames
  - Formula
  - MolecularWeight

Notes:
- Only populates fields that are currently empty.
- AlternateNames extraction depends on the current NIST WebBook HTML layout.
- Formula and MolecularWeight retrieval use structured JSON-LD metadata.
- The script could be adapted to use the PubChem REST API with relatively minor changes.
- Modifying the AlternateNames parser (shown as "Other names" on the NIST webpage) can be used to retrieve additional fields.

### 4. enumerate_properties.libedit.script
Utility script for confirming connectivity to NIST WebBook and identifying candidate properties for import.

Additional Information:
- For column name references and schema details, consult SDK documentation such as:
  - `LibraryDataSet_10_0.pdf`
- All scripts in this repository use the `.libedit.script` extension.

### 5. Possible Routes for Future Updates
Potential future enhancements include: 

- Retrieval of flavor or odor descriptions from:
  - The Good Scents Company
  - Perflavory
  - Scents and Flavors
  - Perfumer Supply House
  - Scentree
  - FlavScents
  - FEMA Flavor Library

- Retrieval of FEMA reference numbers
  - Could pull from FEMA flavor library
  - Pubchem
  - Local excel file

- Add retrieval of Boiling Point and/or Melting Point
  - Pubchem
  - NIST Webbook
  - Chemspider
  - the Good Scents Compny
  - scentsandflavors database

## References
- Agilent MassHunter Quantitative Analysis 10.1 and 10.2
- Agilent Library Editor (installed by Quantitative Analysis), build 10.1.733.0
- NIST WebBook (July 2026)
  - https://webbook.nist.gov/chemistry/
- PubChem REST API (July 2026, no API key required)
  - https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest
- Inspecti MassHunter Scripts
  - https://github.com/Inspecti/masshunter-scripts
