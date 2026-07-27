# mh_libscriptEdit - Import NIST Webbook
Agilent Masshunter Quant 10.x Library Editor - Updated version of Chemspider OEM MOL retrieval script
Massive credit due for Inspecti
https://github.com/Inspecti/masshunter-scripts
I also used Copilot for additional reviews while making these scripts.

NistWebBook Compound Data Import
Formula and MolecularWeight are extracted from NIST WebBook JSON-LD metadata.
AlternateNames are extracted from the NIST "Other names" field.

Retrieves from NIST WebBook using CAS Number:
  AlternateNames
  Formula
  MolecularWeight

Only populates fields that are currently empty.
NOTE: AlternateNames extraction depends on the current NIST WebBook HTML layout.

It is possible to change from NIST Webbook to Pubchem REST API without a lot of changes.

Also, changing from "AlternateNames (shown as "Other Names:" on webpage) will allow you to retrieve a different field.
For some additional info on that, I uploaded an "enumerate_properties" script that will assist with that.

All scripts being added are xxxxx.libedit.script
